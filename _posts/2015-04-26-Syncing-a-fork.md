---
layout: post
title: 如何快速同步派生（Fork）仓库
description: 在 github 上 fork 了一个仓库，当原始远程仓库更新了，如何快速同步 fork 来的仓库到最新版本呢？如果你也有此问题，那么本文也许可以帮到你。
keywords: github,fork,sync
category: [致知录]
tags: [github,fork]
---
如何同步更新自己 Fork 的仓库代码？曾经这个问题困扰着我，以至于我都不敢 fork 了！但现在，我不怕不怕啦，我有个好办法，我不怕不怕不怕啦，遇到好码，我马上 fork 过来……呃，打住- -

以下以我同步 awthink/ife 为例，在操作的时候请注意替换用户名和仓库地址。

**注意事项：在同步自己 Fork 的仓库代码之前，务必先把自己在本地的更改进行提交。**

# 准备工作

- 将自己在 github 上 fork 来的分支 clone 下来（一般来说这个应该已经做过了）

` git  clone git@github.com:awthink/ife.git`

![克隆](http://xuwenrong.qiniudn.com/net/img/Syncing-fork-clone.jpg)

# 开始同步

## 1. Configuring a remote for a fork

1. 使用 git remote -v 查看远程状态。
2. 添加一个远程原始分支的上游仓库（一般命名为 upstream，如果以前已经执行过本操作，则可忽略）。
3. 再次 git remote -v 以确认。

![Configuring a remote for a fork](http://xuwenrong.qiniudn.com/net/img/Syncing-fork-remote.jpg)

## 2. Syncing a fork

- 把远程原始分支的代码拉到本地

`git fetch upstream`

![fetch](http://xuwenrong.qiniudn.com/net/img/Syncing-fork-fetch.jpg)

- 切换到本地主分支(如果不在的话)

`git branch` 检查
`git checkout master` 切换

- 把 upstream/master 分支合并到本地 master 上，这样就完成了同步，并且不会丢掉本地修改的内容。

`git merge upstream/master`

![merge](http://xuwenrong.qiniudn.com/net/img/Syncing-fork-merge.jpg)

内容超过一屏，仅截了一部分图。

- 最后便可以把最新的代码推送到github上

`git push origin master`

![ push](http://xuwenrong.qiniudn.com/net/img/Syncing-fork-push.jpg)


至此，你已成功更新了 fork 来的仓库代码。

# 参考资料

1. 官方文档：[Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
2. [同步一个 fork](http://gaohaoyang.github.io/2015/04/12/Syncing-a-fork/)