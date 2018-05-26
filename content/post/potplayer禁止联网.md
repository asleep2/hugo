---
title: "Potplayer禁止联网"
date: 2018-05-07T11:54:13+08:00
lastmod: 2018-05-07T11:54:13+08:00
draft: false
keywords: []
description: ""
tags: ["potplayer","播放器"]
categories: ["windows软件"]
slug: ""
url: "/archives/140"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/6.png"

thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/6.png
# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/6.jpg
#封面说明内容
coverCaption: "Potplayer"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true

---

potplayer是一款非常受欢迎的视频播放器，其具有非常强大的功能。不过，一些 win10系统 用户反馈，potplayer经常会弹出“自动更新提示”，感觉非常烦人。那么，我们该如何彻底关闭potplayer的自动更新呢？方法非常简单，我们只要利用系统防火墙建立新的出站规则，禁止potplayer联网就可以了。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/6.png)

**具体如下：**

1.打开控制面板，进入防火墙的高级设置；

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/1.png)

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/2.png)

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/3.png)

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/4.png)

2.右键出站规则→新建规则；

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/5.png)

3.程序→下一步→浏览-选择Potplayer安装文件夹下的播放器程序文件→下一步-阻止连接→下下下-最后的名称描述随意→完成。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/windows/potplayer/7.jpg)

以上就是小编给大家带来的win10系统下potplayer经常弹出“自动更新提示”问题的解决方法了。想要禁止potplayer自动更新的朋友们不妨按照上述步骤操作看看。