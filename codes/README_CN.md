# Mini Sora 社区Sora复现小组

<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![Stargazers][stars-shield]][stars-url]
<br />

<!-- PROJECT LOGO -->
<div align="center">

<img src="../assets/logo.jpg" width="600"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

<div align="center">

[English](README.md) | [简体中文](https://github.com/mini-sora/minisora/blob/main/README_CN.md)  


</div>

## Mini Sora 复现目标

1. **GPU-Friendly**: 最好对GPU内存大小和GPU数量要求较低,比如8卡A100,4KA6000,单卡Rtx4090之类的算力可以训练和推理
2. **Training-Efficiency** : 不需要训练太久即可有较好的效果
3. **Inference-Efficiency**: 推理生成视频时, 长度和分辨率不要求过高, 如3-10s,480p都是可接受的

候选复现论文主要有以下三篇, 来作为后续Sora复现的Baseline, 社区已经(02/29)将[OpenDiT](https://github.com/NUS-HPC-AI-Lab/OpenDiT)和[SiT](https://github.com/willisma/SiT)代码Fork到codes文件夹下, 期待贡献者提交PR, 将Baseline代码迁移到Sora复现工作上来. [**Update**] 03/02, 添加[StableCascade](https://github.com/Stability-AI/StableCascade) codes

- DiT with **OpenDiT**
  - OpenDiT采用分布式训练，生成图片采用8卡A100训练。
  - OpenDiT采用的sd的vae编码，采用的是sd的预训练模型，实测出来效果会比VideoGPT的vqvae效果更好。
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

## 其他项目

- 非Sora一键文本生成视频 : [Text2Video](./Others/Text2Video.md)
  - 项目介绍: 这是一个文本转视频的项目，通过输入文本，一键直接生成对应的视频。
  - 技术栈：
    - 文本处理，分割文本，生成 prompt
    - 语音合成，将文本转换为语音 text to speech (TTS)，azure speech
    - 图片生成，将文本转成图片，openai DALL·E
    - 视频合成，将图片和语音合成视频，moviepy
  - 项目要求:
    - openai key，用 DALL·E 生成图片；
    - azure speech key，将文本转成语音。
  
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

[contributors-shield]: https://img.shields.io/github/contributors/mini-sora/minisora.svg?style=flat-square
[contributors-url]: https://github.com/mini-sora/minisora/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/mini-sora/minisora.svg?style=flat-square
[forks-url]: https://github.com/mini-sora/minisora/network/members
[stars-shield]: https://img.shields.io/github/stars/mini-sora/minisora.svg?style=flat-square
[stars-url]: https://github.com/mini-sora/minisora/stargazers
[issues-shield]: https://img.shields.io/github/issues/mini-sora/minisora.svg?style=flat-square
[issues-url]: https://img.shields.io/github/issues/mini-sora/minisora.svg
[license-shield]: https://img.shields.io/github/license/mini-sora/minisora.svg?style=flat-square
[license-url]: https://github.com/mini-sora/minisora/blob/main/LICENSE
