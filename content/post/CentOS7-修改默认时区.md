---
# 常用定义
title: "CentOS7 修改默认时区"           # 标题
date:  2018-04-04T13:50:17+08:00    # 创建时间
draft: false                       # 是否是草稿？
url: /archives/117
tags: ["Linux", "VPS", "CentOS"]  # 标签
categories: ["vps"]              # 分类
author: "3mile"                  # 作者

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/7.jpg

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



Linux](https://www.jiloc.com/tag/linux) 系统(我特指发行版, 没说内核) 下大部分软件的风格就是不会仔细去考虑向后 的兼容性, 比如你上个版本能用这种程序配置, 没准到了下一个版本, 该程序已经不见了. 比如 sysvinit 这种东西.

设置时区同样, 在 [CentOS](https://www.jiloc.com/tag/centos) 7 中, 引入了一个叫 timedatectl 的设置设置程序.

用法很简单:

```cmake
timedatectl # 查看系统时间方面的各种状态
```

$\textcolor{Red}{返回结果:} $

```INI
Local time: 四 2014-12-25 10:52:10 CST

Universal time: 四 2014-12-25 02:52:10 UTC

RTC time: 四 2014-12-25 02:52:10

Timezone: Asia/Shanghai (CST, +0800)

NTP enabled: yes

NTP synchronized: yes

RTC in local TZ: no

DST active: n/a

```

其实不考虑各个发行版的差异化, 从更底层出发的话, 修改时间时区比想象中要简单:

```cmake
timedatectl list-timezones # 列出所有时区
timedatectl set-local-rtc 1 # 将硬件时钟调整为与本地时钟一致, 0 为设置为 UTC 时间
timedatectl set-timezone Asia/Shanghai # 设置系统时区为上海
```

