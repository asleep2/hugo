---
# 常用定义
title: "KeePass与群晖WebDav完美同步"
date: 2018-04-05T12:47:27+08:00    # 创建时间
lastmod: 2018-04-05T12:48:34+08:00 # 最后修改时间
draft: false                       # 是否是草稿？
url: /archives/110
tags: ["群晖", "Webdav", "KeePass"]  # 标签
categories: ["群晖"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d5bc4ef216320.jpg_e600.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/10.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---





## 前言

第一次发贴，属菜鸟心得，老鸟跳过。从2000年开始接触网络，如今网龄已满16周年了，也管是资深网民，各种论坛帐号，各种邮箱帐号，淘宝、支付宝、各种密码，零零总总不下几百个，然后又是各种泄露门，基本上不重要的论坛之类都采用同帐号，同密码，虽然感觉自己不是什么大户，也没有什么隐私，但一想到帐号被人登陆，也够自己恶心的，寻思着找个密码管理软件。看了网上各种评测，最好选定了Keepass，全平台开源密码管理软件。选择Keepass主要是因为先期1Password的贵（据说现在免费了，未试），最主要是[安卓手机](https://www.smzdm.com/fenlei/anzhouji/)端的支持一般，lastpass密码存储在他人[服务器](https://www.smzdm.com/fenlei/fuwuqi/)上（强迫症始然），跨平台收费（据说现在也免费了，未试）。

言归正传，keepass做为一款本地密码管理软件（安全），如果跨平台使用，那么就得把密码数据和密码KEY上传到网上，然后进行同步，一 方面，存在第三方网盘感觉不安全（该死的强迫症），一方面网盘不一定支持这种同步，找了很多教程，其中：

这么好买一个吧的[我的密码我做主 — KEEPASS+群晖实现多平台无忧密码管理](https://post.smzdm.com/p/478691/)

雨侬的[KeePass通过坚果云WebDav同步方法](http://www.jianshu.com/p/2a2d9be153f1)

给了我很大的启发，举一反三下，为什么不通过群晖的WebDAV，达到跟坚果云同样的同步效果呢？

今天主要是讲KeePass与群晖WebDAV完美同步~！

工具如下：

1、Keepass pro 2.35绿色版+中文语言文件，下载见《[我的密码我做主 — KEEPASS+群晖实现多平台无忧密码管理](https://post.smzdm.com/p/478691/)》

2、Keepass2Android.apk

3、群晖213J，系统6.0.2

4、安卓[手机](https://www.smzdm.com/fenlei/shouji/)一台（DS专用），win7系统电脑一台。

## 步骤如下：

1、开通群晖的WebDAV功能，端口5005不变（https端口5006需要导入签发了的证书），记得在[路由器](https://www.smzdm.com/fenlei/luyouqi/)里设置端口转发（PS：DSM6.0把WebDAV套件单独列出来了，5.0的请到控制面板——文件服务里面找）。

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d5bc4ef216320.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d686b6f568416.jpg_e600.jpg)

2、设置共享[文件夹](https://www.smzdm.com/fenlei/wenjianjia/)，专门给Keepass用，这个大家自己把握，可以是已有的共享文件夹，这里为了讲得明白些，新建一个Keepass的专属共享文件夹。

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d688dfabd4000.jpg_e600.jpg)

​     3、设置一个专门的用户，专门访问这个文件夹，一切为了安全。权限用一般用户user、除了Keepass文件夹可读写，该用户不能访问其他文件夹、空间无限制、只能用于WebDAV应用等。

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d68a154ad2626.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d68b1af6c5395.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d68c50b427609.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d68d31c9e8328.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d68eee8707224.jpg_e600.jpg)

4、在Keepass共享文件里上传一个1.txt，内容为“你好”，主要是为了测试是否已经正常使用WebDAV服务。（PS：输入[http://NAS](http://nasf/)地址:5005/keepass/ 1.txt），输入刚设立的群晖帐号,这里是Keepass，密码123456，浏览器显示你好，说明测试通过。

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d690f04fa338.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9ed0b6fd0b1901.jpg_e600.jpg)

5、现在进行Keepass的远程配置（密码数据库和KEY文件我都建在一个地方，当然，大家尽量不放在一起）。如此，Win7端已经可以完美与群晖的WebDAV同步了，进群晖Keepass就可以看到两个新建的文件。

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d6937ca881231.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d694ce8666095.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d6964948f6108.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9f2b7efadb11.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d69ac3a691474.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d69ccf19e4700.jpg_e600.jpg)

6、安卓手机端设置，打开软件——打开文件——http(webdav)——输入或者复制WebDAV地址（http://NAS地址:5005/keepass/pass.kdbx），输入WebDAV帐号keepass，密码123456——输入数据库的登陆密码——输入KEY地址或者复制（http://NAS地址:5005/keepass/pass.key）——输入WebDAV帐号keepass，密码123456——最后按解锁，进入，现在，你可以愉快地完耍了。（PS：Keepass2Android有几个界面不能截图，不过相对比较直观，大家进去就知道了。）

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d69e0b8418417.png_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d6a2430e92566.jpg_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d6a34a8375885.png_e600.jpg)

![KeePass与群晖WebDav完美同步](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webdav/58d9d6a44dca92070.png_e600.jpg)



## 总结

至此，已经全部设置完毕。Keepass具有强大的同步能力，既可以在webdav中新建，同样，也可以在webdav中打开原来已经设置好的，同时可以进行两个密码数据库（*.kdbx）同步，不同的客户端，无缝链接，妈妈再也不怕我记不住密码了。

## 