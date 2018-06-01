---
title: "Rufus_Usb启动制作"
date: 2018-06-01T14:35:24+08:00
lastmod: 2018-06-01T14:35:24+08:00
draft: false
keywords: []
description: ""
tags: [""]
categories: [""]
slug: ""
url: "/archives/2018/06/01"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "http://rufus.akeo.ie/pics/rufus_en_2x.png"

thumbnailImage: http://rufus.akeo.ie/pics/rufus_en_2x.png
# 封面图像相对路径
coverImage: /cover/10.jpg
#封面说明内容
coverCaption: "A beautiful sunrise"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true

---

# ![[rufus icon]](http://rufus.akeo.ie/pics/rufus-128.png) [Rufus](https://github.com/pbatard/rufus)

轻松创建USB启动盘

Rufus 是一个可以帮助格式化和创建可引导USB闪存盘的工具，比如 USB 随身碟，记忆棒等等。

![](http://rufus.akeo.ie/pics/rufus_en_2x.png)

在如下场景中会非常有用：

- 你需要把一些可引导的ISO格式的镜像（Windows，Linux，UEFI等）创建成USB安装盘的时候
- 你需要使用一个还没有安装操作系统的设备的时候
- 你需要从DOS系统刷写BIOS或者其他固件的时候
- 你需要运行一个非常底层的工具的时候

Rufus 麻雀虽小，五脏俱全，体积虽小，功能全面。

哦，对了，Rufus 还 **非常快**，比如，在从ISO镜像创建 Windows 7 USB安装盘的时候，他比 [UNetbootin](http://unetbootin.sourceforge.net/)，[Universal USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3) 或者 [Windows 7 USB download tool](http://wudt.codeplex.com/) 大约快2倍。当然，在创建 Linux 可引导USB设备的时候也比较快。 [(1)](http://rufus.akeo.ie/?locale=zh_CN#ref1)
页面底部也粗略列举了一些 Rufus 支持的ISO镜像。 [(2)](http://rufus.akeo.ie/?locale=zh_CN#ref2)

## 下载

**最后更新于 2018.05.29：**

- **Rufus 3.0** (993 KB)
- [Rufus 3.0 Portable](http://rufus.akeo.ie/downloads/rufus-3.0p.exe) (993 KB)
- [其他版本](http://rufus.akeo.ie/downloads/)

#### 系统需求：

需要Windows 7以上的操作系统，无所谓32位还是64位，下载后开箱即用。

在这里我要借这个机会表达对那些把 Rufus 和这个网页翻译成各种语言的翻译者们的谢意。如果你发现 Rufus 可以支持你们使用的语言，你也应该感谢他们。

## 用法

下载可执行文件后直接运行 – 无需安装，绿色环保。

可执行文件已经进行数字签名，详情如下：

- *"Akeo Consulting"* (v1.3.0 或者更新的版本)
- *"Pete Batard - Open Source Developer"* (v1.2.0 或者更老的版本)

#### 对DOS支持的说明：

如果你创建了一个DOS启动盘，但是没有使用美式键盘，Rufus 会尝试根据设备选择一个键盘布局，在那种情况下推荐使用 [FreeDOS](http://www.freedos.org/)（默认选项）而不是 MS-DOS，因为前者支持更多的键盘布局。

#### 对ISO支持的说明：

Rufus v1.10 及其以后的所有版本都支持从 [ISO 镜像](http://en.wikipedia.org/wiki/ISO_image) (.iso) 创建可引导USB。

通过使用类似 [CDBurnerXP](http://cdburnerxp.se/) 或者 [ImgBurn](http://www.imgburn.com/) 之类的免费CD镜像烧录程序，可以非常方便的从实体光盘或者一系列文件中创建 ISO 镜像。

## 常见问题（FAQ）

Rufus 的常见问题（FAQ）**在此**。

您可以使用 github 的 [issue tracker](https://github.com/pbatard/rufus/issues) 来提供反馈，报告 BUG，或者提交功能需求。当然也可以直接发 [电子邮件](mailto:pete@akeo.ie?subject=Rufus)。