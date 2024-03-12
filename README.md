# Mini Sora Community

<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![Stargazers][stars-shield]][stars-url]
<br />

<!-- PROJECT LOGO -->
<div align="center">
<img src="assets/logo.jpg" width="600"/>

  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

<div align="center">

English | [简体中文](README_zh-CN.md)

</div>

<p align="center">
    👋 join us on  <a href="https://cdn.vansin.top/minisora.jpg" target="_blank">WeChat</a>
</p>

The Mini Sora open-source community is positioned as a community-driven initiative (**free of charge and devoid of any exploitation**) organized spontaneously by community members. The Mini Sora project aims to explore the implementation path and future development direction of Sora.

- Regular round-table discussions will be held with the Sora team and the community to explore possibilities.
- We will delve into existing technological pathways for video generation.

## Hot News

- [**Stable Diffusion 3**: MM-DiT: Scaling Rectified Flow Transformers for High-Resolution Image Synthesis](https://stability.ai/news/stable-diffusion-3-research-paper)
- [Minisora与Sora复现最新进展](./docs/survey_README_zh-CN.md)
![](./docs/Minisora_LPRS/0001.jpg)

## [Reproduction Group of MiniSora Community](./codes/README.md)

### Sora Reproduction Goals of MiniSora

1. **GPU-Friendly**: Ideally, it should have low requirements for GPU memory size and the number of GPUs, such as being trainable and inferable with compute power like 8 A100 80G cards, 8 A6000 48G cards, or RTX4090 24G.
2. **Training-Efficiency**: It should achieve good results without requiring extensive training time.
3. **Inference-Efficiency**: When generating videos during inference, there is no need for high length or resolution; acceptable parameters include 3-10 seconds in length and 480p resolution.

### [MiniSora-DiT](../minisora-DiT/README.md): Reproducing the DiT Paper with XTuner

[https://github.com/mini-sora/minisora-DiT](../minisora-DiT/README.md)

#### Requirements

We are recruiting MiniSora Community contributors to reproduce `DiT` using [XTuner](https://github.com/internLM/xtuner).

We hope the community member has the following characteristics:

1. Familiarity with the `OpenMMLab MMEngine` mechanism.
2. Familiarity with `DiT`.

#### Background

1. The author of `DiT` is the same as the author of `Sora`.
2. [XTuner](https://github.com/internLM/xtuner) has the core technology to efficiently train sequences of length `1000K`.

#### Support

1. Computational resources: 2*A100.
2. Strong supports from [XTuner](https://github.com/internLM/xtuner) core developer [P佬@pppppM](https://github.com/pppppM).

## Recent round-table Discussions

### Paper Interpretation of Stable Diffusion 3 paper: MM-DiT

**Speaker**: MMagic Core Contributors

**Live Streaming Time**: 03/12 20:00

**Highlights**: MMagic core contributors will lead us in interpreting the Stable Diffusion 3 paper, discussing the architecture details and design principles of Stable Diffusion 3. 

**PPT**: [FeiShu Link](https://aicarrier.feishu.cn/file/NXnTbo5eqo8xNYxeHnecjLdJnQq)

<!-- Please scan the QR code with WeChat to book a live video session.

<div align="center">
<img src="assets/SD3论文领读.png" width="100"/>

  <div>&nbsp;</div>
  <div align="center">
  </div>
</div> -->

### Highlights from Previous Discussions

#### [**Night Talk with Sora: Video Diffusion Overview**](https://github.com/mini-sora/minisora/blob/main/notes/README.md)

**ZhiHu Notes**: [A Survey on Generative Diffusion Model: An Overview of Generative Diffusion Models](https://zhuanlan.zhihu.com/p/684795460)

## [Paper Reading Program](./notes/README.md)

- [**Sora**: Creating video from text](https://openai.com/sora)
- **Technical Report**: [Video generation models as world simulators](https://openai.com/research/video-generation-models-as-world-simulators)
- **Latte**: [Latte: Latent Diffusion Transformer for Video Generation](https://maxin-cn.github.io/latte_project/)
  - [Latte Paper Interpretation (zh-CN)](./notes/Latte.md), [ZhiHu(zh-CN)](https://zhuanlan.zhihu.com/p/686407292)
- **DiT**: [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748)
- **Stable Cascade (ICLR 24 Paper)**: [Würstchen: An efficient architecture for large-scale text-to-image diffusion models](https://openreview.net/forum?id=gU58d5QeGv)
- [**Stable Diffusion 3**: MM-DiT: Scaling Rectified Flow Transformers for High-Resolution Image Synthesis](https://stability.ai/news/stable-diffusion-3-research-paper)
  - [SD3 Paper Interpretation (zh-CN)](./notes/SD3_zh-CN.md), [ZhiHu(zh-CN)](https://zhuanlan.zhihu.com/p/686273242)

- Updating...

### Recruitment of Presenters

- [**DiT** (ICCV 23 Paper)](https://github.com/orgs/mini-sora/discussions/39)
- [**Stable Cascade** (ICLR 24 Paper)](https://github.com/orgs/mini-sora/discussions/145)

## Related Work

- 1 [Diffusion Model](#diffusion-models)
- 2 [Diffusion Transformer](#diffusion-transformer)
- 3 [Baseline Video Generation Models](#baseline-video-generation-models)
- 4 [Video Generation](#video-generation)
- 5 [Dataset](#dataset)
- 6 [Patchifying Methods](#patchifying-methods)
- 7 [Long-context](#long-context)
- 8 [Audio Related Resource](#audio-related-resource)
- 9 [Consistency](#consistency)
- 10 [Prompt Engineering](#prompt-engineering)
- 11 [Security](#security)
- 12 [World Model](#world-model)
- 13 [Video Compression](#video-compression)
- 14 [Mamba](#Mamba)
    - 14.1 [Theoretical Foundations and Model Architecture](#theoretical-foundations-and-model-architecture)
    - 14.2 [Image Generation and Visual Applications](#image-generation-and-visual-applications)
    - 14.3 [Video Processing and Understanding](#video-processing-and-understanding)
    - 14.4 [Medical Image Processing](#medical-image-processing)
- 15 [Existing high-quality resources](#existing-high-quality-resources)

| <h3 id="diffusion-models">Diffusion Models</h3> |  |
| :------------- | :------------- |
| **Paper** | **Link** |
| 1) **Guided-Diffusion**: Diffusion Models Beat GANs on Image Synthesis | [**NeurIPS 21 Paper**](https://arxiv.org/abs/2105.05233), [GitHub](https://github.com/openai/guided-diffusion)|
| 2) **Latent Diffusion**: High-Resolution Image Synthesis with Latent Diffusion Models | [**CVPR 22 Paper**](https://arxiv.org/abs/2112.10752), [GitHub](https://github.com/CompVis/latent-diffusion) |
| 3) **EDM**: Elucidating the Design Space of Diffusion-Based Generative Models | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2206.00364), [GitHub](https://github.com/NVlabs/edm) |
| 4) **DDPM**: Denoising Diffusion Probabilistic Models | [**NeurIPS 20 Paper**](https://arxiv.org/abs/2006.11239), [GitHub](https://github.com/hojonathanho/diffusion) |
| 5) **DDIM**: Denoising Diffusion Implicit Models | [**ICLR 21 Paper**](https://arxiv.org/abs/2010.02502), [GitHub](https://github.com/ermongroup/ddim) |
| 6) **Score-Based Diffusion**: Score-Based Generative Modeling through Stochastic Differential Equations | [**ICLR 21 Paper**](https://arxiv.org/abs/2011.13456), [GitHub](https://github.com/yang-song/score_sde), [Blog](https://yang-song.net/blog/2021/score) |
| 7) **Stable Cascade**: Würstchen: An efficient architecture for large-scale text-to-image diffusion models | [**ICLR 24 Paper**](https://openreview.net/forum?id=gU58d5QeGv), [GitHub](https://github.com/Stability-AI/StableCascade), [Blog](https://stability.ai/news/introducing-stable-cascade) |
| 8) Diffusion Models in Vision: A Survey| [**TPAMI 23 Paper**](https://arxiv.org/abs/2011.13456), [GitHub](https://github.com/CroitoruAlin/Diffusion-Models-in-Vision-A-Survey)|
| <h3 id="diffusion-transformer">Diffusion Transformer</h3> | |
| **Paper** | **Link** |
| 1) **UViT**: All are Worth Words: A ViT Backbone for Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2209.12152), [GitHub](https://github.com/baofff/U-ViT), [ModelScope](https://modelscope.cn/models?name=UVit&page=1) |
| 2) **DiT**: Scalable Diffusion Models with Transformers | [**ICCV 23 Paper**](https://arxiv.org/abs/2212.09748), [GitHub](https://github.com/facebookresearch/DiT), [Project](https://www.wpeebles.com/DiT), [ModelScope](https://modelscope.cn/models?name=Dit&page=1)|
| 3) **SiT**: Exploring Flow and Diffusion-based Generative Models with Scalable Interpolant Transformers | [**Paper**](https://arxiv.org/abs/2401.08740), [GitHub](https://github.com/willisma/SiT), [ModelScope](https://modelscope.cn/models/AI-ModelScope/SiT-XL-2-256/summary)|
| 4) **FiT**: Flexible Vision Transformer for Diffusion Model | [**Paper**](https://arxiv.org/abs/2402.12376), [GitHub](https://github.com/whlzy/FiT) |
| 5) **k-diffusion**: Scalable High-Resolution Pixel-Space Image Synthesis with Hourglass Diffusion Transformers | [**Paper**](https://arxiv.org/pdf/2401.11605v1.pdf), [GitHub](https://github.com/crowsonkb/k-diffusion) |
| 6) **Large-DiT**: Large Diffusion Transformer | [GitHub](https://github.com/Alpha-VLLM/LLaMA2-Accessory/tree/main/Large-DiT) |
| 7) **VisionLLaMA**: A Unified LLaMA Interface for Vision Tasks | [**Paper**](https://arxiv.org/abs/2403.00522), [GitHub](https://github.com/Meituan-AutoML/VisionLLaMA) |
| 8) **Stable Diffusion 3**: MM-DiT: Scaling Rectified Flow Transformers for High-Resolution Image Synthesis | [**Paper**](https://stabilityai-public-packages.s3.us-west-2.amazonaws.com/Stable+Diffusion+3+Paper.pdf), [Blog](https://stability.ai/news/stable-diffusion-3-research-paper) |
| <h3 id="baseline-video-generation-models">Baseline Video Generation Models</h3> | |
| **Paper** | **Link** |
| 1) **ViViT**: A Video Vision Transformer | [**ICCV 21 Paper**](https://arxiv.org/pdf/2103.15691v2.pdf), [GitHub](https://github.com/google-research/scenic) |
| 2) **VideoLDM**: Align your Latents: High-Resolution Video Synthesis with Latent Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2304.08818) |
| 3) **DiT**: Scalable Diffusion Models with Transformers | [**ICCV 23 Paper**](https://arxiv.org/abs/2212.09748), [Github](https://github.com/facebookresearch/DiT), [Project](https://www.wpeebles.com/DiT), [ModelScope](https://modelscope.cn/models?name=Dit&page=1)|
| 4) **Text2Video-Zero**: Text-to-Image Diffusion Models are Zero-Shot Video Generators | [**Paper**](https://arxiv.org/abs/2303.13439), [GitHub](https://github.com/Picsart-AI-Research/Text2Video-Zero) |
| 5) **Latte**: Latent Diffusion Transformer for Video Generation | [**Paper**](https://arxiv.org/pdf/2401.03048v1.pdf), [GitHub](https://github.com/Vchitect/Latte), [Project](https://maxin-cn.github.io/latte_project/)|
| <h3 id="video-generation">Video Generation</h3> | |
| **Paper** | **Link** |
| 1) **Animatediff**: Animate Your Personalized Text-to-Image Diffusion Models without Specific Tuning | [**ICLR 24 Paper**](https://arxiv.org/abs/2307.04725), [GitHub](https://github.com/guoyww/animatediff/), [ModelScope](https://modelscope.cn/models?name=Animatediff&page=1) |
| 2) **I2VGen-XL**: High-Quality Image-to-Video Synthesis via Cascaded Diffusion Models | [**Paper**](https://arxiv.org/abs/2311.04145), [GitHub](https://github.com/ali-vilab/i2vgen-xl),  [ModelScope](https://modelscope.cn/models/iic/i2vgen-xl/summary)|
| 3) **Imagen Video**: High Definition Video Generation with Diffusion Models | [**Paper**](https://arxiv.org/abs/2210.02303) |
| 4) **MoCoGAN**: Decomposing Motion and Content for Video Generation | [**CVPR 18 Paper**](https://arxiv.org/abs/1707.04993) |
| 5) Adversarial Video Generation on Complex Datasets | [**Paper**](https://arxiv.org/abs/1907.06571) |
| 6) **W.A.L.T**: Photorealistic Video Generation with Diffusion Models | [**Paper**](https://arxiv.org/abs/2312.06662), [Project](https://walt-video-diffusion.github.io/)|
| 7) **VideoGPT**: Video Generation using VQ-VAE and Transformers | [**Paper**](https://arxiv.org/abs/2104.10157), [GitHub](https://github.com/wilson1yan/VideoGPT) |
| 8) Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2204.03458), [GitHub](https://github.com/lucidrains/video-diffusion-pytorch), [Project](https://video-diffusion.github.io/)|
| 9) **MCVD**: Masked Conditional Video Diffusion for Prediction, Generation, and Interpolation | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2205.09853), [GitHub](https://github.com/voletiv/mcvd-pytorch), [Project](https://mask-cond-video-diffusion.github.io/), [Blog](https://ajolicoeur.ca/2022/05/22/masked-conditional-video-diffusion/) |
| 10) **VideoPoet**: A Large Language Model for Zero-Shot Video Generation | [**Paper**](https://arxiv.org/abs/2312.14125) |
| 11) **MAGVIT**: Masked Generative Video Transformer | [**CVPR 23 Paper**](https://arxiv.org/abs/2212.05199), [GitHub](https://github.com/google-research/magvit), [Project](https://magvit.cs.cmu.edu/), [Colab](https://github.com/google-research/magvit/blob/main) |
| 12) **EMO**: Emote Portrait Alive - Generating Expressive Portrait Videos with Audio2Video Diffusion Model under Weak Conditions | [**Paper**](https://arxiv.org/abs/2402.17485), [GitHub](https://github.com/HumanAIGC/EMO), [Project](https://humanaigc.github.io/emote-portrait-alive/) |
| 13) **SimDA**: Simple Diffusion Adapter for Efficient Video Generation | [**Paper**](https://arxiv.org/pdf/2308.09710.pdf), [GitHub](https://github.com/ChenHsing/SimDA), [Project](https://chenhsing.github.io/SimDA/) |
| 14) **StableVideo**: Text-driven Consistency-aware Diffusion Video Editing | [**ICCV 23 Paper**](https://arxiv.org/abs/2308.09592), [GitHub](https://github.com/rese1f/StableVideo), [Project](https://rese1f.github.io/StableVideo/) |
| 15) **SVD**: Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets| [**Paper**](https://static1.squarespace.com/static/6213c340453c3f502425776e/t/655ce779b9d47d342a93c890/1700587395994/stable_video_diffusion.pdf), [GitHub](https://github.com/Stability-AI/generative-models)|
| 16) **ADD**: Adversarial Diffusion Distillation| [**Paper**](https://static1.squarespace.com/static/6213c340453c3f502425776e/t/65663480a92fba51d0e1023f/1701197769659/adversarial_diffusion_distillation.pdf), [GitHub](https://github.com/Stability-AI/generative-models) |
| 17) **GenTron:** Diffusion Transformers for Image and Video Generation | [**CVPR 24 Paper**](http://arxiv.org/abs/2312.04557), [Project](https://www.shoufachen.com/gentron_website/)|
| 18) **LFDM**: Conditional Image-to-Video Generation with Latent Flow Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2303.13744), [GitHub](https://github.com/nihaomiao/CVPR23_LFDM) |
| 19) **MotionDirector**: Motion Customization of Text-to-Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.08465), [GitHub](https://github.com/showlab/MotionDirector) |
| 20) **TGAN-ODE**: Latent Neural Differential Equations for Video Generation | [**Paper**](https://arxiv.org/pdf/2011.03864v3.pdf), [GitHub](https://github.com/Zasder3/Latent-Neural-Differential-Equations-for-Video-Generation) |
| 21) **VideoCrafter1**: Open Diffusion Models for High-Quality Video Generation | [**Paper**](https://arxiv.org/abs/2310.19512), [GitHub](https://github.com/AILab-CVC/VideoCrafter) |
| 22) **VideoCrafter2**: Overcoming Data Limitations for High-Quality Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2401.09047), [GitHub](https://github.com/AILab-CVC/VideoCrafter) |
| 23) **LVDM**: Latent Video Diffusion Models for High-Fidelity Long Video Generation | [**Paper**](https://arxiv.org/abs/2211.13221), [GitHub](https://github.com/YingqingHe/LVDM) |
| <h3 id="dataset">Dataset</h3> | |
| **Dataset Name - Paper**  | **Link** |
| 1) **Panda-70M** - Panda-70M: Captioning 70M Videos with Multiple Cross-Modality Teachers<br><small>`70M Clips, 720P, Downloadable`</small>|[**CVPR 24 Paper**](https://arxiv.org/abs/2402.19479), [Github](https://github.com/snap-research/Panda-70M), [Project](https://snap-research.github.io/Panda-70M/)|
| 2) **InternVid-10M** - InternVid: A Large-scale Video-Text Dataset for Multimodal Understanding and Generation<br><small>`10M Clips, 720P, Downloadable`</small>|[**ArXiv 24 Paper**](https://arxiv.org/abs/2307.06942), [Github](https://github.com/OpenGVLab/InternVideo/tree/main/Data/InternVid)|
| 3) **CelebV-Text** - CelebV-Text: A Large-Scale Facial Text-Video Dataset<br><small>`70K Clips, 720P, Downloadable`</small>|[**CVPR 23 Paper**](https://arxiv.org/abs/2303.14717), [Github](https://github.com/celebv-text/CelebV-Text), [Project](https://celebv-text.github.io/)|
| 4) **HD-VG-130M** - VideoFactory: Swap Attention in Spatiotemporal Diffusions for Text-to-Video Generation<br><small> `130M Clips, 720P, Downloadable`</small>|[**ArXiv 23 Paper**](https://arxiv.org/abs/2305.10874), [Github](https://github.com/daooshee/HD-VG-130M), [Tool](https://github.com/Breakthrough/PySceneDetect)|
| 5) **HD-VILA-100M** - Advancing High-Resolution Video-Language Representation with Large-Scale Video Transcriptions<br><small> `100M Clips, 720P, Downloadable`</small>|[**CVPR 22 Paper**](https://arxiv.org/abs/2111.10337), [Github](https://github.com/microsoft/XPretrain/blob/main/hd-vila-100m/README.md)|
| 6) **VideoCC** - Learning Audio-Video Modalities from Image Captions<br><small>`10.3M Clips, 720P, Downloadable`</small>|[**ECCV 22 Paper**](https://arxiv.org/abs/2204.00679), [Github](https://github.com/google-research-datasets/videoCC-data)|
| 7) **YT-Temporal-180M** - MERLOT: Multimodal Neural Script Knowledge Models<br><small>`180M Clips, 480P, Downloadable`</small>| [**NeurIPS 21 Paper**](https://arxiv.org/abs/2106.02636), [Github](https://github.com/rowanz/merlot), [Project](https://rowanzellers.com/merlot/#data)|
| 8) **HowTo100M** - HowTo100M: Learning a Text-Video Embedding by Watching Hundred Million Narrated Video Clips<br><small>`136M Clips, 240P, Downloadable`</small>| [**ICCV 19 Paper**](https://arxiv.org/abs/1906.03327), [Github](https://github.com/antoine77340/howto100m), [Project](https://www.di.ens.fr/willow/research/howto100m/)|
| 9) **UCF101** - UCF101: A Dataset of 101 Human Actions Classes From Videos in The Wild<br><small>`13K Clips, 240P, Downloadable`</small>| [**CVPR 12 Paper**](https://arxiv.org/abs/1212.0402), [Project](https://www.crcv.ucf.edu/data/UCF101.php)|
| 10) **MSVD** - Collecting Highly Parallel Data for Paraphrase Evaluation<br><small>`122K Clips, 240P, Downloadable`</small> | [**ACL 11 Paper**](https://aclanthology.org/P11-1020.pdf), [Project](https://www.cs.utexas.edu/users/ml/clamp/videoDescription/)|
| 11) **Fashion-Text2Video** - A human video dataset with rich label and text annotations<br><small>`600 Videos, 480P, Downloadable`</small> | [**ArXiv 23 Paper**](https://arxiv.org/pdf/2304.08483.pdf), [Project](https://yumingj.github.io/projects/Text2Performer.html)|
| 12) **LAION-5B** - A dataset of 5,85 billion CLIP-filtered image-text pairs, 14x bigger than LAION-400M<br><small>`5B Clips, Downloadable`</small> | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2210.08402), [Project](https://laion.ai/blog/laion-5b/)|
| 13) **ActivityNet Captions** -  ActivityNet Captions contains 20k videos amounting to 849 video hours with 100k total descriptions, each with its unique start and end time<br><small>`20k videos, Downloadable`</small> | [**Arxiv 17 Paper**](https://arxiv.org/abs/1705.00754), [Project](https://cs.stanford.edu/people/ranjaykrishna/densevid/)|
| 14) **MSR-VTT** -  A large-scale video benchmark for video understanding<br><small>`10k Clips, Downloadable`</small> | [**CVPR 16 Paper**](https://ieeexplore.ieee.org/document/7780940), [Project](https://cove.thecvf.com/datasets/839)|
| 15) **The Cityscapes Dataset** -  Benchmark suite and evaluation server for pixel-level, instance-level, and panoptic semantic labeling<br><small>`Downloadable`</small> | [**Arxiv 16 Paper**](https://arxiv.org/pdf/1608.02192v1.pdf), [Project](https://www.cityscapes-dataset.com/)|
| 16) **Youku-mPLUG** -  First open-source large-scale Chinese video text dataset<br><small>`Downloadable`</small> | [**Arxiv 23 Paper**](https://arxiv.org/abs/2306.04362), [Project](https://github.com/X-PLUG/Youku-mPLUG)|
| 17) **VidProM** - VidProM: A Million-scale Real Prompt-Gallery Dataset for Text-to-Video Diffusion Models<br><small>`6.69M, Downloadable`</small>| [**Arxiv 24 Paper**](https://arxiv.org/abs/2403.06098), [Github](https://github.com/WangWenhao0716/VidProM) |
| <h4>NMNP: Nice method, not public</h4> |
| 1) **WebVid** -  Large-scale text-video dataset, containing 10 million video-text pairs scraped from the stock footage sites<br><small>`10M video-text pairs`</small> | [**Arxiv 21 Paper**](https://arxiv.org/abs/2104.00650), [Project](https://www.robots.ox.ac.uk/~vgg/research/frozen-in-time/)|
| <h3 id="patchifying-methods">Patchifying Methods</h3> | |
| **Paper** | **Link** |
| 1) **ViT**: An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale | [**CVPR 21 Paper**](https://arxiv.org/abs/2010.11929), [Github](https://github.com/google-research/vision_transformer) |
| 2) **MAE**: Masked Autoencoders Are Scalable Vision Learners| [**CVPR 22 Paper**](https://arxiv.org/abs/2111.06377), [Github](https://github.com/facebookresearch/mae) |
| 3) **ViViT**: A Video Vision Transformer (-)| [**ICCV 21 Paper**](https://arxiv.org/pdf/2103.15691v2.pdf), [GitHub](https://github.com/google-research/scenic) |
| 4) **DiT**: Scalable Diffusion Models with Transformers (-) | [**ICCV 23 Paper**](https://arxiv.org/abs/2212.09748), [GitHub](https://github.com/facebookresearch/DiT), [Project](https://www.wpeebles.com/DiT), [ModelScope](https://modelscope.cn/models?name=Dit&page=1)|
| 5) **U-ViT**: All are Worth Words: A ViT Backbone for Diffusion Models (-) | [**CVPR 23 Paper**](https://arxiv.org/abs/2209.12152), [GitHub](https://github.com/baofff/U-ViT), [ModelScope](https://modelscope.cn/models?name=UVit&page=1) |
| 6) **FlexiViT**: One Model for All Patch Sizes | [**Paper**](https://arxiv.org/pdf/2212.08013.pdf), [Github](https://github.com/bwconrad/flexivit.git) |
| 7) **Patch n’ Pack**: NaViT, a Vision Transformer for any Aspect Ratio and Resolution | [**Paper**](https://arxiv.org/abs/2307.06304), [Github](https://github.com/kyegomez/NaViT) |
| 8) **VQ-VAE**: Neural Discrete Representation Learning | [**Paper**](https://arxiv.org/abs/1711.00937), [Github](https://github.com/MishaLaskin/vqvae) |
| 9) **VQ-GAN**: Neural Discrete Representation Learning | [**CVPR 21 Paper**](https://openaccess.thecvf.com/content/CVPR2021/html/Esser_Taming_Transformers_for_High-Resolution_Image_Synthesis_CVPR_2021_paper.html), [Github](https://github.com/CompVis/taming-transformers) |
| 10) **LVT**: Latent Video Transformer | [**Paper**](https://arxiv.org/abs/2006.10704), [Github](https://github.com/rakhimovv/lvt) |
| 11) **VideoGPT**: Video Generation using VQ-VAE and Transformers (-) | [**Paper**](https://arxiv.org/abs/2104.10157), [GitHub](https://github.com/wilson1yan/VideoGPT) |
| 12) Predicting Video with VQVAE | [**Paper**](https://arxiv.org/abs/2103.01950) |
| 13) **CogVideo**: Large-scale Pretraining for Text-to-Video Generation via Transformers | [**ICLR 23 Paper**](https://arxiv.org/pdf/2205.15868.pdf), [Github](https://github.com/THUDM/CogVideo.git) |
| 14) **TATS**: Long Video Generation with Time-Agnostic VQGAN and Time-Sensitive Transformer | [**ECCV 22 Paper**](https://arxiv.org/abs/2204.03638), [Github](https://bnucsy.github.io/TATS/) |
| 15) **MAGVIT**: Masked Generative Video Transformer (-) | [**CVPR 23 Paper**](https://arxiv.org/abs/2212.05199), [GitHub](https://github.com/google-research/magvit), [Project](https://magvit.cs.cmu.edu/), [Colab](https://github.com/google-research/magvit/blob/main) |
| 16) **MagViT2**: Language Model Beats Diffusion -- Tokenizer is Key to Visual Generation | [**ICLR 24 Paper**](https://arxiv.org/pdf/2310.05737.pdf), [Github](https://github.com/lucidrains/magvit2-pytorch) |
| 17) **VideoPoet**: A Large Language Model for Zero-Shot Video Generation (-) | [**Paper**](https://arxiv.org/abs/2312.14125) |
| 18) **CLIP**: Learning Transferable Visual Models From Natural Language Supervision | [**CVPR 21 Paper**](https://arxiv.org/abs/2010.11929), [Github](https://github.com/openai/CLIP) |
| 19) **BLIP**: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation | [**Paper**](https://arxiv.org/abs/2201.12086), [Github](https://github.com/salesforce/BLIP) |
| 20) **BLIP-2**: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models | [**Paper**](https://arxiv.org/abs/2301.12597), [Github](https://github.com/salesforce/LAVIS/tree/main/projects/blip2) |
| <h3 id="long-context">Long-context</h3> | |
| **Paper** | **Link** |
| 1) World Model on Million-Length Video And Language With RingAttention | [**Paper**](https://arxiv.org/abs/2402.08268), [GitHub](https://github.com/LargeWorldModel/LWM) |
| 2) Ring Attention with Blockwise Transformers for Near-Infinite Context | [**Paper**](https://arxiv.org/abs/2310.01889), [GitHub](https://github.com/lhao499/RingAttention) |
| 3) Extending LLMs' Context Window with 100 Samples | [**Paper**](https://arxiv.org/abs/2401.07004), [GitHub](https://github.com/GAIR-NLP/Entropy-ABF) |
| 4) Efficient Streaming Language Models with Attention Sinks | [**ICLR 24 Paper**](https://arxiv.org/abs/2309.17453), [GitHub](https://github.com/mit-han-lab/streaming-llm) |
| 5) The What, Why, and How of Context Length Extension Techniques in Large Language Models – A Detailed Survey | [**Paper**](https://arxiv.org/pdf/2401.07872) |
| 6) **MovieChat**: From Dense Token to Sparse Memory for Long Video Understanding | [**CVPR 24 Paper**](https://arxiv.org/abs/2307.16449), [GitHub](https://github.com/rese1f/MovieChat), [Project](https://rese1f.github.io/MovieChat/) |
| 7) **MemoryBank**: Enhancing Large Language Models with Long-Term Memory | [**Paper**](https://arxiv.org/pdf/2305.10250.pdf), [GitHub](https://github.com/zhongwanjun/MemoryBank-SiliconFriend) |
| <h3 id="audio-related-resource">Audio Related Resource</h3> | |
| **Paper**  | **Link** |
| 1) **Stable Audio**: Fast Timing-Conditioned Latent Audio Diffusion | [**Paper**](https://arxiv.org/abs/2402.04825), [Github](https://github.com/Stability-AI/stable-audio-tools), [Blog](https://stability.ai/research/stable-audio-efficient-timing-latent-diffusion)|
| 2) **MM-Diffusion**: Learning Multi-Modal Diffusion Models for Joint Audio and Video Generation | [**CVPR 23 Paper**](http://openaccess.thecvf.com/content/CVPR2023/papers/Ruan_MM-Diffusion_Learning_Multi-Modal_Diffusion_Models_for_Joint_Audio_and_Video_CVPR_2023_paper.pdf), [GitHub](https://github.com/researchmm/MM-Diffusion) |
| 3) **Pengi**: An Audio Language Model for Audio Tasks        | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/3a2e5889b4bbef997ddb13b55d5acf77-Paper-Conference.pdf), [GitHub](https://github.com/microsoft/Pengi) |
| 4) **Vast:** A vision-audio-subtitle-text omni-modality foundation model and dataset | [**NeurlPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/e6b2b48b5ed90d07c305932729927781-Paper-Conference.pdf), [GitHub](https://github.com/TXH-mercury/VAST) |
| 5) **Macaw-LLM**: Multi-Modal Language Modeling with Image, Audio, Video, and Text Integration| [**Paper**](https://arxiv.org/abs/2306.09093), [GitHub](https://github.com/lyuchenyang/Macaw-LLM) |
| 6) **NaturalSpeech**: End-to-End Text to Speech Synthesis with Human-Level Quality | [**Paper**](https://arxiv.org/pdf/2205.04421v2.pdf), [GitHub](https://github.com/heatz123/naturalspeech) |
| 7) **NaturalSpeech 2**: Latent Diffusion Models are Natural and Zero-Shot Speech and Singing Synthesizers| [**Paper**](https://arxiv.org/abs/2304.09116), [GitHub](https://github.com/lucidrains/naturalspeech2-pytorch) |
| 8) **UniAudio**: An Audio Foundation Model Toward Universal Audio Generation| [**Paper**](https://arxiv.org/abs/2310.00704), [GitHub](https://github.com/uniaudio666/UniAudio) |
| 9) Audio-Visual LLM for Video Understanding| [**Paper**](https://arxiv.org/abs/2312.06720) |
| 10) **Make-An-Audio**: Text-To-Audio Generation with Prompt-Enhanced Diffusion Models| [**ICML 23 Paper**](https://proceedings.mlr.press/v202/huang23i/huang23i.pdf), [GitHub](https://github.com/Text-to-Audio/Make-An-Audio) |
| 11) **AudioGPT**: Understanding and Generating Speech, Music, Sound, and Talking Head| [**Paper**](https://arxiv.org/abs/2304.12995), [GitHub](https://github.com/AIGC-Audio/AudioGPT) |
| 12) **AudioLM**: a Language Modeling Approach to Audio Generation| [**Paper**](https://arxiv.org/abs/2209.03143) |
| 13) **AudioGen**: Textually Guided Audio Generation| [**ICLR 23 Paper**](https://iclr.cc/virtual/2023/poster/11521), [Project](https://felixkreuk.github.io/audiogen/) |
| <h3 id="consistency">Consistency</h3> | |
| **Paper**  | **Link** |
| 1) Layered Neural Atlases for Consistent Video Editing | [**TOG 21 Paper**](https://arxiv.org/pdf/2109.11418.pdf), [GitHub](https://github.com/ykasten/layered-neural-atlases), [Project](https://layered-neural-atlases.github.io/) |
| 2) **StableVideo**: Text-driven Consistency-aware Diffusion Video Editing | [**ICCV 23 Paper**](https://arxiv.org/abs/2308.09592), [GitHub](https://github.com/rese1f/StableVideo), [Project](https://rese1f.github.io/StableVideo/) |
| 3) **CoDeF**: Content Deformation Fields for Temporally Consistent Video Processing | [**Paper**](https://arxiv.org/pdf/2308.07926.pdf), [GitHub](https://github.com/qiuyu96/CoDeF), [Project](https://qiuyu96.github.io/CoDeF/) |
| 4) Consistency Models | [**ICML 23 Paper**](https://arxiv.org/pdf/2303.01469.pdf), [GitHub](https://github.com/openai/consistency_models) |
| 5) Sora Generates Videos with Stunning Geometrical Consistency | [**Paper**](https://arxiv.org/pdf/2402.17403.pdf), [GitHub](https://github.com/meteorshowers/Sora-Generates-Videos-with-Stunning-Geometrical-Consistency), [Project](https://sora-geometrical-consistency.github.io/) |
| 6) Efficient One-stage Video Object Detection by Exploiting Temporal Consistency | [**ECCV 22 Paper**](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136950001.pdf), [GitHub](https://github.com/guanxiongsun/EOVOD) |
| 7) Bootstrap Motion Forecasting With Self-Consistent Constraints | [**ICCV 23 Paper**](https://ieeexplore.ieee.org/document/10377383) |
| 8) Enforcing Realism and Temporal Consistency for Large-Scale Video Inpainting | [**Paper**](https://dl.acm.org/doi/book/10.5555/AAI28845594) |
| 9) Enhancing Multi-Camera People Tracking with Anchor-Guided Clustering and Spatio-Temporal Consistency ID Re-Assignment | [**CVPRW 23 Paper**](https://ieeexplore.ieee.org/document/10208943), [GitHub](https://github.com/ipl-uw/AIC23_Track1_UWIPL_ETRI/tree/main) |
| 10) Exploiting Spatial-Temporal Semantic Consistency for Video Scene Parsing | [**Paper**](https://arxiv.org/abs/2109.02281) |
| 11) Semi-Supervised Crowd Counting With Spatial Temporal Consistency and Pseudo-Label Filter | [**TCSVT 23 Paper**](https://ieeexplore.ieee.org/document/10032602) |
| 12) Spatio-temporal Consistency and Hierarchical Matching for Multi-Target Multi-Camera Vehicle Tracking | [**CVPRW 19 Paper**](https://openaccess.thecvf.com/content_CVPRW_2019/html/AI_City/Li_Spatio-temporal_Consistency_and_Hierarchical_Matching_for_Multi-Target_Multi-Camera_Vehicle_Tracking_CVPRW_2019_paper.html) |
| 13) **VideoDirectorGPT**: Consistent Multi-scene Video Generation via LLM-Guided Planning (-) | [**Paper**](https://arxiv.org/abs/2309.15091) |
| 14) **VideoDrafter**: Content-Consistent Multi-Scene Video Generation with LLM (-) | [**Paper**](https://arxiv.org/abs/2401.01256) |
| <h3 id="prompt-engineering">Prompt Engineering</h3> | |
| **Paper**  | **Link** |
| 1) **RealCompo**: Dynamic Equilibrium between Realism and Compositionality Improves Text-to-Image Diffusion Models | [**Paper**](https://arxiv.org/abs/2402.12908), [GitHub](https://github.com/YangLing0818/RealCompo), [Project](https://cominclip.github.io/RealCompo_Page/) |
| 2) **Mastering Text-to-Image Diffusion**: Recaptioning, Planning, and Generating with Multimodal LLMs | [**Paper**](https://arxiv.org/abs/2401.11708), [GitHub](https://github.com/YangLing0818/RPG-DiffusionMaster) |
| 3) **LLM-grounded Diffusion**: Enhancing Prompt Understanding of Text-to-Image Diffusion Models with Large Language Models | [**TMLR 23 Paper**](https://arxiv.org/abs/2305.13655), [GitHub](https://github.com/TonyLianLong/LLM-groundedDiffusion) |
| 4) **LLM BLUEPRINT**: ENABLING TEXT-TO-IMAGE GEN-ERATION WITH COMPLEX AND DETAILED PROMPTS | [**ICLR 24 Paper**](https://arxiv.org/abs/2310.10640), [GitHub](https://github.com/hananshafi/llmblueprint) |
| 5) Progressive Text-to-Image Diffusion with Soft Latent Direction | [**Paper**](https://arxiv.org/abs/2309.09466) |
| 6) Self-correcting LLM-controlled Diffusion Models | [**CVPR 24 Paper**](https://arxiv.org/abs/2311.16090), [GitHub](https://github.com/tsunghan-wu/SLD) |
| 7) **LayoutLLM-T2I**: Eliciting Layout Guidance from LLM for Text-to-Image Generation | [**MM 23 Paper**](https://arxiv.org/abs/2308.05095) |
| 8) **LayoutGPT**: Compositional Visual Planning and Generation with Large Language Models | [**NeurIPS 23 Paper**](https://arxiv.org/abs/2305.15393), [GitHub](https://github.com/weixi-feng/LayoutGPT) |
| 9) **Gen4Gen**: Generative Data Pipeline for Generative Multi-Concept Composition | [**Paper**](https://arxiv.org/abs/2402.15504), [GitHub](https://github.com/louisYen/Gen4Gen) |
| 10) **InstructEdit**: Improving Automatic Masks for Diffusion-based Image Editing With User Instructions | [**Paper**](https://arxiv.org/abs/2305.18047), [GitHub](https://github.com/QianWangX/InstructEdit) |
| 11) Controllable Text-to-Image Generation with GPT-4 | [**Paper**](https://arxiv.org/abs/2305.18583) |
| 12) LLM-grounded Video Diffusion Models | [**ICLR 24 Paper**](https://arxiv.org/abs/2309.17444) |
| 13) **VideoDirectorGPT**: Consistent Multi-scene Video Generation via LLM-Guided Planning | [**Paper**](https://arxiv.org/abs/2309.15091) |
| 14) **FlowZero**: Zero-Shot Text-to-Video Synthesis with LLM-Driven Dynamic Scene Syntax | [**Paper**](https://arxiv.org/abs/2311.15813), [Github](https://github.com/aniki-ly/FlowZero), [Project](https://flowzero-video.github.io/) |
| 15) **VideoDrafter**: Content-Consistent Multi-Scene Video Generation with LLM | [**Paper**](https://arxiv.org/abs/2401.01256) |
| 16) **Free-Bloom**: Zero-Shot Text-to-Video Generator with LLM Director and LDM Animator | [**NeurIPS 23 Paper**](https://arxiv.org/abs/2309.14494) |
| 17) Empowering Dynamics-aware Text-to-Video Diffusion with Large Language Models | [**Paper**](https://arxiv.org/abs/2308.13812) |
| 18) **MotionZero**: Exploiting Motion Priors for Zero-shot Text-to-Video Generation | [**Paper**](https://arxiv.org/abs/2311.16635) |
| 19) **GPT4Motion**: Scripting Physical Motions in Text-to-Video Generation via Blender-Oriented GPT Planning | [**Paper**](https://arxiv.org/abs/2311.12631) |
| 20) Multimodal Procedural Planning via Dual Text-Image Prompting | [**Paper**](https://arxiv.org/abs/2305.01795), [Github](https://github.com/YujieLu10/TIP) |
| 21) **InstructCV**: Instruction-Tuned Text-to-Image Diffusion Models as Vision Generalists | [**ICLR 24 Paper**](https://arxiv.org/abs/2310.00390), [Github](https://github.com/AlaaLab/InstructCV) |
| 22) **DreamSync**: Aligning Text-to-Image Generation with Image Understanding Feedback | [**Paper**](https://arxiv.org/abs/2311.17946) |
| 23) **TaleCrafter**: Interactive Story Visualization with Multiple Characters | [**SIGGRAPH Asia 23 Paper**](https://arxiv.org/abs/2310.00390) |
| 24) **Reason out Your Layout**: Evoking the Layout Master from Large Language Models for Text-to-Image Synthesis | [**Paper**](https://arxiv.org/abs/2311.17126), [Github](https://github.com/Xiaohui9607/LLM_layout_generator) |
| 25) **COLE**: A Hierarchical Generation Framework for Graphic Design | [**Paper**](https://arxiv.org/abs/2311.16974) |
| 26) Knowledge-Aware Artifact Image Synthesis with LLM-Enhanced Prompting and Multi-Source Supervision | [**Paper**](https://arxiv.org/abs/2312.08056) |
| 27) **Vlogger**: Make Your Dream A Vlog | [**CVPR 24 Paper**](https://arxiv.org/abs/2401.09414), [Github](https://github.com/Vchitect/Vlogger) |
| 28) **GALA3D**: Towards Text-to-3D Complex Scene Generation via Layout-guided Generative Gaussian Splatting | [**Paper**](https://github.com/VDIGPKU/GALA3D) |
| 29) **MuLan**: Multimodal-LLM Agent for Progressive Multi-Object Diffusion | [**Paper**](https://arxiv.org/abs/2402.12741) |
| <h3 id="security">Security</h3> | |
| **Paper**  | **Link** |
| 1) **BeaverTails:** Towards Improved Safety Alignment of LLM via a Human-Preference Dataset | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/4dbb61cb68671edc4ca3712d70083b9f-Paper-Datasets_and_Benchmarks.pdf), [Github](https://github.com/PKU-Alignment/beavertails) |
| 2) **LIMA:** Less Is More for Alignment | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/ac662d74829e4407ce1d126477f4a03a-Paper-Conference.pdf) |
| 3) **Jailbroken:** How Does LLM Safety Training Fail? | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/fd6613131889a4b656206c50a8bd7790-Paper-Conference.pdf) |
| 4) **Safe Latent Diffusion:** Mitigating Inappropriate Degeneration in Diffusion Models | [**CVPR 23 Paper**](https://openaccess.thecvf.com/content/CVPR2023/papers/Schramowski_Safe_Latent_Diffusion_Mitigating_Inappropriate_Degeneration_in_Diffusion_Models_CVPR_2023_paper.pdf) |
| 5) **Stable Bias:** Evaluating Societal Representations in Diffusion Models | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/b01153e7112b347d8ed54f317840d8af-Paper-Datasets_and_Benchmarks.pdf) |
| 6) Ablating concepts in text-to-image  diffusion models | **[ICCV 23 Paper](https://openaccess.thecvf.com/content/ICCV2023/papers/Kumari_Ablating_Concepts_in_Text-to-Image_Diffusion_Models_ICCV_2023_paper.pdf)** |
| 7) Diffusion art or digital forgery?  investigating data replication in diffusion models | [**ICCV 23 Paper**](https://openaccess.thecvf.com/content/CVPR2023/papers/Somepalli_Diffusion_Art_or_Digital_Forgery_Investigating_Data_Replication_in_Diffusion_CVPR_2023_paper.pdf), [Project](https://somepago.github.io/diffrep.html) |
| 8) Eternal Sunshine of the Spotless Net:  Selective Forgetting in Deep Networks | **[ICCV 20 Paper](https://openaccess.thecvf.com/content_CVPR_2020/papers/Golatkar_Eternal_Sunshine_of_the_Spotless_Net_Selective_Forgetting_in_Deep_CVPR_2020_paper.pdf)** |
| 9) Reliable evaluation of adversarial robustness with an ensemble of diverse parameter-free attacks | [**ICML 20 Paper**](http://proceedings.mlr.press/v119/croce20b/croce20b.pdf) |
| 10) A pilot study of query-free adversarial  attack against stable diffusion | **[ICCV 23 Paper](https://openaccess.thecvf.com/content/CVPR2023W/AML/papers/Zhuang_A_Pilot_Study_of_Query-Free_Adversarial_Attack_Against_Stable_Diffusion_CVPRW_2023_paper.pdf) ** |
| 11) Interpretable-Through-Prototypes Deepfake Detection for Diffusion Models | **[ICCV 23 Paper](https://openaccess.thecvf.com/content/ICCV2023W/DFAD/papers/Aghasanli_Interpretable-Through-Prototypes_Deepfake_Detection_for_Diffusion_Models_ICCVW_2023_paper.pdf)** |
| 12) Erasing Concepts from Diffusion Models                   | **[ICCV 23 Paper](https://openaccess.thecvf.com/content/ICCV2023/papers/Gandikota_Erasing_Concepts_from_Diffusion_Models_ICCV_2023_paper.pdf)**, [Project](http://erasing.baulab.info/) |
| 13) Ablating Concepts in Text-to-Image Diffusion Models      | **[ICCV 23 Paper](https://openaccess.thecvf.com/content/ICCV2023/papers/Kumari_Ablating_Concepts_in_Text-to-Image_Diffusion_Models_ICCV_2023_paper.pdf)**, [Project](https://www.cs.cmu.edu/) |
| 14) **BEAVERTAILS:** Towards Improved Safety Alignment of LLM via a Human-Preference Dataset | **[NeurIPS 23 Paper](https://proceedings.neurips.cc/paper_files/paper/2023/file/4dbb61cb68671edc4ca3712d70083b9f-Paper-Datasets_and_Benchmarks.pdf)**, [Project](https://sites.google.com/view/pku-beavertails) |
| 15) **LIMA:** Less Is More for Alignment                     | **[NeurIPS 23 Paper](https://proceedings.neurips.cc/paper_files/paper/2023/file/ac662d74829e4407ce1d126477f4a03a-Paper-Conference.pdf)** |
| 16) **Stable Bias:** Evaluating Societal Representations in Diffusion Models | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/b01153e7112b347d8ed54f317840d8af-Paper-Datasets_and_Benchmarks.pdf) |
| 17) Threat Model-Agnostic Adversarial Defense using Diffusion Models | **[Paper](https://arxiv.org/pdf/2207.08089)**                |
| 18) How well can Text-to-Image Generative Models understand Ethical Natural Language Interventions? | [**Paper**](https://arxiv.org/pdf/2210.15230), [Github](https://github.com/Hritikbansal/entigen_emnlp) |
| 19) Differentially Private Diffusion Models Generate Useful Synthetic Images | **[Paper](https://arxiv.org/pdf/2302.13861)**                |
| 20) Unsafe Diffusion: On the Generation of Unsafe Images and Hateful Memes From Text-To-Image Models | **[SIGSAC 23 Paper](https://arxiv.org/pdf/2305.13873)**, [Github](https://github.com/YitingQu/unsafe-diffusion) |
| 21) Forget-Me-Not: Learning to Forget in Text-to-Image Diffusion Models | **[Paper](https://arxiv.org/pdf/2303.17591)**, [Github](https://github.com/SHI-Labs/Forget-Me-Not) |
| 22) Unified Concept Editing in Diffusion Models              | [**WACV 24 Paper**](https://openaccess.thecvf.com/content/WACV2024/papers/Gandikota_Unified_Concept_Editing_in_Diffusion_Models_WACV_2024_paper.pdf), [Project](https://unified.baulab.info/) |
| <h3 id="world-model">World Model</h3> | |
| **Paper**  | **Link** |
| 1) **NExT-GPT**: Any-to-Any Multimodal LLM | [**Paper**](https://arxiv.org/abs/2309.05519), [GitHub](https://github.com/NExT-GPT/NExT-GPT) |
| <h3 id="video-compression">Video Compression</h3> ||
| **Paper**  | **Link** |
| 1) **H.261**: Video codec for audiovisual services at p x 64 kbit/s | [**Paper**](https://www.itu.int/rec/T-REC-H.261-199303-I/en) |
| 2) **H.262**: Information technology - Generic coding of moving pictures and associated audio information: Video | [**Paper**](https://www.itu.int/rec/T-REC-H.262-201202-I/en) |
| 3) **H.263**: Video coding for low bit rate communication | [**Paper**](https://www.itu.int/rec/T-REC-H.263-200501-I/en) |
| 4) **H.264**: Overview of the H.264/AVC video coding standard | [**Paper**](https://ieeexplore.ieee.org/document/1218189) |
| 5) **H.265**: Overview of the High Efficiency Video Coding (HEVC) Standard | [**Paper**](https://ieeexplore.ieee.org/document/6316136) |
| 6) **H.266**: Overview of the Versatile Video Coding (VVC) Standard and its Applications | [**Paper**](https://ieeexplore.ieee.org/document/9503377) |
| 7) **DVC**: An End-to-end Deep Video Compression Framework | [**CVPR 19 Paper**](https://arxiv.org/abs/1812.00101), [GitHub](https://github.com/GuoLusjtu/DVC/tree/master) |
| 8) **OpenDVC**: An Open Source Implementation of the DVC Video Compression Method | [**Paper**](https://arxiv.org/abs/2006.15862), [GitHub](https://github.com/RenYang-home/OpenDVC) |
| 9) **HLVC**: Learning for Video Compression with Hierarchical Quality and Recurrent Enhancement | [**CVPR 20 Paper**](https://arxiv.org/abs/2003.01966), [Github](https://github.com/RenYang-home/HLVC) |
| 10) **RLVC**: Learning for Video Compression with Recurrent Auto-Encoder and Recurrent Probability Model | [**J-STSP 21 Paper**](https://ieeexplore.ieee.org/abstract/document/9288876), [Github](https://github.com/RenYang-home/RLVC) |
| 11) **PLVC**: Perceptual Learned Video Compression with Recurrent Conditional GAN | [**IJCAI 22 Paper**](https://arxiv.org/abs/2109.03082), [Github](https://github.com/RenYang-home/PLVC) |
| 12) **ALVC**: Advancing Learned Video Compression with In-loop Frame Prediction | [**T-CSVT 22 Paper**](https://ieeexplore.ieee.org/abstract/document/9950550), [Github](https://github.com/RenYang-home/ALVC) |
| 13) **DCVC**: Deep Contextual Video Compression | [**NeurIPS 21 Paper**](https://proceedings.neurips.cc/paper/2021/file/96b250a90d3cf0868c83f8c965142d2a-Paper.pdf), [Github](https://github.com/microsoft/DCVC/tree/main/DCVC) |
| 14) **DCVC-TCM**: Temporal Context Mining for Learned Video Compression | [**TM 22 Paper**](https://ieeexplore.ieee.org/document/9941493), [Github](https://github.com/microsoft/DCVC/tree/main/DCVC-TCM) |
| 15) **DCVC-HEM**: Hybrid Spatial-Temporal Entropy Modelling for Neural Video Compression | [**MM 22 Paper**](https://arxiv.org/abs/2207.05894), [Github](https://github.com/microsoft/DCVC/tree/main/DCVC-HEM) |
| 16) **DCVC-DC**: Neural Video Compression with Diverse Contexts | [**CVPR 23 Paper**](https://arxiv.org/abs/2302.14402), [Github](https://github.com/microsoft/DCVC/tree/main/DCVC-DC) |
| 17) **DCVC-FM**: Neural Video Compression with Feature Modulation | [**CVPR 24 Paper**](https://arxiv.org/abs/2402.17414), [Github](https://github.com/microsoft/DCVC/tree/main/DCVC-FM) |
| 18) **SSF**: Scale-Space Flow for End-to-End Optimized Video Compression | [**CVPR 20 Paper**](https://openaccess.thecvf.com/content_CVPR_2020/html/Agustsson_Scale-Space_Flow_for_End-to-End_Optimized_Video_Compression_CVPR_2020_paper.html), [Github](https://github.com/InterDigitalInc/CompressAI) |
| <h3 id="Mamba">Mamba</h3> | 
| <h4 id="theoretical-foundations-and-model-architecture">Theoretical Foundations and Model Architecture</h4> | |
| **Paper** | **Link** |
| 1) **Mamba**: Linear-Time Sequence Modeling with Selective State Spaces | [**Paper**](https://arxiv.org/abs/2312.00752), [Github](https://github.com/state-spaces/mamba) |
| 2) Efficiently Modeling Long Sequences with Structured State Spaces | [**ICLR 22 Paper**](https://iclr.cc/virtual/2022/poster/6959), [Github](https://github.com/state-spaces/s4) |
| 3) Modeling Sequences with Structured State Spaces | [**Paper**](https://purl.stanford.edu/mb976vf9362) |
| 4) Long Range Language Modeling via Gated State Spaces | [**Paper**](https://arxiv.org/abs/2206.13947), [GitHub](https://github.com/lucidrains/gated-state-spaces-pytorch) |
| <h4 id="image-generation-and-visual-applications">Image Generation and Visual Applications</h4> | |
| **Paper** | **Link** |
| 1) Diffusion Models Without Attention | [**Paper**](https://arxiv.org/abs/2311.18257) |
| 2) **Pan-Mamba**: Effective Pan-Sharpening with State Space Model  | [**Paper**](https://arxiv.org/abs/2402.12192), [Github](https://github.com/alexhe101/Pan-Mamba) |
| 3) Pretraining Without Attention | [**Paper**](https://arxiv.org/abs/2212.10544), [Github](https://github.com/jxiw/BiGS) |
| 4) Block-State Transformers | [**NIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/hash/16ccd203e9e3696a7ab0dcf568316379-Abstract-Conference.html) |
| 5) **Vision Mamba**: Efficient Visual Representation Learning with Bidirectional State Space Model | [**Paper**](https://arxiv.org/abs/2401.09417), [Github](https://github.com/hustvl/Vim) |
| 6) VMamba: Visual State Space Model | [**Paper**](https://arxiv.org/abs/2401.10166), [Github](https://github.com/MzeroMiko/VMamba) |
| <h4 id="video-processing-and-understanding">Video Processing and Understanding</h4> | |
| **Paper** | **Link** |
| 1) Long Movie Clip Classification with State-Space Video Models | [**ECCV 22 Paper**](https://link.springer.com/chapter/10.1007/978-3-031-19833-5_6), [Github](https://github.com/md-mohaiminul/ViS4mer) |
| 2) Selective Structured State-Spaces for Long-Form Video Understanding | [**CVPR 23 Paper**](https://openaccess.thecvf.com/content/CVPR2023/html/Wang_Selective_Structured_State-Spaces_for_Long-Form_Video_Understanding_CVPR_2023_paper.html) |
| 3) Efficient Movie Scene Detection Using State-Space Transformers | [**CVPR 23 Paper**](https://openaccess.thecvf.com/content/CVPR2023/html/Islam_Efficient_Movie_Scene_Detection_Using_State-Space_Transformers_CVPR_2023_paper.html), [Github](https://github.com/md-mohaiminul/TranS4mer) |
| <h4 id="medical-image-processing">Medical Image Processing</h4> | |
| **Paper** | **Link** |
| 1) **Swin-UMamba**: Mamba-based UNet with ImageNet-based pretraining | [**Paper**](https://arxiv.org/abs/2402.03302), [Github](https://github.com/JiarunLiu/Swin-UMamba) |
| 2) **MambaIR**: A Simple Baseline for Image Restoration with State-Space Model | [**Paper**](https://arxiv.org/abs/2402.15648), [Github](https://github.com/csguoh/MambaIR) |
| 3) VM-UNet: Vision Mamba UNet for Medical Image Segmentation | [**Paper**](https://arxiv.org/abs/2402.02491), [Github](https://github.com/JCruan519/VM-UNet) |
|  | |
| <h3 id="existing-high-quality-resources">Existing high-quality resources</h3> | |
| **Resources**  | **Link** |
| 1) Datawhale - AI视频生成学习 | [Feishu doc](https://datawhaler.feishu.cn/docx/G4LkdaffWopVbwxT1oHceiv9n0c) |
| 2) A Survey on Generative Diffusion Model | [**TKDE 24 Paper**](https://arxiv.org/pdf/2209.02646.pdf), [GitHub](https://github.com/chq1155/A-Survey-on-Generative-Diffusion-Model) |
| 3) Awesome-Video-Diffusion-Models: A Survey on Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.10647), [GitHub](https://github.com/ChenHsing/Awesome-Video-Diffusion-Models) |
| 4) Awesome-Text-To-Video：A Survey on Text-to-Video Generation/Synthesis  | [GitHub](https://github.com/jianzhnie/awesome-text-to-video)|
| 5) video-generation-survey: A reading list of video generation| [GitHub](https://github.com/yzhang2016/video-generation-survey)|
| 6) Awesome-Video-Diffusion |  [GitHub](https://github.com/showlab/Awesome-Video-Diffusion) |
| 7) Video Generation Task in Papers With Code |  [Task](https://paperswithcode.com/task/video-generation) |
| 8) Sora: A Review on Background, Technology, Limitations, and Opportunities of Large Vision Models |  [**Paper**](https://arxiv.org/abs/2402.17177), [GitHub](https://github.com/lichao-sun/SoraReview) |
| 9) Open-Sora-Plan (PKU-YuanGroup) |  [GitHub](https://github.com/PKU-YuanGroup/Open-Sora-Plan) |
| 10) State of the Art on Diffusion Models for Visual Computing | [**Paper**](http://arxiv.org/abs/2310.07204) |
| 11) Diffusion Models: A Comprehensive Survey of Methods and Applications | [**CSUR 24 Paper**](https://arxiv.org/abs/2209.00796), [GitHub](https://github.com/YangLing0818/Diffusion-Models-Papers-Survey-Taxonomy) |
| 12) Generate Impressive Videos with Text Instructions: A Review of OpenAI Sora, Stable Diffusion, Lumiere and Comparable | [**Paper**](https://www.techrxiv.org/users/684880/articles/718900-generate-impressive-videos-with-text-instructions-a-review-of-openai-sora-stable-diffusion-lumiere-and-comparable) |
| 13) On the Design Fundamentals of Diffusion Models: A Survey | [**Paper**](http://arxiv.org/abs/2306.04542) |
| 14) Efficient Diffusion Models for Vision: A Survey | [**Paper**](http://arxiv.org/abs/2210.09292) |
| 15) Text-to-Image Diffusion Models in Generative AI: A Survey | [**Paper**](http://arxiv.org/abs/2303.07909) |
| 16) Awesome-Diffusion-Transformers | [GitHub](https://github.com/ShoufaChen/Awesome-Diffusion-Transformers), [Project](https://www.shoufachen.com/Awesome-Diffusion-Transformers/) |
| 17) Open-Sora (HPC-AI Tech) |  [GitHub](https://github.com/hpcaitech/Open-Sora), [Blog](https://hpc-ai.com/blog/open-sora) |
| 18) **LAVIS** - A Library for Language-Vision Intelligence | [**ACL 23 Paper**](https://aclanthology.org/2023.acl-demo.3.pdf), [GitHub](https://github.com/salesforce/lavis), [Project](https://opensource.salesforce.com/LAVIS//latest/index.html) |
| 19) **OpenDiT**: An Easy, Fast and Memory-Efficient System for DiT Training and Inference | [GitHub](https://github.com/NUS-HPC-AI-Lab/OpenDiT) |

## Minisora Community WeChat Group

<div align="center">

<img src="assets/qrcode.png" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mini-sora/minisora&type=Date)](https://star-history.com/#mini-sora/minisora&Date)

## How to Contribute to the Mini Sora Community

We greatly appreciate your contributions to the Mini Sora open-source community and helping us make it even better than it is now!

For more details, please refer to the [Contribution Guidelines](./.github/CONTRIBUTING.md)

## Community contributors

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
