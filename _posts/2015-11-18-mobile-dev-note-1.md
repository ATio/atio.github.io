---
layout: post
title: 移动端开发中背景图的处理
description: 移动端开发中一些适合当作背景图的图片的处理。
keywords: 移动端开发
category: [致知录]
tags: []
---

一直以为图片用CSS设置背景图的方式无法做到随屏幕大小变化而变化。今天看到一个例子，记录一下。

html 结构：

	<div class="nav">
		<ul>
	    	<li>
	        	<i class="idt"></i>
	            <p>订单</p>
	        </li>
	    	<li class="pt-line">
	        	<i class="clt"></i>
	            <p>收藏</p>
	        </li>
	    	<li>
	        	<i class="rcm"></i>
	            <p>推荐</p>
	        </li>
	    </ul>
	</div>

CSS 代码：

	.idt{
		display:block; 
		position:absolute; 
		top:0.11rem; 
		left:0.68rem; 
		float:left; 
		width:0.28rem; 
		height:0.36rem; 
		background:url(../img/indent.png) no-repeat;
		background-size:0.28rem 0.36rem;
	}

要点：  
- html 中用一个`<i>`标签做锚点，pos-a定位。
- `<i>`标签外层需要一个pos-r的父元素。
- css 中设置`background-size`，大小就是图片的大小，单位为rem。

全文中会多出不少无意义的空标签（\<i\>标签及\<i\>标签的父元素），算是硬伤吧。

另，移动端也可以用浮动的……
