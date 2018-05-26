---
title: "Win10搭建Hexo博客"
date: 2018-04-21T11:41:05+08:00
lastmod: 2018-04-21T11:41:05+08:00
draft: false
url: /archives/130
keywords: []
description: ""
tags: ["hexo"]
categories: ["博客系统"]
author: "3mile"

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/2.jpg

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/2.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---



发现在VPS上部署Hexo博客看着太麻烦了，还是本地配合Github搞吧，这样既不失装B还能超低成本有自己的一个博客，不用自己出服务器钱，不用担心被攻击，如果你不要独立域名直接就是0成本！

在dalao界Hexo博客一直令我等鶸膜拜，在网上找了很多资料后终于搞定了Hexo的博客，以后也可以装B去了。不过你要是不差钱，就是个小白还是用WP吧，这玩意用着其实挺别扭的。。。



Table of Contents

- 一、Windows 10上的部署
  - [1.安装Git](#1.1)
  - [2.配置Git](#1.2)
  - [3.生成密钥文件](#1.3)
  - [4.安装NodeJS](#1.4)
  - [5.安装Hexo](#1.5)
- 二、Hexo的使用
  - [1.新建站点](#2.1)
  - 2.Hexo的配置
    - [（1）替换主题](#2.2.1)
    - [（2）插入图片](#2.2.2)
  - [3.新建博文](#2.3)
  - [4.本地预览](#2.4)
- [三、配置Github Pages或Coding Pages](#3)
- Github的配置方法
  - [1.注册并登录Github帐号。](#3.1.1)
  - [2.添加SSH KEY](#3.1.2)
  - [3.测试SSH连接](#3.1.3)
- Coding中的配置方法
  - [添加SSH keys](#3.2.1)
  - [测试SSH连接](#3.2.2)
- [四、部署你的博客](#4)
- 五、独立域名绑定
  - [1.DNS解析](#5.1)
  - [2.Hexo上的设置](#5.2)
  - [域名绑定Github](#5.3)
  - [域名绑定Coding Pages](#5.4)
- 六、其他辅助工具
  - [Markdown书写工具](#Markdown)
  - [Markdown渲染插件](#Markdown-2)
  - [图床](#i-4)
  - [七牛](#i-5)
  - [MPic](#MPic)
- [七、扩展阅读](#i-6)
- [八、参考文章](#i-7)
- [九、总结](#i-8)

## 一、Windows 10上的部署

本次以比较流行的Win10为例，Win7、8也差不多，XP直接打死。

<span id="1.1"></span>

### 1.安装Git

Git是上传到Github的工具，如果在Github上有项目都会用到这个。

下载：[https://git-scm.com/download/win](https://www.zrj96.com/go/?url=https://git-scm.com/download/win) 选择对应系统的版本即可，一路下一步，记住选择几个功能，这样操作更像是在Linux Shell里操作。

`Use Git from Bash only`、`Checkout Windows-style,commit Unix-style line endings`、`Use MinTTY(the default terminal of MSYS2)`

<span id="1.2"></span>
### 2.配置Git

安装好后需要几行命令说清楚你是谁，这样才能认对人。自行替换自己的用户名和邮箱。

```Bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

<span id="1.3"></span>
### 3.生成密钥文件

这个操作加密你的通信过程，同时后期上传到Github都会用到。

```Bash
ssh-keygen -t rsa -b 4096 -C "email@example.com"
```

按3次回车，全部无视，证书文件会在C:\User\用户名\.ssh 生成两个文件。

<span id="1.4"></span>
### 4.安装NodeJS

去官网下载NodeJS Windows版本，建议选择LTS版本，[https://nodejs.org/en/](https://www.zrj96.com/go/?url=https://nodejs.org/en/)，安装的时候务必选择Add to PATH选项。

<span id="1.5"></span>
### 5.安装Hexo

在Git程序里运行命令行即可安装

```Bash
npm install -g hexo-cli
```

至此在Win上的部署安装已经完成，接下来就是如何使用了。

## 二、Hexo的使用

<span id="2.1"></span>
### 1.新建站点

假设代码存放在D:\hexo\blog

```Bash
cd /d
mkdir hexo
cd hexo
hexo init blog
cd blog
npm install
```

在D:\hexo\blog 里就能看到所有文件了，下面是文件说明：

| 目录名称     | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| scaffolds    | [**模版**](https://www.zrj96.com/go/?url=https://hexo.io/zh-cn/docs/writing.html) 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。 Hexo的模板是指在新建的markdown文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。 |
| source       | 资源文件夹是存放用户资源的地方。除 `_posts` 文件夹之外，开头命名为 `_` (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 `public` 文件夹，而其他文件会被拷贝过去。 |
| themes       | [**主题**](https://www.zrj96.com/go/?url=https://hexo.io/zh-cn/docs/themes.html) 文件夹。Hexo 会根据主题来生成静态页面。 |
| _config.yml  | 网站的 [**配置**](https://www.zrj96.com/go/?url=https://hexo.io/zh-cn/docs/configuration.html) 信息，您可以在此配置大部分的参数。 |
| package.json | 应用程序的信息。[**EJS**](https://www.zrj96.com/go/?url=http://embeddedjs.com/), [**Stylus**](https://www.zrj96.com/go/?url=http://learnboost.github.io/stylus/) 和 [**Markdown**](https://www.zrj96.com/go/?url=http://daringfireball.net/projects/markdown/) renderer 已默认安装，您可以自由移除。 |

### 2.Hexo的配置

<span id="2.2.1"></span>
#### （1）替换主题

推荐[**NexT**](https://www.zrj96.com/go/?url=http://theme-next.iissnan.com/)主题，这是一款知名的Hexo主题，非常漂亮简洁。

```Bash
cd /d/hexo/blog
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

回到根目录，找到_config.yml 文件，在第66行的theme字段里把默认主题名字换成next即可。

<span id="2.2.2"></span>
#### （2）插入图片

`Markdown`支持插入本地图片或外部链接图片，要保证本地和网络上都能访问图片，使用[**hexo-asset-image**](https://www.zrj96.com/go/?url=https://github.com/CodeFalling/hexo-asset-image)

```Bash
# 安装插件
npm install https://github.com/CodeFalling/hexo-asset-image --save
启用插件，确保主题配置文件D:\hexo\blog\_config.yml中
post_asset_folder: true
# 新增博文后，会在D:\hexo\blog\source\_posts目录下生成 xxx.md 和 xxx 目录，将图片存放该目录中，使用时 ![](***.jpg)，这样Typora预览和发布到网上时Hexo博客都能正常显示图片
```

<span id="2.3"></span>
### 3.新建博文

```Bash
hexo new "Hello World"
```

在目录`D:\hexo\blog\source\_posts`下会生成Markdown文件Hello World.md

**手动添加Markdown文件到D:\hexo\blog\source\_posts目录效果一样**

<span id="2.4"></span>
### 4.本地预览

如果以后修改了主题和写了一篇新文章都可以使用这个方法在本地查看，解决BUG。

```Bash
cd /d/hexo/blog
# 生成静态文件
hexo generate
# 启动本地服务器
hexo server --debug
```

打开浏览器，输入http://localhost:4000 即可看到站点的预览了。

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/ui.png)

提醒一点，生成静态化可以使用简化命令

```Bash
hexo g
```

**在后面的上传到Github中，如果你发现明明写了一篇文章，但是网站却没有？那么一定是MD的语法有问题，生成静态化文件的时候就会报错，务必检查一下哪里出问题，修复后才能成功上传和展现文章。**

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/error.png)

<span id="3"></span>
## 三、配置Github Pages或Coding Pages

Github比较出名些，Coding是国内的平台，和Github基本差不多，如果担心访问速度或者其他原因可以选择国内的。

## Github的配置方法

<span id="3.1.1"></span>
### 1.注册并登录Github帐号。

新建一个仓库，建好后可以在仓库首页的Setting里修改为：yourname.github.io

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/github-1.png)](https://odg1

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/github-2.png)

<span id="3.1.2"></span>
### 2.添加SSH KEY

点击Github右上角的头像，有个Setting，找到SSH and GPG keys，新建一个New keys，随便起名，把密钥内容复制进去。密钥是啥？就是最开始生成的那个密钥，id_rsa.pub文件。

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/github-3.png)

<span id="3.1.3"></span>
### 3.测试SSH连接

在本地的Git中执行，

```Bash
ssh -T git@github.com
```

如果出现`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`提示，则表示连接成功。如果不行就重新生成一个密钥再重新上传密钥试试。

## Coding中的配置方法

Github免费用户只能新建公开的代码仓库，而且是国外的服务器，而Coding可以新建私有代码仓库，国内用户访问速度更快。注册[**Coding**](https://www.zrj96.com/go/?url=https://coding.net/)，添加项目，`项目名称为Coding用户名`，分支选择`master`，同时还需要在`D:\hexo\blog\source`目录下创建一个空白文件`Staticfile`:

```Bash
cd /d/hexo/blog/source
touch Staticfile
```

<span id="3.2.1"></span>
### 添加SSH keys

[https://coding.net/help/doc/git/ssh-key.html](https://www.zrj96.com/go/?url=https://coding.net/help/doc/git/ssh-key.html)

在Coding `账户`中找到`SSH 公钥`，新增公钥，复制公钥文件`id_rsa.pub`中的内容

<span id="3.2.2"></span>
### 测试SSH连接

在`Git Bash`中执行:

```Bash
ssh -T git@git.coding.net
```

如果出现`Hello username! You have connected to Coding.net by SSH successfully!`提示，则表示连接成功。

<span id="4"></span>
## 四、部署你的博客

注意**站点配置文件**`D:\hexo\blog\_config.yml`中`deploy`参数配置如下：

```Bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
    github: git@github.com:zrj766/zrj766.github.io.git,master
    coding: git@git.coding.net:zrj766/zrj766.git,master
```

在本地Git中执行：

```Bash
# git方式需要先安装插件
npm install hexo-deployer-git --save
# 上传代码到仓库
hexo clean && hexo generate && hexo deploy
或者:
hexo clean && hexo generate -d
```

如果出现`INFO Deploy done: git`提示，则表示部署成功。访问`用户名.github.io`和`用户名.coding.me`都可以正常打开博客了。

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/github-4.png)

<span id="5"></span>
## 五、独立域名绑定

用个二级域名总是不爽，何况现在主流域名都不贵，现在来绑定自己的域名。

<span id="5.1"></span>
### 1.DNS解析

www和@记录做CNAME解析到 用户名.github.io

如果使用的是Coding同样的方法解析到 pages.coding.me

<span id="5.2"></span>
### 2.Hexo上的设置

<span id="5.3"></span>
### 域名绑定Github

在`D:\hexo\blog\source`目录下新建一个文件`CNAME`，内容为要绑定的域名：

**文件去掉格式，直接空白**

```Bash
www.example.com
example.com
```

<span id="5.4"></span>
### 域名绑定Coding Pages

在Coding网站中进入刚新建的项目，依次单击`代码`、`Pages服务`自定义域名：

![轻快装B低成本–Win10搭建Hexo博客 – 初行博客 - 回归初心，记录生活点滴](assets/coding-domain.png)

重新部署一次代码即可。

## 六、其他辅助工具

<span id="Markdown"></span>
### Markdown书写工具

推荐**Typora，介绍文章：http://www.iplaysoft.com/typora.html**

<span id="Markdown-2"></span>
### Markdown渲染插件

推荐[**Markdown Here**](https://www.zrj96.com/go/?url=http://markdown-here.com/get.html)

<span id="i-4"></span>
### 图床

由于markdown要导入网络图片才能让本地用户和网络用户都能正常访问图片，而且像有道云笔记这种还不能支持插入图片，所以要借助图床和快捷插入图片的小插件来提高写作效率。

<span id="i-5"></span>
### 七牛

注册[**七牛**](https://www.zrj96.com/go/?url=https://portal.qiniu.com/signup?code=3layz9bl08bwy)，在`对象存储`中新建存储空间，要选择公开空间，不然上传图片后无法分享外部链接。

<span id="MPic"></span>
### MPic

下载[**MPic-图床神器**](https://www.zrj96.com/go/?url=http://mpic.lzhaofu.cn/)，设置账号，`空间名`为七牛对象存储空间名称，`AccessKey`和`SecretKey`在七牛`个人面板`下的`密钥管理`中，`域名`为七牛对象存储空间中`内容管理`页签下的`外链默认域名。`

<span id="i-6"></span>
## 七、扩展阅读

推荐一些文章可以帮助你更快的学习使用和解决问题

[Hexo 入门指南（三） – 文章 & 草稿](https://www.zrj96.com/go/?url=http://jingyan.baidu.com/article/63f236280da7770208ab3d27.html)

[搭建Hexo博客中碰到的坑](https://www.zrj96.com/go/?url=http://www.jianshu.com/p/a2fe56d11c4f)

<span id="i-7"></span>
## 八、参考文章

本篇文章的写成参考了以下文章，感谢原作者的奉献！

[Win10搭建hexo-Github-Coding博客](https://www.zrj96.com/go/?url=http://www.madmalls.com/2017/02/11/Win10%E6%90%AD%E5%BB%BAhexo-Github-Coding%E5%8D%9A%E5%AE%A2/)

[搭建Hexo博客中碰到的坑](https://www.zrj96.com/go/?url=http://www.jianshu.com/p/a2fe56d11c4f)

<span id="i-8"></span>
## 九、总结

Hexo这种静态化博客真是轻快，打开速度飞快，比臃肿的WP强了很多。不过因为没有后台之类的东西所以新建文章等操作需要手动操作，不过Hexo的可塑性还是不错的，流行的MD语法，还有文件在本地都可以自由修改，只要懂得一些代码知识就能打造自己的站点。加上配合Github、Coding的使用，完全可以做到0成本拥有自己的博客。如果你对他感兴趣就一起来部署拥有自己的第一个博客吧！