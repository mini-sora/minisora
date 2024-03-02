# Mini Sora 社区Sora复现小组: Sora应用技术的分析
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


## 数据集
...


## 模型架构
...


## 算力需求
...



## Mini Sora 复现目标
1. **GPU-Friendly**: 最好对GPU内存大小和GPU数量要求较低,比如8卡A100,4KA6000,单卡Rtx4090之类的算力可以训练和推理
2. **Training-Efficiency** : 不需要训练太久即可有较好的效果
3. **Inference-Efficiency**: 推理生成视频时, 长度和分辨率不要求过高, 如3-10s,480p都是可接受的

候选复现论文主要有以下三篇, 来作为后续Sora复现的Baseline, 社区已经(02/29)将OpenDiT和SiT代码Fork到codes文件夹下, 期待贡献者提交PR, 将Baseline代码迁移到Sora复现工作上来.
- DiT with OpenDiT
- SiT
- W.A.L.T(还未release)
- StableCascade (03/02): ToDo: make it as a video-based model with additional temp layer in the near future

**提交PR或者Issue后**, 可以申请加入MiniSora贡献者社群并申请加入 Sora 有关论文复现小组！
<!-- 
<div align="center">

<img src="assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>
-->

## Mini Sora 微信社区社区交流群

<div align="center">

<img src="../assets/qrcode.png" width="200"/>
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
