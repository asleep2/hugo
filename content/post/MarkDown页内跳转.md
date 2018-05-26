---
title: "MarkDown页内跳转"
date: 2018-04-23T13:20:06+08:00
lastmod: 2018-04-23T13:20:06+08:00
draft: false
url: /archives/120
keywords: ["MarkDown"]
description: ""
tags: ["Markdown"]
categories: ["博客系统"]
author: "3mile"

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/5.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/5.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---


上一篇博文里跟大家一起啃了啃 Markdown 的语法，其实已经可以满足写博文的基本需求了。Markdown 的本意是想让博主们专注内容的撰写而不是排版，但是如果硬要想做出更漂亮的排版，就需要偷偷学习一些黑魔法👊🎩。

有时候一篇博文太长，我们会想建立一个目录，让小伙伴们能在宏观上把握全文的同时又可以自由的进行页内跳转，立即穿越到自己感兴趣的段子。今天就来聊一聊构建一个支持页内跳转的目录都有些什么奇技淫巧😏。

方法一：Markdown 和 HTML 混编
废话不多说直接看代码：

```html
* [主标题1](#1)
	* [副标题1.1](#1.1)
		* [次级副标题1.1.1](#1.1.1)
	* [副标题1.2](#one-point-two)

<h1 id="1">主标题1</h1>
文本内容。。。

<h2 id="1.1">副标题1.1</h2>
文本内容。。。

<h3 id="1.1.1">次级副标题1.1.1</h3>
文本内容。。。

<h2 id="one-point-two">副标题1.2</h2>
```

* [主标题1](#1)
	* [副标题1.1](#1.1)
		* [次级副标题1.1.1](#1.1.1)
	* [副标题1.2](#one-point-two)

<h1 id="1">主标题1</h1>
文本内容。。。

<h2 id="1.1">副标题1.1</h2>
文本内容。。。

<h3 id="1.1.1">次级副标题1.1.1</h3>
文本内容。。。

<h2 id="one-point-two">副标题1.2</h2>
这是为了演示id也可以设置成*英文*字母
效果：

主标题1
副标题1.1
次级副标题1.1.1
副标题1.2
主标题1
文本内容。。。

副标题1.1
文本内容。。。

次级副标题1.1.1
文本内容。。。

副标题1.2
这是为了演示id也可以设置成英文字母

方法二：Markdown 和 HTML 混编，利用 HTML 元素创建 “锚”
其实第一种方法里已经有 “锚” 的概念了。看如下代码：

```html
* [主标题1](#1)
	* [副标题1.1](#1.1)
		* [次级副标题1.1.1](#1.1.1)
	* [副标题1.2](#one-point-two)

<span id="1"></span>

# 主标题1
文本内容。。。

<span id="1.1"></span>

## 副标题1.1
文本内容。。。

<span id="1.1.1"></span>

### 次级副标题1.1.1
文本内容。。。

<span id="one-point-two"></span>

## 副标题1.2
```

* [主标题1](#1)
	* [副标题1.1](#1.1)
		* [次级副标题1.1.1](#1.1.1)
	* [副标题1.2](#one-point-two)

<span id="1"></span>

# 主标题1
文本内容。。。

<span id="1.1"></span>

## 副标题1.1
文本内容。。。

<span id="1.1.1"></span>

### 次级副标题1.1.1
文本内容。。。

<span id="one-point-two"></span>

## 副标题1.2
这是为了演示id也可以设置成英文字母
注意："锚" 可以是 p 元素也可以是 a 元素也可以是 span 元素等等，"锚" 的下面建议空一行再写其他内容。因为效果和前面那个例子完全一样所以这里就不演示了。

方法三：Markdown 原生支持的页内跳转?
看代码：
```
* [Cat and dog](#cat-and-dog)
	* [Cat](#cat)
		* [A little cat](#a-little-cat)
	* [Dog](#dog)

## Cat and dog

一只单身狗和一只高冷猫的故事。。。

### Cat

有一天高冷猫遇见了单身狗。。。

#### A little cat

高冷猫生的很小巧但是脾气不是很好。。。

### Dog
```

* [Cat and dog](#cat-and-dog)
	* [Cat](#cat)
		* [A little cat](#a-little-cat)
	* [Dog](#dog)

## Cat and dog

一只单身狗和一只高冷猫的故事。。。

### Cat

有一天高冷猫遇见了单身狗。。。

#### A little cat

高冷猫生的很小巧但是脾气不是很好。。。

### Dog

可是，单身狗喜欢上了高冷猫。。。
Theo 知道自己作文水平有限😂，客观先别急着笑，看下这段代码的效果：

Cat and dog
Cat
A little cat
Dog
Cat and dog
一只单身狗和一只高冷猫的故事。。。

Cat
有一天高冷猫遇见了单身狗。。。

A little cat
高冷猫生的很小巧但是脾气不是很好。。。

Dog
从此以后，单身狗喜欢上了高冷猫。。。

注意：Theo 编辑 Markdown 文本时使用的是 Sublime Text 3，测试页面显示效果时用的是一个叫 OmniMarkupPreviewer 的插件。在进行本地测试的时候 Theo 发现，如果单纯的用 OmniMarkupPreviewer 预览，这种写法的页内跳转是没有效果的。但是如果搭建本地 Jekyll 服务器，再用网页浏览器打开，跳转是有效的。另外，在 Github 上直接用这种 Markdown 语法书写，也是可以正常跳转的。
因此结论就是你在浏览这段 Demo 时应该可以正常页内跳转，但是如果你书写并本地测试时发现无法正常跳转也不要感到稀奇，关于这个问题的解释可以引用知乎上的一个回答：

Markdown是没有一个所谓的规范的(作者都不支持这么做)，所以某些特性需要写作工具自己支持才可以。所以有可能A的markdown到B上就无法正确显示了。

OK，这些构造支持页内跳转目录的黑魔法你都学会了吗，快去活动活动手指，写一篇附带目录的长篇博文吧 O(∩_∩)O 哈哈~

著作权声明
博客内的文章如无特殊声明均为 Theo 原创，转载请保留原文链接，谢谢。