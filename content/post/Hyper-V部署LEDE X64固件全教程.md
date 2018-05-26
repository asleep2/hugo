---
title: "Hyper-V部署LEDE X64固件全教程"
date: 2018-04-03T10:13:14+08:00
draft: false
url: /archives/105
categories:
  - 路由器
tags:
  - 软路由
# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163005cu0jhjjydrhge70k.png

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


前言：  本着分享个人心得造福诸位的精神，也想让有的坛友在摸索的路上少走一些弯路，我在这里写一下关于Hyper-V虚拟机部署LEDE的教程。

第一步：开启Hyper-V虚拟机.
   win10以后的系统都可以通过添加系统功能来开启微软自带的Hyper-V虚拟机.
  首先WIN+X，或者右键开始菜单，选择控制面板-程序-启用或关闭Windows功能 ![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/144313wns4nm4rp7mk4pzp.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image//144313cjmk9tq6fm3qyvk1.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/144313bhycymt2hhmmyyh0.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/144314krgmrna3p6mmn6t6.png) 




勾选Hyper-V  然后下一步，根据提示重启。


重启后，在开始菜单-Windows管理工具里找到Hyper-V管理器，把快捷方式拖到磁贴块这里，方便以后使用。



第二步：制作Hyper-V使用的的LEDE镜像


源文件的下载不用我多说了吧，可以直接在论坛-固件下载里下载。
然后，这个时候我们就需要用一个叫StarWind V2V Image Converter的程序把img格式的固件转换为Hyper需要的格式，软件和转好的镜像下载链接: <http://pan.baidu.com/s/1qXJ1vNA> 密码: r1xz

想自己转的朋友请继续看，如果懒得话直接下载我上面链接里面提供的转好的镜像就可以了，跳过这一步去第三步。


把下载好的后缀名为img.gz的固件解压得到后缀为img的固件，然后安装SW V2V这个软件打开，选择解压好的LEDE.img镜像，下一步，选择转换为VHDX的格式，然后一直下一步就可以了。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/151324qgs0a99ulrizmd09.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/151324g01h5u04mccc5l8h.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/151325cbaa2b2oeamauam6.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/151325kp3pcn73k73r69r5.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/151325kgqj7rg6xrhi9euo.png) 


至此，转换完成。

第三步：Hyper-V网络的配置


我这里演示用的机器只有一个网口，我插了一个无线网卡代替另一个网口做WAN口。
诸位在部署之前先打开网络适配器，看一下哪个网络适配器对应的哪个网卡，因为有的主板上的网卡在装了WIN之后，网口顺序会错乱，建议大家可以通过插网线的方式来判断清楚对应关系，以免在下面的部署里闹出别的麻烦。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/152404ed2qi6qulvcqctlq.png)


打开Hyper-V管理器，选择虚拟交换机管理器-新建虚拟网络交换机-外部-创建虚拟交换机


接下来这一步很重要，首先将名字改为WAN，然后选择网卡，选择你要做WAN口的网卡，然后应用，弹出警告对话框直接点确定。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/154444lnnffnmmn7lj3ihv.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/154445yiov8a2evkdkxksc.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/154448ta9opebhlo1obe7h.png) 


接下来，重复上面的步骤，新建LAN口，点击确定。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/154706vyrdd62fmd4266pg.png) 



第四步：部署LEDE

为了管理方便，我们新建一个叫LEDE的文件夹，随便你放在那里，只要你方便。
然后将LEDE的转好的VHDX文件放入这个LEDE文件夹内。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/154959nnv9v143zlrvu36m.png)

接着进入Hyper-V管理器，选择新建虚拟机，然后下一步，虚拟机名字随你爱好起。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155312c5zwamm7barf6v67.png)
然后勾选将虚拟机存储在其他位置，然后选择你刚才新建的LEDE文件夹。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155312q1163bg16mm53a5k.png)
切记选择第一代。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155312u2cff39hy4u8fhf9.png)
内存分多大依你个人情况而定，然后取消勾选动态内存。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155502hmr2co3hke218kdo.png)
网络连接不用管 ，直接下一步，待会再配置。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155548okkzrr3rj3jzsiju.png)
硬盘这里选择使用现有虚拟硬盘，然后选择LEDE文件夹里的VHDX文件。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155720a4p20seei0730er9.png)
点击完成。


然后选择设置
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/155832e79iz0p9wz9u9uu0.png)
选择BIOS，然后将IDE上移。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/160009d6z44xcpp1zzlg66.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/160013j2n97ns81bl9928z.png) 
选择硬盘驱动器-编辑-下一步-扩展-下一步-输入硬盘大小-完成。这里以你个人情况而言，我给了4G。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/160834fqhmnk7o6c7ete9j.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/160835xkp9rk992924akp4.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/160835b7gaj2hgxf76k5dl.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/161311iralb6q8yqvytevv.png) 

接下来选择网络适配器-LAN口，然后应用。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/161809ollxxfl2exv2l9es.png) 

然后添加硬件-网络适配器-添加-选择WAN口-应用。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/162618d6un7ztzqztpnuw6.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/162723hr7m527ezh5uxn2r.png) 

点击应用。
然后是很重要的一点：需要多拨以及LEDE里面LAN口包含多个网卡的，请记得开MAC欺骗模式！
看图
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163005cu0jhjjydrhge70k.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163006am3ciridcmqqd4q4.png) 


然后，请把lan口对应的网口接上随便什么玩意，交换机，电视什么都可以，只要让这个网口处于工作状态，不要显示：网络电缆被拔出就可以了。


选择-连接-启动
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163655mwfityofk5i5g56i.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163655nnwngqbrqe5zmr5b.png) 
出现以下画面说明启动成功了。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/163754o9nteddetf9ctzte.png)
接下来右键-打开网络与共享中心-更改适配器设置
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164036dkbwtnonocvntnot.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164036g0ckpjccu6kmbvtc.png)
选择vEthernet LAN口-右键-算了懒得打了 跟着我图  然后 确定 应用。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164259cqwkwh4a27ca77z1.png) ![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164259ho8x02slhozh4xh0.png) 


然后，打开你的浏览器，登陆192.168.1.1   见证奇迹的时刻到了。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164854szd6ro86oooxz82c.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/164854ap0x0nec08ncp1du.png)



接下来，我们添加wan口。首先进入LAN口-物理设置，取消除了eth0之外其他所有接口的勾选，只留eth0，然后点击应用。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/165816bpn5x96xp5sd605e.png)
![img](http:https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image//image.koolshare.cn/attachment/forum/201702/25/165816s2tllnvyx8lmmkw8.png) 


然后选择添加wan口，选择空闲的eth1，具体是pppoe拨号还是DHCP，视你个人情况而言
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/165938lkquq9uuplgqupg6.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/165939qh51d33v1ph25zrd.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/165939n0mtmqkib3of0tot.png)

然后开启外面vEthernet LAN 自动获取IP地址 ，就可以上网了，大功告成。
![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/170206vum7swsiq7m47aiu.png)![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/170206vzgu2ih3tzaxavgh.png)
[QQ截图20170225170003.png](http://koolshare.cn/forum.php?mod=attachment&aid=MTM0MDgzfGYwMzZlNzQ2fDE1MjI3MjE2NDR8MTAxOTAyfDg0NzM1&nothumb=yes) *(101.2 KB, 下载次数: 2)*

另外，开机自动启动虚拟机![img](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/image/170738ld4244zhfdp8dmve.png) 
