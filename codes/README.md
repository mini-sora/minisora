# Mini Sora Community Sora Reproduction Group

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

[English](./README.md)| [简体中文](./README_CN.md)  

</div>


## Mini Sora Reproduction Objectives

1. **GPU-Friendly**: Ideally, it should have low requirements for GPU memory size and the number of GPUs, such as training and inference on 8 A100 cards, 4K A6000 cards, or a single RTX 4090 card.
2. **Training-Efficiency** : It should achieve good results without requiring long training periods.
3. **Inference-Efficiency**: For video generation, there is no stringent requirement for the length and resolution of the produced videos. For instance, generating videos that are 3 to 10 seconds long with a resolution of 480p is considered acceptable.

The candidate papers for replication primarily include the following three, serving as baselines for subsequent Sora replication efforts. The community has, as of February 29th, forked the [OpenDiT](https://github.com/NUS-HPC-AI-Lab/OpenDiT) and [SiT](https://github.com/willisma/SiT) into the codes folder, looking forward to contributors submitting PRs to migrate the baseline codes to the Sora replication project. [**Update**] On March 2nd, [StableCascade](https://github.com/Stability-AI/StableCascade) codes were added.


- DiT with **OpenDiT**
  - OpenDiT utilizes distributed training for image generation, employing a setup with 8 A100 GPUs for the training process.
  - OpenDiT employs the VAE encoding from Stable Diffusion, utilizing its pre-trained model. In practice, this has been found to yield better results than the vqvae used in VideoGPT.
  - The Sora Leader has experience with DALLE3, and the video generation process utilizes a decoding method similar to the diffusion approach used in DALLE3. Therefore, the encoding process for compression should be the reverse of DALLE3's method.
- **SiT**
- **W.A.L.T**(not release)

- **StableCascade**
  - ToDo: make it as a video-based model with additional temp layer in the near future

## Dataset

...

## Model Architecture

...


## Computational Power Requirements

...


<!-- 
**After submitting a PR or Issue**, you can apply to join the Mini Sora contributors community and request to join the Sora-related paper replication group!

<div align="center">

<img src="assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>
-->


## Sora Replication Team - MiniSora Community WeChat Discussion Group


<div align="center">

<img src="../assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mini-sora/minisora&type=Date)](https://star-history.com/#mini-sora/minisora&Date)

## How to Contribute to the Mini Sora Community


We greatly appreciate your contributions to the Mini Sora open-source community and helping us make it even better than it is now!

For more details, please refer to the [Contribution Guidelines](../docs/CONTRIBUTING.md)

## Community contributors


<!-- readme: collaborators,contributors -start -->

<!-- readme: collaborators,contributors -end -->

<a href="https://github.com/mini-sora/minisora/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mini-sora/minisora" />
</a>

[your-project-path]: mini-sora/minisora
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