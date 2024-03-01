# How to contribute to the Mini Sora community

The Mini Sora open-source community is positioned as a community-driven initiative (**free of charge and devoid of any exploitation**) organized spontaneously by community members. 

We really hope that you can contribute to the Mini Sora open source community and help us make it better than it is now!

## Submitting a Pull Request (PR)

As a contributor, before submitting your request, here are the guidelines we hope you follow:

1. Firstly, please search in the [Mini Sora GitHub](https://github.com/mini-sora/minisora/pulls) to see if there are any open or closed pull requests related to the content you intend to submit. We assume you wouldn't want to duplicate existing work.

2. Next, [fork](https://github.com/mini-sora/minisora/fork) the [minisora](https://github.com/mini-sora/minisora) repository, and download your forked repository to your local machine.

   ```
   git clone 【your-forked-repository-url】
   ```

3. To add the original Mini Sora repository as a remote and facilitate syncing with the latest updates:

   ```
   git remote add upstream https://github.com/mini-sora/minisora
   ```
   
4. Sync the code from the main repository to your local machine, and then sync it back to your forked remote repository.

   ```
   # Pull the latest code from the upstream branch
   git fetch upstream
   
   # Switch to the main branch
   git checkout main
   
   # Merge the updates from the upstream branch into main, synchronizing the local main branch with the upstream
   git merge upstream/main
   
   # Additionally, sync the local main branch to the remote branch of your forked repository
   git push origin main
   ```

   > Note: Before starting each submission, please synchronize the code from the main repository.

   

5. In your forked repository, please create a branch for submitting your changes. The branch name should preferably be meaningful.

   ```
   git checkout -b my-docs-branch main
   ```

6. While making modifications on your branch and committing changes, please adhere to our [Commit Message Format](#Commit-Message-Format) for composing commit descriptions. If you're adding a paper, please follow the [Paper Naming Convention](#Paper-Naming-Convention) when filling in the paper index information.

   ```
   git commit -m "[docs]: xxxx"
   ```

7. Submit your data to your GitHub repository.

   ```
   git push origin  my-docs-branch
   ```

8. Go back to the GitHub repository page and submit a pull request to `minisora:main`.

9. The works added to the "最近更新" Section should be related to Video Generation and should be a Very Impressive Work.

## Commit Message Format

The commit message must include both `<type>` and `<summary>` sections.

```
[<type>]: <summary>
  │        │
  │        └─⫸ Briefly describe your changes, without ending with a period.
  │
  └─⫸ Commit Type: |docs|feat|fix|refactor|
```

### Type 

* **docs**：When you modify a document or add a document, select `docs`

The following types are reserved for future code collaboration if needed.

* **feat**：Here it refers to a new feature.
* **fix**：fix bug
* **refactor**: Refactor code, no new features or bug fixes involved

### summary

* Describe the modifications in English, without ending with a period (.)

> eg: git commit -m "[docs]: add a contributing.md file"

## Paper Naming Convention

```
# [Journal Name] Paper Title
[CVPR 24] lovieChat: From Dense Token to Sparse Memory for Long VideoUnderstanding
```

