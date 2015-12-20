---
layout: post
title: 两种 GitHub Pages 模式搭建博客
description: 你也许听说过可以利用 GitHub Pages 搭建博客，你也许查阅过许多的文章教程，你甚至已经开始动手并成功的搭建起了自己的博客。但是，你知道这个世界上原来还有两种不同的 GitHub Pages 模式吗？
keywords: GitHub,jeklly,gh-pages,GitHub Pages,blog,git
category: [致知录]
tags: [GitHub,jeklly,gh-pages,GitHub Pages,blog,git]
---

当我寻思着折腾 GitHub 多帐号的使用时，我其实只是想利用 GitHub Pages 服务多建几个博客，正巧这周上的一门课（[]()）里提到 GitHub 的多博客策略，我才知道原来一个 GitHub 账号下是能利用 GitHub Pages 建立多个博客的。

在 GitHub 上搭建博客依赖于 GitHub Pages, 而 GitHub Pages 实际上有两种模式：
1. 个人帐号或组织帐号的 Pages;
2. 项目 Pages.

个人/组织的 Pages 估计是大家见得比较多的，当你在别的地方看到类似于“每个帐号只能建一个”这样的话的时候，它其实指的就是个人/组织 Pages. 它对仓库的命名有要求（username/username.github.io），它有一个漂亮的地址供访问（http://username.github.io），它**不需要 gh-pages 分支**。

而项目 Pages 最大的特点是，它使用 gh-pages 分支来构建项目主页，既你想要的博客。

如果同时使用了以上两种 Pages 模式并且又绑定了独立域名，有可能会踩到坑……这个等踩到坑再说，或参阅参考文章。

下面进入操作模式——

### 以下是本次操作过程记录

先在 GitHub 上建个空仓库。然后把以下步骤照做一遍，在`add`这一步之前我先下载了一个自己满意的主题放到根目录上了：

    $ git clone https://github.com/username/project.git  
    $ git checkout --orphan gh-pages  
    $ git rm -rf .  
    $ git add .  
    $ git commit -a -m "First pages commit"  
    $ git push origin gh-pages

然后，setting 是这样的：
> Your site is ready to be published at http://yclub.github.io/Blog. 
>  Your site is published at http://yclub.github.io. 
真·相片：
![]()  
![]()

然而并不能访问，两个都不能。  
查看分支，有两个：  
![]()

依稀记得想要使用 Pages 服务是要把默认分支改为 gh-pages 分支的，于是到网页上手动更改（呃，不会用命令行改……）：
![]()  

改完后出现两种情况：
- Project Pages 成功了，虽然还很难看，但至少不再是 404 了。
- Organization Pages 仍然 404 。

猜想这应该是组织主页和项目主页的不同造成的。通过搜索、对比不同文章，感觉问题出在这：项目主页需要 gh-pages ，个人/组织主页不需要，直接在 master 主分支发布。  
于是接下来做了个验证：
1. 恢复 master 分支为默认分支
1. 合并 gh-pages 分支到主分支上
1. push

重做后，果然成功了。  
这里要注意的是，需要稍等片刻再打开主页链接，刚操作完立刻打开链接有可能还是 404 状态，我差点就要重新排查问题了……

至此，两种形式的 pages 皆操作成功。

关于博客的搭建到此就告一段落了。下面说些别的。  
我们来对比下搭建好之后两个博客的地址：  
	http://yclub.github.io
	http://yclub.github.io/Blog

第一个好理解，个人/组织主页的网址本来就是这个样子的，估计大部分人心里想要的也是这个样子的。  
但第二个呢？好像有点……陌生？是，我们是创建了一个名为 Blog 的仓库，但仓库的地址却是`http://github.com/username/projectname`这样的啊？

- 如果没有使用独立域名，project pages将通过子路径的形式提供服务username.github.com/projectname
- 如果user/org pages使用了独立域名，那么托管在账户下的所有project pages将使用相同的域名进行重定向，除非project pages使用了自己的独立域名；

顺便，如果你绑定的独立域名后来不能访问了，记得查看[这里](https://help.github.com/articles/my-custom-domain-isn-t-working)

### 参考资料
[]()