# Mini Sora 社区

<div align="center">

<img src="assets/logo.jpg" width="600"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

<div align="center">

[简体中文](README.md) | [English](README_EN.md)

</div>

<p align="center">
    👋 加入我们的 <a href="https://cdn.vansin.top/minisora.jpg" target="_blank">微信社区</a>
</p>

Mini Sora 开源社区定位为由社区同学自发组织的开源社区（**免费不收取任何费用、不割韭菜**），Mini Sora 计划探索 Sora 的实现路径和后续的发展方向：

- 将定期举办 Sora 的圆桌和社区一起探讨可能性
- 视频生成的现有技术路径探讨

## 论文复现小组

### 复现目标
1. GPU-Green: 最好对GPU内存大小和GPU数量要求较低,比如8卡A100,4KA6000,单卡Rtx4090之类的算力可以训练和推理
2. 训练时长友好: 不需要训练太久即可有较好的效果
3. 生成视频长度和分辨率不要求过高, 如3-10s,480p都是可接受的

候选复现论文主要有以下三篇, 来作为后续Sora复现的Baseline, 社区已经(02/29)将OpenDiT和SiT代码Fork到codes文件夹下, 期待贡献者提交PR, 将Baseline代码迁移到Sora复现工作上来.

- DiT with OpenDiT
- SiT
- W.A.L.T(还未release)

**提交PR或者Issue后**, 可以申请加入MiniSora贡献者社群并申请加入 Sora 有关论文复现小组！
<!-- 
<div align="center">

<img src="assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>
-->
## 近期圆桌讨论

### Sora 夜谈之Video Diffusion 综述

**主讲**: 邢桢 复旦大学视觉与学习实验室博士生

**直播看点**: 图像生成扩散模型基础/文生视频扩散模型的发展/浅谈 Sora 背后技术和复现挑战

**在线直播时间**: 02/28 20:00-21:00

**回放微信视频号搜索**: 聊聊 Sora 之 Video Diffusion 综述

**PPT**: [飞书下载链接](https://aicarrier.feishu.cn/file/Ds0BbCAo6oTazdxxo3Zciw1Nnne)

## 论文共读计划

- **[Sora: Creating video from text](https://openai.com/sora) 技术报告**: [Video generation models as world simulators](https://openai.com/research/video-generation-models-as-world-simulators)
- **DiT**: [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748)
- **Latte**: [Latte: Latent Diffusion Transformer for Video Generation](https://maxin-cn.github.io/latte_project/)  [**latte论文精读翻译.pdf**](./notes/latte%E8%AE%BA%E6%96%87%E7%B2%BE%E8%AF%BB%E7%BF%BB%E8%AF%91.pdf)    [**Latte论文解读**](./notes/Latte.md)
- 更新中...

### 论文共读发表者募集

- [**DiT** Paper](https://github.com/orgs/mini-sora/discussions/39)
- [**Latte** Paper](https://github.com/orgs/mini-sora/discussions/38)

## 最近更新

- [**OpenDiT**: An Easy, Fast and Memory-Efficient System for DiT Training and Inference](https://github.com/NUS-HPC-AI-Lab/OpenDiT)

## 相关工作

| <h3>Diffusion Model</h3> |  |
| :------------- | :------------- |
| **论文**  | **链接** |
| 1) **Guided-Diffusion**: Diffusion Models Beat GANs on Image Synthesis | [**NeurIPS 21 Paper**](https://arxiv.org/abs/2105.05233), [Github](https://github.com/openai/guided-diffusion)|
| 2) **Latent Diffusion**: High-Resolution Image Synthesis with Latent Diffusion Models | [**CVPR 22 Paper**](https://arxiv.org/abs/2112.10752), [Github](https://github.com/CompVis/latent-diffusion) |
| 3) **EDM**: Elucidating the Design Space of Diffusion-Based Generative Models | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2206.00364), [Github](https://github.com/NVlabs/edm) |
| 4) **DDPM**: Denoising Diffusion Probabilistic Models | [**NeurIPS 20 Paper**](https://arxiv.org/abs/2006.11239), [Github](https://github.com/hojonathanho/diffusion) |
| 5) **DDIM**: Denoising Diffusion Implicit Models | [**ICLR 21 Paper**](https://arxiv.org/abs/2010.02502), [Github](https://github.com/ermongroup/ddim) |
| 6) **Score-Based Diffusion**: Score-Based Generative Modeling through Stochastic Differential Equations | [**ICLR 21 Paper**](https://arxiv.org/abs/2011.13456), [Github](https://github.com/yang-song/score_sde), [Blog](https://yang-song.net/blog/2021/score) |
| 7) **Stable Cascade**: Würstchen: An efficient architecture for large-scale text-to-image diffusion models | [**ICLR 24 Paper**](https://openreview.net/forum?id=gU58d5QeGv), [Github](https://github.com/Stability-AI/StableCascade), [Blog](https://stability.ai/news/introducing-stable-cascade) |
| 8) Diffusion Models in Vision: A Survey| [**TPAMI 23 Paper**](https://arxiv.org/abs/2011.13456), [Github](https://github.com/CroitoruAlin/Diffusion-Models-in-Vision-A-Survey)|
| <h3>Diffusion Transformer</h3> | |
| **论文**  | **链接** |
| 1) **UViT**: All are Worth Words: A ViT Backbone for Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2209.12152), [Github](https://github.com/baofff/U-ViT), [ModelScope](https://modelscope.cn/models?name=UVit&page=1) |
| 2) **DiT**: Scalable Diffusion Models with Transformers | [**ICCV 23 Paper**](https://arxiv.org/abs/2212.09748), [Github](https://github.com/facebookresearch/DiT),  [ModelScope](https://modelscope.cn/models?name=Dit&page=1)|
| 3) **SiT**: Exploring Flow and Diffusion-based Generative Models with Scalable Interpolant Transformers | [**Paper**](https://arxiv.org/abs/2401.08740), [Github](https://github.com/willisma/SiT), [ModelScope](https://modelscope.cn/models/AI-ModelScope/SiT-XL-2-256/summary)|
| 4) **FiT**: Flexible Vision Transformer for Diffusion Model | [**Paper**](https://arxiv.org/abs/2402.12376), [Github](https://github.com/whlzy/FiT) |
| 5) **k-diffusion**: Scalable High-Resolution Pixel-Space Image Synthesis with Hourglass Diffusion Transformers | [**Paper**](https://arxiv.org/pdf/2401.11605v1.pdf), [Github](https://github.com/crowsonkb/k-diffusion) |
| 6) **OpenDiT**: An Easy, Fast and Memory-Efficient System for DiT Training and Inference | [Github](https://github.com/NUS-HPC-AI-Lab/OpenDiT) |
| 7) **Large-DiT**: Large Diffusion Transformer | [Github](https://github.com/Alpha-VLLM/LLaMA2-Accessory/tree/main/Large-DiT) |
| <h3>Video Generation</h3> | |
| **论文**  | **链接** |
| 1) **Animatediff**: Animate Your Personalized Text-to-Image Diffusion Models without Specific Tuning | [**ICLR 24 Paper**](https://arxiv.org/abs/2307.04725), [Github](https://github.com/guoyww/animatediff/), [ModelScope](https://modelscope.cn/models?name=Animatediff&page=1) |
| 2) **I2VGen-XL**: High-Quality Image-to-Video Synthesis via Cascaded Diffusion Models | [**Paper**](https://arxiv.org/abs/2311.04145), [Github](https://github.com/ali-vilab/i2vgen-xl),  [ModelScope](https://modelscope.cn/models/iic/i2vgen-xl/summary)|
| 3) **Imagen Video**: High Definition Video Generation with Diffusion Models | [**Paper**](https://arxiv.org/abs/2210.02303) |
| 4) **MoCoGAN**: Decomposing Motion and Content for Video Generation | [**CVPR 18 Paper**](https://arxiv.org/abs/1707.04993) |
| 5) Adversarial Video Generation on Complex Datasets | [**Paper**](https://arxiv.org/abs/1907.06571) |
| 6) **W.A.L.T**: Photorealistic Video Generation with Diffusion Models | [**Paper**](https://arxiv.org/abs/2312.06662) [Project](https://walt-video-diffusion.github.io/)|
| 7) **VideoGPT**: Video Generation using VQ-VAE and Transformers | [**Paper**](https://arxiv.org/abs/2104.10157), [Github](https://github.com/wilson1yan/VideoGPT) |
| 8) Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2204.03458), [Github](https://github.com/lucidrains/video-diffusion-pytorch), [Project](https://video-diffusion.github.io/)|
| 9) **MCVD**: Masked Conditional Video Diffusion for Prediction, Generation, and Interpolation | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2205.09853), [Github](https://github.com/voletiv/mcvd-pytorch), [Project](https://mask-cond-video-diffusion.github.io/), [Blog](https://ajolicoeur.ca/2022/05/22/masked-conditional-video-diffusion/) |
| 10) **VideoPoet**: A Large Language Model for Zero-Shot Video Generation | [**Paper**](https://arxiv.org/abs/2312.14125) |
| 11) **MAGVIT**: Masked Generative Video Transformer | [**CVPR 23 Paper**](https://arxiv.org/abs/2212.05199), [Github](https://github.com/google-research/magvit), [Project](https://magvit.cs.cmu.edu/), [Colab](https://github.com/google-research/magvit/blob/main) |
| 12) **EMO**: Emote Portrait Alive - Generating Expressive Portrait Videos with Audio2Video Diffusion Model under Weak Conditions | [**Paper**](https://arxiv.org/abs/2402.17485), [Github](https://github.com/HumanAIGC/EMO), [Project](https://humanaigc.github.io/emote-portrait-alive/) |
| 13) **SimDA**: Simple Diffusion Adapter for Efficient Video Generation | [**Paper**](https://arxiv.org/pdf/2308.09710.pdf), [Github](https://github.com/ChenHsing/SimDA), [Project](https://chenhsing.github.io/SimDA/) |
| 14) **StableVideo**: Text-driven Consistency-aware Diffusion Video Editing | [**ICCV 23 Paper**](https://arxiv.org/abs/2308.09592), [Github](https://github.com/rese1f/StableVideo), [Project](https://rese1f.github.io/StableVideo/) |
| 15) **SVD**: Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets| [**Paper**](https://static1.squarespace.com/static/6213c340453c3f502425776e/t/655ce779b9d47d342a93c890/1700587395994/stable_video_diffusion.pdf), [Github](https://github.com/Stability-AI/generative-models)|
| 16) **ADD**: Adversarial Diffusion Distillation| [**Paper**](https://static1.squarespace.com/static/6213c340453c3f502425776e/t/65663480a92fba51d0e1023f/1701197769659/adversarial_diffusion_distillation.pdf), [Github](https://github.com/Stability-AI/generative-models) |
| <h3>Long-context</h3> | |
| **论文**  | **链接** |
| 1) World Model on Million-Length Video And Language With RingAttention | [**Paper**](https://arxiv.org/abs/2402.08268), [Github](https://github.com/LargeWorldModel/LWM) |
| 2) Ring Attention with Blockwise Transformers for Near-Infinite Context | [**Paper**](https://arxiv.org/abs/2310.01889), [Github](https://github.com/lhao499/RingAttention) |
| 3) Extending LLMs' Context Window with 100 Samples | [**Paper**](https://arxiv.org/abs/2401.07004), [Github](https://github.com/GAIR-NLP/Entropy-ABF) |
| 4) Efficient Streaming Language Models with Attention Sinks | [**ICLR 24 Paper**](https://arxiv.org/abs/2309.17453), [Github](https://github.com/mit-han-lab/streaming-llm) |
| 5) The What, Why, and How of Context Length Extension Techniques in Large Language Models – A Detailed Survey | [**Paper**](https://arxiv.org/pdf/2401.07872) |
| 6) **MovieChat**: From Dense Token to Sparse Memory for Long Video Understanding | [**CVPR 24 Paper**](https://arxiv.org/abs/2307.16449), [Github](https://github.com/rese1f/MovieChat), [Project](https://rese1f.github.io/MovieChat/) |
| <h3>Base Video Models</h3> | |
| **论文**  | **链接** |
| 1) **ViViT**: A Video Vision Transformer | [**ICCV 21 Paper**](https://arxiv.org/pdf/2103.15691v2.pdf), [Github](https://github.com/google-research/scenic) |
| 2) **VideoLDM**: Align your Latents: High-Resolution Video Synthesis with Latent Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2304.08818) |
| 3) **LVDM**: Latent Video Diffusion Models for High-Fidelity Long Video Generation | [**Paper**](https://arxiv.org/abs/2211.13221), [Github](https://github.com/YingqingHe/LVDM) |
| 4) **LFDM**: Conditional Image-to-Video Generation with Latent Flow Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2304.08818), [Github](https://github.com/nihaomiao/CVPR23_LFDM) |
| 5) **MotionDirector**: Motion Customization of Text-to-Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.08465), [Github](https://github.com/showlab/MotionDirector) |
| <h3>Audio Related Resource</h3> | |
| **论文**  | **链接** |
| 1) **Stable Audio**: Fast Timing-Conditioned Latent Audio Diffusion | [Link](https://stability.ai/research/stable-audio-efficient-timing-latent-diffusion)|
| <h3>一致性/Consistency </h3> | |
| **论文**  | **链接** |
| 1) Layered Neural Atlases for Consistent Video Editing | [**TOG 21 Paper**](https://arxiv.org/pdf/2109.11418.pdf), [Github](https://github.com/ykasten/layered-neural-atlases), [Project](https://layered-neural-atlases.github.io/), |
| 2) **StableVideo**: Text-driven Consistency-aware Diffusion Video Editing | [**ICCV 23 Paper**](https://arxiv.org/abs/2308.09592), [Github](https://github.com/rese1f/StableVideo), [Project](https://rese1f.github.io/StableVideo/) |
| 3) **CoDeF**: Content Deformation Fields for Temporally Consistent Video Processing | [Paper](https://arxiv.org/pdf/2308.07926.pdf), [Github](https://github.com/qiuyu96/CoDeF), [Project](https://qiuyu96.github.io/CoDeF/) |
| <h3>现有高质量资料</h3> | |
| **资料**  | **链接** |
| 1) Datawhale - AI视频生成学习 | [Feishu doc](https://datawhaler.feishu.cn/docx/G4LkdaffWopVbwxT1oHceiv9n0c) |
| 2) A Survey on Generative Diffusion Model | [**TKDE 24 Paper**](https://arxiv.org/pdf/2209.02646.pdf), [Github](https://github.com/chq1155/A-Survey-on-Generative-Diffusion-Model) |
| 3) Awesome-Video-Diffusion-Models: A Survey on Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.10647), [Github](https://github.com/ChenHsing/Awesome-Video-Diffusion-Models) |
| 4) Awesome-Text-To-Video：A Survey on Text-to-Video Generation/Synthesis  | [Github](https://github.com/jianzhnie/awesome-text-to-video)
| 5) video-generation-survey: A reading list of video generation| [Github](https://github.com/yzhang2016/video-generation-survey)
| 6) Awesome-Video-Diffusion |  [Github](https://github.com/showlab/Awesome-Video-Diffusion) |
| 7) Video Generation Task in Papers With Code |  [Link](https://paperswithcode.com/task/video-generation) |
| 8) Sora: A Review on Background, Technology, Limitations, and Opportunities of Large Vision Models |  [**Paper**](https://arxiv.org/abs/2402.17177), [Github](https://github.com/lichao-sun/SoraReview) |
| 9) Open-Sora-Plan (PKU-YuanGroup) |  [Github](https://github.com/PKU-YuanGroup/Open-Sora-Plan) |

## Mini Sora 微信社区社区交流群

<div align="center">

<img src="assets/qrcode.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mini-sora/minisora&type=Date)](https://star-history.com/#mini-sora/minisora&Date)

## 如何向Mini Sora 社区贡献

我们非常希望你们能够为 Mini Sora 开源社区做出贡献，并且帮助我们把它做得比现在更好！

具体查看[贡献指南](./docs/CONTRIBUTING.md)

## 社区贡献者

<!-- readme: collaborators,contributors -start -->

<!-- readme: collaborators,contributors -end -->

<a href="https://github.com/mini-sora/minisora/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mini-sora/minisora" />
</a>

