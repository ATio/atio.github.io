---
layout: post
title: 初探 HTML&CSS 相对路径
description: HTML的链接和CSS中的图片引用，经常需要用到相对路径。那么什么是相对路径？如何运用？今天就来做个梳理。如果你也经常写错相对路径，不妨点进来看一看。
keywords: 相对路径,绝对路径
category: [致知录]
tags: [RelativePath,AbsolutePath,HTML,CSS]
---

# 前言

相对路径和绝对路径的概念似乎没什么难的，因为我们都学过物体的相对运动，相对的理解起来就比较容易。但是懂得了概念不代表就不会出错了，事实上在过去相对路径常常是令我头疼的一个问题，十次错八次。今天就来梳理一下，如果你也有类似的烦恼，那么这篇文章也许可以帮到你。

首先假设有如下目录结构：

    /
      |- images
        |- logo.png
        |- nav-icon.png
        |- 404.jpg
      |- css
        |- style.css
        |- bootstrap.min.css
      |- index.html
      |- about.html
      |- 404.html
      |- page
        |- archive.html

然后说一个我观察总结出来的“三步走”，如果不准，请指正：

1. 先对比两个文件的绝对路径，提取“公因式”，去掉相同的部分；
2. 看源文件还剩几个上级的目录，剩几级，写几个`../`；
3. 把 2 的`../`加到目标文件（剩余的）目录前。

下面，我们开始针对不同情况的相对路径引用进行举例。

# 1. 同目录文件引用

同目录引用比较简单，我们使用`./`来表示当前所在的目录，不过一般都会省略掉，直接写文件名即可.

如，index.html 链接 about.html 可以这么写：

	<a href = "./about.html">关于我们</a>
	或
	<a href = "about.html">关于我们</a>

# 2. 下级目录文件引用

先说个概念，此概念同样适用于下一节：`../`表示源文件所在目录的上一级目录，`../../`表示源文件所在目录的上上级目录，以此类推。

**验证：**

index.html要引入css，怎么写？首先我们按“三步走”的步骤来分析一下：

1. 两个文件的目录结构是这样子的：

		index.html
		css/style.css

2. index.html 上面已经没有更上一层的目录了，所以是0个`../`，也就是不写。
3. 第2步既然没有，那目标文件的目录就照抄就好了：`css/style.css`

所以在index.html中引入css文件可以这么写：

	<link rel="stylesheet" href="css/style.css">

404.html要引用图片404.jpg，怎么写？

	<img src="images/404.jpg" alt="">

# 3. 上级目录文件引用

那么引用上一级目录的文件如何写呢？先对上面的结构做个改造，增加一个名为page的文件夹，并在其中增加一个页面archive.html。然后为archive增加一个返回首页的链接。

1. 同样地分析，两个文件的目录结构分别为：

		index.html
		page/archive.html

2. archive.html 上面有一个文件夹，所以待会要写一个`../`
3. 因为index.html前面没有目录了，所以就把`../`直接加在它前面，变成`../index.html`

所以在archive中增加一个返回首页的链接应该这么写：

	<a href="../index.html"></a>

# 4. 交叉引用

跨目录、非线性层级的引用，暂且称之为交叉引用吧。譬如archive中引入css，css中将图片logo.png作为背景图片引入。

	<link rel="stylesheet" href="../css/site.css">

	.logo {
	    background-image: url(../images/logo.png);
	}

# 结语

至此，我们通过举例分析了不同情况下相对路径的写法，看完后你是否已了然于胸？关于相对路径的写法，如有任何疑问，欢迎留言探讨。