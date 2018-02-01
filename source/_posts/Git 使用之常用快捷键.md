title: Git 使用之常用快捷键
date: 2017-11-30
author: 张天军
category: 技术文章
tags: [git]
photos: [https://ws1.sinaimg.cn/large/006tNc79ly1flj1gjk68dj3069069dfn.jpg]
---

### **Git 使用的常用快捷键**

    上篇文章给大家分享了重写历史记录的文章之后，有热爱和喜欢学习 Git 的小伙伴咨询相关问题，也解决了部分问题，介于很多小伙伴对 Git 的关注和使用，因此分享一篇这篇文章


<!--more-->

### [猴子都能懂的 git 入门](http://backlogtool.com/git-guide/cn/)


命令 | 描述
---|---
`ssh-keygen -t rsa -C ""` | 生成 ssh key
`git reflog` | 查看所有 log
`git cherry-pick commit_id` | 樱桃摘取
`git fetch --all --tags --prune` | 拉取所有的 tag
`git remote add [name] [url]` | 添加远程仓库
`git remote -v` | 查看远程仓库
`git remote rm [name]` | 删除远程仓库
`git remote set-url --push[name][newUrl]` | 修改远程仓库
`git pull [remoteName] [localBranchName]` | 拉取远程仓库
`git pull [remoteName] [localBranchName] --allow-unrelated-historie` | 允许拉取未关联历史的分支
`git push [remoteName] [localBranchName]` | 推送远程仓库
`git branch -r` | 查看远程分支
`git branch -m <oldname> <newname>` | 将 `oldname` 分支重命名
`git branch -m <newname>` | 重命名当前分支
`git branch -D <name>` | 删除本地分支
` git merge [name] ` | 将名称为[name]的分支与当前分支合并
`git push origin [name]` | 创建远程分支(本地分支push到远程)
`git push origin test:master` | 提交本地test分支作为远程的master分支 
`git push origin test:test` | 提交本地test分支作为远程的test分支
`git push origin --delete <name>` | 删除远程分支
`git tag` | 查看版本
`git tag [name]` | 创建版本
`git tag -d [name]` | 删除版本
`git tag -r` | 查看远程版本
`git push [remote] [tag]` | 提交指定版本
`git push origin :refs/tags/[name]` | 删除远程版本
`git submodule add [url] [path]` | 添加子模块 `git submodule add git://github.com/soberh/ui-libs.git src/main/webapp/ui-libs`
`git submodule init` | 初始化子模块 -只在首次检出仓库时运行一次就行
`git submodule update` | 每次更新或切换分支后都需要运行一下
`git init` | 在当前目录新建一个Git代码库
`git init [project-name]` | 新建一个目录，将其初始化为Git代码库
`git clone [url]` | 下载一个项目和它的整个代码历史
`git add [file1] [file2] ...` | 添加指定文件到暂存区
`git rm [file1] [file2] ...` | 删除工作区文件，并且将这次删除放入暂存区
`git commit -m [message]` | 提交暂存区到仓库区
`git commit -a` | 提交工作区自上次commit之后的变化，直接到仓库区
`git commit [file1] [file2] ... -m [message]` | 提交暂存区的指定文件到仓库区
`git commit --amend -m [message]` | 如果代码没有任何新变化，则用来改写上一次commit的提交信息
`git diff --cached []` | 显示暂存区和上一个commit的差异
`git diff HEAD` | 显示工作区与当前分支最新commit之间的差异
`git diff [first-branch]...[second-branch]` | 显示两次提交之间的差异
`git checkout .` | 恢复上一个commit的所有文件到工作区
`git checkout [file]` | 恢复暂存区的指定文件到工作区
`git checkout [commit] [file]` | 恢复某个commit的指定文件到工作区
`git checkout -b [name]` | 创建新分支并立即切换到新分支
`git checkout -b newbranch tagname` | 检出并创建分支 newbranch 以 tagname 的 tag 为 base
`git reset [file]` | 重置暂存区的指定文件，与上一次 commit 保持一致，但工作区不变
`git reset --hard` | 重置暂存区与工作区，与上一次 commit 保持一致
`git reset [commit]` | 重置当前分支的指针为指定 commit，同时重置暂存区，但工作区不变
`git reset --hard [commit]` | 重置当前分支的 HEAD 为指定 commit，同时重置暂存区和工作区，与指定 commit 一致
`git revert [commit]` | 新建一个commit，用来撤销指定 commit - 后者的所有变化都将被前者抵消，并且应用到当前分支
`git archive` | 生成一个可供发布的压缩包
`git svn` | 从 svn 迁移到 git. see more: `git svn --help`

注，删除子模块：

1) git rm --cached [path]
2) 编辑“.gitmodules”文件，将子模块的相关配置节点删除掉
3) 编辑“.git/config”文件，将子模块的相关配置节点删除掉
4) 手动删除子模块残留的目录


