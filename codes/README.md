# Mini Sora Community Sora Reproduction Team

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

## Mini Sora Reproduction Goals

1. **GPU-Friendly**: It is best to have lower requirements on GPU memory size and number of GPUs, such as 8-card A100, 4-card A6000, single-card RTX4090 and other Computility for training and inference.
2. **Training-Efficiency** : You don’t need to train for too long to get better results
3. **Inference-Efficiency**: When generating videos through inference, the length and resolution are not required to be too high. For example, 3 to 10 seconds and 480p are acceptable.

There are mainly three candidate reproduction papers as the baseline for subsequent Sora reproduction. The community has (02/29) Fork the [OpenDiT](https://github.com/NUS-HPC-AI-Lab/OpenDiT) and [SiT](https://github.com/willisma/SiT) codes into the codes folder. Contributors are expected to submit PR to migrate the Baseline code to Sora Reproduction work up. [**Update**] 03/02, add [StableCascade](https://github.com/Stability-AI/StableCascade) codes


- DiT with **OpenDiT**
  - OpenDiT uses distributed training and uses 8-card A100 to generate images.
  - In addition, community members consulted the OpenDiT manager and got the following information
    - Using hundreds of graphics cards, more test videos can be produced from one month of training to March 15th.
    - To run Sora with OpenDiT, he estimates that at least thousands of cards are needed.If there are only a few cards, it can still be trained, but the effect is very poor. If there are not enough cards, when a video is used as a token, some can only be discarded during diffusion generation. , the video restoration degree is very low
  - OpenDiT uses sd's vae encoding and uses sd's pre-trained model, which may not be suitable for video generation data sets at all. Sora should have retrained vae and has a high compression rate.
  - Sora Leader has done DALLE3, and the decoding of the generated video uses a diffusion method similar to DALLE3, so the compression and encoding should be in the reverse direction of DALLE3.
- **SiT**
- **W.A.L.T**(Not released yet)
- **StableCascade**
  - ToDo: make it as a video-based model with additional temp layer in the near future

## Datasets

...

## Model architecture

...

## Computility demand

...

## Other projects

- Non-Sora one-click text generation video: [Text2Video](./Others/Text2Video.md)
  - Project Introduction: This is a text to video project that generates corresponding videos directly with just one click by inputting text.
  - Technology stack：
    - Text processing, Segment text, Generating prompts
    - Speech synthesis, converting text to speech, text to speech (TTS)，azure speech
    - Image generation, convert text into images，openai DALL·E
    - Video synthesis, combine pictures and speech into video，moviepy
  - Project requirements:
    - openai key，Generate images using DALL · E；
    - azure speech key，Convert text to speech。
  
<!-- 
**After submitting a PR or Issue**, You can apply to join the MiniSora contributor community and apply to join the Sora related paper reproduction group！

<div align="center">

<img src="assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>
-->

## Sora Reappearance Group-MiniSora Community WeChat Communication Group

<div align="center">

<img src="../assets/sora-reproduce.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mini-sora/minisora&type=Date)](https://star-history.com/#mini-sora/minisora&Date)

## How to contribute to the Mini Sora community

We really hope that you can contribute to the Mini Sora open source community and help us make it better than it is now!

Check specifically[Contribution Guide](../docs/CONTRIBUTING.md)

## Community contributor

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