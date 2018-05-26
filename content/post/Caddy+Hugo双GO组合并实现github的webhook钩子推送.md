---
title: "Caddy+Hugo双GO组合并实现github的webhook钩子推送"
date: 2018-05-26T11:51:03+08:00
lastmod: 2018-05-26T11:51:03+08:00
draft: false
keywords: []
description: ""
tags: ["caddy","webhook","hugo","github"]
categories: [""]
slug: ""
url: "/archives/2018/0526"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/QQ截图20180526133351.jpg"

thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/QQ截图20180526133351.jpg
# 封面图像相对路径
coverImage: /cover/8.jpg
#封面说明内容
coverCaption: "A beautiful sunrise"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true
---



<!--toc-->

## 原因

###	一. 首先,为什么要用这么复杂的标题?  

为什么标题会这么复杂呢？原因很简单。我自己被搞昏了，为了体现我的眩晕程度，所以用了这个复杂的名字。

另外，还有一个最重要的原因：本博内容本来就容易让人昏，并且本博也不是给别人看的，只是为了怕自己忘记而写的教程笔记而已。

## 目的

这么容易让人发昏的目的是什么呢?

目的很简单,一个字"懒"

在本地计算机上写博客,然后推送到GITHUB上，让Github Webhook push 给VPS Caddy.server,然后Caddy.git pull Github内容修改,最后Caddy.hugo自动生成静态页面.

这样说有点绕,还是上个思维导图吧

![思维导图](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/01.png)

### 二. 为什么要用Hugo

原因是建立了一个VPS小鸡，但是内存只有512M. 另外博主也使用过几个不同的博客系统,最终还是决定选用hugo作为博客系统.

1. 用过wordpress系统,放弃.原因很简单,博主的VPS小鸡经常更换（至少是经常更换IP,经常被墙啊）用这种动态博客，耗费资源不说，起码要LAMP或者LNMP组合。换主机就要涉及到迁移，又是数据库,又是文章，又是IP，太麻烦了。还是静态的方便。
2. typecho ，放弃，虽然轻量，但放弃原因同上
3. hexo,优点是部署方便,教程资料多,但编译速度太让人绝望了,放弃
4. jekyll,ruby编写,不想装ruby,就这么简单

### 三. 为什么用Caddy

原因很简单啊.Caddy简单,开源.GO编写，只需要一个文件搞定，以后迁移方便。这个优点就够了。

并且插件也很多，比如.git, .hugo, .minify...这些都是本博中会用到的插件.



## 教程

{{< alert info >}} 本教程以Vultr作为VPS主机，本地系统为windows10 x64(安装Git bash,hugo),Github地址为github.com/mile3033 {{< /alert >}} 

### 循序渐进法

#### 1. 安装Caddy

Caddy的安装详见本人博客 [[Centos7上安装和配置Caddy](https://blog.3mile.top/archives/2018/05/26/)]

里面有些坑,我后面去填.

#### 2.安装Hugo

Hugo可以安装在几乎所有的主流平台上。对于CentOS，您只需要将最新的程序文件下载到`.tar.gz`档案中，并将其解压缩到一个方便的位置。在撰写本文时，最新版本是0.15。

```
sudo yum update -y
sudo yum install git -y
cd ~
wget https://github.com/spf13/hugo/releases/download/v0.15/hugo_0.15_linux_amd64.tar.gz
tar -zxvf hugo_0.15_linux_amd64.tar.gz
sudo mv hugo_0.15_linux_amd64/hugo_0.15_linux_amd64 /usr/local/bin/hugo
```

使用以下命令测试您的安装：

```
 hugo version
```

到这里就完成hugo的安装了,至于很多教程里关于如何建立新站点,如何设置主题...这里不作教程,原因是我们的目的是方便以后网站的整体迁移.So,关于Hugo的安装就到这里足够了

#### 建立本地电脑生产系统

Windows上面建立Hugo系统很简单,一个二进制文件搞定.这就是Go的优越性

##### 假设[ ](https://gohugo.io/getting-started/installing/#assumptions-1)

1. 您将`C:\Hugo\Sites`用作新项目的起点。
2. 您将使用`C:\Hugo\bin`存储可执行文件。

##### 设置您的目录[ ](https://gohugo.io/getting-started/installing/#set-up-your-directories)

您需要一个地方来存储Hugo可执行文件，您的[内容](https://gohugo.io/content-management/)以及生成的Hugo网站：

1. 打开Windows资源管理器
2. 创建一个新文件夹：`C:\Hugo`，假设你想在你的C盘上使用Hugo，尽管这可以放在任何地方
3. 在Hugo文件夹中创建一个子文件夹： `C:\Hugo\bin`
4. 在Hugo中创建另一个子文件夹： `C:\Hugo\Sites`

##### 技术用户[ ](https://gohugo.io/getting-started/installing/#technical-users)

1. 从[Hugo发布](https://github.com/gohugoio/hugo/releases)下载最新的压缩Hugo可执行文件。
2. 将所有内容提取到您的`..\Hugo\bin`文件夹。
3. 该`hugo`可执行文件将被命名为`hugo_hugo-version_platform_arch.exe`。重命名可执行文件以便`hugo.exe`于使用。
4. 在PowerShell或您的首选CLI中，`hugo.exe`通过导航到`C:\Hugo\bin`（或您的hugo.exe文件的位置）并使用该命令将可执行文件添加到PATH `set PATH=%PATH%;C:\Hugo\bin`。如果该`hugo`命令在重新启动后不起作用，则可能必须以管理员身份运行命令提示符。

##### 技术含量较低的用户[ ](https://gohugo.io/getting-started/installing/#less-technical-users)

1. 转到[Hugo发布](https://github.com/gohugoio/hugo/releases)页面。
2. 最新发布的版本在上面公布。滚动到发布公告的底部查看下载。他们都是ZIP文件。
3. 找到靠近底部的Windows文件（它们按字母顺序排列，因此Windows是最后一个） - 根据您是32位还是64位Windows，下载32位或64位文件。（如果你不知道，[请看这里](https://esupport.trendmicro.com/en-us/home/pages/technical-support/1038680.aspx)。）
4. 将ZIP文件移动到您的`C:\Hugo\bin`文件夹中。
5. 双击ZIP文件并提取其内容。一定要将内容解压缩到同一个`C:\Hugo\bin`文件夹中 - Windows将默认执行此操作，除非您将其解压到其他位置。
6. 你现在应该有三个新文件：hugo可执行文件（eg `hugo_0.18_windows_amd64.exe`）`license.md`，和`readme.md`。（您现在可以删除ZIP下载。）重命名该hugo可执行文件（`hugo_hugo-version_platform_arch.exe`）以便`hugo.exe`于使用。

现在您需要将Hugo添加到您的Windows PATH设置中：

##### 对于Windows 10用户：[ ](https://gohugo.io/getting-started/installing/#for-windows-10-users)

- 右键单击**开始**按钮。
- 点击**系统**。
- 点击左边的**高级系统设置**。
- 点击底部的**环境变量...**按钮。
- 在用户变量部分，找到以PATH开头的行（PATH将全部大写）。
- 双击**PATH**。
- 点击**新建...**按钮。
- 键入`hugo.exe`提取的文件夹，这是`C:\Hugo\bin`如果您按照上述说明操作的。*PATH条目应该是Hugo所在的文件夹，而不是二进制文件。*按Enter完成键入后按。
- 在每个窗口中单击确定以退出。

Windows 10中的路径编辑器已添加到[2015年11月的更新中](https://blogs.windows.com/windowsexperience/2015/11/12/first-major-update-for-windows-10-available-today/)。您需要安装该更新或更高版本的更新才能运行上述步骤。您可以通过单击来查看Windows 10的构建 开始按钮→设置→系统→关于。请参阅[这里](https://www.howtogeek.com/236195/how-to-find-out-which-build-and-version-of-windows-10-you-have/)了解更多。）

#### 创建Github项目

1、在任意的页面右上角点击 **+**，然后点击新建仓库 **New repository**。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/QQ截图20180526133622.jpg)

2、为你的仓库创建一个简短便于记忆的名字。例如 “hello-world”。

![创建名为hugo的项目](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/1-1527313275847.jpg)

3、为你的仓库添加一个描述（非必须的）。例如 “My first repository on GitHub”。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/3.jpg)

4、选择你的仓库类型为公有或者私有：

- **Public**：公有仓库对于一个刚入门的新手来说是一个不错的选择。这些仓库在 GitHub 上对于每个人是可见，你可以从协作型社区中受益。
- **Private**：私有仓库需要更多地步骤。它们只对于你来说是可用的，这个仓库的所有者属于你和你所指定要分享的合作者。私有仓库仅仅对付费账户可用。更多的信息请参照 "[What plan should I choose?](https://help.github.com/articles/what-plan-should-i-choose)"。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/2.jpg)

5、选择**Initialize this repository with a README**。

![Initialize this repository with a README](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/create-new-repository-5.png)

6、点击**Create repository**。

![Create repository](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/create-new-repository-5.png)

恭喜！你已经成功地创建你的第一个仓库，并且通过 README 文件初始化了它。

#### push到githug

现在我们已经建立了http://github.com/mile3033/hugo项目,所以我们要把**本地计算机**的项目推送到Github上面了.

因为现在是做测试,所以只需要在本地的G:\hugo\hugo下面建立一个index.html的文件就可以了

```bash
git init
echo ^<h1^> Test Caddy Working^</h1^>
git add .
git commit -m "first Test"
git remote add origin https://github.com/mile3033/hugo
git push -u origin master
```

**本地计算机**推送到github的hugo项目后,回到**Vultr 虚拟主机**

在/var/www 下面建立hugo目录

```bash
mkdir /var/www/hugo
cd /var/www
```

为什么要进入/var/www目录下面呢,是因为我们现在暂时不用Linux的服务运行Caddy.测试嘛,现在暂时用的Root账号,方便查找出错的原因

生成Caddyfile文件

```bash
nano /var/www/Caddyfile
```

文件内容如下:

```yaml
http://blog.3mile.top
git github.com/mile3033/hugo .
root /var/www/hugo
```

然后运行Caddy进行测试,

```
Caddy
```

如果没有报错的话,可以打开浏览器 

>http://blog.3mile.top

可以看到刚才我们做的index.html的内容了

#### 测试Webhook

继续编辑Caddyfile文件

```bash
http://blog.3mile.top
git github.com/mile3033/hugo . {
    hook /webhooks some-keys
}
root /var/www/hugo
```

然后打开Github页面,进入项目->设置->webhook->Add Webhook

添加webhook,PayloadURL填写你域名/webhook比如我的

```
http://blog.3mile.top/webhooks
```

content-type选json
secret填写和Caddyfile中的口令保持一致(some-keys)
其他保持默认即可。

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/webhook.jpg)

当你看到这个画面时,成功了

然后,在**本地计算机**的index.html上随便修改一下,然后推送到Github

```
git add .
git commit -m "modify index.html"
git push origin master
```

推送完成之后,观察putty里面Caddy的提示,有变化了吧.那就成功了

打开

>http://blog.3mile.top

看到页面变化了吧.哈哈

各位可自备梯子查看 YouTube 上的视频教程 

{{< youtube dmat1MUT0fc>}} 

然后重点来了,重点来了

现在我们要以服务的方式后台运行,并且建立一个名为**caddy用户组和用户**,增加网站和VPS的安全性

1. 现在先结束caddy进程

2. 重新温习一遍 [Centos7上安装和配置Caddy](https://blog.3mile.top/archives/2018/05/26/)

3. 首先停用caddy.server服务,不然不知道会不会出错

4. ```
   sudo systemctl stop caddy.service
   sudo systemctl disable caddy.service
   ```

5. 然后修改/etc/caddy/Caddyfile文件

6. ```yaml
  blog.3mile.top {
  ```
#tls mile3@gmail.com
git github.com/mile3033/hugo . {
	repo github.com/mile3033/hugo
	path /var/www/hugo-blog
	hook /webhooks some-keys
	hook_type github
	then hugo --destination=/var/www/blog.3mile.top
	interval 600
	}
   root /var/www/blog.3mile.top
}
```

   

7. 因为是使用Caddy账号,没有权限.所以要重新给他权限,否则Caddy会报错

8. ```
   sudo chown -R caddy:caddy /var/www
   sudo chown -R caddy:root /etc/ssl/caddy
   sudo chmod 0770 /etc/ssl/caddy
   sudo chown -R root:caddy /etc/caddy
```

9. 这时先不打开Caddy服务,或都是先不要运行Caddy

10. 在本地计算机设置Hugo页面,主题,反正一句话,你的Hugo要正常工作.我这里只是为了方便网站整体迁移,所以Hugo是完整的,所以只需要把相关文件复制过来就可以了

11. 如果Hugo是正常的,那么就Push到Github吧

12. 先删除刚才生成的测试文件index.html

13. ```
    git add .
    git commit -m "modify index.html"
    git push origin master
    ```

    

14. 然后打开Caddy服务

15. ```
    sudo systemctl daemon-reload
    sudo systemctl start caddy.service
    sudo systemctl enable caddy.service
    ```

16. 运行`sudo systemctl status caddy.service -l`看Caddy服务是否正常运行了

17. ![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/assets/QQ截图20180526133351.jpg)



