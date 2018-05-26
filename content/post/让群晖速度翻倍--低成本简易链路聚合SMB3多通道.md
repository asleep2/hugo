---
title: 群晖SMB3多通道
author: 3mile
type: post
date: 2018-04-01T05:45:46+00:00
url: /archives/1024
categories:
  - vps
# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/220405m02kkk0gbyk03tkb.png

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/3.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial  
---


群晖DSM 6.1-15047 带来的新福利，免费功能--SMB3 Multi-Channel


DS3615xs Release Notes -- DSM6.1-15047

> \6. 文件服务
> Windows 文件服务及 Mac 文件服务已分別更名为 SMB 及 AFP。
> **所有的 SMB 服務 (SMB1/2/3) 现由 Samba 4.4 所提供**
> 支持 Mac OS 10.12 或以上版本中，通过 SMB3 使用 Time Machine。
> 支持 Bonjour 服务，您可以通过 Time Machine 将文件备份至多个共享文件夹。
> 支持在 SMB 协议下使用稀疏文件 (sparse file)，以提升文件系统空间及网络带宽的使用效率。
> 通过 SMB 协议挂载 home 文件夹时，可于 Windows 文件资源管理中还原至先前的版本。
> 於文件服务的高级设置中启动文件快速复制后，当您复制文件时，若来源于目的地位于相同的 Btrfs 存储空间，文件复制将更为快速。

如果你的群晖NAS带2个或更多网卡，升级到DSM 6.1-15047及以上版本后

在PC端增加一张千兆网卡，台式机可以加PCI-E的独立网卡，笔记本可以用USB3.0的千兆网卡，型号品牌不限

便宜的PCI-E螃蟹卡一张15元包邮，然后就可以享受内网NAS读写传输速度翻倍的快感

（当然前提是本身NAS的性能能突破1Gbps，正常x86版本的NAS硬盘不要太慢都可以突破1Gbps）

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/204442d3366r419ureue99.png)

2017.04.28更新

在P大的指导下，实践确认除了Windows Server 2012/2016，黑群晖也支持SMB3多通道传输

目前测试的DSM版本是最新的DSM 6.1-15047 Update 2

步骤一，

群晖WEB管理界面暂时没有SMB3多通道传输的相关设置项，需要手工修改smb.conf配置文件

修改方法，参考：

https://forum.synology.com/enu/viewtopic.php?t=128482

samba配置文件路径/etc/samba/smb.conf，添加以下命令，保存后重启

```
server multi channel support = yes
aio read size = 1
aio write size = 1
```

可以直接用SSH终端root权限运行vi命令修改添加（P大提供），vi的使用方法请自行百度

```sudo vi /etc/samba/smb.conf```

复制代码

或者用使用root用户进入WinSCP修改

DSM5.2 root和admin密码相同，DSM6开始需要使用root账户的话需要手工修改其密码

DMS6及以上版本修改root密码，参考：

https://www.panpinche.com/zhishi/20170313

使用telnet或者SSH终端，分别输入以下2行命令，xxx为root密码可自行更改，具体见下图

```sudo su -```

```synouser --setpw root xxx```

复制代码

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/220405m02kkk0gbyk03tkb.png) 

然后，WinSCP使用root用户及密码进入DSM目录，修改并保存

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/220406o8kccyq8raydd8k8.png)

步骤二，

群晖控制台WEB界面，控制面板--文件共享--文件服务--高级设置：

最大SMB协议：SMB3

最小SMB协议：SMB2和Large MTU

设置完毕，点应用

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/220405p9c94gxrina9rxnv.png)

群晖设置完毕，重启群晖文件共享服务（重启群晖也可以）

步骤三，

客户端PC分别用\\IP进入群晖的2个IP的共享，填入访问凭据（用户名和密码）

双网卡，Win10 PC客户端从黑群晖读取，SMB3多通道效果如下：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/103843r11z3sx11x76zggw.jpg)

相比SMB3多通道传输，之前传统的链路聚合做法是

把几张网卡绑成一张速度叠加的虚拟网卡，用来满足局域网多终端同时大吞吐量传输的需要

譬如2张1Gbps的千兆网卡绑成1个2Gbps的网卡；3张1Gbps的千兆网卡绑成1个3Gbps的网卡

实现链路聚合，需要满足以下条件

```
1，文件共享服务端有多张或者加装支持链路聚合的多张网卡（一般要求是同品牌）
2，支持链路聚合的交换机，譬如支持802.3ad
3，链路中的网线上不能接入其他设备

```



然后，一般认为，这种传统的链路聚合的方式，以常见的譬如2张1Gbps的千兆网卡绑成1个2Gbps的网卡为例：

虽然可以通过给客户端加装网卡的方式链路聚合，实现服务端到客户端都是2Gbps的链路连接速度

但是，单个客户端和服务端之间单文件或者说单线程的传输，都只能跑1条线路，即1Gbps

只有当多个客户端，同时和服务端传输，才能跑满服务端的2Gbps

因此，以上常规链路聚合的方式，存在成本高，单终端传输速度不叠加等缺点

前一阵在网上闲逛，看到了几个帖子，突然感到眼前一亮：

lucifersun网友的帖子，

https://www.chiphell.com/forum.php?mod=viewthread&tid=696565&page=3&authorid=50709

xmaan网友的帖子，

https://www.chiphell.com/thread-1663962-1-1.html

Vespa网友的帖子，

https://test.smzdm.com/pingce/p/36063/

于是请教了Pufer大，指出这种文件共享单线程拷贝产生叠加效果，应该是smb3.0多通道自动速度叠加的作用

然后查看了一下samba官方的一些信息：

https://www.samba.org/samba/history/samba-4.4.0.html

> EXPERIMENTAL FEATURES
> =====================
> SMB3 Multi-Channel
> \------------------
> Samba 4.4.0 adds *experimental* support for SMB3 Multi-Channel.
> Multi-Channel is an SMB3 protocol feature that allows the client
> to bind multiple transport connections into one authenticated
> SMB session. This allows for increased fault tolerance and
> throughput.

上面的几篇文章都能看到，单线程拷贝时，每个网卡上都有速度

看来smb传输自动调用将流量分配到了多张网卡上，达到了速度叠加的效果

smb3多通道生效，家庭常规网络部署结构：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/105521n58epr84pjpg8z63.png) 

相比传统的链路聚合，smb3多通道传输速度叠加的方式，有设置简单、成本低等特点

一，价格

1，驱动支持链路聚合的网卡，譬如Intel的独立网卡一般都比较贵；而PCI-E的螃蟹卡只要15元包邮就可以买到，而且可以混搭

2，支持链路聚合的路由器或者交换机，YLJ一般几百起步，行货更贵；smb3多通道叠加普通路由器LAN口或者傻瓜交换机都可以

二，设置

传统链路聚合，从网卡到交换机，都要做链路聚合设置；smb3多通道叠加基本无需任何操作

可惜上面几篇文章中对如何实现，并未有太详细的描述

于是，自己实践了下：

服务端是2012、2016，客户端是Win10，客户端上操作，向服务端共享读写都可以顺利叠加

但是服务端上操作，向客户端共享读写，不能叠加

所以，又试了用2台PC（DELL台式机和3215U小主机），分别都安装了Windows Server 2016数据中心GUI版这

样实现了2边PC上操作都有叠加效果

操作很简单，给各个网卡设置了同网段的固定IP，新建共享文件夹，关闭防火墙

4网卡SMB3 Multi-Channel叠加效果：

DELL台式机上操作

从服务端3215U小主机上的共享读取：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/161304w9699y0e9yxt3tcy.png)

写入服务端3215U小主机上的共享：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/161304zq2irvui2vtsu12i.png)

3215U小主机上操作

从服务端DELL主机上的共享读取：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/161304u93pcp333bpqzp0c.png)

写入服务端DELL主机上的共享：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/161305zigqmfsiccc6jm6f.png)

通过微软的TCPView监听工具，我们来看下SMB3多通道的传输情况

先看一下迅雷的下载方式，多线程从本地多个端口连接远程服务器的端口进行下载

这边可以看到基本都是TCP协议连接的服务端80端口

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/171543sffnf8inikn7ftzr.png)

然后再看smb3多通道的传输情况，这边以双网卡的情况为例

无论是读还是写，都是本地双网卡2个IP的2个端口去和服务端对应网卡2个IP的TCP 445端口传输

形成双线程传输产生速度2倍叠加的效果

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/171543nl4fizb51r6jaatf.png)

由此可以看到SMB3多通道传输利用了多线程传输来达到速度翻倍的效果

但是关于多线程传输本身，也需要辩证的看待它的优缺点

我们知道，不管是硬盘还是U盘，如果同时读取或者写入2个文件，速度会下降很多

以HDD为例，单文件传输时理想情况磁头可以做单方向顺序读写

而同时操作2个文件磁头将会在2个位置区域不停的来回切换，所以传输速度大大降低

2个以上多文件的话，传输速度下降更多，SSD和HDD RAID的情况还会更复杂

所以一定程度增加读写线程，可以增加NAS吞吐量，但是线程太多的话反而会影响NAS传输速度

所以这一点也需要在实际操作中留意

测试过程中也遇到了一些问题

1，虽然各品牌网卡混搭，包括低端的螃蟹网卡、USB网卡也可以顺利叠加

但是碰到1例Intel 9301CT PCI-E网卡加入后不能叠加的情况

2，Windows Server 2012/2016做服务器，搭配Win10客户端叠加，日常家庭简易共享场景应该够用了

但是如果群晖配合Win10客户端能实现的话，实际意义就更大了

据P大介绍，DSM6.1以上版本支持，接下来将会进行进一步测试