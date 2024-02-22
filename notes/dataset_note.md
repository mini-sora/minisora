# 数据

## Sora技术报告节选
> We first train a **highly descriptive captioner model** and then use it to produce text captions for all videos in our training set.
> 
> 我们首先训练一个高度描述性的字幕模型，然后用它为我们训练集中的所有视频生成文字字幕。

用AI assistant辅助生成高质量数据集，用于进行更大规模AI的训练。


> Similar to DALL·E 3, we also leverage GPT to turn short user prompts into longer detailed captions that are sent to the video model. This enables Sora to generate high quality videos that accurately follow user prompts.
>
> 与DALL·E 3类似，我们也利用GPT将用户的简短提示转化为发送给视频模型的更长的详细字幕。这使得Sora能够生成准确遵循用户提示的高质量视频。
  
AI assistant - Prompt工程： 将人为输入的prompt改写成更高质量的prompt。即，重述提示词技术（RePrompt）。

## 视频-文本生成模型

用于高质量大规模数据集构建。

- **BibiGPT**: [Bilibili](https://www.bilibili.com/video/BV1fX4y1Q7Ux/?vd_source=dd5a650b0ad84edd0d54bb18196ecb86) , [Github](https://github.com/JimmyLv/BibiGPT-v1)

- **VideoBERT**：一个早期尝试，利用自监督学习在大规模未标注视频上训练，以理解视频内容并生成描述文本。

- **S3D (Separable 3D ConvNets)**：使用3D卷积网络处理视频帧，捕捉时间和空间信息，常与语言模型结合用于视频理解和描述。

- **HERO (Hierarchical Encoder Representation for Video+Language Omni-representation)**：专为视频+语言任务设计，通过分层编码器提高了视频理解和文本生成的能力。

- **ViLBERT (Vision-and-Language BERT)** 和 **VideoBERT**：这两个模型结合了视觉和语言信息，通过类似BERT的结构实现跨模态理解，可以用于视频描述生成。

- **OpenAI's CLIP**：虽然CLIP主要设计用于图像和文本的匹配，但其强大的跨模态理解能力也被应用于视频内容的理解和描述。

- **Transformer-based models**：基于Transformer的模型，如GPT和BERT，通过预训练和微调，也可以应用于视频描述的任务。

## 重述提示词技术

- **RePrompt**: Automatic Prompt Editing to Refine AI-Generative Art Towards Precise Expressions [Paper](https://arxiv.org/abs/2302.09466)
- Retrieval-Enhanced Visual Prompt Learning for Few-shot Classification [Paper](https://arxiv.org/pdf/2306.02243.pdf)
- [deepgram.com/ai-apps/reprompt](https://deepgram.com/ai-apps/reprompt) , [foundr.ai/product/reprompt](https://foundr.ai/product/reprompt)
