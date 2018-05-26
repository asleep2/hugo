---
title: "Hugo + Github Pages搭建静态博客"
date: 2018-04-27T13:13:44+08:00
lastmod: 2018-04-27T13:13:44+08:00
draft: false
cover: "https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/img/cover.jpg"
keywords: []
description: ""
tags: ["hugo","github","博客","静态博客"]
categories: ["博客系统"]
slug: "hugo+github"
author: "3mile"

# 索引页面上显示的缩略图
thumbnailImage: /image-3.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/4.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---


> 由于最近再次安装hugo,就想纪录一下这个过程，有什么不对的地方请指出来。

### 一. 安装hugo

*hugo有两种安装方式，homebrew包管理工具安装以及github源码下载安装*

- homebrew安装

  > homebrew简称brew, 是Mac OSX上的软件包管理工具，能在Mac中方便的安装软件或者卸载软件

  通过下面命令就可以安装brew

  ```
     ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" 
  ```

  然后安装hugo

  ```
     brew install hugo
  ```

- github源码编译安装，首先安装好依赖的工具：

  - Git
  - Mercurial
  - Go 1.3+ (Go 1.4+ on Windows)

  设置好 GOPATH 环境变量，获取源码并编译：

  ```
     $ export GOPATH=$HOME/go
     $ go get -v github.com/spf13/hugo
  ```

  源码会下载到


  GOPATH/src

   

  目录，二进制在

   

  $GOPATH/bin/

### 二. 创建Site，生成静态页面

- 创建站点

  ```
    hugo new site MyBlog
  ```

  然后hugo会自动在MyBlog目录下生成这样一个目录结构：

  ```
    |-archetypes   //包括内容类型，在创建新内容时自动生成内容的配置
    |-config.toml  // 网站的配置文件，这是一个TOML文件
    |-content	   // content目录里放你写的markdown文章
    |-data		   //
    |-layouts	   // 网站的模板文件
    |-static	   // 放一些图片、css、js等资源
    |-themes	   // 网站的主题，这里spf13上面有很多theme
  ```

  关于config.toml配置文件，下面会详细说明[1](https://tracydeng.github.io/2016/07/hugo/#fn:1)

- 创建md文档 ( *需先进到MyBlog目录下* )

  ```
   hugo new about.md
  ```

  执行完后，会在content目录自动生成一个MarkDown格式的about.md文件，内容如下：

  ```
   +++
   date = "2016-04-27T20:37:17+08:00"
   draft = true
   title = "about"
   +++
  ```

  如果是博客日志，最好将md文件放在content的post目录里。

  ```
   hugo new post/first.md
  ```

执行完后，会在content/post目录创建一个MarkDown格式的first.md文件

- 添加主题模版

  > 默认生成的网站是没有任何皮肤模板的，还得去Github上下载一个网页模板下来。如果你网络够好，网速够快，你可以在刚才的目录将Hugo官方的所有模板都下载下来：

  ```
   git clone --recursive https://github.com/spf13/hugoThemes themes
  ```

  下载的主题存放在 themes/ 文件夹中,也可以只选择下载自己喜欢的模版： 进到themes目录

  ```
   cd themes
  ```

  下载hyde主题模版

  ```
   git clone https://github.com/spf13/hyde.git
  ```

- 本地调试

  ```
   hugo server --theme=hyde --buildDrafts --watch
  ```

  参数说明：

  ```
    --theme 选择主题，如果安装了多个主题，这里指定就好，随意切换
    --watch 监控到文章的改动从而自动去刷新浏览器，不需要自己手工去刷新浏览器，非常方便, 现在默认是这样的，可以不用带 (hugo server --theme=hyde --buildDrafts也是同样效果)
    --buildDrafts  与content目录下的md文件结合来，如果md文档中 draft = true,就必须要加上--buildDrafts参数
  ```

  效果图如下：![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/first-post-screenshot.jpg)

### 三. 托管到github pages

> 其实这一步更像是git操作，即将生成的静态页面push到git服务端。

要部署在 GitHub Pages 上，首先你需要在GitHub上创建一个Repository，命名为：tracydeng.github.io （tracydeng替换为你的github用户名）

接着回到站点根目录，也就是MyBlog目录下，执行命令：

```bash
  hugo --theme=hyde --baseUrl="http://mile3033.github.io/"
```

命令执行完在站点根目录下会生成一个public目录，该目录下包含了所有通过hugo生成的静态页面，接下来要做的就是将这些静态页面push到刚刚创建仓库的master分支。

首先进到public目录

```bash
$ cd public
$ git init
$ git remote add origin https://github.com/tracydeng/traydeng.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```

如果没出错的话，到这里也就已经执行完了，到浏览器输入tracydeng.github.io就可以访问你刚才写的内容了。

### 四. 添加评论模块

下载的模版里基本上都带了评论模块，找到自己使用的theme，到layouts/partials目录下，可以看到comments.html(有些不是这个名字，像hyde模版是disqus.html)，没有的话，就是模版没带这个模块，需要自己添加，打开我使用的hugo－uno模版下面的comments.html,可以看到以下代码：

```html
<section class="post-comments">
 <a class="muut" href="https://muut.com/i//comments:">Comments</a>
 <script src="//cdn.muut.com/1/moot.min.js"></script>
</section>


<div id="discourse-comments"></div>
<script type="text/javascript">
  	var discourseUrl = ,
    discourseEmbedUrl = ;
  	(function() {
  	 	var d = document.createElement('script'); d.type = 'text/javascript'; d.async = true;
  	    d.src = discourseUrl + 'javascripts/embed.js';
    	(document.getElementsByTagName('head')[0] || 		document.getElementsByTagName('body')[0]).appendChild(d);
	})();
</script>


<div id="disqus_thread"></div>
<script type="text/javascript">
 	 var disqusUsername = ;
 	(function() { // DON'T EDIT BELOW THIS LINE
  		var d = document, s = d.createElement('script');
  		s.src = '//' + disqusUsername + '.disqus.com/embed.js';
  		s.setAttribute('data-timestamp', +new Date());
  		(d.head || d.body).appendChild(s);
 	 })();
</script>
<noscript>Please enable JavaScript to view the <a 	href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>

	
```

上面代码可以看到是支持到了muut，discourse，disqus的评论，除了这些比较出名的第三方评论服务还有多说，这里以disqus为例来说下添加评论模块：

##### 获取disqusShortname

到disqus注册一个账号，登录，选择**add a newsite to disqus**,Site就填写自己的博客地址：*tracydeng.github.io*,并且设置好你的disqusShortname，默认时你站点拼接**tracydenggithubio**，当然自己可以修改，我改短一点改成**tracydeng**，这个name就是之后配置时要用到的,其它操作就是下一步，下一步了

##### 配置disqusShortname

这里要结合/theme/layouts/partials下.html文件来配置 ，在MyBlog/config.toml中配置disqusShortname/disqus, 如上comments.html文件中:

```toml
  var disqusUsername = ;
```

disqusUsername便是取的站点下配置文件中的参数disqus，于是在config.toml文件中params下面添加disqus就好。

```toml
 [params]
   	disqus = "3mile"
```

### 五. 我做的一些改动

- 修改config.toml  

```toml
   title : 修改为Coder Steven
     
   description : "3mile"
```

- 修改.md  文档

添加menu菜单

```toml
   +++
   date = "2016-04-27T20:37:17+08:00"
   draft = true
   title = "about"
   menu ＝ "main"
   +++
```

当然这里还可以添加category等，看自己需求了

再次启动，可以看到刚刚修改后的效果图：

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/github/first-post-screenshot.jpg)

### 参考链接

- http://www.tuicool.com/articles/yeaYFjF

1. 包括 baseurl :主站地址, title：标题 , theme：主题，copyright 等等网站参数。 [↩](https://tracydeng.github.io/2016/07/hugo/#fnref:1)