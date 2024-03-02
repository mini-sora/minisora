# Mini Sora Community 

<div align="center">

<img src="assets/logo.jpg" width="600"/>
  <div>&nbsp;</div>
  <div align="center">
  </div>
</div>


<div align="center">

  [简体中文](README.md) | [English](https://github.com/mini-sora/minisora/blob/main/README_EN.md)

</div>


<p align="center">
    👋 join us on  <a href="https://cdn.vansin.top/minisora.jpg" target="_blank">WeChat</a>
</p>

The Mini Sora open-source community is positioned as a community-driven initiative (**free of charge and devoid of any exploitation**) organized spontaneously by community members. The Mini Sora project aims to explore the implementation path and future development direction of Sora.

- Regular roundtable discussions will be held with the Sora team and the community to explore possibilities.
- We will delve into existing technological pathways for video generation.


## Paper Reading Program

- **[Sora: Creating video from text](https://openai.com/sora) Technical Report**: [Video generation models as world simulators](https://openai.com/research/video-generation-models-as-world-simulators)
- **DiT**: [Scalable Diffusion Models with Transformers](https://arxiv.org/abs/2212.09748)
- **Latte**: [Latte: Latent Diffusion Transformer for Video Generation](https://maxin-cn.github.io/latte_project/)
- Updating...

### Recruitment of Presenters
- [**DiT** Paper](https://github.com/orgs/mini-sora/discussions/39)
- [**Latte** Paper](https://github.com/orgs/mini-sora/discussions/38)  [**Intensive Reading of Translated Latte Paper**](./notes/latte%E8%AE%BA%E6%96%87%E7%B2%BE%E8%AF%BB%E7%BF%BB%E8%AF%91.pdf)    [**Notes of Latte Paper in Chinese**](./notes/Latte.md)

## Hot News
- [**OpenDiT**: An Easy, Fast and Memory-Efficient System for DiT Training and Inference](https://github.com/NUS-HPC-AI-Lab/OpenDiT)

## Related Work


| <h3>Diffusion Models</h3> |  |
| :------------- | :------------- |
| **Paper** | **Link** |
| 1) **Guided-Diffusion**: Diffusion Models Beat GANs on Image Synthesis | [**NeurIPS 21 Paper**](https://arxiv.org/abs/2105.05233), [Github](https://github.com/openai/guided-diffusion)|
| 2) **Latent Diffusion**: High-Resolution Image Synthesis with Latent Diffusion Models | [**CVPR 22 Paper**](https://arxiv.org/abs/2112.10752), [Github](https://github.com/CompVis/latent-diffusion) |
| 3) **EDM**: Elucidating the Design Space of Diffusion-Based Generative Models | [**NeurIPS 22 Paper**](https://arxiv.org/abs/2206.00364), [Github](https://github.com/NVlabs/edm) |
| 4) **DDPM**: Denoising Diffusion Probabilistic Models | [**NeurIPS 20 Paper**](https://arxiv.org/abs/2006.11239), [Github](https://github.com/hojonathanho/diffusion) |
| 5) **DDIM**: Denoising Diffusion Implicit Models | [**ICLR 21 Paper**](https://arxiv.org/abs/2010.02502), [Github](https://github.com/ermongroup/ddim) |
| 6) **Score-Based Diffusion**: Score-Based Generative Modeling through Stochastic Differential Equations | [**ICLR 21 Paper**](https://arxiv.org/abs/2011.13456), [Github](https://github.com/yang-song/score_sde), [Blog](https://yang-song.net/blog/2021/score) |
| 7) **Stable Cascade**: Würstchen: An efficient architecture for large-scale text-to-image diffusion models | [**ICLR 24 Paper**](https://openreview.net/forum?id=gU58d5QeGv), [Github](https://github.com/Stability-AI/StableCascade), [Blog](https://stability.ai/news/introducing-stable-cascade) |
| 8) Diffusion Models in Vision: A Survey| [**TPAMI 23 Paper**](https://arxiv.org/abs/2011.13456), [Github](https://github.com/CroitoruAlin/Diffusion-Models-in-Vision-A-Survey)|
| <h3>Diffusion Transformer</h3> | |
| **Paper** | **Link** |
| 1) **UViT**: All are Worth Words: A ViT Backbone for Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2209.12152), [Github](https://github.com/baofff/U-ViT), [ModelScope](https://modelscope.cn/models?name=UVit&page=1) |
| 2) **DiT**: Scalable Diffusion Models with Transformers | [**ICCV 23 Paper**](https://arxiv.org/abs/2212.09748), [Github](https://github.com/facebookresearch/DiT),  [ModelScope](https://modelscope.cn/models?name=Dit&page=1)|
| 3) **SiT**: Exploring Flow and Diffusion-based Generative Models with Scalable Interpolant Transformers | [**Paper**](https://arxiv.org/abs/2401.08740), [Github](https://github.com/willisma/SiT), [ModelScope](https://modelscope.cn/models/AI-ModelScope/SiT-XL-2-256/summary)|
| 4) **FiT**: Flexible Vision Transformer for Diffusion Model | [**Paper**](https://arxiv.org/abs/2402.12376), [Github](https://github.com/whlzy/FiT) |
| 5) **k-diffusion**: Scalable High-Resolution Pixel-Space Image Synthesis with Hourglass Diffusion Transformers | [**Paper**](https://arxiv.org/pdf/2401.11605v1.pdf), [Github](https://github.com/crowsonkb/k-diffusion) |
| 6) **OpenDiT**: An Easy, Fast and Memory-Efficient System for DiT Training and Inference | [Github](https://github.com/NUS-HPC-AI-Lab/OpenDiT) |
| 7) **Large-DiT**: Large Diffusion Transformer | [Github](https://github.com/Alpha-VLLM/LLaMA2-Accessory/tree/main/Large-DiT) |
| <h3>Video Generation</h3> | |
| **Paper** | **Link** |
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
| <h3>Long-context</h3> | |
| **Paper** | **Link** |
| 1) World Model on Million-Length Video And Language With RingAttention | [**Paper**](https://arxiv.org/abs/2402.08268), [Github](https://github.com/LargeWorldModel/LWM) |
| 2) Ring Attention with Blockwise Transformers for Near-Infinite Context | [**Paper**](https://arxiv.org/abs/2310.01889), [Github](https://github.com/lhao499/RingAttention) |
| 3) Extending LLMs' Context Window with 100 Samples | [**Paper**](https://arxiv.org/abs/2401.07004), [Github](https://github.com/GAIR-NLP/Entropy-ABF) |
| 4) Efficient Streaming Language Models with Attention Sinks | [**ICLR 24 Paper**](https://arxiv.org/abs/2309.17453), [Github](https://github.com/mit-han-lab/streaming-llm) |
| 5) The What, Why, and How of Context Length Extension Techniques in Large Language Models – A Detailed Survey | [**Paper**](https://arxiv.org/pdf/2401.07872) |
| 6) **MovieChat**: From Dense Token to Sparse Memory for Long Video Understanding | [**CVPR 24 Paper**](https://arxiv.org/abs/2307.16449), [Github](https://github.com/rese1f/MovieChat), [Project](https://rese1f.github.io/MovieChat/) |
| <h3>Base Video Generation Models</h3> | |
| **Paper** | **Link** |
| 1) **ViViT**: A Video Vision Transformer | [**ICCV 21 Paper**](https://arxiv.org/pdf/2103.15691v2.pdf), [Github](https://github.com/google-research/scenic) |
| 2) **VideoLDM**: Align your Latents: High-Resolution Video Synthesis with Latent Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2304.08818) |
| 3) **LVDM**: Latent Video Diffusion Models for High-Fidelity Long Video Generation | [**Paper**](https://arxiv.org/abs/2211.13221), [Github](https://github.com/YingqingHe/LVDM) |
| 4) **LFDM**: Conditional Image-to-Video Generation with Latent Flow Diffusion Models | [**CVPR 23 Paper**](https://arxiv.org/abs/2304.08818), [Github](https://github.com/nihaomiao/CVPR23_LFDM) |
| 5) **MotionDirector**: Motion Customization of Text-to-Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.08465), [Github](https://github.com/showlab/MotionDirector) |
| <h3>Audio Related Resource</h3> | |
| **Paper**  | **Link** |
| 1) **Stable Audio**: Fast Timing-Conditioned Latent Audio Diffusion | [Link](https://stability.ai/research/stable-audio-efficient-timing-latent-diffusion)|
| 2) **MM-Diffusion**: Learning Multi-Modal Diffusion Models for Joint Audio and Video Generation | [**CVPR 23 Paper**](http://openaccess.thecvf.com/content/CVPR2023/papers/Ruan_MM-Diffusion_Learning_Multi-Modal_Diffusion_Models_for_Joint_Audio_and_Video_CVPR_2023_paper.pdf), [Github](https://github.com/researchmm/MM-Diffusion) |
| 3) **Pengi**: An Audio Language Model for Audio Tasks        | [**NeurIPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/3a2e5889b4bbef997ddb13b55d5acf77-Paper-Conference.pdf), [Github](https://github.com/microsoft/Pengi) |
| 4) **Vast:** A vision-audio-subtitle-text omni-modality foundation model and dataset | [**NeurlPS 23 Paper**](https://proceedings.neurips.cc/paper_files/paper/2023/file/e6b2b48b5ed90d07c305932729927781-Paper-Conference.pdf), [Github](https://github.com/TXH-mercury/VAST) |
| <h3>Consistency</h3> | |
| **Paper**  | **Link** |
| 1) Layered Neural Atlases for Consistent Video Editing | [**TOG 21 Paper**](https://arxiv.org/pdf/2109.11418.pdf), [Github](https://github.com/ykasten/layered-neural-atlases), [Project](https://layered-neural-atlases.github.io/), |
| 2) **StableVideo**: Text-driven Consistency-aware Diffusion Video Editing | [**ICCV 23 Paper**](https://arxiv.org/abs/2308.09592), [Github](https://github.com/rese1f/StableVideo), [Project](https://rese1f.github.io/StableVideo/) |
| 3) **CoDeF**: Content Deformation Fields for Temporally Consistent Video Processing | [Paper](https://arxiv.org/pdf/2308.07926.pdf), [Github](https://github.com/qiuyu96/CoDeF), [Project](https://qiuyu96.github.io/CoDeF/) |
| <h3>Dataset</h3> | |
| **Dataset Name**  | **Link** |
| 1) **Panda-70M**: Captioning 70M Videos with Multiple Cross-Modality Teachers | [Paper](https://arxiv.org/abs/2402.19479), [Github](https://github.com/snap-research/Panda-70M), [Project](https://snap-research.github.io/Panda-70M/), |
| 2) **UCF101**: Action Recognition Data Set | [Paper](https://arxiv.org/abs/1212.0402), [Project](https://www.crcv.ucf.edu/research/data-sets/ucf101/), |
| <h3>Existing high-quality resources</h3> | |
| **Resources**  | **Link** |
| 1) Datawhale - AI视频生成学习 | [Feishu doc](https://datawhaler.feishu.cn/docx/G4LkdaffWopVbwxT1oHceiv9n0c) |
| 2) A Survey on Generative Diffusion Model | [**TKDE 24 Paper**](https://arxiv.org/pdf/2209.02646.pdf), [Github](https://github.com/chq1155/A-Survey-on-Generative-Diffusion-Model) |
| 3) Awesome-Video-Diffusion-Models: A Survey on Video Diffusion Models | [**Paper**](https://arxiv.org/abs/2310.10647), [Github](https://github.com/ChenHsing/Awesome-Video-Diffusion-Models) |
| 4) Awesome-Text-To-Video：A Survey on Text-to-Video Generation/Synthesis  | [Github](https://github.com/jianzhnie/awesome-text-to-video)|
| 5) video-generation-survey: A reading list of video generation| [Github](https://github.com/yzhang2016/video-generation-survey)|
| 6) Awesome-Video-Diffusion |  [Github](https://github.com/showlab/Awesome-Video-Diffusion) |
| 7) Video Generation Task in Papers With Code |  [Task](https://paperswithcode.com/task/video-generation) |
| 8) Sora: A Review on Background, Technology, Limitations, and Opportunities of Large Vision Models |  [**Paper**](https://arxiv.org/abs/2402.17177), [Github](https://github.com/lichao-sun/SoraReview) |
| 9) Open-Sora-Plan (PKU-YuanGroup) |  [Github](https://github.com/PKU-YuanGroup/Open-Sora-Plan) |
| 10) State of the Art on Diffusion Models for Visual Computing | [Paper](http://arxiv.org/abs/2310.07204)  |
| 11) Diffusion Models: A Comprehensive Survey of Methods and Applications | [**CSUR 24 Paper**](https://arxiv.org/abs/2209.00796), [Github](https://github.com/YangLing0818/Diffusion-Models-Papers-Survey-Taxonomy) |

## Mini Sora WeChat Community Exchange Group

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

For more details, please refer to the [Contribution Guidelines](./docs/CONTRIBUTING_EN.md)

## Community contributors

<a href="https://github.com/mini-sora/minisora/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=mini-sora/minisora" />
</a>
