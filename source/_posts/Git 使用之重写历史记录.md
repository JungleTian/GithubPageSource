title: Git 使用之重写历史记录
date: 2017-11-16
author: 张天军
category: 技术文章
tags: [git]
photos: [https://ws1.sinaimg.cn/large/006tNc79ly1flj1gjk68dj3069069dfn.jpg]
---

    Git 是免费开源的分布式版本控制系统，主要工作就是确保永远不会丢失已经提交的记录，但是 Git 的设计初衷也是为了让我们掌控开发的工作流程和规范，如 `[adr]fix: resolve NPE at ...` 方便以后查看历史提交记录。然而开发过程中难免会遇到提交信息错误或不符合规范的情况，下面将直奔主题介绍一下如何修改 git 的提交历史记录。

<!--more-->

## **修改最后一个提交记录**

​	当提交的信息不明确、不符合规范或包含敏感信息时，则可以先在本地使用 `git commit --amend` 命令修改后再 push 到远程仓库。这个命令是修改本地最近提交记录的一种便捷方法，将之前的提交记录替换为新的提交记录，而不是创建新的提交记录，操作步骤如下：
    1. 在命令行切换到当前要修改的分支。
    2. 输入 `git commit —amend` 或 `git commit --amend -m ’xxx‘`。 
    3. 在编辑器中，编辑要修改的提交信息并保存（添加 `-m` 参数则跳过此步骤）。

​	若不修改提交信息的情况下，提交新的文件或修改文件内容，例如上次提交漏掉某个文件或添加代码注释，可以添加 `--no-edit` 参数：
    1. 在命令行切换到当前要修改的分支。
    2. 添加暂存区 `git add xxx.txt` 。
    3. 输入 `git commit --amend --no-edit` 命令。

​	**注意：**修改历史提交信息实际上是生成全新的 commit 替换旧的 commit，当前提交的 commit ID ( [SHA-1值](http://smilejay.com/2012/08/git-commit-sha-1/) ) 也会改变，因此要**避免本地分支已经 push 到远程仓库的情况下修改历史提交记录**。 

​	当本地修改提交历史的分支已经在远程仓库时（如下图），远程分支（master）与本地分支（feature）HEAD 指针的 commit ID 不一致，所以 Git 默认认为本地分支不是 `fast-forward` 而不允许 `push`，因此只能先 `git pull`（`fetch` + `merge`） 远程代码才能执行 `push` 操作，我们知道 `merge` 时会产生一次没意义的提交记录，这样反而生成了两次 commit，对其他开发者来说比较困惑，而且历史记录变得更不清晰。

![](https://ws2.sinaimg.cn/large/006tNc79ly1flislphzggj30hc08sdgm.jpg)

## **修改多次提交记录** 

​	`git rebase ` 命令可以修改多次提交历史，你可以重新排序，修改或合并多个提交记录。大多数情况下，使用 `git rebase` 命令的主要场景：

### **1. 修改多个提交信息**
如下图将 Feature 分支 `fix update` 和 `fix update2` 两次 commit 信息按标准规范修改提交信息：

![](https://ws1.sinaimg.cn/large/006tNc79ly1flisnqwr9sj30gd092dgw.jpg)

1. 使用 `git rebase -i HEAD~n` 命令可在默认编辑器中显示 `n` 条最近提交历史的列表。

   ```
   pick 4e77435 first commit
   pick 994b124 [adr]完成需求
   pick 09di13d fix update
   pick 1a2c0f7 fix update2

   # Rebase 4e77435..1a2c0f7 onto 4e77435 (4 commands)
   #
   # Commands:
   # p, pick = use commit 
   # r, reword = use commit, but edit the commit message
   # e, edit = use commit, but stop for amending 
   # s, squash = use commit, but meld into previous commit 
   # f, fixup = like "squash", but discard this commit's log message 
   # x, exec = run command (the rest of the line) using shell 
   # d, drop = remove commit 
   #
   # These lines can be re-ordered; they are executed from top to bottom.
   #
   # If you remove a line here THAT COMMIT WILL BE LOST.
   #
   # However, if you remove everything, the rebase will be aborted.
   #
   # Note that empty commits are commented out
   ```

2.  将要修改的 commit 的 `pick` 命令修改为 `reword` 并保存退出：

   ```
   pick 4e77435 first commit
   pick 994b124 [adr]完成需求
   reword 09di13d fix update
   reword 1a2c0f7 fix update2
   ```

3. 按顺序依次打开文本编辑器，按标准规范编辑提交信息并依次保存退出，`git log` 查看历史信息：

   ```
   * 01ac0f7 - (HEAD -> master) [adr]添加注释 (4 minutes ago) <jungletian>
   * 085fc03 - [adr]优化代码 (4 minutes ago) <jungletian>
   * 994b124 - [adr]完成需求 (27 hours ago) <jungletian>
   * 4e77435 - first commit (4 weeks ago) <jungletian>
   ```

### **2. 合并多个提交**

​	如下图，为了使 Feature 分支保留清晰的提交历史记录，将后面两次的 commit 合并到一个 commit 再 push 到远程仓库：

![](https://ws3.sinaimg.cn/large/006tNc79ly1flisj8c5zuj30f8063wex.jpg)

1. 按上文执行 `git rebase -i HEAD~n` 命令。

2. 将最后两次 commit 的 `pick` 命令修改为 `fixup`，根据自己情况决定是否需要重写（reword）合并之后的提交信息：

   ```
   pick 4e77435 first commit
   reword 994b124 [adr]完成需求
   fixup 085fc03 [adr]优化代码
   fixup 01ac0f7 [adr]添加注释
   ```

3. 保存退出编辑器，如果使用 `reword` 命令则会打开新的编辑器，输入新的提交信息并保存退出 (wq)：

   ```
   [adr]完成需求 + 优化代码 + 添加注释

   # Please enter the commit message for your changes. Lines starting
   # with '#' will be ignored, and an empty message aborts the commit.
   #
   # Date:      Tue Nov 14 14:31:54 2017 +0800
   #
   # interactive rebase in progress; onto d4b6ad8
   # Last commands done (1 commands done):
   #    r 994b124 [adr]完成需求
   # Next commands to do (2 remaining commands):
   #    f 085fc03 [adr]优化代码
   #    f 01ac0f7 [adr]添加注释
   # You are currently editing a commit while rebasing branch 'master' on 'd4b6ad8'.
   #
   # Changes to be committed:
   #       new file:   f.txt
   ```

### 3. **`git pull --rebase`**

​	当多人维护一个分支时，你的同伴先于你 `push` 了代码到远程分支上，所以按上文提到的 Git 默认策略，你必须先执行 `git pull` 来获取同伴的提交，然后才能 `push` 自己的提交到远程分支。上文介绍了 Git 的默认策略，会执行一次  `merge` 操作，因此产生一次没意义的提交记录。

​	其实在 `git pull` 操作的时候，使用 `git pull --rebase` 选项即可很好地解决上述问题。 加上 `--rebase` 参数的作用是，提交线图有分叉的话，Git 会 rebase 策略来代替默认的 merge 策略。 使用 rebase 策略有什么好处呢？下图就可以很好地说明清楚了：

![](https://ws1.sinaimg.cn/large/006tKfTcly1fl9eqclcyhj30g00c93z2.jpg)



## **数据永远不会丢失**

​	在使用 Git 过程中，修改历史记录相对来说是一个比较危险的动作，有时会操作不小心“丢失”了 commit 信息，但是我们开篇已经介绍了 Git 的主要工作就是确保永远不会丢失已经提交的记录，因此 Git 提供了 `git reflog` 命令来查看所有提交过的 commit 信息，一般操作步骤如下：

1. 命令行切换到指定分支，执行 `git reflog`/`git log -g` 命令。

   ```
   ebacbc7 (HEAD -> master) HEAD@{0}: reset: moving to ebacbc703ee082ad3551982ceafe37e96e07813a
   d4bdce4 HEAD@{1}: commit: 丢失了信息
   2ee891c HEAD@{2}: rebase -i (finish): returning to refs/heads/master
   2ee891c HEAD@{3}: rebase -i (reword): [adr]添加注释
   6bcaf2d HEAD@{4}: rebase -i (reword): [adr]优化代码
   bd857f4 HEAD@{5}: rebase -i: fast-forward
   ebacbc7 (HEAD -> master) HEAD@{6}: rebase -i (start): checkout refs/remotes/origin/master
   ...
   ```

2. 复制要回退的 commit ID  并退出文本编辑器，命令行执行 `git reset --hard <commitID>` 或 checkout 一个新的分支。 

3. 命令行执行 `git log --pretty=oneline` 查看当前历史提交信息是否正确，如果不正确仍可按照第一个步骤继续操作。


## **总结**

​	Git 是一个当前最流行的分布式版本控制工具之一，其可以完全离线操作的特点直中 SVN 的痛点，因此深受开发者喜爱，关于 Git 的要学习的内容还有很多，本篇文章只介绍了其中的一部分—重写历史记录，后续会持续给大家分享关于 Git 使用上的技巧和使用场景。如果有不完善或者表述不正确的地方欢迎大家指正，谢谢！

### **参考文献**
[Rewriting history](https://www.atlassian.com/git/tutorials/rewriting-history) 
[Changing a commit message](https://help.github.com/articles/changing-a-commit-message/) 
[About Git rebase](https://help.github.com/articles/about-git-rebase/) 
[About pull request merges](https://help.github.com/articles/about-pull-request-merges/) 
[洁癖者用 Git：pull --rebase 和 merge --no-ff](http://hungyuhei.github.io/2012/08/07/better-git-commit-graph-using-pull---rebase-and-merge---no-ff.html) 



