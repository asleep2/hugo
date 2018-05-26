---
title: "谷歌插件Ublock Origin"
date: 2018-05-05T11:37:15+08:00
lastmod: 2018-05-05T11:37:15+08:00
draft: false
keywords: []
description: ""
tags: ["chrome"]
categories: ["chrome"]
slug: ""
url: "/archives/136"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/auto-orient1.jpg"

thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/auto-orient1.jpg
# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/3.jpg
#封面说明内容
coverCaption: "A beautiful sunrise"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true

---

关于 uBlock Origin
 有人曾经做过对比：uBlock Origin对比ABP有性能上的优势，其最为突然的性能优势就是其占用极低的内存和 CPU。有分析说adp主要靠的是屏蔽，而ublock Origin主要靠的是阻断，ABP的工作需要在所有网页插入屏蔽脚本和css，而uBlock Origin直接阻止需要屏蔽的内容进入当前网页。一般的拦截请求的规则大家都差不多，关键的是元素隐藏规则，uBlock 把它叫做修饰规则 cosmetic filters，ABP 不管是什么网页都会插入 14000 多条元素隐藏规则，所以占用内存很大，uBlock 插入的很少，因为他是在网页开始加载以后才判断需要用到哪些元素隐藏规则。所以才在性能上面要更加优越。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/auto-orient) 

uBlock Origin性能优势

 http://chromecj.com/productivity/2017-06/770.html

 

![巨大的电源按钮](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/auto-orient1.jpg) 

 

 

(3)元素吸管图标：点击滴管图标可以进入元素选择器模式，在这里你可以交互地从页面选择元素并创建过滤规则来永久移除该元素。屏蔽元素按钮(用过ABP的都知道)
 (4)列表图标：网络请求日志(个人理解:网络请求记录监控中心)：可以按照网络资源查看/屏蔽的控制系统 。网络请求日志与开发工具的网络 不同之处在于，不单单可以查看网络资源，还可以屏蔽不想要的脚本等等之流 。你可以在浏览器里实时查看网络通信情况。提示：点击图标的同时按住 Shift 键可以切换选择是在新窗口还是新标签页中打开记录台。uBO 会在你未按 Shift 键打开记录台时记住你的选择。

(5）禁止网页弹窗按钮，开启后，该网页永久无法弹窗 。默认情况下弹出窗口是允许显示的，除非有相应的过滤规则屏蔽。但如果开启该选项，不管规则如何，当前站点的所有弹出窗口都会被屏蔽：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/164.png) 

ublock origin禁止弹窗

 

 

基于 Chromium 的浏览器请注意：

uBlock Origin

 

 

(7)禁止修饰生效按钮，开启，隐藏元素规则失效 。该特性生效时，图标旁边的数字表示被 uBO 修饰规则隐藏的元素数量。如果网页有被隐藏的元素，那么一旦你禁用修饰规则，这些元素就会立即显示，一旦启用立即隐藏。

(8)禁止第三方字体：三种颜色：红(block)、灰(noop)、绿(allow) 出于安全和隐私方面考虑，许多人希望默认能屏蔽所有网页字体。你只需在控制面板的 "自定义规则 " 版块直接添加下面这条规则：no-remote-fonts: * true
 这样 uBlock 就会默认屏蔽任何地方的网页字体，而你又可以根据不同的站点点击这个开关来允许使用网页字体。
 基于 Chromium 的浏览器请注意：Chromium 的 webRequest API 无法准确报出 font 类的请求，所以字体会被归为 other 类型。uBlock 是根据一条 URL 路径的"扩展名"来判断一条请求是否属于字体资源，但一条 URL 的请求类型可以千变万化，所以对于基于 Chromium 的浏览器，uBlock 也许得在请求产生以后才能屏蔽字体，也就是从远端服务器接收到响应标头以后，毕竟从响应标头可以确认资源属于哪种类型。
 uBlock Origin如何添加白名单
 许多用户的反馈希望增加能将网站加为白名单的功能，也就是在特定的网站禁用 uBlock。其实这项功能已经有了，就是那个巨大的电源按钮。点击这个按钮你可以将当前网站加入白名单，在你下次访问该网站时仍会记住你的选择。如下图所示：

 

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/311.png) 

ublock origin白名单

 

常见的uBlock Origin规则推荐
 初始默认加载和执行下列过滤规则列表：

- EasyList
- Peter Lowe’s Ad server list
- EasyPrivacy
- Malware domains

这里还有更多的规则列表供你选择：

- Fanboy’s Enhanced Tracking List
- Dan Pollock’s hosts file
- hpHosts’s Ad and tracking servers
- MVPS HOSTS
- Spam404
- 等等

当然，启用越多的过滤规则就会产生越高的内存占用。 然而，即使再添加 Fanboy 额外的两个规则列表，如 hpHosts’s Ad 和 tracking servers，uBlock₀ 的内存占用依然比其他常见的过滤工具要低的多。
 uBlock Origin小结
 ABP的过滤规则建立或许比较直观方便，但对于不想详细研究直接用其他人维护的列表且对性能要求较高的人来说，uBlock Origin也许更适合（说的就是我~~）。

 

 

 

 

 