---
title: CentOS 7一键安装Seafile搭建私有云存储
author: 3mile
type: post
date: 2018-04-03T10:43:14+08:00
draft: false
url: /archives/901
categories:
  - vps
tag:
  - VPS

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/Seafile-image-915x330.png

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/1.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---

 




Seafile 是一款开源企业云盘，和Owncloud类似，个人感觉Seafile更加稳定，搭建也很简单，为了方便，xiaoz写了一个一键脚本，方便快速搭建自己的私有云。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/Seafile-image-915x330.png)

### 环境要求

> - CentOS 7 64位
> - Python >= 2.7
> - SqLite 3

### 开始安装

复制下面的命令，依次输入，如果不出意外，会看到如下截图，请分别按照截图中的注释操作。

```
yum -y install wget
wget https://raw.githubusercontent.com/helloxz/seafile/master/install_seafile.sh
chmod +x install_seafile.sh && ./install_seafile.sh
```

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_181353.png)

输入数字1进行安装

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_181734.png)

看到该信息直接回车键继续

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_181839.png)

输入服务名（如mycloud）

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_182135.png)

填写服务器公网IP

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_182741.png)

一路4个回车

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_183030.png)

设置管理员邮箱和密码（密码是不会显示的，输入完毕后直接回车）

当你看到如下界面，说明已经安装完成，直接输入`http//:IP:8000`进行访问，接下来的操作只要你能看懂中文就不是什么问题了，Seafile还提供了多平台客户端（见文末）。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_183258.png)

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/seafile/snipaste_20170612_183456.png)

输入刚刚设置的邮箱和密码登录

### 其它说明

安装目录和服务如下，如果您还需要配置更多的功能或扩展，请访问官方帮助文档：<https://manual-cn.seafile.com/>

```
#安装目录
/home/MyCloud
#启动服务
/home/MyCloud/seafile-server/seafile.sh start
/home/MyCloud/seafile-server/seahub.sh start
#停止服务
/home/MyCloud/seafile-server/seafile.sh stop
/home/MyCloud/seafile-server/seahub.sh stop
```

### 总结

Seafile支持全平台客户端，非常适合私有云方案，一台VPS可搞定一切。曾在文章《[CentOS一键安装Resilio Sync脚本](https://www.xiaoz.me/archives/8219)》分享过Resilio Sync一键脚本，有兴趣的也可以试试。