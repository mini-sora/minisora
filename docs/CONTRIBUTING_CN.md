# 如何向Mini Sora 社区贡献

Mini Sora 开源社区定位为由社区同学自发组织的开源社区（**免费不收取任何费用、不割韭菜**）

我们非常希望你们能够为 Mini Sora 开源社区做出贡献，并且帮助我们把它做得比现在更好！如果你首次为 Mini Sora 做贡献，可以查看 [good first PR](https://github.com/mini-sora/minisora/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+PR%22) 的 issue 列表。

## 提交请求（PR）

作为贡献者，在你提交你的请求之前，以下是我们希望你遵循的规范：

1. 首先，在 [Mini Sora GitHub](https://github.com/mini-sora/minisora/pulls) 中搜索与您想要提交相关的内容开放或关闭的 PR。我们想您也不希望重复现有的工作。

2. 然后 [Fork](https://github.com/mini-sora/minisora/fork) [minisora](https://github.com/mini-sora/minisora) 仓库，并下载你的仓库到本地

   ```
   git clone 【你fork的仓库地址】
   ```

3. 添加mini-sora原仓库，方便同步远程仓库最新的更新

   ```
   git remote add upstream https://github.com/mini-sora/minisora
   ```
   
4. 同步主仓库代码到你本地，以及同步回你fork的远程仓库

   ```
   # 从upstream分支上，拉取最新代码
   git fetch upstream
   # 切换到main分支上
   git checkout main
   # 把upstream分支上的更新内容合并到mian上,本地的main分支就和上游同步了
   git merge upstream/main
   # 还需把本地main同步到【你fork的仓库地址】的远程分支
   git push origin main
   ```

   > 注意：每次开始提交前，请先同步主仓库的代码

   

5. 在你自己fork的仓库，请创建一个分支用于提交你的变更内容。分支名尽可能的有一定意义。

   ```
   git checkout -b my-docs-branch main
   ```

6. 在你的分支上面进行修改，提交commit时，请按照我们的[Commit消息格式](#Commit消息格式)进行编写commit描述，当你是添加了论文，在填写论文索引时，请按照[论文命名规范](#论文命名规范)填写索引数据。

   ```
   git commit -m "[docs]: xxxx"
   ```

7. 提交数据到你的GitHub仓库

   ```
   git push origin  my-docs-branch
   ```

8. 回到GitHub仓库页面，提交PR到`minisora:main`

9. 加入"最近更新"的工作栏目中添加的工作应该与视频生成有关，并且应该是非常令人印象深刻的工作。

## Commit消息格式

提交的 commit message  必须包含`<type>`和`<summary>`两部分

```
[<type>]: <summary>
  │        │
  │        └─⫸ 简短描述你的修改内容，结尾没有句号
  │
  └─⫸ Commit Type: |docs|feat|fix|refactor|
```

### Type 

* **docs**：当你修改了文档，或者添加了文档，选择`docs`

以下类型是如果后续涉及到代码协作预留

* **feat**：这里是指一个新的功能
* **fix**：修复bug
* **refactor**: 重构代码，不涉及新功能或者bug修复

### summary

* 用英文描述修改的内容，不要用句号(.)结尾

> eg: git commit -m "[docs]: add a contributing.md file"

## 论文命名规范

>格式—— [**期刊名**] 论文名称
>
>样例1——[**CVPR 24** paper] **lovieChat**: From Dense Token to Sparse Memory for Long Video Understanding
>
>样例2——[**Paper**] **Sora**: Creating video from text
