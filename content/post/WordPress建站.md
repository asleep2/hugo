---
# 常用定义
title: "搭建WordPress博客网站"           # 标题
date:  2018-04-10T09:16:52+08:00   # 创建时间
lastmod: 2018-04-10T09:16:58+08:00 # 最后修改时间
draft: false     
url: /archives/104                  # 是否是草稿？
tags: ["虚拟主机", "wordpress", "vultr"]  # 标签
categories: ["博客系统"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/domain-a-record-1522662595033.png

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




讲真，曾经我特别佩服使用服务器（比如VPS）搭建WordPress博客网站的站长们。

因为，我觉得仅仅在漆黑的屏幕上敲几行代码就能把一个网站玩的风生水起很了不得，感觉有点黑客大神的气派。而那时我才刚刚开始研究独立博客和虚拟主机，还是个只知道使用简单办公软件的上班族。

后来，慢慢的发现许多事情原本都很简单，是自己想复杂了。

比如在VPS上搭建WordPress博客，其实根本就不需要你精通什么编程，懂什么系统，你只要掌握一些常用到命令就能DIY。因为在互联网时代，很多东西都是现成的，你只要会搜索，会整合，会学习使用就万事不难了。

当然，如果你是个什么都懂的IT男，想必更是极好的。

言归正传，这篇文章主要记录了我放弃虚拟主机后，如何一步步在VPS上安装CentOS6系统和LAMP环境进而搭建WordPress博客的。

因为打算当做教程来写，所以会尽量写的详细一点。以下是文章目录，不想听博主唠叨的话可自行略过前面的介绍部分。


文章目录

* [1 WordPress](#1)
* [2 选择虚拟主机还是VPS](#2)
  * [2.1  虚拟主机](#2.1)
  * [2.2  什么是VPS](#2.2)
* [3 + 注册域名](#3)
* [4 + 如何选购便宜的VPS](#4)
  * [4.1 + 搬瓦工VPS和Vultr哪个好](#4.1)
  * [4.2 + 如何购买搬瓦工VPS](#4.2)
  * [4.3 + 如何购买Vultr-VPS](#4.3)
* [5 + SSH连接VPS](#5)
* [6 + 搭建LAMP环境](#6)
* [7 + 添加域名 / 虚拟主机](#7)
* [8 + 安装WordPress程序](#8)
* [9 + VPS配置优化](#9)
  * [9.1 + 优化php.ini配置](#9.1)
  * [9.2 + 添加swap交换分区](#9.2)
  * [9.3 + 开启Keep-Alive功能 + 优化Httpd配置](#9.3)
* [10 + 删除mysql-bin.0000*日志文件](#10)
* [11 + Linux-VPS安全配置 / 防护措施](#9)
  * [11.1 + 修改SSH端口](#11.1)
  * [11.2 + 阻止SSH暴力破解](#11.2)
  * [11.3 + 防御DDOS攻击](#11.3)
* [12 + MySQL数据库优化](#12)
* [13 + 创建VPS快照](#13)
* [14 + WordPress博客的备份和迁移](#14)
  * [14.1 + 文件备份](#14.1)
  * [14.2 + 数据库备份](#14.2)
  * [14.3 + WordPress迁移 / 搬家](#14.3)
  * [14.4 + WordPress搬家脚本](#14.4)
  * [14.5 + 备份小技巧](#14.5)
* [15 + 写在最后](#15)

<span id="1"></span>
## WordPress

[WordPress](https://wordpress.org/)是一种使用PHP语言和MySQL数据库开发的个人博客系统，其稳定可靠，易于使用，且是免费开源的。而最让我看重的，是它支持一大波优秀的插件和模板，比如SEO优化、静态缓存和数据备份等。

具体可参看百度文库相关介绍：<http://baike.baidu.com/item/WordPress>

<span id="2"></span>
## 选择虚拟主机还是VPS

在回答这个问题之前，让我们先来弄清楚虚拟主机和VPS的区别。

<span id="2.1"></span>
### 什么是虚拟主机

[![VPS和虚拟主机区别对比](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/vps-vs-shared-hosting.jpg)](https://www.seoimo.com/wp-content/uploads/2016/11/vps-vs-shared-hosting.jpg)

虚拟主机（Virtual Hosting）又叫共享主机（Shared Hosting），是使用特殊的软硬件技术，把一台真实的主机分割成多个的逻辑存储单元，每个单元都没有物理实体，但是每一个物理单元都能像真实的物理主机一样在网络上工作，具有共享IP地址(或独立IP地址)以及必要的互联网功能。

通俗一点讲，就是一个出租屋里分了好多床位，租客们共用水、电、卫生间等生活设施。

- 优点：便宜、便捷，自带被褥，拎包即住
- 缺点：居住性能差

<span id="2.2"></span>
### 什么是VPS

[VPS（Virtual Private Server）](http://baike.baidu.com/item/VPS)即虚拟专用服务器，就是利用虚拟化技术（如KVM、Xen、OpenVZ等）把一台真实的服务器分割成若干虚拟的服务器，具有独立的操作系统及开关机等功能，能自行搭建和配置特定的服务。

通俗的说，就如同买了小区里的一套房子，空间及设施都是自己的，想怎么装就怎么装。

- 优点：爱咋用咋用，居住性能好
- 缺点：价格价高，需要懂点技术

由上可以看出，究竟是选用虚拟主机还是VPS建站主要看你的使用目的和性能要求。

一般来说，如果你对服务器配置和维护并不太懂，且个人博客的访问量不大（比如日均1000PV以下），虚拟主机（带独立IP最好）是首选，价格通常年付二三百RMB的样子。

但是，如果你和博主一样喜欢折腾，喜欢追求更高性能，同时也想学习一点Linux相关知识，那么可以考虑使用VPS。

实际上有些性能很不错的国外VPS也很便宜，一般月付5美元甚至更少即可。这样算下来，其实并不比虚拟主机贵到哪去。

博主选用的是美国Vultr公司的最便宜的一款VPS，日本东京的机房，感觉速度要比美国西海岸洛杉矶机房好一些。

博客现已搬迁至**搬瓦工年付$19.99这款小内存VPS**，具体购买及安装过程详见下文。

<span id="3"></span>
## 3注册域名

考虑到性价比（免费隐私保护）和支付便利（支持支付宝），博主目前在用以下两个域名注册商，在这也推荐给大家。

- NameSilo：[https://www.namesilo.com/](https://www.seoimo.com/go/namesilo/)
- 阿里云（万网）：[https://wanwang.aliyun.com/domain/](https://www.seoimo.com/go/aliyun-domain/)

2018年2月1日起，阿里云域名涨价了，.COM 续费 ￥69 每年！（感觉是时候转出去了）

反观NameSilo，价格一直比较稳定，甚至不定期赠送优惠，注册和转移时还能再省点。

> 【优惠活动】2018年12月31日前，使用NameSilo优惠码 **the1usd** 可减免一美元，首年只需 $7.99！

<span id="4"></span>
## 4如何选购便宜的VPS

坦白说，虽然网上有不少推荐和介绍，比如知乎回答和一些评测博客，但如何选择一款便宜好用且性能不错的VPS还着实让我头疼了一阵。

为什么呢？

网上有些推荐的文章仅仅只是为了推荐而推荐，拿来主义，人云亦云，缺乏实际的使用体验。这就可能导致推荐者对VPS整体的稳定性缺乏深入的评测，而稳定可靠恰恰是一个网站长期发展的重要保障。

尽管128MB甚至更低内存的VPS也可以搭建WordPress建站，但博主并不推荐这样做。因为我们的目的是要做一个省时省力又能长期稳定运行的网站，而不是炫耀VPS优化技术。

于是，在兼顾价格（5美元以下）、速度（ping值200左右）以及稳定性（在线率99.95以上）三个前提下，最终筛选出三个便宜的国外VPS：**Vultr、BandwagonHost（搬瓦工）**和**DigitalOcean（DO）**。

但是这三个到底哪个最适合自己呢？感觉还是一头雾水。

纸上得来终觉浅，绝知此事要躬行。于是，就三个VPS全部试用了一遍，并通过我能用得到的各种测试，最终选定了Vultr-VPS（日本机房）。

<span id="4.1"></span>
### 4.1搬瓦工VPS和Vultr哪个好

[![Vultr-VPS月付2.5美元](WordPress建站.https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/vultr-banner-w300.png)](http://www.seoimo.com/go/vultr-basic/)

首先，Vultr和DigitalOcean（DO）几乎一样，最便宜的一款VPS月付都是5美元。但是Vultr给的内存是768MB，DO的则只有512MB。

尽管DO在SSD空间上比较大方，给了20GB，而Vultr的则是15GB。但是，博主可以很负责任的告诉你，一般的网站存储+备份+环境一共5-10GB的空间就足够了。显然，内存比空间更实用！

> 【温馨提示】Vultr现已更改套餐，价格、流量及空间大小均有所调整，可直达官网[查看详情](http://www.seoimo.com/go/vultr-basic/)。

其次，Vultr快照（Snapshot）是免费的，且不同VPS甚至不同机房之间可以无缝迁移。

比如，刚开始我把网站放在美国西海岸的洛杉矶机房，后来发现日本东京机房的速度更快。于是，我只需要把洛杉矶的VPS快照备份，然后在新开的东京VPS上一键恢复就把数据搬过去了，不用再重装系统和优化配置了。

第三，Vultr是KVM虚化技术，私以为比BandwagonHost（搬瓦工）的OpenVZ好一些。

但是，搬瓦工年付19.99刀的VPS也的确不错，无论CPU性能还是硬盘I/O读写速度（可达900MB/s，见下图）目前都比Vultr（平均450MB/s）要好一些。若优化得当，搭建三两个流量不大的WordPress博客应该不是问题。

![搬瓦工OVZ-256MB套餐I/O读写速度测试](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-io-256mb-ovz.png)

再来看下经过优化加速之后，本页面（多图长文）的全国打开速度：（可点击放大）

[![seoimo全国各地页面打开速度](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/speed-test-17ce-w1180.png)](https://www.seoimo.com/wp-content/uploads/2016/11/speed-test-17ce-w1180.png)

**那么，搬瓦工VPS和Vultr到底哪个好呢？**

搬瓦工采用的是OpenVZ虚拟化技术，博主担心日后可能会严重超售，影响VPS性能。~~再加上目前Vultr搞活动，新注册就送20美元（需信用卡或PayPal验证并建议充值10美元），足够免费折腾四个月，等于花$10使用6个月，算算比虚拟主机都便宜！~~所以，博主最终还是选择了Vultr。

利好消息：Vultr最近下调了价格，**最低套餐（512MB/500GB）只需2.5美元/月**！

遗憾的是月付2.5美元这款平时只有纽约和迈阿密机房有货，但这俩机房靠近美国东海岸，离国内实在有点太远了，略坑。建站的话博主还是推荐Vultr的洛杉矶、西雅图和硅谷这三个美西机房，距离国内比较近，带宽也足。

但是，如果抢不到2.5刀那款的话，这几个美西机房要月付5刀了。当然，5刀的配置会更好一些，看个人需要了。

另外，降价之后赠送20美元的优惠活动也随之取消了。

如果你对网站的访问速度不像博主这么挑剔的话，月付$2.5的美东机房还是可以接受的。

VULTR-VPS的优点（博主喜欢的）

- 稳定：真的很稳，官方承诺VPS在线率100%
- 便宜：最低$2.5/月（支持按小时计费）
- IP随便换：可多机房间相互转移，主机IP随时更换（简直逆天）
- 备份方便：后台一键 SnapShot 备份整机，省心放心（无需关机，比搬瓦工更贴心）
- 速度较好：东京和洛杉矶机房速度相对不错，但需要月付5美元

VULTR-VPS的不足（博主不满的）

- 月付2.5美元仅限纽约和迈阿密机房，距大陆较远
- 主机I/O读写稍低，300MB-500MB/s（搬瓦工500-1000MB/s）
- 实在想不出还有啥不满意的

~~Vultr赠送20美元活动~~直达链接：[https://www.vultr.com/20-dollars/](http://www.seoimo.com/go/vultr-basic/)

*（由于众所周知的原因，目前东京、洛杉矶和纽约等机房IP被Q严重，可能需要多刷几次才能开出一个可用的IP。怕麻烦的话，建议首选硅谷或伦敦机房。）*

[![搬瓦工VPS年付19.99美元](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagon-host-256mb.png)](http://www.seoimo.com/go/bandwagon-ovz-512mb/)

实际上，便宜的VPS不超售是不可能的。因为VPS商家是做生意赚钱的，而不是来搞慈善。

但是，从过去几个月的使用情况来看，搬瓦工这款[年付19.99美元~~（256MB/500GB）~~（512MB/500GB）](http://www.seoimo.com/go/bandwagon-ovz-512mb/)~~小内存~~VPS速度和稳定性确实很不错。

在过去的几个月里，除了博主备份系统和更换机房时 reboot 几下，还从未宕过机。经过适当的优化（见下文）后，博客页面也基本可以达到秒开。

再加上Vultr赠送的小钱钱也早已经用完，所以本博客（即SEOIMO.COM）目前已从Vultr迁移至搬瓦工的洛杉矶机房。

**搬瓦工VPS和Vultr到底哪个更适合，博主的建议是：**

如果你只有三两个流量不大的网站，比如每天5000PV以内，搬瓦工256MB/500GB这款小鸡还是完全能够胜任的。

因为，博主经过测试（[LoadImpact](https://loadimpact.com/)），模拟5分钟内100个访客持续访问本页也没有搞垮这个小鸡。非但没搞垮，这款小内存VPS表现还很不错。

不相信博主？有图有真相，直接上图（看不清可点击放大）：

[![搬瓦工VPS模拟100个同时在线](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-loadimpact.png)](https://www.seoimo.com/wp-content/uploads/2016/11/bandwagonhost-loadimpact.png)

从上图可以看出，在5分钟内，模拟100个访客持续访问本页，打开时间基本维持在0.8-1.2秒之间。倘若从早10点至晚22点算起（[百度上网时间分布统计](http://tongji.baidu.com/data/hour)），按12个小时持续访问的话，每天有大约15000PV的访问量！

是否可以这样理解：即使像本页面这样有这么多的图片和文字，每天大约15000PV的流量，经过适当的优化，在搬瓦工这款256MB的小内存VPS上也基本是秒开的。

是不是有点吓到了？

再来看一下100访客在线时VPS的系统平均负载：

![搬瓦工VPS的系统负载](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-phpinfo-100vu.png)

内存耗尽是意料之中的事情，毕竟只有256MB。但出乎博主意料的是：系统平均负载并不高，甚至还不到0.2！这么高的流量，博主原以为起码也要超过1的，即CPU刚好跑满。现在非但没有跑满，竟还有足够多的剩余。不得不说，搬瓦工的技术还真是可以！

由此可见，小内存VPS不一定就不能搭建大流量WordPress博客，关键要优化得当。

当然了，如果网站真有每天超过10000PV的流量，博主还是建议提升下VPS配置，比如升级到搬瓦工1024MB/1024GB这个套餐。因为每天10000PV的流量即便挂Adsense广告每天也该有10美元的收入了，就不要再扣VPS月租这点小钱了。

搬瓦工VPS的优点（博主喜欢的）

- 便宜：最低$19.99/年（使用优惠码更省）
- 稳定：承诺99.5%在线率保证，经博主过去一年多对本站的检测来看，除了博主认为重启之外，在线率实际几乎100%
- 够快：洛杉矶机房，CN2线路，ping值低，速度快（本站所用）；香港机房更快，但是价格就无爱了
- IP可换：可多机房间相互转移，实现随意更换IP地址（博主大爱）
- 备份方便：后台一键 SnapShot 备份整机，省心放心

搬瓦工VPS的不足（博主不满的）

- 进行 SnapShot 时强制关闭VPS，持续5分钟左右（不如Vultr周到）
- 系统过于精简，建站时某些必备软件可能需要自己手动安装
- 香港机房VPS太贵，真心贵

建议首选KVM架构，最低$19.99/年，可安装BBR加速，看视频方便。

KVM-512MB/500GB直达链接：[https://bandwagonhost.com/kvm-512mb/](http://www.seoimo.com/go/bandwagon-kvm-512mb/)

限时供货，使用优惠码 **BWH1ZBPVK** 可省6%（目前最高）；

推荐**洛杉矶CN2**直连线路（后台切换）；请务必确保注册信息真实有效，且与登录IP地址相符。否则，大概率会被视为欺诈（Fraud）而上黑名单。

一般来说，512MB内存足够个人建站使用了。但若是年付 $19.99 这款紧俏套餐已经脱销，或者你需要更高配置的，年付 $49.99 这款也足够好：20GB空间，1024MB内存，多机房可自由切换。

至于其余的高价套餐，博主以为仅对搭建wordpress博客来说，性价比并不高。因此，也就没必要去花冤枉钱（土豪请随意）。

KVM-1024MB/1024GB直达链接：[https://bandwagonhost.com/kvm-1024mb/](http://www.seoimo.com/go/bandwagon-kvm-1024mb/)

| 价格： |      |
| ------ | ---- |
| 稳定： |      |
| 速度： |      |
| 操作： |      |
| 优惠： |      |

> 【温馨提示】DigitalOcean只支持信用卡和PayPal付款，而搬瓦工和Vultr则可使用支付宝（Alipay）。

<span id="4.2"></span>
### #4.2如何购买搬瓦工VPS

默认折叠，请单击展开 / 折叠 ..

![搬瓦工256MB小内存vps](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-256mb-vps.png)

![洛杉矶QNET和MCOM机房选择](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/la-qnet-mcom.png)

![搬瓦工优惠码](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagon-promo-code.png)

![搬瓦工支付宝付款](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-alipay.png)

![BandwagonHost后台管理 - My Services](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagon-my-services.png)

![搬瓦工KiwiVM Control Panel](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/kiwivm-control-panel.png)

![搬瓦工VPS主机信息](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/vps-information.png)

![重装系统](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/install-new-os.png)

![系统备份（Snapshots）](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/bandwagonhost-snapshots.png)

![更换机房（Migrate to another DC）](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/migrate-to-another-dc.png)

<span id="4.3"></span>
### #4.3如何购买Vultr-VPS

默认折叠，请单击展开 / 折叠 ..

![Vultr开通新的VPS](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/deploy-new-vps.png)

![日本东京机房](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/ri-ben-ji-fang.png)

\~~~~

![32位CentOS6系统](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/centos6-i386.png)

![立即开通VPS](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/deploy-now.png)

![域名添加A记录](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/domain-a-record.png)

接下来，正式进入本文的最重要环节：**通过SSH连接VPS搭建LAMP环境，进而安装WordPress博客**。

<span id="5"></span>
## #5SSH连接VPS

SSH（Secure Shell）即安全外壳协议，是目前较可靠、专为远程登录会话和其他网络服务提供安全性的协议。我们需要一种SSH工具来连接VPS，个人推荐PuTTY，最好使用英文原版。

下载地址：<http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html>

下载后免安装，直接打开。填入刚才开通的VPS地址，默认端口22。然后点击Open打开，弹出的新窗口点击左边 “Yes” 。

![打开PuTTY连接VPS](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/open-putty.png)

回到我们刚才打开的Vultr-VPS管理页面，左边有登陆名root和密码，复制密码。

![vultr-VPS管理后台](/https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/vultr-vps-overview.png)

在PuTTY界面输入root后回车，单击右键即可输入密码。

> 【温馨提示】PuTTY中输入密码是不显示的，单击右键即为粘贴。

登陆成功后，首先需要修改root密码，因为初始密码太复杂不好记，也不一定安全。

`# passwd`

回车后设置新密码，再回车重新输入。然后界面显示如下，说明密码修改成功。

*（密码长度建议20字符以上，字母大小写 + 数字 + 特殊字符）*

![修改VPS登录密码](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/change-vps-passwd.png)

之后，最好再升级一下系统，以保证获得最新的软件和内核。

`# yum -y update`

回车，等待升级完成。

此外，为防止SSH登录一段时间后自动断开，可更改如下设置以保持SSH长时间在线。

`# vi /etc/ssh/sshd_config`

将如下两行代码前的 # 去掉，然后做相应修改：（若无此两行代码请在末尾自行添加）

\#PermitUserEnvironment no
\#Compression delayed
**ClientAliveInterval 60**
**ClientAliveCountMax 3**
\#ShowPatchLevel no
\#UseDNS yes

保存，重启SSH即可生效：

`# service sshd restart`

**开启BBR加速**

BBR是Google提出的一个开源的TCP拥塞控制算法，应用于Linux4.9+内核上，对提升网速效果显著。

因此，对于KVM架构的VPS，博主倾向于在正式部署生产环境之前，首先开启BBR。

但这并不意味着你一定要这么做。倘若你的VPS线路已经很不错，完全可以跳过这一步。

切换到 root 目录：

`# cd ~`

下载安装脚本：

`# wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh`

如提示 wget: command not found ，可执行命令 # yum install wget 进行安装。

安装BBR：

`# chmod +x bbr.sh && ./bbr.sh`

按要求输入 y 后，自动重启VPS。

重新登入后，查看结果：

`# sysctl net.ipv4.tcp_available_congestion_control`

出现形如以下字样时，说明BBR开启成功。

net.ipv4.tcp_available_congestion_control = **bbr** cubic reno

<span id="6"></span>
## #6搭建LAMP环境

![什么是LAMP](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/lamp-linux-apache-mysql-php-w720.png)

LAMP指的是Linux（操作系统）、Apache（HTTP服务器），MySQL（数据库软件） 和PHP（有时也是指Perl或Python）的第一个字母，主要用来建立web应用平台。

博主使用的是LNMP一键安装包，具体可参看这里：<https://lnmp.org/install.html>

> 【温馨提示】为提高效率，可直接复制代码，然后在PuTTY窗口单击右键进行粘贴。

首先，创建screen会话：

`# screen -S lamp`

如提示 screen: command not found ，可执行命令 # yum install screen 进行安装。

如果安装过程中出现异常中断，重新登入VPS后，输入 # screen -r lamp 恢复安装界面。

由于LNMP1.4版本可一键设置SSL，所以推荐优先安装1.4版本：

LNMP1.4-FULLLNMP1.3-FULL

`# wget -c http://soft.vpser.net/lnmp/lnmp1.4-full.tar.gz && tar -zxf lnmp1.4-full.tar.gz && cd lnmp1.4-full && ./install.sh **lamp**`

当然，如果你之前已经安装的是LNMP1.3，也可以[一键升级到1.4版本](https://www.seoimo.com/lamp-ssl/#lnmp1.3-to-lnmp1.4)。

以下安装过程不再赘述，选项一般默认即可，主要设置详见下图（LNMP1.3示意）。

这里设置的数据库ROOT密码**务必记牢**，下面添加域名时会用到！！

LNMP安装成功之后，如果数据库密码忘记了，可参看这里[进行重置](http://www.vpser.net/manage/linux-reset-mysql-root-password.html)。

*（建议安装\**PHP5.6**版本；安装SSL证书时如出现问题，可以参考博主安装Let’s-Encrypt免费的SSL证书时遇到的几个大坑）*

![设置root用户数据库密码](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/setup-lamp-mysql.png)

![安装php5.4](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/setup-lamp-php.png)

![安装apache2.2](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/setup-lamp-apache.png)

当出现上图中的绿字 "Press any key to install...or Press Ctrl+c to cancel" 后，按回车键确认开始安装。

安装大约持续半个小时左右。安装成功后的界面如下图所示：

![安装lamp成功](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/install-lamp-completed.png)

至此，LAMP环境已经在VPS上搭建完成。**输入VPS的IP访问**，会出现以下界面：

![LNMP在VPS中安装成功](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/lnmp-in-vps.png)

在安装WordPress之前，建议**安装PHP缓存加速类扩展**，对降低VPS压力和提高WordPress速度大有裨益。

推荐安装两个：OPcache和Memcached。

首先，需要进入LNMP解压目录 lnmp1.4-full （lnmp1.3则改为lnmp1.3-full）：

`# cd /root/lnmp1.4-full`

回车，接下来安装Opcache：

`# **.**/addons.sh install opcache`

回车，再回车。

当出现 “Opcache installed successfully, enjoy it!” 字样时，即表示安装成功。

接着安装Memcached：

`# **.**/addons.sh install memcached`

回车，选择2，回车，再回车。

当出现 “Memcached installed successfully, enjoy it!” 字样时，即表示安装成功。

此时，可以删除之前下载的lnmp1.4安装包，以节省空间。

`# rm -rf /root/lnmp1.4-full.tar.gz`

回车即可。

接下来就可以添加域名安装WordPress了。

添加域名
## 7添加域名 / 虚拟主机

请提前做好域名解析，例如：

![域名添加A记录](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/domain-a-record-1522662595033.png)

添加域名：

`# lnmp vhost add`

回车，提示输入域名：

`# seoimo.com`

回车，提示是否添加多个域名：

`# y`

回车，博主习惯绑定带 www 的域名：

`# www.seoimo.com`

回车，显示网站目录。默认 /home/wwwroot/seoimo.com 即可。

> 若是绑定二级域名，必须**输入完整的目录路径**。例如：
>
> 将 tools.seoimo.com 绑定到网站根目录下的 tools 文件夹，则应输入：
>
> /home/wwwroot/seoimo.com/tools

回车。博主习惯不需要日志记录，但建议你开启（y）：

`# n`

会车后，输入站长邮箱。

继续回车，提示数据库名和数据库用户名是否保持一致。

`# y`

回车，输入 root 用户的数据库密码（不会显示，在[#6搭建LAMP环境](http://www.seoimo.com/wordpress-vps/#setup-lamp)中设置好的）。

回车，输入数据库名，自行设置。例如：

`# sjk_seoimo`

回车，设置数据库密码。例如：

`# sjkmmseoimo`

回车，再回车。

当出现下图所示画面时候，说明添加域名已经成功。

![添加域名/虚拟主机](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/lnmp-vhost-add.png)

**关于FTP功能**

LNMP1.3默认是不安装FTP服务的。

需要上下传文件时，设置FTP软件（如FlashFXP）连接类型为 “**SFTP over SSH**”即可。

![FlashFXP通过SSH方式连接VPS](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/sftp-over-ssh.png)

但是，特定情况下仍需要开启FTP服务的话，可进行如下操作：

`# cd /root/lnmp1.3-full`

`# ./pureftpd.sh`

安装成功后，添加FTP用户：

`# lnmp ftp add`

设置好FTP用户名、密码以及访问目录的**绝对路径**（以 “**/**” 开头）！！

**特别提示：**

使用FTP软件连接VPS后，若无法进行上传和下载，并提示 “553 Can’t open that file: Permission denied” 时，可能需要更改下权限：

`# chown www:www -R /目录路径/`

<span id="8"></span>
## #8安装WordPress程序

以下的步骤想必应该很熟悉，和带Cpanel或DirectAdmin面板安装WordPress过程比较类似。只不过，在面板上操作是可视化的，比较直观。而在这里是通过命令执行的，非可视。只要输入命令时细心点，一般是不会出问题的。

首先，进入添加的域名目录：

`# cd /home/wwwroot/seoimo.com`

回车。然后浏览器中打开[WordPress中文站点](https://cn.wordpress.org/)，下载最新的程序压缩包：

`# wget https://cn.wordpress.org/wordpress-4.9.4-zh_CN.tar.gz`

回车。等待下载完之后，解压压缩包：

`# tar -zxvf wordpress-4.9.4-zh_CN.tar.gz`

回车。

接下来，将解压出来的wordpress文件夹内全部文件移动到当前的域名目录下（别忘了后面的**.**）。

`# mv wordpress/* **.**`

回车。然后，可以选择删掉空文件夹wordpress及源程序（可选）。

`# rm -rf wordpress`

`# rm -rf wordpress-4.9.4-zh_CN.tar.gz`

回车，搞定。

为避免因权限的问题导致安装出错，**比如wp-config.php无法创建、需要提供FTP用户密码以及主题和插件不能更新等**，建议赋予网站根目录文件的可写权限。

`# chmod -R 755 /home/wwwroot# chown -R www /home/wwwroot`

> 【温馨提示】以后每添加一个域名，都要对应地执行一次以上两步操作。

另外，LNMP安装包默认禁用了 scandir 函数，这会导致WordPress后台看不到安装的主题，以及当前主题总显示 “有新的翻译可用” 的提醒。所以，需要开启此函数。

`# vi /usr/local/php/etc/php.ini`

回车，然后查找 scandir 函数。

`?scandir 或者 /scandir`

回车，然后按delete键删除，接下来需要保存并退出vi命令。

`# **:**wq`

回车。然后重启一下LNMP：

`# lnmp restart`

好了，打开博客网址进行最后的安装吧！（注意要提前设置好域名解析）

![搭建WordPress博客](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/setup-wordpress-blog.png)

至此，在VPS上通过搭建LAMP环境安装WordPress博客已经大功告成了。

接下来，我们来对VPS进行必要的配置优化，以便进一步提高主机性能。

<span id="9"></span>
## #9VPS配置优化

关于VPS服务器方面的配置优化绝对是个技术活，如果深入研究的话会比较复杂。博主非技术大牛，在这里仅介绍一下常用的三点：**优化php.ini配置、添加swap交换分区**和**开启Keep-Alive功能 + 优化Httpd配置**。

<span id="9.1"></span>
### #9.1优化php.ini配置

用vi命令修改 php.ini 文件。

`# vi /usr/local/php/etc/php.ini`

单击 i 键进入 insert 模式，按 “上下左右” 四个方向键找到并修改以下两项：

max_execution_time = 300
memory_limit = 64M

前者表示允许脚本最大执行时间300秒，后者表示允许单个脚本允许使用的最大内存64M（通常1G内存以下设置64M或128M即可）。

单击 Esc 键退出 insert 模式，输入以下命令保存退出。注意英文状态下输入！

`# :wq`

回车。然后重启一下LNMP：

`# lnmp restart`

回车。

<span id="9.2"></span>
### #9.2添加Swap交换分区

> ①此方法只适用于虚拟化技术为KVM和Xen的VPS，OpenVZ不支持添加Swap交换分区，也就说说搬瓦工VPS（[KVM-512MB套餐](http://www.seoimo.com/go/bandwagon-kvm-512mb/)除外）不能用此方法增加Swap空间；
>
> ②若搬瓦工VPS管理后台Swap状态长期显示红色，则表明VPS内存已满，该考虑升级VPS了。

关于Swap分区的具体含义在此不再赘述，详细可以参考百度百科：[Swap分区](https://baike.baidu.com/item/Swap%E5%88%86%E5%8C%BA)

简单来说，当VPS的物理内存不够用时，系统会占用一部分Swap分区作为临时内存，目的是防止因物理内存耗尽而可能出现的错误。

因此，对小内存VPS来说，设置一定大小的Swap交换分区显然很有意义。

但是，由于硬盘的 I/O 读写速度远不能和内存的读写速度相提并论（可能相差几十倍），使用Swap交换分区时，系统可能会变得特别缓慢、卡顿，甚至程序会出现错误。

因此，要尽量避免使用Swap分区，不得不使用时也不宜设置过大（大了也没用还占用空间），也就是说：**我们不能指望用Swap来代替物理内存使用**。甚至于，当你的VPS物理内存很充足时，完全可以禁用Swap以提高VPS的响应速度。

当物理内存（实际使用内存）长期处于耗尽状态时，正确的做法就是该升级套餐了。

**添加Swap交换分区**

使用root用户登陆PuTTY，先看看是否已经添加了Swap:

`# free -m`

若显示为 Swap = 0 的话，表明没有添加。否则，说明系统已自带Swap交换分区。

进入var文件目录：

`# cd /var/`

获取256MB的文件块（一般设置为内存的0.5倍即可）：

`# dd if=/dev/zero of=swapfile bs=1M count=256`

创建Swap文件：

`# /sbin/mkswap swapfile`

激活Swap文件：

`# /sbin/swapon swapfile`

为了安全，建议修改一下权限：

`# chmod 0600 /var/swapfile`

将swapfile添加到fstab文件中，开机自动启动：

`# echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab`

搞定了。此时查看内存信息:

`# free -m`

出现 “Swap: 256” 字样表示设置成功。

**修改 swappiness 默认值**

上面说了，我们要尽量避免使用Swap分区。所以，这里我们需要额外做些修改，使系统尽可能的优先使用物理内存。

首先查看下 swappiness 的默认值：

`# cat /proc/sys/vm/swappiness`

通常，返回值是60（默认值）。

实际上，swappiness = 0 表示最大限度使用物理内存，然后才使用swap分区；swappiness ＝ 100 表示系统积极的使用swap分区，然后才使用物理内存。

显然，这里我们需要降低 swappiness 的默认值。

`# vi /etc/sysctl.conf`

在里面添加 vm.swappiness = 10 字段，然后退出保存。

或者：

`# echo "vm.swappiness = 10" >> /etc/sysctl.conf`

然后 # reboot 一下VPS即可。

**重置Swap交换分区**

若系统已设置Swap，但是需要对其做出更改的话，可以将其删除。

首先查看Swap位置：

`# swapon -s`

比如显示为 /var/swap，则停止并删除swap：

`# /sbin/swapoff /var/swap# rm -rf /var/swap`

然后，将其删除开机启动：

`# vi /etc/fstab`

将 /var/swap swap swap defaults 0 0 该行删除，然后保存退出。

<span id="9.3"></span>
### #9.3开启Keep-Alive功能 + 优化Httpd配置

开启Keep-Alive功能可使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive功能避免了建立或者重新建立连接。可见，对访问静态网页时，开启Keep-Alive是很有用的。

因为在进行WordPress管理方面上的优化时，需要安装静态缓存插件，所以，开启Keep-Alive功能十分必要。

`# vi /usr/local/apache/conf/extra/httpd-default.conf`

依次修改以下四条：

Timeout 30
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 5

退出，保存：

`# :wq`

接下来优化 Httpd 配置（ prefork 模式下），以降低Apache内存占用。此步骤对小内存VPS（如搬瓦工256MB方案）尤为重要。

`# vi /usr/local/apache/conf/extra/httpd-mpm.conf`

依次修改如下：

![优化Apache中Httpd & 配置prefork](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/apache-httpd-prefork.png)

退出，保存：

`# :wq`

然后，重启httpd服务：

`# service httpd restart`

<span id="10"></span>
## #10删除mysql-bin.0000*日志文件

博主所用的LNMP一键安装包默认开启了日志记录，这样就会在 /usr/local/mysql/var/目录下面生成大量 mysql-bin.0000* 类似的文件，大小甚至达到几个G！

所以，我们需要做下调整，禁止保留日志记录以防止占用太多空间。

于是，编辑 /etc/my.cnf 文件：

`# vi /etc/my.cnf`

找到以下两行代码，在前面添加 #，彻底禁用MySQL日志：

max_connect_errors = 100
open_files_limit = 65535
\#log-bin=mysql-bin
\#binlog_format=mixed
server-id = 1
expire_logs_days = 10

保存退出，重启一下MySQL：

`# /etc/init.d/mysql restart`

<span id="11"></span>
## #11Linux-VPS安全配置 / 防护措施

博主以为，VPS的安全防护绝对是运行网站的重中之重。防护措施做不好，轻者给后期运行带来无穷无尽的烦恼，重者造成网站瘫痪甚至数据清空，那就真的欲哭无泪了。

好在Linux本身已经足够安全稳定，只要你不泄露关键的登录信息（比如SSH端口和ROOT密码等），通常不会产生重大事故。但即便如此，我们还是应该未雨绸缪，提前做好VPS的安全防护措施。

那么，VPS安全配置究竟该如何做呢？

在这里，博主结合自己建站经验，介绍一下Linux-VPS安防措施里最有效的三个方面：**修改SSH端口**、**阻止SSH暴力破解**和**防御DDOS攻击**。

<span id="11.1"></span>
### #11.1修改SSH端口（强烈推荐）

首先，编辑配置文件：

`# vi /etc/ssh/sshd_config`

找到 `#Port 22` 这行（默认端口22），把前面的 **#** 去掉，然后再添加一个新的端口（不超过65535），比如 Port 56789：

![更改ssh端口](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/change-ssh-port.png)

保存，重启SSH即可：

`# service sshd restart`

接下来，在防火墙 /etc/sysconfig/iptables 里开启此端口：

`# iptables -A INPUT -p tcp -m tcp --dport **56789** -j ACCEPT`

保存并重启防火墙：

`# service iptables save# service iptables restart`

或者，也可以编辑 /etc/sysconfig/iptables 文件，复制端口 22 的规则，粘贴在其下另起一行。

按 :wq 保存退出后，重启防火墙。

查看防火墙状态，看看端口是否开启成功：

`# service iptables status`

现在，使用新的端口连接SSH。

若成功登录，则再次编辑 /etc/ssh/sshd_config，将里面的 `Port 22` 前加 **#** 保存后，重启SSH即可。

**温馨提示：**

CentOS7.X中默认的防火墙 firewalld 而非CentOS6.X中的 iptables 。如果你也像博主一样感觉用着很不爽，需要换回 iptables 的，可以参考如下设置。

1、关闭firewall并禁止开启启动：

`# service firewalld stop# systemctl disable firewalld.service`

2、安装iptables：

`# yum install iptables-services`

3、修改iptables配置：

`# vi /etc/sysconfig/iptables`

粘贴如下内容（可按需要自行增删）：

*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 3306 -j DROP
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 11211 -j DROP
-A INPUT -p udp -m udp --dport 11211 -j DROP
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT

按 :wq 保存退出后，重启iptables，并设置为开机启动：

`# service iptables restart# systemctl enable iptables.service`

> 【温馨提示】搬瓦工VPS生成的SSH端口是随机的（非默认端口22），因此，可无需再次修改。

<span id="11.2"></span>
### #11.2阻止SSH暴力破解（可选）

更改默认的22端口后，已经可以阻止绝大多数的SSH非法请求了。

但是，如果遇到程序自动扫描SSH端口并进行暴力破解，那么仅仅修改端口的话，可能还是不够的。因此，我们需要安装[DenyHosts](http://denyhosts.sourceforge.net/)进行自动拦截。

*（温馨提示：设置高强度密码+更改默认SSH端口后，视实际需要，本步骤可以省略。）*

首先，下载 DenyHosts 并解压到 root 目录：

`# cd ~`

`# wget http://soft.vpser.net/security/denyhosts/DenyHosts-2.6.tar.gz`

`# tar -zxvf DenyHosts-2.6.tar.gz`

`# cd DenyHosts-2.6`

接下来，进行安装和配置：

`# python setup.py install`

`# cd /usr/share/denyhosts/`

`# cp denyhosts.cfg-dist denyhosts.cfg`

`# cp daemon-control-dist daemon-control`

然后，设置开机启动：

`# chown root daemon-control`

`# chmod 700 daemon-control`

`# ./daemon-control start`

`# echo "/usr/share/denyhosts/daemon-control start" >> /etc/rc.local`

至此，DenyHosts就算安装完成了。通常，DenyHosts默认的阻拦配置就可以。当然，你也可以自行设置：

`# vi /usr/share/denyhosts/denyhosts.cfg`

自行设置如下几个主要的参数：

PURGE_DENY = 5d
DENY_THRESHOLD_INVALID = 5
DENY_THRESHOLD_VALID = 5
DENY_THRESHOLD_ROOT = 5
HOSTNAME_LOOKUP = NO

最后，重启一下DenyHosts即可：

`# /usr/share/denyhosts/daemon-control restart`

倘若自己的IP（[如何查看](http://www.ip.cn/)）被误封，可在 /etc/hosts.deny 中删除对应的IP后重启DenyHosts即可。

**卸载DenyHosts**

卸载DenyHosts比较麻烦，官方貌似没有提供具体卸载方法。

不过，我们可以通过 **停用 + 禁止开机启动** 来将其关闭。

停用DenyHosts：

`# /usr/share/denyhosts/daemon-control stop`

禁止开机启动，编辑 /etc/rc.local ：

`# vi /etc/rc.local`

将 /usr/share/denyhosts/daemon-control start 这行删除，保存退出。

如此，就实现了停用DenyHosts的目的。

<span id="11.3"></span>
### #11.3防御DDOS攻击

这里主要用到一款优秀的免费软件DDoS Deflate：<http://deflate.medialayer.com/>

首先，下载DDoS Deflate并安装：

`# cd ~`

`# wget http://www.inetbase.com/scripts/ddos/install.sh`

`# chmod 0700 install.sh`

`# ./install.sh`

按 Q 键退出，然后编辑配置文件：

`# vi /usr/local/ddos/ddos.conf`

推荐做如下更改，其余默认即可：

NO_OF_CONNECTIONS = 100
APF_BAN = 0
BAN_PERIOD = 36000

保存后退出。

<span id="12"></span>
## #12MySQL数据库优化

众所周知，LAMP是比较依赖数据库的。尤其是搭建的WordPress博客没进行HTML静态缓存的情况下，对数据库的依赖更加严重。

在我看来，对MySQL数据库的优化是特别重要也是特别困难的一项工作。不仅仅是因为MySQL设置里参数众多，让人看着头疼迷糊，更是因为这些参数没有一个固定的最优组合。参数设置的激进，浪费VPS资源，设置的保守，又可能限制程序的正常运行。

那么，究竟该怎么设置才合理呢？

根据博主的经验，对MySQL众多参数中最重要的以下几点进行合理的优化后，基本可以保证中小流量（比如＜5000IP/天）博客的正常访问。

为确保安全，首先备份一下 /etc/my.cnf ：

`# cp /etc/my.cnf /etc/my.cnf.old`

接下来，修改 /etc/my.cnf 中的以下参数：

`# vi /etc/my.cnf`

key_buffer_size = 15M
query_cache_size = 15M
max_connections = 100

修改后，保存退出。重启一下MySQL数据库即可：

`# /etc/init.d/mysql restart`

**特别提示：★★★★★**

随着博客流量的日益增长，这些设置可能不再适合，需要不断调整，以达到最合理的方案。

那么，如何调整呢？

在这里，博主根据自己的实际经验，提供以下方法。同时，也建议你定期监测调整。

**一、连接MySQL数据库：**

`# mysql -uroot -p`

回车，输入数据库密码（root用户）。

出现提示符 mysql> 后，即表示成功进入MySQL数据库中。

**二、查看服务器响应的最大连接数（Max_used_connections）：**

`mysql> show global status like 'Max_used_connections';`

返回值中，Max_used_connections 表示服务器过去发生的最大连接数。

博主建议：

max_connections / Max_used_connections = 1.5

比值可以大一些，但太小的话可能出现 1040 错误：“MySQL: ERROR 1040: Too many connections”

**三、查看key_buffer_size使用情况：**

`mysql> show global status like 'key_read%';`

得到返回值（单位：Byte），索引未命中缓存的概率：

key_cache_miss_rate ＝ Key_reads / Key_read_requests * 100%

博主建议：

*key_cache_miss_rate ＜ 0.1%* 即可，表示1000个索引读取请求才有一个直接读硬盘；

如果比值过小（比如*＜ 0.01%*），则表示 key_buffer_size 分配的过多，可适当减少。

**四、查询缓存（query cache）利用率：**

`mysql> show global status like 'qcache%';`

返回值中，Qcache_free_memory 表示缓存中的空闲内存（单位：Byte）

则查询缓存利用率：

x = (query_cache_size - Qcache_free_memory) / query_cache_size * 100%

博主建议：

查询缓存利用率 *＞80%* 时，可适当提高 query_cache_size 数值；

查询缓存利用率 *＜20%* 时，可适当降低 query_cache_size 数值。

**五、退出MySQL数据库：**

`mysql> exit`

<span id="13"></span>
## #13创建VPS快照

为了数据安全，一定要养成定期备份的好习惯。否则一旦有个闪失，可真的要一夜回到解放前了。

所幸，Vultr提供免费的VPS快照备份，可以通过一键恢复（restoring），无缝迁移系统到别的机子或者机房。实在是太方便了。

操作也很简单：打开VPS管理页面，点击 “Snapshots” ，方框内填入标签即可。

![创建VPS快照](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/setup-vps-snapshot-label.png)

值得一提的是，Vultr的 Snapshots 恢复的时候有个小坑：备份恢复只能向等于或大于备份空间的机子进行操作。

也就是说，你在月付$5机子上可以一键恢复月付$2.5的机子上的备份。反之则不行，因为小空间没法恢复大空间。

所以，博主备份时的标签一般都注明套餐类型和日期，以便于管理。

如上图中：512MB-SEOIMO-2017-10-01

> 【温馨提示】搬瓦工VPS快照备份请参看：[#4.2 + 如何购买搬瓦工VPS](http://www.seoimo.com/wordpress-vps/#how-buy-bandwagon-vps)

<span id="14"></span>
## #14WordPress博客的备份和迁移

网站备份的重要性就不需要博主多说了。在Linux系统下，对WordPress进行备份其实并不难。主要涉及两部分：文件备份和数据库备份

<span id="14.1"></span>
### #14.1 文件备份

*温馨提示：以下命令中涉及的数据库和域名，请根据你VPS上具体设置，自行修改。*

为了方便管理，我们先建立一个文件夹专门存放备份数据，比如 /home/backup/ ：

`# mkdir /home/backup`

以本站所在文件夹 seoimo.com 为例，压缩整站并移动到 /home/backup/ 文件夹下（为方便管理，博主添加了备份日期）：

`# cd /home/wwwroot# tar -zcf seoimo.com-20171001.tar.gz seoimo.com# mv seoimo.com-20171001.tar.gz /home/backup/`

好了，整站已经打包备份完成。接下来，开始备份数据库。

<span id="14.2"></span>
### #14.2 数据库备份

首先，打开 /home/backup/ 文件夹，我们需要将数据库备份在这里：

`# cd /home/backup# lnmp database list`

输入 root 数据库密码（在[#6 + 搭建LAMP环境](http://www.seoimo.com/wordpress-vps/#setup-lamp)设置的），即可查看当前数据库列表。

选择需要备份网站的对应数据库，以选定 sjk_seoimo 为例：

`mysqldump -uroot -p sjk_seoimo > sjk_seoimo-20171001.sql`

再次输入数据库密码，即可完成数据库备份。

可键入命令 # ls 查看当前目录下已经存在了备份好的文件。

此时，可以用通过 FTP 下载到本地保存，也可上传到别的 VPS 上备份保存。

<span id="14.3"></span>
### #14.3 WordPress迁移 / 搬家

某些情况下，我们可能需要进行网站迁移，从一个VPS搬家到另一个VPS上。如果是没有开通 SSH 功能的虚拟主机，搬家起来可能会比较麻烦，来来回回的下载和上传。但是，在VPS上操作则相对简单的多。

假设新VPS的IP为 8.8.8.8，SSH端口为 22，则打开备份目录，选择需要的文件备份和数据库备份上传：

`# cd /home/backup# ls# scp -P 22 seoimo.com-20171001.tar.gz root@8.8.8.8:/home/backup# scp -P 22 sjk_seoimo-20171001.sql root@8.8.8.8:/home/backup`

回车后，按要求输入新的VPS登陆密码。

接下来，**SSH登入新的VPS**。然后解压或替换网站域名目录：

`# cp /home/backup/seoimo.com-20171001.tar.gz /home/wwwroot# cd /home/wwwroot# tar -zxf seoimo.com-20171001.tar.gz# rm -rf seoimo.com-20171001.tar.gz`

搬家后解压的文件可能存在权限的问题，建议赋予网站根目录文件的可写权限。

`# chmod -R 755 /home/wwwroot/seoimo.com# chown -R www /home/wwwroot/seoimo.com`

之后，导入数据库，仍以 sjk_seoimo 为例：

`# cd /home/backup# ls# mysql -uroot -p sjk_seoimo < sjk_seoimo-20171001.sql`

倘若虚拟主机转虚拟主机，或者虚拟主机转VPS，数据库密码和某些插件文件路径可能不同，这就需要额外去查找更改了。

但如果都是在VPS上通过LNMP搭建WordPress，通常则无需再做额外操作。

注意：如果网站开启了 `HTTPS` 访问，且是安装的 `Let's Encrypt` 提供的免费SSL证书，那么除了上面的操作之外，还需要使用命令 `# lnmp ssl add` 再重新添加SSL证书。

> 【温馨提示】数据库的导出用的符号是 ">"，导入用的是 "<"；注意方向，千万别搞错了。

<span id="14.4"></span>
### #14.4 WordPress搬家脚本

*使用此脚本前请务必提前做好备份（SnapShot），万一搬家出错，还有得恢复！！*

如果你像博主一样，厌倦了每次搬家都要一遍一遍的执行压缩、传输、解压以及添加网站等操作，尤其是当VPS上有多个域名时。那么，这里有个高（偷）效（懒）的方法。

博主写了一个自动迁移WordPress的Shell脚本（WP-Migration），在你新的VPS执行就可以。但前提是你的新旧两个VPS系统最好一致，比如同为CentOS6.x或者CentOS7.x。否则，可能出现未知的问题（博主猜测）。

优点：不需要用lnmp命令提前添加好域名和数据库，全部从旧的VPS上直接复制。

博主水平有限，Linux勉强算是入门。故而把源码贴在下面，也希望有路过的大神能提点意见和建议。

脚本源码：

\# 记录程序起始时间
echo "[Starting time: `date +'%Y-%m-%d %H:%M:%S'`]"
time_start=$(date +%s)

\# 停止lnmp
lnmp stop

\# 输入旧的VPS地址和端口
read -p "Please enter your Old VPS IP (e.g. 58.58.58.58): " old_vps_ip
read -p "Please enter your Old VPS SSH Port (e.g. 58585): " old_ssh_port

\# 迁移旧的VPS上添加的[所有]网站/域名（形如：xxx.com）
echo -e "\033[32;49;1m[#1 Copy the WWWROOT files from your Old VPS now.]\033[39;49;0m"
scp -P $old_ssh_port -rC root@$old_vps_ip:/home/wwwroot/*.com /home/wwwroot/

\# 更改网站权限
chmod -R 755 /home/wwwroot
chown -R www /home/wwwroot

\# 迁移旧的VPS上添加的[所有]网站的数据库（先备份本机数据库）
echo -e "\033[32;49;1m[#2 Copy the DATABASE files from your Old VPS now.]\033[39;49;0m"
cp -r /usr/local/mysql/var /usr/local/mysql/var.old
scp -P $old_ssh_port -rC root@$old_vps_ip:/usr/local/mysql/var/ /usr/local/mysql/

\# 更改数据库权限
chown -R mysql:mysql /usr/local/mysql/var

\# 迁移旧的VPS上Apache中绑定的[所有]域名设置（先备份本机域名设置）
echo -e "\033[32;49;1m[#3 Copy the HTTPD files from your Old VPS now.]\033[39;49;0m"
cp -r /usr/local/apache/conf /usr/local/apache/conf.old
scp -P $old_ssh_port -rC root@$old_vps_ip:/usr/local/apache/conf/ /usr/local/apache/

\# 旧的VPS上网站是否启用了Let's Encrypt免费的SSL证书
echo -e "\033[32;49;1m[#4 Copy the Let's Encrypt files from your Old VPS now.]\033[39;49;0m"
read -p "Did you set up the Let's Encrypt SSL in your Old VPS before? (yes or no): " letsencrypt
if [ "$letsencrypt" = "yes" ] || [ "$letsencrypt" = "y" ]; then
scp -P $old_ssh_port -rC root@$old_vps_ip:/etc/letsencrypt /etc/
else
echo "[Skipping.]"
fi

\# 重启lnmp
lnmp start

\# 计算程序耗时并输出
echo "[End time: `date +'%Y-%m-%d %H:%M:%S'`]"
time_end=$(date +%s)
echo -e "\033[32;49;1m[Successfully done! Command takes $((time_end-time_start)) seconds.]\033[39;49;0m"

\# 退出
exit 0

**使用方法：**

在你**新的VPS上**依次执行以下命令：

`# cd ~ && wget https://www.seoimo.com/wp-content/shells/wp-migration.sh# chmod +x wp-migration.sh && ./wp-migration.sh`

脚本执行期间需要输入3-4次旧VPS的SSH访问密码，建议提前写好。用时直接复制粘贴，免得出错。

脚本执行完成，显示如下字样，说明WordPress迁移成功。否则，本脚本可能在你的系统上无法正常使用，建议按前面的常规方法搬家。

Starting LAMP...
start apache... done
Starting MySQL SUCCESS!
[Successfully done! Command takes 105 seconds.]

关于SSL证书的说明

如果在旧的VPS上已经安装了免费的 `Let's Encrypt` 证书，但新的VPS上从未安装过（包括为其他域名），那么搬家之后，建议在新的VPS上按照如下命令添加证书，以便安装相关依赖。

`# lnmp ssl add`

但是，倘若旧的VPS上已经为网站添加了证书，且新的VPS上也成功安装过 `Let's Encrypt` 证书（包括为其他域名），即系统上已经安装了相关依赖。

那么，搬家之后，证书通常不会出现问题，但自动续期时可能会显示如下错误：

expected /etc/letsencrypt/live/seoimo.com/cert.pem to be a symlink
Renewal configuration file /etc/letsencrypt/renewal/seoimo.com.conf is broken. Skipping.

这是因为在复制过程中，相关软链接（类似于快捷方式）会出现问题。因此，需要重建一下 `cert` 相关软链接：

`# cd ~ && wget https://www.seoimo.com/wp-content/shells/cert-symlink.sh# chmod +x cert-symlink.sh && ./cert-symlink.sh`

显示提示后，输入已安装 `Let's Encrypt` 证书的域名即可。

脚本执行完成后，再试着手动更新下证书，看看是否可以正常续期：

`# /bin/certbot renew --**renew-by-default** --disable-hook-validation --renew-hook "/etc/init.d/httpd restart"`

如仍提示续期失败，你可能需要手动重新安装证书：`# lnmp ssl add`

*附上 cert-symlink.sh 脚本源码如下：*

\# 记录程序起始时间
echo "[Starting time: `date +'%Y-%m-%d %H:%M:%S'`]"
time_start=$(date +%s)

\# 输入重建Symlink链接的网站/域名（形如：xxx.com）
read -p "Please enter your SSL domain (e.g. xxx.com): " cert_domain

\# 重建Symlink链接
rm -rf /etc/letsencrypt/live/$cert_domain/*.pem
ln -s /etc/letsencrypt/archive/$cert_domain/fullchain1.pem /etc/letsencrypt/live/$cert_domain/fullchain.pem
ln -s /etc/letsencrypt/archive/$cert_domain/cert1.pem /etc/letsencrypt/live/$cert_domain/cert.pem
ln -s /etc/letsencrypt/archive/$cert_domain/chain1.pem /etc/letsencrypt/live/$cert_domain/chain.pem
ln -s /etc/letsencrypt/archive/$cert_domain/privkey1.pem /etc/letsencrypt/live/$cert_domain/privkey.pem

\# 计算程序耗时并输出
echo "[End time: `date +'%Y-%m-%d %H:%M:%S'`]"
time_end=$(date +%s)
echo -e "\033[32;49;1m[Successfully done! Command takes $((time_end-time_start)) seconds.]\033[39;49;0m"

\# 退出
exit 0

<span id="14.5"></span>
### #14.5 备份小技巧

上文提到过，备份后的文件可以通过 FTP 软件下载到本地保存，也可以通过 SCP 命令上传到其他VPS上备份。

那么，哪个方法更好呢？

看个人喜好了。不过博主倾向于后者，即 scp 到其他VPS上备份保存。因为一旦你的网站出现问题，重新开VPS和从本地上传的话，一般只有几十到几百KB/s的上传速度，比较慢。而VPS之间的 scp 传速则快得多，通常几十MB/s的速度，简直天壤之别。

那是不是意味着需要额外单独买个VPS作为备份？

条件允许当然更好。但是，也不一定需要。因为Vultr自带免费的 "Snapshots" 功能。

虽然搬瓦工（和Vultr）很不错，但鸡蛋都放在一个篮子里总是不够安全的。博主的做法是：

在Vultr上另开一个机子（比如[最便宜的月付$2.5](http://www.seoimo.com/go/vultr-basic/)），然后按本文教程搭建好本站一毛一样的站点。然后 "Snapshots"，之后把新开的VPS销毁。这样一来，即使不再新开VPS，后台依然保留备份的 "Snapshots" 。

博主需要做的就是定期花几毛钱重开VPS（每月1-2次），恢复（Restoring），然后把备份上传过来，再重新 "Snapshots" 后销毁。

这样，一旦由于某些原因本站甚至搬瓦工出了问题，博客也可以在Vultr上很快恢复访问。

Snapshots-Restoring的具体步骤：

登录Vultr → 左侧Servers → 选中VPS → 上面Snapshot → 右下Restore-Snapshot

[![恢复VPS快照](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/restore-snapshot-how-w640.png)](https://www.seoimo.com/wp-content/uploads/2016/11/restore-snapshot-how-w1150.png)

<span id="15"></span>
## #15写在最后

到这里，关于在月付2.5美元（甚至更少）的便宜VPS上搭建LAMP环境，进而安装WordPress建站并进行主要的优化配置已全部完成。是不是突然觉得豁然开朗？

当然，在搭建完博客后，你也可以开启 `HTTPS` 访问。这不仅仅是为了跟风装13，其对关键词排名也确有一定的帮助。

博客安装免费SSL证书：<https://www.seoimo.com/lamp-ssl/>

其实，把网站安装成功只是万里长征开始的第一步，后面还要涉及WordPress内部的优化和加速、博客的内容建设、运营管理、安全防护等等，这在以后的文章中会继续和大家分享。

博主以为，一个优秀的博客，就像小树苗一样，需要博主长期精心的培育和维护，才能最终长成参天大树。

不过，千万要记得：一定要养成定期备份的好习惯！

在安装过程中，如遇到问题或对本文有好的想法或建议，请在下面留言评论。

倘若本文对你有所帮助，欢迎分享传播。举手之劳，也许就能够帮助更多想尝试VPS建站的朋友们少走一些弯路。