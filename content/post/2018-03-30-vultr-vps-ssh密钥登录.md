---
title: Vultr VPS SSH密钥登录
author: 3mile
type: post
date: 2018-03-30T05:19:40+00:00
url: /archives/964

categories:
  - vps

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/20170528149595407252948.jpg

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
### 需求 {#需求}

当VPS暴露在外网中，就会有人不断暴力破解你的SSH登录。于是就有必要使用SSH密钥来登录。并关闭密码登录。
  
用以下命令可以查看别人暴力破解你SSH密码登录的大概情况！<figure class="highlight plain"> 

<pre class="lang:default decode:true ">grep "Failed password for invalid user" /var/log/secure | awk '{print $13}' | sort | uniq -c | sort -nr | more</pre>

&nbsp;</figure> 

![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/20170528149595407252948.jpg)
  
就我自己的购买的VPS来说。暴力破解次数最多达到2475次！各位也可以去看看自己的。。

### 生成 {#生成}

使用`ssh-keygen`在自己的PC上来生成密钥对。Linux或者macOS都可以直接通过terminal来操作！如果是windows。需要用PuTTYgen软件来生成。<figure class="highlight plain"> 
```bash
">[root@host ~]$ ssh-keygen -t rsa &lt;== 建立密钥对
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): &lt;== 按 Enter
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): &lt;== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again: &lt;== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa. &lt;== 私钥
Your public key has been saved in /root/.ssh/id_rsa.pub. &lt;== 公钥
```
&nbsp;</figure> 

可参考<a href="https://www.vultr.com/docs/how-do-i-generate-ssh-keys/" target="_blank" rel="external noopener">Vultr官方生成教程</a>

### 配置Vultr {#配置Vultr}

创建VPS的时候可以直接制定SSH密钥登录。。如果是已经创建好的VPS。

  1. 将`id_rsa.pub` 放到`/root/.ssh`目录下。并改名为`authorized_keys`
  2. 修改sshd_config配置文件`vi /etc/ssh/sshd_config`
  3. 重启SSH服务，centos7使用命令`systemctl restart sshd`，centos6使用命令`/etc/init.d/sshd restart`

sshd_config配置文件修改相关选项如下：

```conf
RSAAuthentication yes #RSA认证
PubkeyAuthentication yes #开启公钥验证
AuthorizedKeysFile .ssh/authorized_keys #验证文件路径
PasswordAuthentication no #禁止密码认证
PermitEmptyPasswords no #禁止空密码
```


自此。便成功更改为密钥登录！

### 其他 {#其他}

如果你用的是Window系统要登录VPS需要将私钥下载到客户端，然后转换为 PuTTY 能使用的格式

使用 WinSCP、SFTP 等工具将私钥文件 id_rsa 下载到客户端机器上。然后打开 PuTTYGen，单击 Actions 中的 Load 按钮，载入你刚才下载到的私钥文件。如果你刚才设置了密钥锁码，这时则需要输入。

载入成功后，PuTTYGen 会显示密钥相关的信息。在 Key comment 中键入对密钥的说明信息，然后单击 Save private key 按钮即可将私钥文件存放为 PuTTY 能使用的格式。

今后，当你使用 PuTTY 登录时，可以在左侧的 Connection -> SSH -> Auth 中的 Private key file for authentication: 处选择你的私钥文件，然后即可登录了，过程中只需输入密钥锁码即可。