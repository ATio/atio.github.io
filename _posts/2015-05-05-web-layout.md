---
layout: post
title: 基础网页布局
description: 基础的网页布局实现方式。包含一、二、三列布局等多重情况。
keywords: 网页布局
category: [致知录]
tags: [web,layout]
---
# 简介

这是慕课网上[《网页布局基础》](http://www.imooc.com/learn/95)这门课程的概要。介绍了自动居中的单列布局实现方式和两列布局的两种不同的实现方式。

已增补三列布局。

# 自动居中一列布局

要点：给元素设置一定宽度，并将margin左右两边的值设为auto时，即可实现自动居中布局。

	#wrap{
		width: 960px;
		margin: 0 auto;
	}

# 横向两列布局

横向两列布局有两种实现方式：浮动（float）和绝对定位（position:absolute）。

## 浮动（float）

要点：两块元素均设置浮动，可以

- 分别设置为左浮动和右浮动；
- 均设置为左浮动，同时设置`margin`隔开。

		#main {
			width: 960px;
			margin:0 auto;
		}

		.left {
			width: 200px;
			float: left;
		}

		.right {
			width: 700px;
			float: left;
			margin-left: 60px;
		}

width 设置为百分数，就是两列自适应的布局；设置像素值，就是定宽的。

## 绝对定位（position）

适用于一列固定宽度，另一列自适应的布局当中。

要点：最近的父元素设置相对定位，自适应那一列设置绝对定位，再设置适合的偏移量，如margin-left。

注意：使用此方法，固定宽度那一列的高度必须大于自适应那列，否则自适应那一列的内容会覆盖下面的内容（设置绝对定位的元素会脱离文档流）。

也因为它有此限制，所以在实际应用中并不常用。

	#main {
		width: 100%;
		position: relative;
	}

	.left {
		width: 200px;
	}

	.right {
		position: absolute;
		margin-left: 210px;
	}

### 更新另一种表现形式

为什么说是另一种表现形式，因为原理仍然是上面的原理，只是换了个思路。

绝对定位知识回顾：绝对定位相对于离它最近的设置了定位的父元素进行偏移，如没有，则相对根元素`html`进行偏移。

因此在简单的布局当中，可以让它根据`html`进行定位。下例中`top:50px;`即为相对根元素进行的定位。以下的高和背景色都是为了在浏览器中便于不同元素而设置的，非必须。

	#main {
		height:100px;background-color: #f00;}

	.left {
		width: 200px;
		height:100px;
		position:absolute;
		left:0;
		top:50px;
		background-color: #0000FE;
	}

	.right {
		height:100px;
		margin-left:210px;
		background-color: #9ACC99;
	}

# 三列布局

左右两边用绝对定位固定住，中间部分用marigin。想要自适应就用百分比，想要固定就用像素值，但中间部分都是自适应的。

## 三列自适应布局

	div { 
		text-align:center;
		line-height:50px；
	}

	.left {
		width:20%;
		position:absolute;
		left:0;
		top:0；
	}

	.main{
		margin:0 20%;
	}

	.right{
		width:20%;
		position:absolute;
		top:0;
		right:0;
	}

## 三列左右固定布局

	div{
		text-align:center;
		line-height:50px;
	}

	.left{
		width:240px;
		position:absolute;
		left:0;
		top:0
	}

	.main{
		margin:0 240px;
	}

	.right{
		width:240px;
		position:absolute;
		top:0;
		right:0;
	}

