---
# 常用定义
title: "华为悦盒获取IPTV播放地址免抓包方法"           # 标题
date: 2018-04-05T13:00:56+08:00    # 创建时间
lastmod: 2018-04-05T13:01:01+08:00  # 最后修改时间
draft: false                       # 是否是草稿？
url: /archives/111
tags: ["IPTV", "抓包", "电视盒"]  # 标签
categories: ["windows软件"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/114655kh1a1zpaptpyay12.jpg

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





如果你想在T1上看IPTV，恰巧运营商送你的电视盒子是华为悦盒，请继续往下看，不是请退出免得浪费时间。
小白发帖求不喷！
1.盒子和电脑必须在同一路由器网段下。
2.盒子开机点击遥控器上的设置键，进入盒子设置界面，在“网络设置”中查看盒子的IP地址。在“更多”选项中找到“远程维护连接”将禁止改为允许。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/114655kh1a1zpaptpyay12.jpg)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/114654v1pncpct9h93cnf9.jpg)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/114655ci6624in4kpbj4iq.jpg) 
3.下载华为STB管理工具下载链接：<https://pan.baidu.com/s/1EYVIt8ZkGb86HaGNzSe_Iw> 密码：p3py
4.下载解压缩后放在电脑任意地方，运行解压后文件夹里面的STBManage\STBManageTool.exe，点导入许可
证,浏览找到STBManage\license.dat导入，在软件自动跳回的首页填入机顶盒的IP地址，密码：.287aW
(前面有个点!前面有个点!前面有个点!），点连接，连上后看右下角启用远程登陆，选“开”，点提交。
5.打开盒子自带的IPTV，直至开始播放节目。

6.选择故障诊断选项卡，点击“视频质量”--“频道列表”--“导出频道列表”
7.导出的txt文档里就是所有的频道和播放源地址了。
8.图片上红线就是频道名称和播放源地址了，播放源地址以rtsp://开头  .smil结尾（以我这里的播放地址为例，也有其他后缀名.m3u8 .flv自己判断吧）
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/121136xvz5y6taca3v3na3.jpg)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/121136d5j3c62c2urw4dar.jpg)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/121137qo7hfucu6ugzolrl.jpg) 

设置里没有远程维护的试试进入--设置--更多--高级设置，看看里面有没有（密码一般是运营商客服电话（10000、10086、10010），除此之外，还有8288、6321、2878、3008、8005等等。）


盒子直接连在光猫上的，电脑连接在路由器上的朋友可以试试
“@无线无极限”说的方法：华为的盒子，先打开正常播放后，拔掉网线，遥控上，设置》网络连接，选wifi，连到电脑的上级路由就可以了。再按楼主说的操作。

用管理工具导出的频道列表需要自己去分析播放源地址，rtsp://开头  .smil后缀结尾 关键是这个后缀有很多种，需要大家自己判断，电脑上直接用这个播放源打不开，我在友窝上导入编辑好的播放列表后测试成功