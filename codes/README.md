# Mini Sora Community Sora Replication Team

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

English | [简体中文](./README_CN.md)  

</div>

## Mini Sora Replication Goals

1. **GPU-Friendly**: Preferably, the model should have low GPU memory requirements and be able to train and infer on hardware such as 8-card A100, 4-card A6000, or single-card RTX4090.
2. **Training Efficiency**: The model should achieve good results without requiring excessively long training times.
3. **Inference Efficiency**: When generating videos during inference, the length and resolution of the videos should not be excessively high; for example, lengths of 3-10 seconds and resolutions of 480p are acceptable.

The three candidate papers for replication, which will serve as baselines for future Sora replication, are already (as of 02/29) forked into the "codes" directory by the community. We look forward to contributors submitting pull requests to migrate the baseline code to the Sora replication effort. [**Update**] 03/02, Added [StableCascade](https://github.com/Stability-AI/StableCascade) codes.

* DiT with **OpenDiT**
  * OpenDiT adopts distributed training and trains image generation using 8-card A100.
  * Additionally, community members consulted the OpenDiT project lead and received the following information:
    - Training with hundreds of cards could produce more test videos by March 15th.
    - Running Sora with OpenDiT would ideally require thousands of cards. While it's possible to train with fewer cards, the results would be subpar. If there aren't enough cards, some tokens in a video may need to be discarded during tokenization, resulting in poor video reconstruction during diffusion generation.
  * OpenDiT utilizes SD's VAE encoding with pretrained models, which may not be suitable for video generation datasets. Sora likely retrained the VAE, resulting in higher compression rates.
  * The Sora team, having worked on DALLE3, employs a diffusion-like decoding method for video generation. Thus, during compression encoding, they likely utilize a reverse process similar to DALLE3.

- **SiT**
- **W.A.L.T**(Not yet released)
- **StableCascade**
  - ToDo: make it as a video-based model with additional temp layer in the near future

## Dataset

...

## Model Architecture

...

## Computational Requirements

...

## Other Projects

- Non-Sora One-Click Text-to-Video Generation: [Text2Video](./Others/Text2Video.md)

  - Project Description: This is a project for generating videos directly from text input with a single click.
- Technology Stack:
    - Text processing, text segmentation, and prompt generation
    - Speech synthesis, converting text to speech (TTS) using Azure Speech
    - Image generation, converting text to images using OpenAI DALL·E
    - Video composition, combining images and speech to generate videos using MoviePy
  - Project Requirements:
    - OpenAI key for using DALL·E to generate images
    - Azure Speech key for converting text to speech

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