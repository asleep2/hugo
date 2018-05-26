---
# 常用定义
title: "群晖中用docker安装pi-hole给家庭局域网的设备滤除广告"           # 标题
date:  2018-04-05T13:12:20+08:00   # 创建时间
lastmod: 2018-04-05T13:15:54+08:00 # 最后修改时间
draft: false                       # 是否是草稿？
url: /archives/112
tags: ["群晖", "去广告", "docker"]  # 标签
categories: ["群晖"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/194545bmy5rv6niyy8tg2j.png.thumb.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/9.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---





Pi-hole采用域名过滤的方式滤除广告，通过在群晖docker中安装pi-hole,同时在路由器中将dns server设为群晖的ip地址，可以实现路由器下的所有设备都达到去除广告的作用。同时，Pi-hole中还有dnsmasq，还可以实现dns功能

1、在DSM Docker中下载pi-hole镜像,diginc/pi-hole镜像

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/194545bmy5rv6niyy8tg2j.png.thumb.jpg)

2、启动镜像

A、端口设置：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/195221wxegun3g643qqtqg.png.thumb.jpg) 

其中蓝框中的端口要一致;红框的端口如果群晖http已经占用了80端口，可以改成其它端口

注意：

群晖中不要安装dns server套件，也不要启用dhcp服务器

，否则会造成53端口冲突

B、卷设置：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/200014qwb4rrb28k8mb8v6.png.thumb.jpg) 

红框中的文件夹是在群晖中已经建立好的文件夹，按图中所示映射文件夹，方式为读写（去掉只读的框）

C、环境变量设置：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/200924v140o2t0twg43t14.png.thumb.jpg) 

#### 本帖隐藏的内容

「ServerIP」填写群晖内网ip地址，如群晖在内网的地址是192.168.1.10，则填

192.168.1.10

「TZ」填写时区，便于pi-hole在半夜更新广告清单

「WEBPASSWORD」为pi-hole网页管理页面密码

「DNS1」、「DNS2」填写网络运营商的dns服务器地址如

D、设定完后，启动pi-hole后，稍等一会，再打开

```shell
http://ServerIP:Port /admin
```
 就可以看到pi-hole管理页面（如果看不到，再等一会，多刷新几下），其中serverip为群晖的

内网ip地址，如192.168.1.10，port为端口设置中的地址，此例中为36778，界面如下：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/202639u1mjmy25vyj1552y.png.thumb.jpg)

登录后，可以看到更详细的信息，并可以在settings设定dns服务器，可以选择google,opendns等dns服务器

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/203920rrok9c5k9rqnqcv5.png.thumb.jpg)

E、在路由器中将dns中的第一个dns地址设为群晖的内网地址,详见后面的PC端和路由器设置说明，如

192.168.1.10

通过这些设置后，路由器下的设备都用群晖的pi-hole过滤广告了。

利用pi-hole的dnsmasq还能实现

```HTML
<http://www.nasyun.com/thread-39869-1-1.html>
```

中的自动识别内网和外网连接的功能：

#### 本帖隐藏的内容

1、PC中

新建02-lan.conf的文件，文件中写入红字所示的一句

```
addn-hosts=/etc/pihole/lan.list
```

利用群晖的file station 上传至/docker/pihole/dnsmasq.d/目录

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/204604mj8iiljrj1bdikci.png.thumb.jpg)

利用群晖的file station 上传至/docker/pihole/config/目录

3、登入
```
http://192.168.1.10:36778
```

/admin，其中的192.168.1.10换成你自己的群晖内网地址。利用设定的密码进入管理界面后，在

settings页面，点击restart dnsmasq，等待10分钟后，你要解析的域名就可正常解析了，你可能ping nas.123.com试试，看解析是否成功。

补充pc端和路由端的配置：

1、Pc机的dns应设置为自动获取，ip也设为自动获取，同时，路由器上的dns服务器设置成群晖的ip地址。另外，查看pi-hole的管理页面dashboard上的queries blocks上显示的数字，就是过滤的域名数量。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/164110zqu7zbob15j1wowj.jpg.thumb.jpg) 

2、路由器界面的dns设置（水星路由器原版固件为例，

注：建议略过这步，在下面的dhcp中设置dns，有些路由只能在此设定dns服务器，不能在dhcp中设定dns，可进行此步

）：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/164149zb0d9y4qushs89s4.jpg.thumb.jpg) 

红框中填写你的群晖ip地址，这样所有的局域网中的设备都可以通过pi-hole dns进行广告过滤了。

3、路由器的dhcp设置（如果上面的第2步做过了

此步骤可省略。注：也可以只进行下面的dhcp设置，上面的第2步不操作，这样的话，局域网中通过设置固定ip的网络设备可以不走pi-hole dns，不进行广告过滤，而通过dhcp获得ip的网络设备则走pi-hole dns进行广告过滤

）：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/220757x1cm1jc04lknatcn.png.thumb.jpg) 

红框中填写群晖ip地址，缺省域名填写：lan，在dhcp中填写缺省域名和dns服务器是为了实现免配置局域网全自动kms激活，具体方法可在网站自行搜索