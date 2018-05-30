---
title: Linux开放HTTP服务并下载文件到本地以测试VPS回程速度
author: 3mile
type: post
date: 2018-04-02T05:19:40+00:00
url: /archives/103
categories:
  - vps

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/3.jpg

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



<font color=red>内容</font>

在 [Linux中使用 路由追踪 测试VPS回程路由（回程路由比去程更影响SS速度）](https://doub.io/linux-jc4/) 文章中，我说过如果你的服务器是做代理的，那么最影响速度的就是回程路由质量，那个文章中教你如何通过路由追踪测试VPS回程路由质量，但是毕竟路由质量不代表最终速度，而现在这篇文章就是让你测试，你在下载VPS上面的文件到本地的速度(回程速度)。

------

大部分情况下，你挂代理比如Shadowsocks(R)，大部分情况下你都是在下载数据(VPS传给你)，无论是看视频还是看网页。所以这个速度才是最终影响你体验的指数。

而如何测试呢？很简单，只要在VPS上面开放HTTP服务，然后在VPS开放的文件夹中下载一个 100MB的测试文件，然后我们从浏览器打开并下载这个 100MB的测试文件，在下载期间看文件的下载速度。

当然这篇文章不仅限于，测试VPS回程速度，有时候你需要开放/共享 VPS上的一些文件，你也可以看这篇文章。

------

搭建HTTP服务有很多方法，但是我们只是测试一下VPS上面的文件下载到本地的速度，所以要排除那些步骤复杂，设置颇多的HTTP工具。

所以这里我选择了：**SimpleHTTPServer 和 Caddy** （注意：只需要选择其中一个就行了！

## SimpleHTTPServer

SimpleHTTPServer是Pyhton自带的一个简易HTTP Server，所以要使用这个工具，VPS中要安装的有 Python，优点是大部分Linux系统中都会安装 Python。

> **缺点：**经过逗比们反馈，SimpleHTTPServer似乎存在 **下载速度不稳定/很慢** 的问题，而且不支持多线程下载，如果觉得不好用，请看Caddy。

### 检查Python是否安装：

```
python -V# 正常情况下应该返回 Python 2.7.x # 如果返回命令找不到 python: command not found ，那么说明没有安装Python。
```

如果没有安装，那么请**安装 Python：**

```
# CentOS 系统：yum update && yum install python python2.7 -y # Debian/Ubuntu 系统：apt-get update && apt-get install python python2.7 -y# 安装后使用 python -V 查看是否安装成功，如果不成功就去谷歌吧！
```

------

确认Python安装正常后，就可以看下面这个教程继续操作了，很早就写过，当时还写了一个一键脚本。

- [『原创』SimpleHTTPServer 快速搭建HTTP Web服务 + 一键脚本](https://doub.io/wlzy-8/)

在使用 SimpleHTTPServer 开放HTTP服务后，**进入你开放HTTP服务的文件夹内**，然后生成一个 100MB的测试文件。

```
dd if=/dev/zero of=Test bs=1M count=100# 100MB
# 文件太小，测试不过瘾？那只需要把最后的数字改成你想要的，比如 500=500MB
dd if=/dev/zero of=Test bs=1M count=500
# Test就是生成的测试文件的文件名，1M是每次写入1M大小，500是写入500次，也就是名为Test的500MB大小文件。
```

最后，我们打开` http://VPS_IP:端口 `即可看到虚拟主机文件夹内的文件了，开始下载名为 Test的文件测速吧！

### 卸载 SimpleHTTPServer：

SimpleHTTPServer是集成与 Python的，所以无法卸载，只需要把脚本（如果用的话）和下载测速的文件删除即可。

```
rm -rf Test
```

## Caddy

Caddy是一个Go语言编写的很简单的 HTTP Server，配置文件异常简单，相比于 SimpleHTTPServer 的不稳定和不支持多线程，Caddy更适合长期使用，当然不代表不适合短期使用。

### 部署方法：

```
wget -N --no-check-certificate https://softs.fun/Bash/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh install http.filemanager 
# 如果上面这个脚本无法下载，尝试使用备用下载：wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh install http.filemanager
```

安装Caddy成功后，继续新建一个虚拟主机文件夹，

```
mkdir /usr/local/caddy/www && mkdir /usr/local/caddy/www/speeder
```

### 写入配置文件

写入配置到 Caddy 配置文件，注意下面这六行要一起复制粘贴，不是一行一行复制！

```
# 以下全部内容是一个整体，是一个命令，全部复制粘贴到SSH软件中并一起执行！
echo ":80 {
root /usr/local/caddy/www/speeder
timeouts none
gzip
browse
}" > /usr/local/caddy/Caddyfile
# 如果要绑定域名，只要把上面第一行的 :80 { 改成域名比如[ http://tooyo.ml { ]即可(不需要加端口号了)#
```

上面的代码执行完后，启动 Caddy即可。

```
/etc/init.d/caddy start
```

### 下载测速文件

然后我们进入 虚拟主机文件夹，并下载 测速文件：

```
cd /usr/local/caddy/www/speederdd 
if=/dev/zero of=Test bs=1M count=100
# 100MB文件太小，测试不过瘾？那只需要把最后的数字改成你想要的，比如 500=500MB
dd if=/dev/zero of=Test bs=1M count=500
# Test就是生成的测试文件的文件名，1M是每次写入1M大小，500是写入500次，也就是名为Test的500MB大小文件。
```

最后，我们打开` http://VPS_IP `即可看到虚拟主机文件夹内的文件了，开始下载名为 Test的文件测速吧！

### Caddy 使用方法

**启动：**/etc/init.d/caddy start

**停止：**/etc/init.d/caddy stop

**重启：**/etc/init.d/caddy restart

**查看状态：**/etc/init.d/caddy status

### 卸载 Caddy

进入你下载caddy安装脚本的文件夹，并用下面代码运行脚本即可完全卸载。

```
bash caddy_install.sh uninstall
```

### 启动显示成功，但是实际未运行

因为 服务脚本判断的问题，只判断了nohub是否运行 Caddy成功，但没有判断 Caddy 是否保持正常运行。

你可以理解为，nohub成功启动了 Caddy，但是 Caddy因为配置文件错误等原因，启动后又退出了。

所以这种情况下，你应该去查看启动日志：

```
tail -f /tmp/caddy.log
```