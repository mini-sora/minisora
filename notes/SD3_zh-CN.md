# 文生图之SD3：迈向transformer时代

在发布[Stable Diffusion 3](https://stability.ai/news/stable-diffusion-3)之后，StabilityAI最近终于放出了[SD3的技术报告](https://stability.ai/news/stable-diffusion-3-research-paper)，相比SD之前的版本，SD3有比较大的改进。

- 首先，SD3是一个基于Rectified Flow的生成模型；
- 其次，SD3引入了T5-XXL来作为text encoder来提升模型的文本理解能力；
- 最后，SD3采用了一个多模态的DiT架构，并且将模型参数量扩展为8B。

从目前给出的例子和评测上，SD3在文字渲染和对文本提示词的遵循上，已经达到甚至超过目前STOA的文生图模型如DALL·E 3、Midjourney v6和Ideogram v1。这篇文章将根据SD3的论文分析SD3的具体实现细节。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1709871143271-c299f747-c675-46e1-9edf-db7bee6baab7.png#averageHue=%2380c8e1&clientId=u0cd23905-4720-4&from=paste&height=561&id=ub2bc6e58&originHeight=1235&originWidth=1920&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=3412261&status=done&style=none&taskId=u38b03b1a-8524-4475-a704-445bd0c5d8e&title=&width=872.7272538114189)

## 改进的RF

SD3相比之前的SD一个最大的变化是采用**Rectified Flow**来作为生成模型，Rectified Flow在[Flow Straight and Fast: Learning to Generate and Transfer Data with Rectified Flow](https://arxiv.org/abs/2209.03003)被首先提出，但其实也有同期的工作比如[Flow Matching for Generative Modeling](https://arxiv.org/abs/2210.02747)提出了类似的想法。

这里和SD3的论文一样，首先将基于**Flow Matching**来介绍RF，然后再介绍SD3在RF上的具体改进。

### Flow Matching

**Flow Matching（FM）**是建立在[continuous normalizing flows](https://arxiv.org/abs/1806.07366)的基础上，这里将生成模型定义为一个**常微分方程（ODE）**：

$$dz_{t}=v(z_{t},t)\,dt$$
这里 $t\in[0,1]$，而 $v(z_{t},t)$称之为**向量场（vector field）**。我们用这样的一个ODE来构建一个**概率路径（probability path）** $p_t$，它可以实现从一个噪音分布 $p_1 $到另外一个数据分布$p_0$的转变（可以称之为**a flow**），注意这里我们在时间上是和FM论文中的定义是相反的，这其实是为了后面和扩散模型统一起来。这里的噪音分布我们采用高斯噪音，即$p_{1}=\mathcal{N}(0,1)$，而$p_0$是我们要建模的数据分布$q(x_0)$。一旦我们知道了$v(z_{t},t)$，我们就可以用ODE的求解器比如欧拉方法（Euler method）实现从一个噪音到真实数据的生成。这里，我们可以用一个参数为$\theta$的神经网络$v_\theta(z_{t},t)$来建模向量场，FM的优化目标为：
$$\displaystyle\mathcal{L}_{FM}=\mathbb{E}_{t,p_{t}(z)}||v_{\theta}(z,t)-u_{t}(z)||_{2}^{2}$$
这里的$u_{t}(z)$是目标向量场，它可以产生噪音分布$p_1$到真实数据分布$q(x_0)$的概率路径$p_t(z)$。所以其实FM的优化目标就是直接回归目标向量场。有很多的概率路径可以满足$p_1\approx q(x_0)$，但是果没有任何先验，$u_{t}(z)$是不可知的，FM的优化目标也就无法实现。
一个解决思路是我们先预先构建一个$u_{t}(z)$，并让它能够保证我们的目标概率路径$p_t(z)$。为此，FM论文中引入了条件概率路径$p_t(z|x_0)$，这里的条件是真实数据$x_0$，这个条件概率采用如下的高斯分布：
$$p_{t}(z|x_{0})=\mathcal{N}(z|a_{t}x_{0}, b_{t}^{2}I)$$
这个高斯分布的均值为$a_{t}x_{0}$，而方差为$b_t$，这里的$a_t$和$b_t$都是和$t$有关的函数，并且是可导的。同时，当$t=0$要满足$a_0=1, b_0=0$，这样$p_{0}(z|x_{0})=q(x_0)$；而当$t=1$要满足$a_1=0, b_1=1$，这样$p_{1}(z|x_{0})=p_1$。这样，这里定义的条件概率路径$p_t(z|x_0)$能够保证噪音分布$p_1$到真实数据分布$q(x_0)$的转变。
细心的你可能会发现$p_t(z|x_0)$和扩散模型的扩散过程有相同的形式。其实，引入条件概率路径，就是相当于我们定义了一个前向过程：
$$z_{t}=a_{t}x_{0}+b_{t}\epsilon\quad\text{where}\;\epsilon\sim\mathcal{N}(0,I)$$
后面我们也会看到FM其实是可以看成扩散模型，只是采用了不一样的优化目标（等价于采用不同的loss权重）。

接下来，我们来看一个新的优化目标，那就是**Conditional Flow Matching** (**CFM**)目标：
$$\mathcal{L}_{CFM}=\mathbb{E}_{t,q(x_0),p_{t}(z|x_0)}||v_{\theta}(z,t)-u_{t}(z|x_0)||_{2}^{2}$$
这里的条件向量场$u_{t}(z|x_0)$产生条件概率路径$p_t(z|x_0)$。对于CM目标和CFM目标，一个很重要的结论是两者之间只相差一个与参数$\theta$无关的常量，这也就意味着：
$$\nabla_{\theta} \mathcal{L}_{FM}(\theta) = \nabla_{\theta} \mathcal{L}_{CFM}(\theta)$$
换句话说，使用CFM目标来训练$\theta$是和采用CM目标来训练$\theta$是等价的。这里我们就不展开证明了，感兴趣的可以看FM论文中的证明。一个直观的解释是，我们采用CFM目标来训练$\theta$也是能够达到我们的目标，那就是从噪音分布$p_1$到真实数据分布$q(x_0)$，只不过这里我们人工设定了一个路径$u_{t}(z|x_0)$而已。而且后面我们会看到不同的生成模型的差异除了优化目标之外就在于定义的路径（前向过程）的差异。
虽然$u_{t}(z)$是不可知的，但是引入条件后的$u_{t}(z|x_0)$是可以计算出来的：
$$u_{t}(z|x_0)=z'_t=a'_{t}x_{0}+b'_{t}\epsilon$$
进一步根据前向过程我们有：$x_0=(z_t-b_t\epsilon)/a_t$，我们将其代入上式，可以得到：
$$u_{t}(z|x_0)=\frac{a_{t}^{\prime}}{a_{t}}z_{t}-
\epsilon b_{t}(\frac{a_{t}^{\prime}}{a_{t}}-\frac{b_{t}^{\prime}}{b_{t}})$$
这里我们定义信噪比$\lambda_{t}=\log\frac{a_{t}^{2}}{b_{t}^{2}}$，进而有$\lambda_{t}^{\prime}=2(\frac{a_{t}^{\prime}}{a_{t}}-\frac{b_{t}^{\prime}}{b_{t
}})$，所以有：
$$u_{t}(z|x_0)=\frac{a_{t}^{\prime}}{a_{t}}z_{t}-\frac{b_{t}}{2}\lambda
_{t}^{\prime}\epsilon$$
我们将上式代入CFM目标中，就可以得到：
$$\mathcal{L}_{CFM}=\mathbb{E}_{t,q(x_0),p_{t}(z|x_0),\epsilon\sim\mathcal{N}(0,I)}||v_{\theta}(z,t)-
\frac{a_{t}^{\prime}}{a_{t}}z+\frac{b_{t}}{2}\lambda_{t}^{\prime}\epsilon||_{2
}^{2}$$
这里我们对$v_{\theta}(z,t)$进一步定义为：
$$v_{\theta}(z,t)=\frac{a_{t}^{\prime}}{a_{t}}z_{t}-\frac{b_{t}}{2}\lambda
_{t}^{\prime}\epsilon_{\theta}(z,t)$$
代入CFM优化目标可得到：
$$\mathcal{L}_{CFM}=\mathbb{E}_{t,q(x_0),p_{t}(z|x_0),\epsilon\sim\mathcal{N}(0,I)}\left(-\frac{b_{t}}{
2}\lambda_{t}^{\prime}\right)^{2}||\epsilon_{\theta}(z,t)-\epsilon||_{2}^{2}$$
此时相当于神经网络变成了预测噪音，这和扩散模型DDPM预测噪音是一样的，但是优化目标的多了一个和$t$有关的权重系数。所以，FM其实可以看成一个采用不同的权重系数的扩散模型。
Google的工作[Understanding Diffusion Objectives as the ELBO with Simple Data Augmentation](https://arxiv.org/abs/2303.00848)提出了一个统一的视角，即不同的生成模型包括[DDPM](https://arxiv.org/abs/2006.11239)，[SDE](https://arxiv.org/abs/2011.13456)，[EDM](https://arxiv.org/abs/2206.00364)以及[FM](https://arxiv.org/abs/2210.02747)等的优化目标都可以统一为：
$$\mathcal{L}_{w}(x_{0})=-\frac{1}{2}\mathbb{E}_{t\sim\mathcal{U}(0, 1),\epsilon
\sim\mathcal{N}(0,I)}\left[w_{t}\lambda_{t}^{\prime}\|\epsilon_{\theta}(z_{t},
t)-\epsilon\|^{2}\right]$$
不同的生成模型所采用的优化目标不同，等价于采用不同的权重$w_t$。对于DDPM所采用的$\mathcal{L}_{simple}$，这里$w_t=-2/\lambda'_t$。而对于FM的$\mathcal{L}_{CFM}$，有$w_t=-\frac{1}{2}\lambda'_tb_t^2$。
更具体地说，不同类型的生成模型差异在于前向过程和预测目标的差异。不同的前向过程采用不同$a_t$和$b_t$，导致不同的概率路径。而预测目标可以为预测噪音$\epsilon$（DDPM），预测分数$s$（SDE），以及预测向量场$v$（FM）等等。但是它们都可以最终统一为基于预测噪音$\epsilon$的优化目标，只是权重$w_t$的差异。

### Rectified Flow

在FM中，作者给出了一个基于最优传输（ Optimal Transport）具体的前向过程：
$$z_t=(1-t)x_0+((1-t)\sigma_{min}+t)\epsilon$$
当$\sigma_{min}=0$，我们就可以得到和[Rectified Flow](https://arxiv.org/abs/2209.03003)中一样的前向过程：
$$z_t=(1-t)x_0+t\epsilon$$
RF的前向过程一个特点是$z_t$由数据$x_0$和噪音$\epsilon$线性插值得到，这也意味我们人工定义的概率路径是一条直线。直线的一个好处是采样时我们可以步子迈大一点，这就相当于我们可以减少采样的总步数。关于理论的分析涉及到最优传输，感兴趣的话可以看看论文。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709954243903-7d0255cc-7220-4aa3-8d4c-23ef451b0288.png#averageHue=%236ead5f&clientId=ue3b9ce99-4c1b-4&from=paste&height=187&id=u052dd81c&originHeight=412&originWidth=594&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=81030&status=done&style=none&taskId=u2084ac39-34e4-4f19-8137-0e397d5dc38&title=&width=269.9999941479077" width="40%"/>
  <div align="center">
  </div>
</div>

对于RF，有$z'_t=-x_0+\epsilon$，所以其优化目标就变成了：
$$\mathcal{L}_{RF}=\mathbb{E}_{t,q(x_0),p_{t}(z|x_0),\epsilon\sim\mathcal{N}(0,I)}||v_{\theta}(z,t)-
(\epsilon-x_0)||_{2
}^{2}$$
可以看到，最终RF的损失函数是非常简单的。如果将RF转成$\mathcal{L}_{w}(x_{0})$，其对应的$w_t=-\frac{1}{2}\lambda'_tb_t^2=\frac{t}{1-t}$。

SD3论文中除了实验RF模型外，还对其它模型做了对比实验，这里也需要简单介绍一下。

首先是之前版本的SD所采用的(**LDM-**)**Linear**，LDM是基于DDPM，但和DDPM采用了不同的noise schedule。DDPM是基于离散时间$t=0,\dots,T-1$的扩散模型，给定扩散系数$\beta_0$和$\beta_T$，$\beta_{t}=\beta_{0}+\frac{t}{T-1}(\beta_{T-1}-\beta_{0})$（DDPM的noise schedule是线性的）。对于LDM，$\beta_{t}=\left(\sqrt{\beta_{0}\vphantom{\beta_{T-1}}}+\frac{t}{T-1}(\sqrt{%
\beta_{T-1}}-\sqrt{\beta_{0}\vphantom{\beta_{T-1}}})\right)^{2}$。根据$\beta_t$，可以得到：
$a_{t}=(\prod_{s=0}^{t}(1-\beta_{s}))^{\frac{1}{2}}, b_t=\sqrt{1-a^2_t}$

除了线性noise schedule，[I-DDPM](https://arxiv.org/abs/2102.09672)还提出了cosine noise schedule，其前向过程可以定义为（采用连续时间）：
$$z_{t}=\cos (\frac{\pi}{2}t)x_{0}+\sin(\frac{\pi}{2}t)\epsilon$$

除了此外，SD3还实验了[EDM](https://arxiv.org/abs/2206.00364)，但这里我们不再展开了。

### 改进的采样方法

这里所说的采样是指的训练过程对时间步$t$的采样，由于$t$是和信噪比SNR正相关的，所以也可以说是对SNR的采样。对于RF，其默认使用均匀分布$t\sim\mathcal{U}(0, 1)$进行采样，这也就是说各个时间步$t$是同等对待的。但是SD3论文中认为不同时间步的任务难度是一样：两边相对容易，而中间是比较难的。所以，这里是设计了一些新的采样方法来提高中间时间步的权重。改变采样的分布，等价于改变权重系数：
$$w_{t}^{\pi}=\frac{t}{1-t}\pi(t)$$
这里的$\pi(t)$是采样$t$所遵循的概率分布，当使用均匀分布$t\sim\mathcal{U}(0, 1)$时，$\pi(t)=1$。

下面我们介绍一下SD3论文中所实验的几种采样方法。
1. **Logit-Normal Sampling**
2. **Mode Sampling with Heavy Tails**
3. **CosMap**

第一个采样方法是**Logit-Normal Sampling**，这是采用[Logit-Normal分布](https://en.wikipedia.org/wiki/Logit-normal_distribution)，所谓的Logit-Normal分布是指变量的logit满足正态分布，对于Logit-Normal分布，其概率密度为：
$$\pi_{\text{ln}}(t;m,s)=\frac{1}{s\sqrt{2\pi}}\frac{1}{t(1-t)}\exp(-
\frac{(\text{logit}(t)-m)^{2}}{2s^{2}})$$
这里$\text{logit}(t)=\log\frac{t}{1-t}$。其中参数$m$可以控制$t$的偏向（其中$m=0$时，$t=0.5$是分布的峰值），参数$s$控制分布的宽度（或者说是胖瘦）。下面是不同的参数下分布的可视化：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1709977129602-7e207ac3-d181-4cd4-a47e-43fbb3dcaeaf.png#averageHue=%23c0aba4&clientId=ud43ec78a-4dae-4&from=paste&height=430&id=u0c5406ad&originHeight=947&originWidth=1320&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=70150&status=done&style=none&taskId=u094a2a0b-a8a3-42d1-9527-5c8fb014039&title=&width=599.9999869953505)

在采样过程中，我们可以先基于正态分布$u\sim\mathcal{N}(u;m,s)$采样出一个$u$，然后再转成$t=\frac{e^u}{1+e^u}$。

第二个采样方法是**Mode Sampling with Heavy Tails**。Logit-Normal分布的一个问题是两边$t=0$和$t=1$附近基本采样不到，这个可能会对性能有一定的影响。所以这个第二个采样方法是基于一个重尾分布。首先我们用定义如下的函数：
$$f_{\text{mode}}(u;s)=1-u-s\cdot(\cos^{2}(\frac{\pi}{2}u)-
1+u)$$
这里$-1\leq s\leq\frac{2}{\pi-2}$，此时函数是单调的，我们可以通过$u\sim[0, 1], t=f_{\text{mode}}(u;s)$来采样时间步$t$。根据[变量变换定理](https://en.wikipedia.org/wiki/Probability_density_function#Function_of_random_variables_and_change_of_variables_in_the_probability_density_function)，有$\pi_{\text{mode}}(t;s)=\pi(u)\left|\frac{d}{dt}f_{\text{mode}}^{-1}(t)\right|=\left|\frac{d}{dt}f_{\text{mode}}^{-1}(t)\right|$。这里的参数$s$控制分布是偏向中间（>0）还是偏向两边（<0），当$s=0$时，此时就相当于均匀分布了，即$\pi_{\text{mode}}(t;0)=1$。下面是不同$s$下的分布可视化。
<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709988419049-70ffb93f-27c5-44c5-81e1-3eb4db30fc79.png#averageHue=%23c5b6ae&clientId=uf9cd0e18-eeef-4&from=paste&height=430&id=ud27a5e9f&originHeight=947&originWidth=1320&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=70402&status=done&style=none&taskId=u20f08f83-ae04-4245-9a1e-f5476f24e28&title=&width=599.9999869953505" width="70%"/>
  <div align="center">
  </div>
</div>

最后一个采样方法是**CosMap**。这里其实是想实现下RF下的cosine schedule ，我们可以求解一个映射$f:u\mapsto f(u)=t,\;u\in[0,1]$，让SNR和cosine schedule是一样的，即：
$$2\log\frac{\cos(\frac{\pi}{2}u)}{\sin(\frac{\pi}{2}u)}=2\log\frac{1-f(u)}{f(u)}$$
通过上述等式可得：
$$t=f(u)=1-\frac{1}{\tan(\frac{\pi}{2}u)+1}$$
同样根据变量变换定理，我们可以得到$t$的概率密度：
$$\pi_{\text{CosMap}}(t)=\left|\frac{d}{dt}f^{-1}(t)\right|=\frac{2}{\pi-2\pi t+%
2\pi t^{2}}$$

这里我们可以画出这个分布，如下所示，它也是中间概率密度高：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709989279278-5c0ac254-cdee-45b7-aeab-1a3a8d24626b.png#averageHue=%23fbf9f9&clientId=u3f04dd1d-ba34-4&from=paste&height=566&id=u9ecb2841&originHeight=1245&originWidth=1643&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=87568&status=done&style=none&taskId=u7f6a2022-e850-433b-b10f-19a150292cc&title=&width=746.818165631334" width="60%"/>
  <div align="center">
  </div>
</div>

### 对比实验

为了验证RF是否在文生图上是有效的，SD3论文中做了一系列的对比实验，实验的模型共包括61个，分别是：

- 采用$\epsilon$和$v$优化目标，同时noise schedule采用linear和cosine，这共4个配置：`eps/linear`，`v/linear`，`eps/cos`, `v/cos`，其中`eps/linear`就是LDM所采用的配置。
- 采用RF和$\pi_{\text{mode}}(t;s)$，这里记为`rf/mode(s)`，其中其中$s$在−1～1.75之间均匀选取7个值，另外还包含一个$s=0$的配置，这其实就是原来的RF。所以这组总共8个配置。
- 采用RF和$\pi_{\text{ln}}(t;m,s)$，这里记为`rf/lognorm(m, s)`，其中在$m\sim[-1,1]$和$s\sim[0.2,2.2]$以网格方式选择30组$(m,s)$。
- 采用RF和$\pi_{\text{CosMap}}(t)$，这里记为`rf/cosmap`。
- 采用EDM，记为$edm(P_{m}, P_{s})$，这两个参数决定EDM的SNR，其中在$P_{m}\sim [-1.2,1.2]$和$P_{s}\sim [0.6,1.8]$均匀选择15组。
- 采用EDM，但是schedule分别设置为`edm`和`rf`与`v/cos`的`log-SNR`加权匹配，这两个配置分别记为$rf(edm/rf)$和$v/cos(edm/cos)$。

每个模型的实验配置如下：

- **训练数据集**：ImageNet和CC12M两个数据集，其中ImageNet数据通过"a photo of a <class name>"构造成文本-图像对数据集。
- **评测指标**：CLIP score和FID（这里的FID采用CLIP来计算特征，而不是基于Inception V3），同时还基于validation loss选择模型。
- **评测数据集**：COCO-2014验证集。
- **采样器设置**：推理阶段均采用欧拉方法，共包括不同steps和CFG scale的6个配置，50 steps（CFG scale为1.0, 2.5, 5.0）以及CFG scale为5.0的5, 10, 25 steps。
- **权重**：非EMA和EMA权重。

每个实验用EMA权重在不同的训练steps基于validation loss最小来确定最优的模型。这里2个训练数据集+6个采样器设置+2套参数共产生24个组合，所以每个模型也会得到24个评测结果。由于评测指标是2个，所以采用多目标优化中非支配排序算法（基于Pareto最优）来进行排序。每一种配置（24种）单独进行排序，然后取平均值。下表展示了不同模型的rank结果（这里只展示每组配置的top 2）：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709996338848-684bad56-5796-456f-9347-cf3d1e2d2dc3.png#averageHue=%23e9e9e9&clientId=u7b2f79d3-b092-4&from=paste&height=389&id=uadc214c6&originHeight=856&originWidth=876&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=163213&status=done&style=none&taskId=ub3c934b1-3690-4f6c-aba8-4058809b4dc&title=&width=398.1818095514599" width="60%"/>
  <div align="center">
  </div>
</div>

可以看到`rf/lognorm(0.00, 1.00)`是综合rank最高的，而且在`5 steps`和`50 steps`下也可以取得较好的rank。这里所采用的`lognorm(0.00, 1.00)`的时间采样方法也恰好是偏向中间时间步的，这说明对中间时间步加权是重要且有效的。这里也可以看到未改进的RF效果上反而是不如LDM所采用的`eps/linear`，而且经典的`eps/linear`的rank也仅次于几个改进的RF。

下表展示了不同的模型在`25 steps`下具体的CLIP score和FID，`rf/lognorm(0.00, 1.00)`两个数据集均表现不错，而经典的`eps/linear`其实也不差。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709996841971-e610598d-2848-456a-8fa8-8c89989376f8.png#averageHue=%23e5e5e5&clientId=u2073db70-a462-4&from=paste&height=320&id=uc2d434f4&originHeight=704&originWidth=898&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=147794&status=done&style=none&taskId=ua1c4c7a7-21fd-4ed4-94e3-5eb2c3779ab&title=&width=408.18180933471575" width="60%"/>
  <div align="center">
  </div>
</div>

我们可以进一步去观察不同steps下各个模型的表现，如下图所示：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1709997009241-dc3b32e6-6ffc-410b-bfb7-9c69db47aef3.png#averageHue=%23fdfbfa&clientId=u2073db70-a462-4&from=paste&height=191&id=u0ad70fbf&originHeight=420&originWidth=747&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=180896&status=done&style=none&taskId=u2b85d0eb-ee26-4353-8b99-f92a5719f3a&title=&width=339.54544718600516" width="80%"/>
  <div align="center">
  </div>
</div>

可以看到RF模型在steps比较小时展现比较明显的优势，说明RF模型可以减少推理阶段的采样步数。当steps增加时，RF不如`eps/linear`，但是改进后的`rf/lognorm(0.00, 1.00)`依然能够超过`eps/linear`。

**总结：RF模型推理高效，但是通过改进时间采样方法对中间时间步加权能进一步提升效果，这里基于`lognorm(0.00, 1.00)`的采样方法从实验看是最优的。**

## 多模态DiT

SD3除了采用改进的RF，另外一个重要的改进就是采用了一个多模态DiT。多模态DiT的一个核心对图像的latent tokens和文本tokens拼接在一起，并采用两套独立的权重处理，但是在attention时统一处理。整个架构图如下所示：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1709997663380-2d5695d8-1710-49f7-b3f2-44332c7c6163.png#averageHue=%23f7f7f6&clientId=u4360d094-f3dc-4&from=paste&height=576&id=ue4fdd277&originHeight=1268&originWidth=1790&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=328031&status=done&style=none&taskId=udacba099-6bd1-4bb0-8952-d78363567c0&title=&width=813.6363460012708)

### 改进的autoencoder

这里的MM-DiT和DiT一样，依然是使用一个autoencoder（VAE）来将图像编码为latent，然后将latent转成patches，送入transformer处理。之前版本的SD所使用的autoencoder是将一个$H\times W\times 3$的图像编码为$\frac{H}{8}\times \frac{W}{8} \times d$的latent，这里的$d=4$，这个压缩还是比较狠的，带来的不利影响是容易产生小物体畸变（比如人眼，文字等）。所以SD3通过增加$d$来提升autoencoder的重建质量。下面是不同的$d$的定量评估：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710027366566-054cc2ee-9f66-4fca-bf40-0b72a9ba2397.png#averageHue=%23e6e6e6&clientId=u31486502-bc18-4&from=paste&height=238&id=ue334de01&originHeight=524&originWidth=1196&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=101821&status=done&style=none&taskId=u60e958b9-b75e-4f91-9130-10be8968aba&title=&width=543.6363518533631" width="60%"/>
  <div align="center">
  </div>
</div>

当$d=16$时，autoencoder的性能相比的$d=4$有一个比较大的提升，所以SD3使用16通道的autoencoder。要注意，虽然增加通道并不会对生成模型（UNet或者DiT）的参数带来大的影响（只需要修改网络第一层和最后一层的通道数），但是会增加任务的难度，当通道数从4增加到16，网络要拟合的内容增加了4倍，这也意味模型需要增加参数来提供足够的容量。SD3论文中的一个实验对比结果如下所示：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710027665358-6eeb4bb4-40b7-49cd-8eb2-4fa951cc7625.png#averageHue=%23f4f4f4&clientId=u31486502-bc18-4&from=paste&height=420&id=u8f7dba8d&originHeight=924&originWidth=2458&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=256203&status=done&style=none&taskId=u3a834ac5-472e-44df-bedc-db1bd5b3398&title=&width=1117.2727030564936)

当模型参数小时，16通道的autoencoder并没有比4通道的autoencoder更好，但当模型参数增加时，16通道的autoencoder的优势慢慢展示出来，当模型深度到22时，16通道的autoencoder明显优于4通道的autoencoder。不过这里8通道的autoencoder在FID上也不差于16通道的autoencoder，但FID只是图像质量的一个间接评价指标，并不能提现图像细节的差异，从重建效果上看，16通道的autoencoder应该优势更明显，而且当模型变大后，上限更高。

比较类似的是，之前Meta的文生图模型[Emu](https://arxiv.org/abs/2309.15807)也采用16通道的autoencoder来提升图像细节。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710028080032-19a56e26-c71e-4aef-a637-ba6cc9597631.png#averageHue=%23464b45&clientId=u31486502-bc18-4&from=paste&height=680&id=uf028abe4&originHeight=1496&originWidth=982&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=1270764&status=done&style=none&taskId=ua8743073-d092-423c-8d4c-3834baa72ae&title=&width=446.3636266889653" width="60%"/>
  <div align="center">
  </div>
</div>

而DALLE-3则是通过训练一个基于扩散模型的[latent decoder](https://github.com/openai/consistencydecoder)来解决4通道autoencoder的问题，但是不如直接采用16通道的autoencoder，直接从源头解决问题。

### 文本编码器

SD3的text encoder包含3个预训练好的模型：

- [CLIP ViT-L](https://huggingface.co/openai/clip-vit-large-patch14)：参数量约124M
- [OpenCLIP ViT-bigG](https://huggingface.co/laion/CLIP-ViT-bigG-14-laion2B-39B-b160k)：参数量约695M
- [T5-XXL encoder](https://huggingface.co/google/t5-v1_1-xxl)：参数量约4.7B

对比其他版本的Stable Diffusion 模型的text encoder
1. SD 1.x模型的text encoder使用CLIP ViT-L，
2. SD 2.x模型的text encoder采用OpenCLIP ViT-H，
3. 而SDXL的text encoder使用CLIP ViT-L + OpenCLIP ViT-bigG。
4. SD3更上一个台阶，加上了一个更大的T5-XXL encoder。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710043899488-d17b835d-e9bc-4a49-b8ac-09a988ce933f.png#averageHue=%23dae8bf&clientId=uc68c02ea-a127-4&from=paste&height=475&id=ub3a47cdd&originHeight=1046&originWidth=1198&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=164610&status=done&style=none&taskId=u2732b966-5048-41be-b52a-3a90ddfb711&title=&width=544.54544274275" width="60%"/>
  <div align="center">
  </div>
</div>

谷歌的[Imagen](https://arxiv.org/abs/2205.11487)最早使用T5-XXL encoder作为文生图模型的text encoder，并证明预训练好的纯文本模型可以实现更好的文本理解能力，后面的工作，如NVIDIA的[eDiff-I](https://research.nvidia.com/labs/dir/eDiff-I/)和Meta的[Emu](https://arxiv.org/abs/2309.15807)采用T5-XXL encoder + CLIP作为text encoder，OpenAI的DALL-E 3也采用T5-XXL encoder。SD3加入T5-XXL encoder也是模型在文本理解能力特别是文字渲染上提升的一个关键。

具体地，SD3总共提取两个层面的特征。

首先提取两个CLIP text encoder的pooled embedding，它们是文本的全局语义特征，维度大小分别是768和1280，两个embedding拼接在一起得到2048的embedding，然后经过一个MLP网络之后和timestep embedding相加。

然后是文本细粒度特征。这里也先分别提取两个CLIP模型的倒数第二层的特征，拼接在一起可以得到77x2048维度的CLIP text embeddings；同样地也从T5-XXL encoder提取最后一层的特征T5 text embeddings，维度大小是77x4096（这里也限制token长度为77）。然后对CLIP text embeddings使用zero-padding得到和T5 text embeddings同维度的特征。最后，将padding后的CLIP text embeddings和T5 text embeddings在token维度上拼接在一起，得到154x4096大小的混合text embeddings。text embeddings将通过一个linear层映射到与图像latent的patch embeddings同维度大小，并和patch embeddings拼接在一起送入MM-DiT中。

采用CLIP+T5-XXL encoder相比单独的T5-XXL encoder可能带来性能增益，但是一个不利的影响是CLIP text encoder只能默认编码77 tokens长度的文本，这也限制了T5-XXL encoder的token长度（T5-XXL encoder能够编码512 tokens）。DALL-E 3可以输入比较长的文本，而这里的SD3默认只能处理77 tokens长度的文本。

### MM-DiT

MM-DiT和DiT一样也是处理图像latent空间，这里先对图像的latent转成patches，这里的patch size=2x2，和DiT的默认配置是一样的。patch embedding再加上positional embedding送入transformer中。

这里的重点是如何处理前面说的文本特征。对于CLIP pooled embedding可以直接和timestep embedding加在一起，并像DiT中所设计的adaLN-Zero一样将特征插入transformer block。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710045264433-5b7383c3-0f6b-4b10-b819-7e381fe808dd.png#averageHue=%23c2d9b9&clientId=u877d4773-6aec-4&from=paste&height=415&id=ue135e485&originHeight=912&originWidth=1048&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=141666&status=done&style=none&taskId=u2c35a40d-4808-4ce6-8e84-0214557e44c&title=&width=476.36362603873283" width="60%"/>
  <div align="center">
  </div>
</div>

具体的实现代码如下所示：

```python
def modulate(x, shift, scale):
    return x * (1 + scale.unsqueeze(1)) + shift.unsqueeze(1)

class DiTBlock(nn.Module):
    """
    A DiT block with adaptive layer norm zero (adaLN-Zero) conditioning.
    """
    def __init__(self, hidden_size, num_heads, mlp_ratio=4.0, **block_kwargs):
        super().__init__()
        self.norm1 = nn.LayerNorm(hidden_size, elementwise_affine=False, eps=1e-6)
        self.attn = Attention(hidden_size, num_heads=num_heads, qkv_bias=True, **block_kwargs)
        self.norm2 = nn.LayerNorm(hidden_size, elementwise_affine=False, eps=1e-6)
        mlp_hidden_dim = int(hidden_size * mlp_ratio)
        approx_gelu = lambda: nn.GELU(approximate="tanh")
        self.mlp = Mlp(in_features=hidden_size, hidden_features=mlp_hidden_dim, act_layer=approx_gelu, drop=0)
        self.adaLN_modulation = nn.Sequential(
            nn.SiLU(),
            nn.Linear(hidden_size, 6 * hidden_size, bias=True)
        )

    def forward(self, x, c):
        shift_msa, scale_msa, gate_msa, shift_mlp, scale_mlp, gate_mlp = self.adaLN_modulation(c).chunk(6, dim=1)
        x = x + gate_msa.unsqueeze(1) * self.attn(modulate(self.norm1(x), shift_msa, scale_msa))
        x = x + gate_mlp.unsqueeze(1) * self.mlp(modulate(self.norm2(x), shift_mlp, scale_mlp))
        return x

```

对于序列的text embeddings，常规的处理方式是增加cross attention层来处理，其中text embeddings作为attention的keys和values，比如SD的UNet以及[PIXART-α](https://pixart-alpha.github.io/)（基于DiT）。但是SD3是直接将text embeddings和patch embeddings拼在一起处理，这样不需要额外引入cross-attention。由于text和image属于两个不同的模态，这里采用两套独立的参数来处理，即所有transformer层的学习参数是不共享的，但是共用一个self-attention来实现特征的交互。这等价于采用两个transformer模型来处理文本和图像，但在attention层连接，所以这是一个多模态模型，称之为MM-DiT。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710079070290-a538fc10-6f73-49ff-8bb3-73429ffb617c.png#averageHue=%23eeeeef&clientId=ud46937b5-a5c6-4&from=paste&height=236&id=u7fa7b3eb&originHeight=520&originWidth=596&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=46153&status=done&style=none&taskId=ucb055a89-66aa-48bb-b4f0-0f45a6046bc&title=&width=270.90908503729463" width="60%"/>
  <div align="center">
  </div>
</div>

MM-DiT和之前文生图模型的一个区别是文本特征不再只是作为一个条件，而是和图像特征同等对待处理。论文中也基于CC12M数据集将MM-DiT和其它架构做了对比实验，这里对比的模型有DiT（这里的DiT是指的不引入cross-attention，直接将text tokens和patches拼接，但只有一套参数），CrossDiT（额外引入cross-attention），UViT（UNet和transformer混合架构），还有3套参数的MM-DiT（CLIP text tokens，T5-XXL text tokens和patches各一套参数）。不同架构的模型表现如下所示：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710056801664-43f549d3-99f7-4bbe-958f-9da37f6ab0ba.png#averageHue=%23ededec&clientId=u8e1153aa-9cc4-4&from=paste&height=267&id=ua9e01bfe&originHeight=588&originWidth=990&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=278905&status=done&style=none&taskId=u77df6a8a-dd03-43c4-bf73-25c1aac8e10&title=&width=449.9999902465129" width="60%"/>
  <div align="center">
  </div>
</div>

可以看到MM-DiT是优于其它架构的，其中3套参数的MM-DiT略好于2套参数的MM-DiT，最终还是选择参数量更少的2套参数的MM-DiT。不过，这里和其它架构的对比是否保证了同参数大小，否则实验就显得有点不公平了。

MM-DiT的模型参数主要是模型的深度$d$，即transformer block的数量，此时对应的模型中间特征的维度大小是$64\cdot d$。这意味着当模型的深度$d$增大为$r\cdot d$，模型的参数量会增大$r^3$。比如深度为24的MM-DiT参数量为2B，最大的MM-DiT深度为38，其参数量为$2B*(38/24)^3\approx 8B$。

### QK-Normalization

为了提升混合精度训练的稳定性，MM-DiT的self-attention层还采用了QK-Normalization。当模型变大，而且在高分辨率图像上训练时，attention层的attention-logit（Q和K的矩阵乘）会变得不稳定，导致训练出现NAN。这里的解决方案是采用[RMSNorm](https://arxiv.org/abs/1910.07467)（简化版LayerNorm）对attention的Q和K进行归一化。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710058467147-3d36b382-82c6-4d77-ba67-d3276454ca02.png#averageHue=%23e9e9e9&clientId=ua5bc5921-c51e-4&from=paste&height=365&id=u25007bde&originHeight=802&originWidth=988&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=216160&status=done&style=none&taskId=u1301982c-020b-4534-8500-f64fce735f1&title=&width=449.090899357126" width="60%"/>
  <div align="center">
  </div>
</div>

### 变尺度位置编码

MM-DiT的位置编码和ViT一样采用2d的frequency embeddings（两个1d frequency embeddings进行concat）。SD3先在256x256尺寸下预训练，但最终会在以1024x1024为中心的多尺度上微调，这就需要MM-DiT的位置编码需要支持变尺度。SD3采用的解决方案是插值+扩展。

这里假定我们的目标分辨率的像素量为$S^2$，各个尺寸的图像满足$H\times W\approx S^2$(比如1024x1024，512x2048，2048x512），其中图像的宽和高最大分别为$H_{\text {max}}$和$W_{\text {max}}$。如果换算为MM-DiT的patches，有$h_{\text{max}}=H_{\text{max}}/16,w_{\text{max}}=W_{\text{max}}/16, s=S/16$，因为autoencoder下采样8x，而patch size为2x2，所以最终下采样16x。预训练模型的位置编码是在256x256下训练的，我们可以先通过插值的方式将位置编码应用到$S\times S$尺度上，此时相当于位置$p$处的网格值为$p\cdot\frac{256}{S}$，进一步地，我们可以将其扩展支持最大的宽和高，以高为例子，这里有$(p-\frac{h_{\text{max}}-s}{2})\cdot\frac{256}{S}$。对于不同的尺寸，我们只需要center crop出对应的2d网格进行embedding得到位置编码。下面的一个比较直观的示意图：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710060830033-04baa21a-9610-4c33-a5c1-acbc2183f0e6.png#averageHue=%23fdfbfa&clientId=u1bfa8ed1-197c-4&from=paste&height=315&id=u42944c6d&originHeight=694&originWidth=708&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=25693&status=done&style=none&taskId=ue49e223a-7bf7-48c8-b1fb-47852649599&title=&width=321.81817484296073" width="30%"/>
  <div align="center">
  </div>
</div>

### timestep schedule的shift

对高分辨率的图像，如果采用和低分辨率图像的一样的noise schedule，会出现对图像的破坏不够的情况，如下图所示（图源自[On the Importance of Noise Scheduling for Diffusion Models](https://arxiv.org/abs/2301.10972)）：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710061124200-58492ff4-882c-4751-b3f6-33dd80d39d5b.png#averageHue=%239da37e&clientId=ud6e82a60-3f2c-4&from=paste&height=285&id=ucdaa57f4&originHeight=628&originWidth=1948&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=1333797&status=done&style=none&taskId=u054cf05e-83a1-48df-86bd-b0528e9bff6&title=&width=885.4545262628354)

一个解决办法是对noise schedule进行偏移，对于RF模型来说，就是timestep schedule的shift。下面我们来理论分析如何进行shift。假定要处理的图像包含$n=H\times W$个像素，但它是一个常量图像，所有的像素值均为$c$。根据RF的前向过程，我们有$z_{t}=(1-t)c\mathbf {1}+t\epsilon$，这里$\mathbf {1},\epsilon\in\mathbb{R}^{n}$。$z_t$可以产生$n$个观察变量$Y=(1-t)c+t\eta$，我们可以计算出均值和标准差：$\mathbb{E}(Y)=(1-t)c, \sigma(Y)=t$。根据$z_t$我们可以估计出$c$，其中估计值$\hat{c}=\frac{1}{1-t}\frac{1}{n}\sum_{i=1}^{n}z_{t,i}$，其标准差为$\sigma(t,n)=\frac{t}{1-t}\sqrt{\frac{1}{n}}$。这里的标准差可以看成我们对$c$的破坏程度，可以看到当图像的宽和高都增大一倍时，破坏程度也相应降低了一倍。这里我们希望，分辨率$n$下的$\sigma(t_n,n)$和分辨率$m$下的$\sigma(t_m,m)$相同。求解可以得到：
$$t_{m}=\frac{\sqrt{\frac{m}{n}}t_{n}}{1+(\sqrt{\frac{m}{n}}-1)t_{n}}$$
根据上式，我们可以计算出SNR，有：
$$\lambda_{t_{m}}=2\log\frac{1-t_{m}}{t_m}=2\log\frac{1-t_{n}}{\sqrt{\frac{m}{n}}t_{n}}=\lambda_{t_{n}}-\log\frac{m}{n}$$
这意味两者的SNR要偏移一个$\log\frac{m}{n}$。当分辨率变成1024x1024，论文中是通过人工评测实验来选择最优的$\sqrt\frac{m}{n}$，实验最优值是3.0。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710063072517-27b10d5a-94d7-4704-b12b-9adb25a4bb2a.png#averageHue=%23856d4e&clientId=u6ae7a9d4-5c99-4&from=paste&height=423&id=uf8260f07&originHeight=930&originWidth=976&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=761184&status=done&style=none&taskId=ub20c3128-4a19-45d4-855b-570dc248a84&title=&width=443.6363540208046" width="60%"/>
  <div align="center">
  </div>
</div>

### 模型scaling

transformer一个比较大的优势是有好的scaling能力：当增大模型带来性能的稳定提升。论文中也选择了不同规模大小的MM-DiT进行实验，不同大小的网络深度分别是15，18，21，30，38，其中最大的模型参数量为8B。结论是MM-DiT同样表现了比较好的scaling能力，当模型变大后，性能稳步提升，如下图所示：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710072876414-84861915-7114-4b36-9037-2845420d2a37.png#averageHue=%23ededed&clientId=u65dfa064-d128-4&from=paste&height=475&id=udb111d76&originHeight=1046&originWidth=1974&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=567798&status=done&style=none&taskId=ubca5cf36-4dfe-4a5d-925b-0eb33cfa3e6&title=&width=897.272707824865)

这里的另外一个结论是validation loss可以作为一个很好的模型性能的衡量指标，它和文生图模型的一些评测指标如[CompBench](https://karine-h.github.io/T2I-CompBench/)和[GenEval](https://arxiv.org/abs/2310.11513)，以及人类偏好是正相关的。而且从目前的实验结果来看，还没有看到出现性能的饱和，这意味着继续增大模型，依然有可能继续提升。

下图展示了三个不同大小的模型生成图像的差异，可以看到大模型确实是质量最好的。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710073453446-52fa6fe1-4693-45a8-8e4a-55ae8b76e359.png#averageHue=%23ccc3b5&clientId=u65dfa064-d128-4&from=paste&height=299&id=u6f55e84f&originHeight=658&originWidth=2000&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=1459648&status=done&style=none&taskId=u42ffe689-c891-488e-9216-3b09b33e0fc&title=&width=909.0908893868947)

而且更大的模型不仅性能更好，而且生成时可以用较少的采样步数，比如当步数为5步时，大模型的性能下降要比小模型要低。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710073682350-92ae72d8-34e3-40a2-84eb-660f34536da2.png#averageHue=%23e1e1e1&clientId=u65dfa064-d128-4&from=paste&height=364&id=uc5ed8660&originHeight=800&originWidth=1222&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=162815&status=done&style=none&taskId=u172c5554-ba99-424b-8654-e77b158e13c&title=&width=555.4545334153927" width="60%"/>
  <div align="center">
  </div>
</div>

## 实现细节

这部分简单介绍一下SD3的一些实现细节，包括训练数据的处理以及训练参数等。

### 预训练数据处理

预训练数据集的大小和来源是没有的，但是预训练数据会进行一些筛选，包括：

1. 色情内容：使用NSFW检测模型来过滤。
2. 图像美学：使用评分系统移除预测分数较低的图像。
3. 重复内容：基于聚类的去重方法来移除训练数据中重复的图像，防止模型直接复制训练数据集中图像。（这部分策略附录部分很详细）

### 图像caption

和DALL-E 3一样，这里也对训练数据集中的图像生成高质量caption，这里使用的模型是多模态大模型[CogVLM](https://arxiv.org/abs/2311.03079)。训练过程中，使用50%的原始caption和50%的合成caption，使用合成caption能够提升模型性能，如下表所示。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710077033336-266d1b2f-cfe4-4d91-a829-afb79c08691f.png#averageHue=%23eaeaea&clientId=ufbd695b2-1ca1-4&from=paste&height=374&id=udc4a6ca5&originHeight=822&originWidth=1232&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=168366&status=done&style=none&taskId=u8b1a8838-619b-4d0a-b390-ddf500bac83&title=&width=559.9999878623271" width="60%"/>
  <div align="center">
  </div>
</div>

### 预计算图像和文本特征

为了减少训练过程中所需显存，这里预先计算好图像经过autoencoder编码得到的latent，以及文本对应的text embedding，特别是T5，可以节省接近20B的显存。同时预先计算好特征，也会节省一部分时间。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710077319739-7709b8d9-5290-4de5-b73a-ea633fe43af9.png#averageHue=%23ededed&clientId=ufbd695b2-1ca1-4&from=paste&height=275&id=uf7845797&originHeight=604&originWidth=2484&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=155796&status=done&style=none&taskId=u490f0a78-22c9-4b47-869a-ee3f24ac5d5&title=&width=1129.0908846185232)

但是预计算特征也不是没有代价的，首先是图像就不能做数据增强，好在文生图模型训练一般不太需要数据增强，其次需要一定的存储空间，而且加载特征也需要时间。预计算特征其实就是空间换时间。

### Classifier-Free Guidance

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710043899488-d17b835d-e9bc-4a49-b8ac-09a988ce933f.png#averageHue=%23dae8bf&clientId=uc68c02ea-a127-4&from=paste&height=475&id=ub3a47cdd&originHeight=1046&originWidth=1198&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=164610&status=done&style=none&taskId=u2732b966-5048-41be-b52a-3a90ddfb711&title=&width=544.54544274275" width="60%"/>
  <div align="center">
  </div>
</div>

训练过程需要对文本进行一定的drop来实现Classifier-Free Guidance，这里是三个text encoder各以46.4%的比例单独drop，这也意味着text完全drop的比例为$(46.4\%)^3\approx10\%$。

三个text encoder独立drop的一个好处是推理时可以灵活使用text encoder。比如，我们可以去掉比较吃显存的T5模型，只保留两个CLIP text encoder，实验发现这并不会影响视觉美感（没有T5的胜率为50%），并且只会导致文本遵循度略有下降（胜率为46%），这种情况包括文本提示词包含高度详细的场景描述或大量文字。然而，如果想生成文字，还是加上T5，没有T5的胜率只有38%。下面是一些具体的例子：

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710079180625-9e38bb96-f37b-4d7b-8cfb-c9a961a2e6e5.png#averageHue=%23cbc2b8&clientId=ud46937b5-a5c6-4&from=paste&height=580&id=uae41fe71&originHeight=1276&originWidth=1256&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=1451122&status=done&style=none&taskId=u07660504-1f87-4569-8d97-2087a78025a&title=&width=570.9090785349699" width="60%"/>
  <div align="center">
  </div>
</div>

### Direct Preference Optimization(DPO) 直接偏好优化

SD3最后基于DPO来进一步提升性能，DPO相比RLHF的一个优势不需要单独训练一个reward模型，而且直接基于成对的比较数据训练。

DPO目前已经成功应用在文生图上：[Diffusion Model Alignment Using Direct Preference Optimization](https://arxiv.org/abs/2311.12908)。SD3这里没有finetune整个网络，而是基于rank=128的LoRA，经过DPO后，图像生成质量有一定的提升，如下所示：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710080225202-ab0ee4c2-976d-4aed-afe6-40ba7bd923f4.png#averageHue=%23768753&clientId=u4b3e7416-8f0d-4&from=paste&height=615&id=ua020c3cd&originHeight=1352&originWidth=1708&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=3027510&status=done&style=none&taskId=uab9a93f7-3f98-40da-8597-ca0dcc92009&title=&width=776.3636195364081)

## 性能评测

性能评测包括定量评测和人工评测。

### 定量评测

定量评测基于GenEval，SD3和其它模型的对比如下所示，可以看到最大的模型在经过DPO后超过DALL-E 3。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710080365933-6ff71bc7-27e7-4792-a350-e9d533c8ed31.png#averageHue=%23e6e6e6&clientId=u4b3e7416-8f0d-4&from=paste&height=480&id=u8992a16c&originHeight=1056&originWidth=1346&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=276189&status=done&style=none&taskId=ub47b8866-a959-44b5-8e14-9bd1129159b&title=&width=611.8181685573801" width="60%"/>
  <div align="center">
  </div>
</div>

![image.png](https://cdn.nlark.com/yuque/0/2024/png/21973811/1710079812121-162e0aa0-2b94-4300-b686-a813bf2ebc48.png#averageHue=%23449695&clientId=u4b3e7416-8f0d-4&from=paste&height=1048&id=u1982f846&originHeight=2305&originWidth=3953&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=13739371&status=done&style=none&taskId=u99f09682-040c-4dd8-b1a0-dbf200e56dd&title=&width=1796.8181428731973)

### 人工评测

人工评测包括三个方面：
- **Prompt following**: Which image looks more representative to the text shown above and faithfully follows it?
- **Visual aesthetics**: Given the prompt, which image is of higher-quality and aesthetically more pleasing? 
- **Typography**: Which image more accurately shows/displays the text specified in the above description? More accurate spelling is preferred! Ignore other aspects.

评测结果如下所示，这里对比的模型有SOTA的模型：MJ-V6，Ideogram-V1.0，DALL-E 3，在文字生成方面，SD3基本大幅赢过其它模型（和Ideogram-V1.0相差上下），在图像质量和文本提示词遵循方面也和SOTA模型不相上下。

<div align="center">
<img src="https://cdn.nlark.com/yuque/0/2024/png/21973811/1710080613817-dd0cd8e0-3058-4398-8dc3-645f31f5e40a.png#averageHue=%23f5f3e3&clientId=u4b3e7416-8f0d-4&from=paste&height=408&id=u0154f149&originHeight=897&originWidth=1196&originalType=binary&ratio=2.200000047683716&rotation=0&showTitle=false&size=319593&status=done&style=none&taskId=u44b3bf4e-5120-4c6f-8a21-bb9775ea2cd&title=&width=543.6363518533631" width="60%"/>
  <div align="center">
  </div>
</div>

## 小结

SD3可以说是集大成者，基本上把业界最好的或者最成熟的方案都用上了，比如RF和DiT，以及DPO等等。

SD3的正式发布，也基本宣告文生图进入transformer时代了，现在的模型才是8B，未来更大的模型也定会出现。

## 参考

- [https://stability.ai/news/stable-diffusion-3-research-paper](https://stability.ai/news/stable-diffusion-3-research-paper)
- [https://arxiv.org/abs/2212.09748](https://arxiv.org/abs/2212.09748)
- [https://arxiv.org/abs/2403.03206](https://arxiv.org/abs/2403.03206)
- [https://arxiv.org/abs/2210.02747](https://arxiv.org/abs/2210.02747)
- [https://arxiv.org/abs/2303.00848](https://arxiv.org/abs/2303.00848)
- [https://arxiv.org/abs/2209.03003](https://arxiv.org/abs/2209.03003)
- [https://arxiv.org/abs/2209.14577](https://arxiv.org/abs/2209.14577)
