---
title: "谷歌插件Tampermonkey"
date: 2018-05-05T10:44:13+08:00
lastmod: 2018-05-05T10:44:13+08:00
draft: false
keywords: []
description: ""
tags: ["chrome","油猴"]
categories: ["chrome"]
slug: "Tampermonkey"
url: "/archives/134"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t1.jpg"

thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t1.jpg
# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/1.jpg
#封面说明内容
coverCaption: "A beautiful sunrise"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true

---

不装扩展（Extensions）的 Chrome 只能发挥它 40% 的能力。

各类实用的 Chrome 扩展是不少人选择 Chrome 浏览器的重要原因，经过多年发展，Chrome 的扩展种类已经非常丰富，除了那些「即装即用」的小工具之外，也有很多被誉为「神器」的强大扩展程序。

少数派此前介绍过的 [Stylish](https://sspai.com/post/34508) 就算一款「神器」，通过安装各类 CSS 模板，它几乎可以美化一切网页。而另一款不得不提的「神器」就是今天要介绍的 Tampermonkey，也被戏称为「油猴」。

和 Stylish 类似，「油猴」也可以通过安装各类脚本对网站进行定制。不过它能定制的不仅仅是网站的样式，还能实现更多更强大的功能，例如：

- 直接下载百度网盘文件
- 重新定制繁杂的微博页面
- 去掉视频播放广告
- 将网站默认的「二维码登录」改回「账号密码登录」
- 绕过搜索引擎的跳转提示
- 还原清新的小说阅读模式
- 豆瓣和 IMDb 互相显示评分
- ……

你可能听说过「油猴」，但是因为看到「脚本」而不敢尝试，其实它的操作非常简单，只要经过简单设置，下载一些现成脚本，就可以实现上面提到的实用的功能。

## 何使用 Tampermonkey

如果能正常访问 Chrome 应用商店，可以直接在商店内下载 [Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)。

如果不能，在这里推荐一个叫 [Crx4Chrome](https://www.crx4chrome.com/) 的网站，可以直接下载 Chrome Store 插件，在 Crx4Chrome 搜索并下载 [Tampermonkey 插件](https://www.crx4chrome.com/extensions/dhdgffkkebhmkfjojejmpbldmpobfkfo/) 到本地之后，再打开 Chrome 浏览器「扩展程序」页面，将下载的 crx 文件拖拽到页面即可完成安装。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t1.jpg)

另外，Tampermonkey 还支持 Microsoft Edge、Safari、Opera Next、Firefox、Dolphin Browser、UC Browser 等浏览器平台，你可以在 [软件官网](https://tampermonkey.net/) 下载到对应版本。

### Tampermonkey 设置选项

安装好之后，会在浏览器地址栏右侧看到类似望远镜的图标，这个就是 Tampermonkey，点击右键选择选项，即可看到设置页面：

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t2.jpg)

Tampermonkey 提供了友好的中文化界面，懒得折腾的用户使用默认设置即可，无需更改任何选项。

如果需要更多高级设置选项的话，可自行打开「初学者」或者「高级」配置模式，设置将提供动作菜单、更细致的脚本更新、TESLA、加强版编辑器、安全、黑名单检查等高级选项。

### 脚本安装和管理

油猴默认是没有安装任何脚本的，你可以通过设置页面的「已安装脚本 - 获取脚本…」来下载各种脚本。

比较常用的下载渠道有三个：

- [Greasy Fork](https://greasyfork.org/zh-CN)：支持中文，按照今日安装、总安装数、得分、创建日期等的排序方式给出脚本列表，可按脚本生效的网站过滤，每一脚本都有中文介绍，并且详细列出了作者、安装数、更新日期日志、安装使用截图、兼容性、应用到、代码查看等信息描述。
- [OpenUserJS](https://openuserjs.org/)、[Userscripts Mirror](https://userscripts-mirror.org/)：这两个网站都没有提供中文界面，Userscripts Mirror 已经停止了更新，用户可以在这个站点找到历史资源。

找到需要的脚本后，会在介绍页面看到安装（install）按钮，点击下载脚本后会自动跳转到安装界面，再点击安装就可以享用脚本了。

比如，在 OpenUserJS 的 Yet Another Weibo Filter 脚本页面，点击右侧 Install 之后会跳转到 Tampermonkey 的安装页面，这里列出了脚本的基本说明和源代码，再次点击页面中的「安装」按钮即可。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t3.jpg)

此时打开微博网站，点击地址栏右侧的 Tampermonkey 图标，可以看到这个 Yet Another Weibo Filter 已经成功启用，用户可以点击 ON 按钮临时关闭使用该脚本。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t4.jpg)

打开 Tampermonkey 设置页面的「已安装脚本」，我们可以看到刚安好的 Yet Another Weibo Filter 脚本，用户在这里可以选择是否打开脚本，或是对脚本进行编辑、提交 Bug 以及删除脚本等多项操作。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t5.jpg)

建议在安装好各个脚本之后，在实用程序的页面中，将脚本存储和 Tampermonkey 设置以文件或者压缩包的形式导出，方便以后数据备份。

## 优秀脚本推荐

在上面提供的三个网站大家可以看到各种功能的脚本，你可以根据自己的需求进行下载，如果不知道该下载哪些，下面为大家推荐 15 个优秀实用的用户脚本，不妨先来看看。

### 1. userscripts 只显示中文

在 userscripts、greasyfork 脚本页面只显示中文脚本，支持 AutoPager 和其它翻页脚本。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t22.jpg)

[下载地址](https://greasyfork.org/zh-CN/scripts/305-userscripts-%E5%8F%AA%E6%98%BE%E7%A4%BA%E4%B8%AD%E6%96%87)

### 2. AC-从Google Baidu Bing搜索结果中屏蔽卡饭教程

从Google Baidu Bing Haosou Youdao搜索结果中屏蔽'卡饭教程'

[点击下载](https://greasyfork.org/zh-CN/scripts/13404-ac-%E4%BB%8Egoogle-baidu-bing%E6%90%9C%E7%B4%A2%E7%BB%93%E6%9E%9C%E4%B8%AD%E5%B1%8F%E8%94%BD%E5%8D%A1%E9%A5%AD%E6%95%99%E7%A8%8B)

### 3. 吾爱破解网盘链接激活工具 by lsj8924

激活吾爱破解论坛的百度和360网盘的链接，可以直接点击。
[点击下载](https://greasyfork.org/zh-CN/scripts/23600-%E5%90%BE%E7%88%B1%E7%A0%B4%E8%A7%A3%E7%BD%91%E7%9B%98%E9%93%BE%E6%8E%A5%E6%BF%80%E6%B4%BB%E5%B7%A5%E5%85%B7-by-lsj8924)

### 4. Userscript+ : 显示当前网站所有可用的UserJS脚本 Jaeger

显示当前网站的所有可用UserJS(Tampermonkey)脚本,交流QQ群:104267383

![userscript+cn.gif](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/userscript+cn.gif)

**Userscript+** 是一款`Tampermonkey`脚本,作用是当你浏览网页的时候,从右下角自动为你推荐适用于当前页面的`Tampermonkey`脚本，并且可以一键安装指定的脚本。

很多时候，我们并不知道一些网站是否有用户提供用来优化页面的脚本，而**Userscript+** 就能帮你自动寻找适用的UserJS，并默认按照评分高低排序推荐给你,给你带来一种全新的`Tampermonkey`使用体验！
[下载地址](https://greasyfork.org/zh-CN/scripts/24508-userscript-show-site-all-userjs)

### 5.百度网盘直接下载助手修改版

网盘内和分享页均显示[下载助手]按钮，支持获取直接下载链接+压缩下载链接；
大文件/单文件/多文件/文件夹，支持点击直接下载免强制调用百度网盘客户端；
[下载地址](https://greasyfork.org/zh-CN/scripts/39776-%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98%E7%9B%B4%E6%8E%A5%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B%E4%BF%AE%E6%94%B9%E7%89%88)

### 5. 看真正想看的微博：[Yet Another Weibo Filter](https://greasyfork.org/zh-CN/scripts/3249-yet-another-weibo-filter)

Weibo 官方界面已经成为不少脚本应用必修的对象，ts 开发的这款脚本可以高度定制 Weibo 电脑端版面，去除各类广告、微博主自带的各种徽标、过滤热门话题等主要功能，用户需要在脚本的设置中启用相应功能。

如果希望单独安装浏览器插件的话，推荐 [眼不见心不烦](https://openuserjs.org/scripts/ts/[https://code.google.com/p/weibo-content-filter/)，其支持 [Chrome](https://chrome.google.com/webstore/detail/aognaapdfnnldnjglanfbbklaakbpejm) 和 [Firefox 脚本](https://bitbucket.org/salviati/weibo-cleaner/downloads/weiboCleaner-latest.user.js)

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t6.jpg)

### 6. 还原真实下载地址：[百度网盘直接下载助手](https://greasyfork.org/zh-CN/scripts/23635-%E7%99%BE%E5%BA%A6%E7%BD%91%E7%9B%98%E7%9B%B4%E6%8E%A5%E4%B8%8B%E8%BD%BD%E5%8A%A9%E6%89%8B)

安装百度网盘直接下载助手之后，打开需要下载的资源页面，会出现下载助手的按钮，提供直接下载（支持多文件和目录下载）、显示链接以及外链下载的选项，可实现直接复制到下载工具使用。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t7.jpg)

### 7. 让所有视频网页全屏：[视频网页全屏](https://greasyfork.org/zh-CN/scripts/4870-maximize-video)

可以让网页中任何一个视频网页全屏播放的「神器」，目前支持有多个视频的任意网页、HTML5 格式的视频。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t9.jpg)

### 8. 豆瓣和 IMDb 互相显示评分：[MoreMovieRatings](https://greasyfork.org/zh-CN/scripts/7687-moremovieratings)

不少人看电影时喜欢参考 IMDb 和豆瓣电源的评分，这款脚本正好满足两者需求，可以在豆瓣和 IMDb 互相显示评分，电影党必备。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t10.jpg)

### 9. 查看完整的知乎回答而无需注册登录：[Zhihu Visitor](https://openuserjs.org/scripts/ts/Zhihu_Visitor)

知乎问题页面里，比较长的答案添加展开按钮，点击可以显示全文。点击「更多回答」可以加载更多回答而非登录框。隐藏了必须登录才能使用的相关功能的按钮，如点赞或收藏等。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t11.jpg)

### 10. 增强版的 YouTube 功能改造：[YouTube +](https://openuserjs.org/scripts/ParticleCore/YouTube_+)

YouTube + 可以给 Youtube 增加更多的功能选项，包括但不限于小窗口播放视频、播放您最近订阅播放列表、视频截图保存、只允许你订阅频道的视频播放广告等等。不过目前 YouTube + 不支持 YouTube beta Material Layout 测试版。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t12.jpg)

### 11.  自动翻页 Google 搜索结果：[Endless Google](https://openuserjs.org/scripts/tumpio/Endless_Google)

实现无需手动点击 Google 搜索结果的页码，实现自动翻页显示搜索内容。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t13.jpg)

### 12. 轻松下载 Instagram 图片和视频：[IGHelper](https://greasyfork.org/en/scripts/22660-ighelper-download-instagram-pic-vids)

方便用户下载 Instagram 的图片和视频，将鼠标移动到图片或者视频上，即可看到下载按钮。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t14.jpg)

### 13. 悬停查看和下载图片：[Mouseover Popup Image Viewer](https://greasyfork.org/en/scripts/404-mouseover-popup-image-viewer)

只需将鼠标光标悬停在多媒体资源的链接上，即可直接显示完整的图像和视频剪辑，避免了用户二次点击，并且通过快捷键实现下载、缩小放大、顺序浏览图册等功能。脚本已经上百个图像和视频托管服务（如 Facebook、500px、Flick 和 YouTube）。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t15.jpg)

### 14. YouTube 影片下载为 MP3 格式文件：[Simple YouTube MP3 Button](https://greasyfork.org/en/scripts/20015-simple-youtube-mp3-button)

脚本提供了即时转换功能，可将 YouTube 影片以 MP3 音频文件格式下载到本地。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t16.jpg)

### 15. GitHub 中文化界面：[GitHub 汉化插件](https://openuserjs.org/scripts/52cik/GitHub_%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6)

很多新手朋友不太会玩 GitHub，可能被全英文界面所困扰，这款脚本实现汉化了 GitHub 界面的部分菜单及内容，新手熟悉之后可选择停用脚本恢复英文模式。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t17.jpg)

### 16. 给你最好用的 YouTube 视频下载工具：[Youtube Best Video Downloader 2](https://greasyfork.org/en/scripts/19592-youtube-best-video-downloader-2)

脚本提供了 YouTube 视频下载的快捷功能，可保存为 Full-HD MP4、FLV、3GP、MP3（码率为 128kbps 或者 192kbps）、M4A 以及 AAC 格式。经测试，这款脚本会和上面提及到的 YouTube + 脚本有冲突，需要暂时停用 YouTube +，才可看到下载按钮。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t18.jpg)

### 17. Feedly 订阅工具增强版：[Feedly filtering and sorting](https://greasyfork.org/en/scripts/20483-feedly-filtering-and-sorting)

此脚本主要是为 Feedly 订阅增强了部分功能，包括了高级关键字匹配、自动加载、高亮显示自定义标题、订阅内容高级排序规则等。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t19.jpg)

### 18. 还你清新的小说阅读模式：[My Novel Reader](https://greasyfork.org/zh-CN/scripts/292-my-novel-reader)

小说阅读脚本实现了统一阅读样式，内容去广告、修正拼音字、段落整理，自动下一页的功能，相当适合重度的小说阅读用户。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t20.jpg)

### 19. 绕过搜索结果的自我跳转，直接访问原始网页：[AC-baidu](https://greasyfork.org/zh-CN/scripts/14178-ac-baidu-%E4%BC%98%E5%8C%96%E7%99%BE%E5%BA%A6-%E6%90%9C%E7%8B%97-%E8%B0%B7%E6%AD%8C%E6%90%9C%E7%B4%A2%E7%BB%93%E6%9E%9C%E4%B9%8B%E9%87%8D%E5%AE%9A%E5%90%91%E5%8E%BB%E9%99%A4-%E5%8E%BB%E5%B9%BF%E5%91%8A-favicon)

脚本可实现绕过百度、搜狗搜索结果中的自己的跳转链接，直接访问原始网页（间接缩短访问目标网页的时间）；可去除百度搜索结果中多余广告 ；添加 Favicon 显示；添加计数。

![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/chrome/t21.jpg)

## 结语 | 动手玩

上面给出的 15 个脚本只是很小的一部分，脚本工具可以专门改变特定网站的行为，比如过滤广告、添加下载按钮、网页界面定制等等，同时由于涉及到版权的问题，并没有向大家推荐类似绕过 VIP 视频限制之类的脚本。这些在 Greasy Fork 和 OpenUserJS 都提供了相当不错的选择，大家根据需求自行下载试玩。

如果觉得现有的脚本还不够完善，那就动手写一个吧。最后，欢迎大家在留言中批评、指点、分享、投币，也可以留言哪些脚本神器值得推荐。

**参考链接：**

- [不喜欢某个网站的样子？用 Stylish 给它一键「换肤」](https://sspai.com/post/34508)
- [有哪些值得推荐的油猴脚本?](http://www.runningcheese.com/userscripts)