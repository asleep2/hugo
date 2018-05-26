---
title: "Centos7上安装和配置Caddy"
date: 2018-05-26T10:44:27+08:00
lastmod: 2018-05-26T10:44:27+08:00
draft: false
keywords: []
description: ""
tags: ["vultr","centos7","caddy"]
categories: ["虚拟主机"]
slug: ""
url: "/archives/2018/05/26"

author: "3mile"

#主页面缩略图,通常用帖子内图像
cover: "/cover/3.jpg"

thumbnailImage: /cover/3.jpg
# 封面图像相对路径
coverImage: /cover/3.jpg
#封面说明内容
coverCaption: "A beautiful sunrise"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true

---

#### 介绍

Caddy是一个新兴的Web服务器程序，它支持HTTP / 2和自动HTTPS。考虑到易用性和安全性，Caddy可用于通过单个配置文件快速部署支持HTTPS的站点。

#### 先决条件

- 新鲜的Vultr CentOS 7 x64服务器实例。我们将`203.0.113.1`以此为例。
- 一个[sudo用户](https://www.vultr.com/docs/how-to-use-sudo-on-debian-centos-and-freebsd)。
- [使用EPEL YUM回购](https://www.vultr.com/docs/how-to-update-centos-7-ubuntu-16-04-and-debian-8)服务器实例已[更新到最新的稳定状态](https://www.vultr.com/docs/how-to-update-centos-7-ubuntu-16-04-and-debian-8)。
- 一个域`example.com`已被配置为指向`203.0.113.1`服务器实例。在另一个[Vultr教程中](https://www.vultr.com/docs/introduction-to-vultr-dns)查看细节。

#### 第一步：安装Caddy的最新稳定版本

在Linux，Mac或BSD操作系统上，使用以下命令安装Caddy最新稳定的系统特定版本：

```
curl https://getcaddy.com | bash
```

出现提示时，输入您的sudo密码以完成安装。

Caddy二进制文件将被安装到该`/usr/local/bin`目录。使用以下命令确认：

```
which caddy
```

输出应该是：

```
/usr/local/bin/caddy
```

为了安全起见，**切勿**以root身份运行Caddy二进制文件。为了让Caddy能够以非root用户身份绑定到特权端口（例如80,443），您需要`setcap`按如下所示运行命令：

```
sudo setcap 'cap_net_bind_service=+ep' /usr/local/bin/caddy
```

#### 第2步：配置Caddy

创建一个专门的系统用户：`caddy` 和一组同名的Caddy：

```
sudo useradd -r -d /var/www -M -s /sbin/nologin caddy
```

**注意**：*此处创建**的用户caddy只能用于管理Caddy服务，不能用于登录。*

`/var/www`为Caddy Web服务器创建主目录，并`/var/www/example.com`为您的网站创建主目录：

```
sudo mkdir -p /var/www/example.com
sudo chown -R caddy:caddy /var/www
```

创建一个目录来存储SSL证书：

```
sudo mkdir /etc/ssl/caddy
sudo chown -R caddy:root /etc/ssl/caddy
sudo chmod 0770 /etc/ssl/caddy
```

创建专用目录来存储Caddy配置文件`Caddyfile`：

```
sudo mkdir /etc/caddy
sudo chown -R root:caddy /etc/caddy
```

创建名为的Caddy配置文件`Caddyfile`：

```
sudo touch /etc/caddy/Caddyfile
sudo chown caddy:caddy /etc/caddy/Caddyfile
sudo chmod 444 /etc/caddy/Caddyfile
cat <<EOF | sudo tee -a /etc/caddy/Caddyfile
example.com {
    root /var/www/example.com
    gzip
    tls admin@example.com
}
EOF
```

**注意**：*上面创建**的Caddyfile文件只是运行静态网站的基本配置。您可以在这里了解更多关于如何编写Caddyfile的信息。*

为了方便Caddy的操作，您可以`systemd`为Caddy 设置一个单元文件，然后用它`systemd`来管理Caddy。

使用`vi`编辑器创建Caddy `systemd`单元文件：

```
sudo vi /etc/systemd/system/caddy.service
```

填充文件：

```
[Unit]
Description=Caddy HTTP/2 web server
Documentation=https://caddyserver.com/docs
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
Restart=on-abnormal

; User and group the process will run as.
User=caddy
Group=caddy

; Letsencrypt-issued certificates will be written to this directory.
Environment=CADDYPATH=/etc/ssl/caddy

; Always set "-root" to something safe in case it gets forgotten in the Caddyfile.
ExecStart=/usr/local/bin/caddy -log stdout -agree=true -conf=/etc/caddy/Caddyfile -root=/var/tmp
ExecReload=/bin/kill -USR1 $MAINPID

; Use graceful shutdown with a reasonable timeout
KillMode=mixed
KillSignal=SIGQUIT
TimeoutStopSec=5s

; Limit the number of file descriptors; see `man systemd.exec` for more limit settings.
LimitNOFILE=1048576
; Unmodified caddy is not expected to use more than that.
LimitNPROC=512

; Use private /tmp and /var/tmp, which are discarded after caddy stops.
PrivateTmp=true
; Use a minimal /dev
PrivateDevices=true
; Hide /home, /root, and /run/user. Nobody will steal your SSH-keys.
ProtectHome=true
; Make /usr, /boot, /etc and possibly some more folders read-only.
ProtectSystem=full
; … except /etc/ssl/caddy, because we want Letsencrypt-certificates there.
;   This merely retains r/w access rights, it does not add any new. Must still be writable on the host!
ReadWriteDirectories=/etc/ssl/caddy

; The following additional security directives only work with systemd v229 or later.
; They further retrict privileges that can be gained by caddy. Uncomment if you like.
; Note that you may have to add capabilities required by any plugins in use.
;CapabilityBoundingSet=CAP_NET_BIND_SERVICE
;AmbientCapabilities=CAP_NET_BIND_SERVICE
;NoNewPrivileges=true

[Install]
WantedBy=multi-user.target
```

保存并退出：

```
:wq!
```

启动Caddy服务并使其在系统引导时自动启动：

```
sudo systemctl daemon-reload
sudo systemctl start caddy.service
sudo systemctl enable caddy.service
```

#### 第3步：修改防火墙规则

为了允许访问者访问您的Caddy网站，您需要打开端口80和443：

```
sudo firewall-cmd --permanent --zone=public --add-service=http 
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
```

#### 第4步：为您的网站创建一个测试页面

使用以下命令`index.html`在您的Caddy网站主目录中创建一个名为的文件：

```
echo '<h1>Hello World!</h1>' | sudo tee /var/www/example.com/index.html
```

重新启动Caddy服务以加载新内容：

```
sudo systemctl restart caddy.service
```

最后，将您的网页浏览器指向`http://example.com`或`https://example.com`。您应该看到`Hello World!`预期的消息。