---
title: NETGEAR官方救砖软件，NMRP使用教程
author: 3mile
type: post
date: 2018-03-29T09:13:40+00:00
url: /archives/837
featured_image: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/124917lszeu8eukcz8nshh.png
views:
  - 4
categories:
  - 路由器

# 索引页面上显示的缩略图
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/124917lszeu8eukcz8nshh.png

# 索引页上缩略图位置left,right,bottom
# thumbnailImagePosition: right

#如果没有封面,自动使用默许封面
autoThumbnailImage: false

#标题位置(left center right)
metaAlignment: center

# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/1.jpg

#封面说明内容
coverCaption: "A beautiful cover"

#标题在封面内(in),还是封面外(out)
coverMeta: in

# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---
喜欢折腾NETGEAR设备的坛友们，大家都应试过把路由器刷砖，这里给大家介绍一个软件“Netgear FIRMWARE REWORKING PROCEDURE”，简称NMRP
  
只要路由器还能通电，ROM没有硬件损坏，只要CFE没有被修改，那么就可以通过这个软件把NETGEAR的绝大部分设备修复。

  
要进行修复，必须准备几样工具

<span style="font-size: large;"><span style="color: red;"><strong>1，一台运行XP的电脑（WIN7下经常有问题，WIN10无法安装）<br /> 2，固件<br /> 3，坏路由器（有个前提，原厂的CFE还在，这一点非常重要）<br /> 4，网线一根</strong></span></span>
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
  
准备工作
  
1，下载NMRP软件并解压，链接：<a href="http://pan.baidu.com/s/1i5yibPj" target="_blank" rel="noopener">http://pan.baidu.com/s/1i5yibPj</a> 密码：1bhm
  
2，安装，安装时需注意检查文件没有做过如下修改，如果有，请把选择去掉
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/124917lszeu8eukcz8nshh.png)
  
安装需要选择“Everyone”
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/124917hah5wwzaeg8i6xy5.png)
  
随后，会要求你安装wincap，这个不能省略，一定要安装。
  
2，NMRP界面介绍
  
安装完成之后运行，可以看到这样的界面
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/140707jvapghahr2pg0qzq.png)
  
在一开始，你是没有办法修改任何设置的，您需要登录_Supervisor_ 才可以经行修改设置
  
点击 _Supervisor Login _登录，默认密码为空
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/141034mpaivizygdpddgoa.png)
  
然后就可以看到可以修改的地方了，界面简要说明如下
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/142745nsqvv288s8o8qtmg.png)
  
A，网卡选择，选择和您的路由器通信的网卡
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/141900hojfx73q87x0oq0z.png)
  
B,Region选择，这个和您的路由有关，不过您可以可以在这里改变您的路由器的Region，比如把北美版的改为中国版本，当然也有一些是无法更改的设备， 如果您不希望改变，你可以选择 NO-CHANGE
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/141900yv0xvvrxdssxl22h.png)
  
C,固件路径就是指向您下载好的设备的固件
  
D,语言包这个不需要理会
  
E,日志文件这个也不需要理会
  
F,左下方为运行/停止，如果在运行中将会是下图的状态
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/141901m8lgxvvlh86hvlrm.png)
  
G,如果NMRP在运行，那么将会是以下状态
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/143321m5guh4i9uu72zz72.png)
  
知道以上的东西之后，就可以开始准备救砖了
  
NETGEAR推荐的方式是，把电脑连接至交换机，然后把要修复的设备也连在该交换机下修复
  
步骤
  
1，打开NMRP
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/144256aqdn20iq3y700m8q.png)
  
2，连接至交换机，在电脑端的NMRP上选着好固件文件
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/144257ij1g99mebbz99v0z.png)
  
3，接入要修复的设备，并等待NMRP修复
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/144257or1r0f82f909ri41.png)
  
或者同时接入多台相同的需要修复的设备
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/144257h085lxcit05xjzfa.png)
  
以上办法是NETGEAR推荐的办法，当然，可能我们都没有交换机，下面说一个单机连接故障设备修复的办法
  
1，打开NMRP,选好固件，选好网卡，而且建议点开Debug Windows，这样可以监控NMRP的状态
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/144810s5tw7b7tyir7xz5b.png)
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/145400l1mgmbg1v7gof1uo.png)
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/145400eygsrov1w487o75z.png)
  
2,把电脑连载坏的路由器的LAN口上，无需关心是否能拿到IP地址，只要连上了，就点击“Start”开启
  
如果出现以下问题，请确保电脑和设备的连接
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/150003en0s06m9v6666osc.png)
  
当看到右下角的状态已经是运行中之后，快速的把需要修复的设备断电，在通电设备
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/150054oonpho66l6joz6oz.png)
  
3，只要没问题就可以看到Debug有输出，并且开始修复，这里，我打开了连接了TTL线，以便让大家更好的看到工作状态
  
修复中1
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/150258axawa882sux382wr.png)
  
修复中2
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/150258pq6ttvenay6bdg61.png)
  
修复完成
  
![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/150259nrd4qenl4ngjlm8r.png)
  
可以看到状态是DONE,到了这一步之后，只要停止NMRP，然后把设备重启即可，并且电脑最好把网卡然后再启用，以免无法获取到IP地址
  
至此，NMRP修复完毕
  
最后附上TTL显示的全部过程

```inf

  1. U-Boot 1.1.4 (Aug 12 2014 &#8211; 15:21:46)
  2. 
  3. U-boot dni29 V0.5 for DNI HW ID: 29764821 NOR flash 2MB NAND flash 128MB RAM 128MB
  4. &#8211; Dragonfly 1.0DRAM:
  5. sri
  6. ath\_ddr\_initial_config(278): (ddr2 init)
  7. ath\_sys\_frequency: cpu 775 ddr 650 ahb 258
  8. Tap values = (0xf, 0xf, 0xf, 0xf)
  9. 128 MB
 10. Top of RAM usable for U-Boot at: 88000000
 11. Reserving 265k for U-Boot at: 87fbc000
 12. Reserving 192k for malloc() at: 87f8c000
 13. Reserving 44 Bytes for Board Info at: 87f8bfd4
 14. Reserving 36 Bytes for Global Data at: 87f8bfb0
 15. Reserving 128k for boot params() at: 87f6bfb0
 16. Stack Pointer at: 87f6bf98
 17. Now running in RAM &#8211; U-Boot at: 87fbc000
 18. Flash Manuf Id 0xc2, DeviceId0 0x20, DeviceId1 0x15
 19. flash size 2MB, sector count = 32
 20. Flash:  2 MB
 21. Qualcomm Atheros SPI NAND Driver, Version 0.1 (c) 2014  Qualcomm Atheros Inc.
 22. ath\_parse\_read_id: SPI NAND V.Id: 0xc8 D.Id: 0xf1
 23. ====== NAND Parameters ======
 24. sc = 0x87ff77e4 page = 0x800 block = 0x20000In:    serial
 25. Out:   serial
 26. Err:   serial
 27. Net:   ath\_gmac\_enet_initialize&#8230;
 28. Fetching MAC Address from 0x87fe914c
 29. ath\_gmac\_enet_initialize: reset mask:c02200
 30. athr\_mgmt\_init ::done
 31. Dragonfly  &#8212;-> S17 PHY *
 32. athrs17\_reg\_init: complete
 33. SGMII in forced mode
 34. athr\_gmac\_sgmii_setup SGMII done
 35. : cfg1 0x80000000 cfg2 0x7114
 36. eth0: 6c:b0:ce:14:f0:f4
 37. eth0 up
 38. eth0
 39. Setting 0x181162c0 to 0x48902100
 40. Hit any key to stop autoboot:  0
 41. Trying eth0
 42. dup 1 speed 1000
 43. 
 44. <font color=&#8221;Red&#8221;>Client starts&#8230;[Listening] for ADVERTISE&#8230;Tchecksum bad #NMRP在这里启动，优先于固件启动
 45. 
 46. NMRP CONFIGING
 47. Recv FW-UP option
 48. 
 49. No ST-UP option
 50. 
 51. NMRP WAITING FOR UPLOAD FIRMWARE or STRING TABLES!
 52. Trying eth0
 53. Listening on Port : 69, IP Address: 10.0.0.2&#8230;</font>
 54. 
 55. Rcv:
 56. 
 57. Rcv:
 58.         checksum bad
 59. 
 60. Rcv:
 61. 
 62. Rcv:
 63.         &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..
 64.         &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..
 65.         &#8230;&#8230;&#8230;&#8230;&#8230;中间很长一部分无用信息省略&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;
 66.         &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..
 67.         &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..
 68.         &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..
 69. 
 70. 
 71. Done!
 72. Bytes transferred = 14352517 (db0085 hex)
 73. TFTP upload done
 74. Ignore Magic number checking when upgrade via NMRP,Magic number is 27051956!
 75. HW ID on board: 29764821+2+128+128+3&#215;3+3&#215;3+5508012175
 76. HW ID on image: 29764821+2+128+128
 77. Firmware Image HW ID matched Board HW ID
 78. 
 79. nand erase: off 0, size 20000: OK
 80. nand write 0 : 20000 bytes written, OK
 81. Alive-timer 0
 82.     擦除部分很长。这里也省略了
 83. nand erase: off da0000, size 20000: OK
 84. nand write da0000 : 20000 bytes written, OK
 85. Alive-timer 11
 86. Original board MODEL ID: WNDR4500series           #设备在NG里面归类于WNDR4500下面，虽然设备是WNDR4300V2
 87. New MODEL ID from image: WNDR4500series
 88. Updating MODEL ID
 89. 
 90. First 0x1f last 0x1f sector size 0x10000
 91.   31
 92. write addr: 9f1f0000
 93. done
 94. 
 95. NMRP Send Closing REQ
 96. Trying eth0
 97. 
 98. NMRP CLOSEDRestore to factory default
 99. Erase Flash from 0x9f060000 to 0x9f06ffff in Bank # 1
100. First 0x6 last 0x6 sector size 0x10000
101.    6
102. Erased 1 sectors
103. 
104. press ctrl+C to continue&#8230;..

```