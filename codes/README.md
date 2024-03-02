# Mini Sora 社区Sora复现小组
<!-- 
## Replication Group of Mini Sora

Welcome everyone to join the replication group! 

Please check out the latest updates and relevant materials on https://github.com/mini-sora/. 

Currently, the selected baseline papers for replication are **OpenDiT**(02/29), **SiT**(02/29), and **W.A.L.T**(after codes are released). 

Feel free to contribute with other improvements to replicate Sora.
-->
<div align="center">

<img src="../assets/logo.jpg" width="600"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

<div align="center">

[简体中文]([./README.md](./README.md)) | English

</div>

## Mini Sora 复现目标

1. **GPU-Friendly**: 最好对GPU内存大小和GPU数量要求较低,比如8卡A100,4KA6000,单卡Rtx4090之类的算力可以训练和推理
2. **Training-Efficiency** : 不需要训练太久即可有较好的效果
3. **Inference-Efficiency**: 推理生成视频时, 长度和分辨率不要求过高, 如3-10s,480p都是可接受的

候选复现论文主要有以下三篇, 来作为后续Sora复现的Baseline, 社区已经(02/29)将[OpenDiT](https://github.com/NUS-HPC-AI-Lab/OpenDiT)和[SiT](https://github.com/willisma/SiT)代码Fork到codes文件夹下, 期待贡献者提交PR, 将Baseline代码迁移到Sora复现工作上来. [**Update**] 03/02, 添加[StableCascade](https://github.com/Stability-AI/StableCascade) codes

- DiT with **OpenDiT**
  - OpenDiT采用分布式训练，生成图片采用8卡A100训练
  - 另外社区小伙伴咨询了OpenDiT负责人，得到如下信息
    - 采用百卡，训练一个月到3月15号可以出更多的测试视频
    - 用OpenDiT跑Sora，他估计最少要千卡，如果只有很少的卡也能训练起来，但是效果非常差，如果卡不够，一个视频做token时，只能丢弃一些，在扩散生成的时候，视频还原度很低
  - OpenDiT采用的sd的vae编码，采用的是sd的预训练模型，可能根本不适合视频生成数据集，Sora应该是重新训练了vae，压缩率高了
  - Sora Leader做过DALLE3，生成视频 的 解码 是用类似DALLE3的扩散方式, 所以压缩编码的时候应该是DALLE3的 反方向的方式
- **SiT**
- **W.A.L.T**(还未release)
- **StableCascade**
  - ToDo: make it as a video-based model with additional temp layer in the near future

## 数据集

...

## 模型架构

...

## 算力需求

...

<!-- 
**提交PR或者Issue后**, 可以申请加入MiniSora贡献者社群并申请加入 Sora 有关论文复现小组！

<div align="center">

<img src="assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>
-->

## Sora复现小组-MiniSora社区微信交流群

<div align="center">

<img src="../assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mini-sora/minisora&type=Date)](https://star-history.com/#mini-sora/minisora&Date)

## 如何向Mini Sora 社区贡献

我们非常希望你们能够为 Mini Sora 开源社区做出贡献，并且帮助我们把它做得比现在更好！

具体查看[贡献指南](../docs/CONTRIBUTING.md)

## 社区贡献者

<!-- readme: collaborators,contributors -start -->

<!-- readme: collaborators,contributors -end -->

<a href="https://github.com/mini-sora/minisora/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mini-sora/minisora" />
</a>
