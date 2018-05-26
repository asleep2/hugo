---
# 常用定义
title: "Markdown 设置字体颜色"           # 标题
date:  2018-04-04T14:02:33+08:00    # 创建时间
lastmod: 2018-04-04T14:02:43+08:00 # 最后修改时间
draft: false                       # 是否是草稿？
url: /archives/107
tags: ["Typora", "Markdown"]  # 标签
categories: ["博客系统"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/BE20180107134249989.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/7.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---

<p style="color:blue;">Red paragraph text</p>
<font color="red">this is a test</font> 

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/DQ.jpg)

Summary:
Typora is a very good markdown editor, and today I'll show you how to use typora to set the color of the font, Example is as follow.
Typora虽然是一款markdown编辑器，但是其实也可以设置字体颜色，因为typora集成了不少扩展，所以可以通过别的语句轻松设置字体颜色。为什么要设置颜色，因为颜色可以突出我们想表达的内容，尤其是公式，方程式等表达上，可以把一些参数凸显出来。下面先看下实例：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/BE20180107134249989.jpg)

样例语句：

```HTML
$\textcolor{Magenta}{Jubi} $:这是一个$\textcolor{RedOrange}{例子} $，设置字体颜色很$\textcolor{Blue}{简单} $。
$ \textcolor{red}{\int_a^b}\textcolor{blue}{f(x)}\textcolor{green}{dx}\textcolor{brown}{=c}$
```

$\textcolor{Magenta}{Jubi} $:这是一个$\textcolor{RedOrange}{例子} $，设置字体颜色很$\textcolor{Blue}{简单} $。
$ \textcolor{red}{\int_a^b}\textcolor{blue}{f(x)}\textcolor{green}{dx}\textcolor{brown}{=c}$

## 1.文本颜色设置

```HTML
$\textcolor{Blue}{文字} $。
```
$\textcolor{Blue}{文字} $

替换颜色代码就可以实现不同的颜色。代码也可以简写为：

```HTML
$\color{Blue}{文字} $。
```

## 2.颜色代码大全

```HTML
$\textcolor{GreenYellow}{GreenYellow} $
$\textcolor{Yellow}{Yellow}$
$\textcolor{Goldenrod}{Goldenrod} $
$\textcolor{Dandelion}{Dandelion}$
$\textcolor{Apricot}{Apricot} $
$\textcolor{Peach}{Peach}$
$\textcolor{Melon}{Melon} $
$\textcolor{YellowOrange}{YellowOrange}$
$\textcolor{Orange}{Orange} $
$\textcolor{BurntOrange}{BurntOrange}$
$\textcolor{Bittersweet}{Bittersweet}$
$\textcolor{RedOrange}{RedOrange} $
$\textcolor{Mahogany}{Mahogany}$
$\textcolor{Maroon}{Maroon} $
$\textcolor{BrickRed}{BrickRed}$
$\textcolor{Red}{Red} $
$\textcolor{OrangeRed}{OrangeRed}$
$\textcolor{RubineRed}{RubineRed}$
$\textcolor{WildStrawberry}{WildStrawberry}$
$\textcolor{Salmon}{Salmon}$
$\textcolor{CarnationPink}{CarnationPink}$
$\textcolor{Magenta}{Magenta} $
$\textcolor{VioletRed}{VioletRed}$
$\textcolor{Rhodamine}{Rhodamine} $
$\textcolor{Mulberry}{Mulberry}$
$\textcolor{RedViolet}{RedViolet} $
$\textcolor{Fuchsia}{Fuchsia}$
$\textcolor{Lavender}{Lavender} $
$\textcolor{Thistle}{Thistle}$
$\textcolor{Orchid}{Orchid} $
$\textcolor{DarkOrchid}{DarkOrchid}$
$\textcolor{Purple}{Purple} $
$\textcolor{Plum}{Plum}$
$\textcolor{Violet}{Violet} $
$\textcolor{RoyalPurple}{RoyalPurple}$
$\textcolor{BlueViolet}{BlueViolet}$
$\textcolor{Periwinkle}{Periwinkle}$
$\textcolor{CadetBlue}{CadetBlue}$
$\textcolor{CornflowerBlue}{CornflowerBlue}$
$\textcolor{MidnightBlue}{MidnightBlue}$
$\textcolor{NavyBlue}{NavyBlue} $
$\textcolor{RoyalBlue}{RoyalBlue}$
$\textcolor{Blue}{Blue} $
$\textcolor{Cerulean}{Cerulean}$
$\textcolor{Cyan}{Cyan} $
$\textcolor{ProcessBlue}{ProcessBlue}$
$\textcolor{SkyBlue}{SkyBlue} $
$\textcolor{Turquoise}{Turquoise}$
$\textcolor{TealBlue}{TealBlue} $
$\textcolor{Aquamarine}{Aquamarine}$
$\textcolor{BlueGreen}{BlueGreen} $
$\textcolor{Emerald}{Emerald}$
$\textcolor{JungleGreen}{JungleGreen}$
$\textcolor{SeaGreen}{SeaGreen} $
$\textcolor{Green}{Green}$
$\textcolor{ForestGreen}{ForestGreen}$
$\textcolor{PineGreen}{PineGreen} $
$\textcolor{LimeGreen}{LimeGreen}$
$\textcolor{YellowGreen}{YellowGreen}$
$\textcolor{SpringGreen}{SpringGreen}$
$\textcolor{OliveGreen}{OliveGreen}$
$\textcolor{RawSienna}{RawSienna} $
$\textcolor{Sepia}{Sepia}$
$\textcolor{Brown}{Brown} $
$\textcolor{Tan}{Tan}$
$\textcolor{Gray}{Gray} $
$\textcolor{Black}{Black}$
```

显示如下：

![](/assets\BE20180107135121970.jpg)

## 3.数学/方程式颜色设置

代码如下：

```HTML
$ \textcolor{red}{\int_a^b}\textcolor{blue}{f(x)}\textcolor{green}{dx}\textcolor{brown}{=c}$
```

显示结果：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/BE20180107135311977.jpg)

同样是使用textcolor混合在公式里面实现了 公式颜色设置，至于公式部分，可以参考：

- [使用typora添加化学方程式/ Typora tutorial: chemical equation — Steemit](https://steemit.com/utopian-io/@jubi/typora-typora-tutorial-chemical-equation)
- [使用Typora添加数学公式\ Typora tutorial :mathematical formula — Steemit](https://steemit.com/utopian-io/@jubi/typora-typora-tutorial-mathematical-formula)

今天关于typora设置颜色的教程到此结束，感谢您阅读！