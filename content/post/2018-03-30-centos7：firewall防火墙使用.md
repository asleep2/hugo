---
title: CentOS7：firewall防火墙使用
author: 3mile
type: post
date: 2018-03-30T05:15:21+00:00
url: /archives/102
featured_image: ![](https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310493233-687x500.png)
views:
  - 6
categories:
  - vps
tags:
  - Linux
  - centos

---
### 一、Firewalld防火墙

红帽RHEL7系统已经用firewalld服务替代了iptables服务，新的防火墙管理命令**firewall-cmd**与图形化工具**firewall-config**。特点是拥有运行时配置与永久配置选项且能够支持动态更新以及”zone”的区域功能概念，使用图形化工具firewall-config或文本管理工具firewall-cmd，下面实验中会讲到~

另外，你可以可以安装iptables-services服务，这样就可以按照之前的操作来操作iptables了。可以使用service save iptables来保存规则，也可以使用service iptables start|stop来开启和关闭iptables了。

`$ yum install iptables-services`

**1）区域概念与作用**

防火墙的网络区域定义了网络连接的可信等级，我们可以根据不同场景来调用不同的firewalld区域，区域规则有：

<table width="712">
  <tr>
    <td width="95">
      区域
    </td>
    
    <td width="617">
      默认规则策略
    </td>
  </tr>
  
  <tr>
    <td width="95">
      trusted
    </td>
    
    <td width="617">
      允许所有的数据包。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      home
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关或是ssh,mdns,ipp-client,samba-client与dhcpv6-client服务则允许。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      internal
    </td>
    
    <td width="617">
      等同于home区域
    </td>
  </tr>
  
  <tr>
    <td width="95">
      work
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关或是ssh,ipp-client与dhcpv6-client服务则允许。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      public
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关或是ssh,dhcpv6-client服务则允许。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      external
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关或是ssh服务则允许。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      dmz
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关或是ssh服务则允许。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      block
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关。
    </td>
  </tr>
  
  <tr>
    <td width="95">
      drop
    </td>
    
    <td width="617">
      拒绝流入的数据包，除非与输出流量数据包相关。
    </td>
  </tr>
</table>

简单来讲就是为用户预先准备了几套规则集合，我们可以根据场景的不同选择合适的规矩集合，而默认区域是**public**。

**2）字符管理工具**

如果想要更高效的配置妥当防火墙，那么就一定要学习字符管理工具firewall-cmd命令,命令参数有：

<table width="712">
  <tr>
    <td>
      参数
    </td>
    
    <td>
      作用
    </td>
  </tr>
  
  <tr>
    <td>
      –get-default-zone
    </td>
    
    <td>
      查询默认的区域名称。
    </td>
  </tr>
  
  <tr>
    <td>
      –set-default-zone=<区域名称>
    </td>
    
    <td>
      设置默认的区域，永久生效。
    </td>
  </tr>
  
  <tr>
    <td>
      –get-zones
    </td>
    
    <td>
      显示可用的区域。
    </td>
  </tr>
  
  <tr>
    <td>
      –get-services
    </td>
    
    <td>
      显示预先定义的服务。
    </td>
  </tr>
  
  <tr>
    <td>
      –get-active-zones
    </td>
    
    <td>
      显示当前正在使用的区域与网卡名称。
    </td>
  </tr>
  
  <tr>
    <td>
      –add-source=
    </td>
    
    <td>
      将来源于此IP或子网的流量导向指定的区域。
    </td>
  </tr>
  
  <tr>
    <td>
      –remove-source=
    </td>
    
    <td>
      不再将此IP或子网的流量导向某个指定区域。
    </td>
  </tr>
  
  <tr>
    <td>
      –add-interface=<网卡名称>
    </td>
    
    <td>
      将来自于该网卡的所有流量都导向某个指定区域。
    </td>
  </tr>
  
  <tr>
    <td>
      –change-interface=<网卡名称>
    </td>
    
    <td>
      将某个网卡与区域做关联。
    </td>
  </tr>
  
  <tr>
    <td>
      –list-all
    </td>
    
    <td>
      显示当前区域的网卡配置参数，资源，端口以及服务等信息。
    </td>
  </tr>
  
  <tr>
    <td>
      –list-all-zones
    </td>
    
    <td>
      显示所有区域的网卡配置参数，资源，端口以及服务等信息。
    </td>
  </tr>
  
  <tr>
    <td>
      –add-service=<服务名>
    </td>
    
    <td>
      设置默认区域允许该服务的流量。
    </td>
  </tr>
  
  <tr>
    <td>
      –add-port=<端口号/协议>
    </td>
    
    <td>
      允许默认区域允许该端口的流量。
    </td>
  </tr>
  
  <tr>
    <td>
      –remove-service=<服务名>
    </td>
    
    <td>
      设置默认区域不再允许该服务的流量。
    </td>
  </tr>
  
  <tr>
    <td>
      –remove-port=<端口号/协议>
    </td>
    
    <td>
      允许默认区域不再允许该端口的流量。
    </td>
  </tr>
  
  <tr>
    <td>
      –reload
    </td>
    
    <td>
      让“永久生效”的配置规则立即生效，覆盖当前的。
    </td>
  </tr>
</table>

特别需要注意的是firewalld服务有两份规则策略配置记录，必需要能够区分：

RunTime：当前正在生效的。

Permanent：永久生效的。

当下面实验修改的是永久生效的策略记录时，必须执行”–reload”参数后才能立即生效，否则要重启后再生效。

查看当前的区域：


```
$ firewall-cmd --get-default-zone public
$ firewall-cmd --get-default-zone public

```

查询eno16777728网卡的区域：

<div id="crayon-5abdc6c5d74a0691589426" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a0691589426-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a0691589426-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74a0691589426-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-r">get</span><span class="crayon-o">&#8211;</span><span class="crayon-v">zone</span><span class="crayon-o">&#8211;</span><span class="crayon-v">of</span><span class="crayon-o">&#8211;</span><span class="crayon-t">interface</span><span class="crayon-o">=</span><span class="crayon-e">eno16777728</span>
            </div>
            
            <div id="crayon-5abdc6c5d74a0691589426-2" class="crayon-line">
              <span class="crayon-v">public</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

在public中分别查询ssh与http服务是否被允许：

<div id="crayon-5abdc6c5d74a4006396407" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a4006396407-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a4006396407-2">
              2
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a4006396407-3">
              3
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a4006396407-4">
              4
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74a4006396407-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">query</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-e">ssh</span>
            </div>
            
            <div id="crayon-5abdc6c5d74a4006396407-2" class="crayon-line">
              <span class="crayon-i">yes</span>
            </div>
            
            <div id="crayon-5abdc6c5d74a4006396407-3" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">query</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-e">http</span>
            </div>
            
            <div id="crayon-5abdc6c5d74a4006396407-4" class="crayon-line">
              <span class="crayon-v">no</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

设置默认规则为dmz：

<div id="crayon-5abdc6c5d74a8063854720" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74a8063854720-1">
              1
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74a8063854720-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">set</span><span class="crayon-o">&#8211;</span><span class="crayon-st">default</span><span class="crayon-o">&#8211;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">dmz</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

让“永久生效”的配置文件立即生效：

<div id="crayon-5abdc6c5d74ac168113846" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ac168113846-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ac168113846-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74ac168113846-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-e">reload</span>
            </div>
            
            <div id="crayon-5abdc6c5d74ac168113846-2" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

启动/关闭应急状况模式，阻断所有网络连接：

应急状况模式启动后会禁止所有的网络连接，一切服务的请求也都会被拒绝，当心，请慎用。

<div id="crayon-5abdc6c5d74af368243892" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74af368243892-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74af368243892-2">
              2
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74af368243892-3">
              3
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74af368243892-4">
              4
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74af368243892-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">panic</span><span class="crayon-o">&#8211;</span><span class="crayon-e">on</span>
            </div>
            
            <div id="crayon-5abdc6c5d74af368243892-2" class="crayon-line">
              <span class="crayon-i">success</span>
            </div>
            
            <div id="crayon-5abdc6c5d74af368243892-3" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">panic</span><span class="crayon-o">&#8211;</span><span class="crayon-e">off</span>
            </div>
            
            <div id="crayon-5abdc6c5d74af368243892-4" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

如果您已经能够完全理解上面练习中firewall-cmd命令的参数作用，不妨来尝试完成下面的模拟训练吧。

**4）规则配置实战**

**模拟训练A**：允许https服务流量通过public区域，要求立即生效且永久有效。

方法一：分别设置当前生效与永久有效的规则记录

<div id="crayon-5abdc6c5d74b3139077929" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74b3139077929-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74b3139077929-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74b3139077929-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-i">https</span>
            </div>
            
            <div id="crayon-5abdc6c5d74b3139077929-2" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-v">https</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

方法二：设置永久生效的规则记录后读取记录

<div id="crayon-5abdc6c5d74b6489520668" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74b6489520668-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74b6489520668-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74b6489520668-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-i">https</span>
            </div>
            
            <div id="crayon-5abdc6c5d74b6489520668-2" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">reload</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

**模拟训练B**：不再允许http服务流量通过public区域，要求立即生效且永久生效。

<div id="crayon-5abdc6c5d74ba526591798" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ba526591798-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ba526591798-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74ba526591798-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">remove</span><span class="crayon-o">&#8211;</span><span class="crayon-v">service</span><span class="crayon-o">=</span><span class="crayon-e">http</span>
            </div>
            
            <div id="crayon-5abdc6c5d74ba526591798-2" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

使用参数”–reload”让永久生效的配置文件立即生效：

<div id="crayon-5abdc6c5d74bd925646740" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74bd925646740-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74bd925646740-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74bd925646740-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-e">reload</span>
            </div>
            
            <div id="crayon-5abdc6c5d74bd925646740-2" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

**模拟训练C**：允许8080与8081端口流量通过public区域，立即生效且永久生效。

<div id="crayon-5abdc6c5d74c0476119097" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c0476119097-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c0476119097-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74c0476119097-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">port</span><span class="crayon-o">=</span><span class="crayon-cn">8080</span><span class="crayon-o">&#8211;</span><span class="crayon-cn">8081</span><span class="crayon-o">/</span><span class="crayon-i">tcp</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c0476119097-2" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">reload</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

**模拟训练D**：查看模拟实验C中要求加入的端口操作是否成功。

<div id="crayon-5abdc6c5d74c4754666535" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c4754666535-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c4754666535-2">
              2
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c4754666535-3">
              3
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c4754666535-4">
              4
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74c4754666535-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">list</span><span class="crayon-o">&#8211;</span><span class="crayon-i">ports</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c4754666535-2" class="crayon-line">
              <span class="crayon-cn">8080</span><span class="crayon-o">&#8211;</span><span class="crayon-cn">8081</span><span class="crayon-o">/</span><span class="crayon-i">tcp</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c4754666535-3" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">list</span><span class="crayon-o">&#8211;</span><span class="crayon-i">ports</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c4754666535-4" class="crayon-line">
              <span class="crayon-cn">8080</span><span class="crayon-o">&#8211;</span><span class="crayon-cn">8081</span><span class="crayon-o">/</span><span class="crayon-v">tcp</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

**模拟实验E**：将eno16777728网卡的区域修改为external，重启后生效。

<div id="crayon-5abdc6c5d74c7729254600" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c7729254600-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c7729254600-2">
              2
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c7729254600-3">
              3
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74c7729254600-4">
              4
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74c7729254600-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">external</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">change</span><span class="crayon-o">&#8211;</span><span class="crayon-t">interface</span><span class="crayon-o">=</span><span class="crayon-e">eno16777728</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c7729254600-2" class="crayon-line">
              <span class="crayon-i">success</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c7729254600-3" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-r">get</span><span class="crayon-o">&#8211;</span><span class="crayon-v">zone</span><span class="crayon-o">&#8211;</span><span class="crayon-v">of</span><span class="crayon-o">&#8211;</span><span class="crayon-t">interface</span><span class="crayon-o">=</span><span class="crayon-e">eno16777728</span>
            </div>
            
            <div id="crayon-5abdc6c5d74c7729254600-4" class="crayon-line">
              <span class="crayon-v">public</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

端口转发功能可以将原本到某端口的数据包转发到其他端口:

<div id="crayon-5abdc6c5d74cb360834370" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74cb360834370-1">
              1
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74cb360834370-1" class="crayon-line">
              <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-o"><</span>区域<span class="crayon-o">></span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">forward</span><span class="crayon-o">&#8211;</span><span class="crayon-v">port</span><span class="crayon-o">=</span><span class="crayon-v">port</span><span class="crayon-o">=</span><span class="crayon-o"><</span>源端口号<span class="crayon-o">></span><span class="crayon-o">:</span><span class="crayon-v">proto</span><span class="crayon-o">=</span><span class="crayon-o"><</span>协议<span class="crayon-o">></span><span class="crayon-o">:</span><span class="crayon-v">toport</span><span class="crayon-o">=</span><span class="crayon-o"><</span>目标端口号<span class="crayon-o">></span><span class="crayon-o">:</span><span class="crayon-v">toaddr</span><span class="crayon-o">=</span><span class="crayon-o"><</span>目标<span class="crayon-i">IP</span>地址<span class="crayon-o">></span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

将访问192.168.10.10主机888端口的请求转发至22端口：

<div id="crayon-5abdc6c5d74ce086546388" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ce086546388-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74ce086546388-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74ce086546388-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">forward</span><span class="crayon-o">&#8211;</span><span class="crayon-v">port</span><span class="crayon-o">=</span><span class="crayon-v">port</span><span class="crayon-o">=</span><span class="crayon-cn">888</span><span class="crayon-o">:</span><span class="crayon-v">proto</span><span class="crayon-o">=</span><span class="crayon-v">tcp</span><span class="crayon-o">:</span><span class="crayon-v">toport</span><span class="crayon-o">=</span><span class="crayon-cn">22</span><span class="crayon-o">:</span><span class="crayon-v">toaddr</span><span class="crayon-o">=</span><span class="crayon-cn">192.168.10.10</span>
            </div>
            
            <div id="crayon-5abdc6c5d74ce086546388-2" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

使用客户机的ssh命令访问192.168.10.10主机的888端口：

<div id="crayon-5abdc6c5d74d2686144421" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-2">
              2
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-3">
              3
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-4">
              4
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-5">
              5
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-6">
              6
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d2686144421-7">
              7
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74d2686144421-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">ssh</span> <span class="crayon-o">&#8211;</span><span class="crayon-i">p</span> <span class="crayon-cn">888</span> <span class="crayon-cn">192.168.10.10</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-2" class="crayon-line">
              <span class="crayon-e">The </span><span class="crayon-e">authenticity </span><span class="crayon-e">of </span><span class="crayon-i">host</span> <span class="crayon-s">&#8216;[192.168.10.10]:888 ([192.168.10.10]:888)&#8217;</span> <span class="crayon-i">can</span>&#8216;<span class="crayon-i">t</span> <span class="crayon-e">be </span><span class="crayon-v">established</span><span class="crayon-sy">.</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-3" class="crayon-line">
              <span class="crayon-e">ECDSA </span><span class="crayon-e">key </span><span class="crayon-e">fingerprint </span><span class="crayon-st">is</span> <span class="crayon-v">b8</span><span class="crayon-o">:</span><span class="crayon-cn">25</span><span class="crayon-o">:</span><span class="crayon-cn">88</span><span class="crayon-o">:</span><span class="crayon-cn">89</span><span class="crayon-o">:</span><span class="crayon-cn">5c</span><span class="crayon-o">:</span><span class="crayon-cn">05</span><span class="crayon-o">:</span><span class="crayon-v">b6</span><span class="crayon-o">:</span><span class="crayon-r">dd</span><span class="crayon-o">:</span><span class="crayon-v">ef</span><span class="crayon-o">:</span><span class="crayon-cn">76</span><span class="crayon-o">:</span><span class="crayon-cn">63</span><span class="crayon-o">:</span><span class="crayon-v">ff</span><span class="crayon-o">:</span><span class="crayon-cn">1a</span><span class="crayon-o">:</span><span class="crayon-cn">54</span><span class="crayon-o">:</span><span class="crayon-cn">02</span><span class="crayon-o">:</span><span class="crayon-cn">1a.</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-4" class="crayon-line">
              <span class="crayon-e">Are </span><span class="crayon-e">you </span><span class="crayon-e">sure </span><span class="crayon-e">you </span><span class="crayon-e">want </span><span class="crayon-st">to</span> <span class="crayon-st">continue</span> <span class="crayon-e">connecting</span> <span class="crayon-sy">(</span><span class="crayon-v">yes</span><span class="crayon-o">/</span><span class="crayon-v">no</span><span class="crayon-sy">)</span><span class="crayon-sy">?</span> <span class="crayon-e">yes</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-5" class="crayon-line">
              <span class="crayon-v">Warning</span><span class="crayon-o">:</span> <span class="crayon-e">Permanently </span><span class="crayon-i">added</span> <span class="crayon-s">&#8216;[192.168.10.10]:888&#8217;</span> <span class="crayon-sy">(</span><span class="crayon-v">ECDSA</span><span class="crayon-sy">)</span> <span class="crayon-st">to</span> <span class="crayon-e">the </span><span class="crayon-e">list </span><span class="crayon-e">of </span><span class="crayon-e">known </span><span class="crayon-v">hosts</span><span class="crayon-sy">.</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-6" class="crayon-line">
              <span class="crayon-v">root</span><span class="crayon-sy">@</span><span class="crayon-cn">192.168.10.10</span>&#8216;<span class="crayon-i">s</span> <span class="crayon-v">password</span><span class="crayon-o">:</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d2686144421-7" class="crayon-line">
              <span class="crayon-e">Last </span><span class="crayon-v">login</span><span class="crayon-o">:</span> <span class="crayon-e">Sun </span><span class="crayon-i">Jul</span> <span class="crayon-cn">19</span> <span class="crayon-cn">21</span><span class="crayon-o">:</span><span class="crayon-cn">43</span><span class="crayon-o">:</span><span class="crayon-cn">48</span> <span class="crayon-cn">2015</span> <span class="crayon-i">from</span> <span class="crayon-cn">192.168.10.10</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

再次提示:请读者们再仔细琢磨下立即生效与重启后依然生效的差别，千万不要修改错了。

**模拟实验F**：设置富规则，拒绝192.168.10.0/24网段的用户访问ssh服务。

firewalld服务的富规则用于对服务、端口、协议进行更详细的配置，规则的优先级最高。

<div id="crayon-5abdc6c5d74d6866482606" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d6866482606-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d6866482606-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74d6866482606-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">cmd</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">permanent</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">zone</span><span class="crayon-o">=</span><span class="crayon-v">public</span> <span class="crayon-o">&#8212;</span><span class="crayon-v">add</span><span class="crayon-o">&#8211;</span><span class="crayon-v">rich</span><span class="crayon-o">&#8211;</span><span class="crayon-v">rule</span><span class="crayon-o">=</span><span class="crayon-s">&#8220;rule family=&#8221;</span><span class="crayon-i">ipv4</span><span class="crayon-s">&#8221; source address=&#8221;</span><span class="crayon-cn">192.168.10.0</span><span class="crayon-o">/</span><span class="crayon-cn">24</span><span class="crayon-s">&#8221; service name=&#8221;</span><span class="crayon-i">ssh</span><span class="crayon-s">&#8221; reject&#8221;</span>
            </div>
            
            <div id="crayon-5abdc6c5d74d6866482606-2" class="crayon-line">
              <span class="crayon-v">success</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

### 二、图形管理工具

执行firewall-config命令即可看到firewalld的防火墙图形化管理工具，真的很强大，可以完成很多复杂的工作。

<div id="crayon-5abdc6c5d74d9516570893" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74d9516570893-1">
              1
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74d9516570893-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-e">yum </span><span class="crayon-e">install </span><span class="crayon-v">firewall</span><span class="crayon-o">&#8211;</span><span class="crayon-v">config</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

firewalld防火墙图形化管理工具界面详解：

<img class="alignnone size-full wp-image-945" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310493233-687x500-1.png" alt="CentOS7：firewall防火墙使用" width="687" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310493233-687x500-1.png 687w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310493233-687x500-1-300x218.png 300w" sizes="(max-width: 687px) 100vw, 687px" />

①：选择”立即生效”或”重启后依然生效”配置。

②：区域列表。

③：服务列表。

④：当前选中的区域。

⑤：被选中区域的服务。

⑥：被选中区域的端口。

⑦：被选中区域的伪装。

⑧：被选中区域的端口转发。

⑨：被选中区域的ICMP包。

⑩：被选中区域的富规则。

⑪：被选中区域的网卡设备。

⑫：被选中区域的服务，前面有√的表示允许。

⑬：firewalld防火墙的状态。

请注意：firewall-config图形化管理工具中没有保存/完成按钮，只要修改就会生效。

允许其他主机访问http服务，仅当前生效：

<img class="alignnone size-full wp-image-948" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310512288-738x500-1.png" alt="CentOS7：firewall防火墙使用" width="738" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310512288-738x500-1.png 738w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310512288-738x500-1-300x203.png 300w" sizes="(max-width: 738px) 100vw, 738px" />

**允许其他主机访问****8080-8088****端口且重启后依然生效：**

<img class="alignnone size-full wp-image-949" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/201612231052089-1.png" alt="CentOS7：firewall防火墙使用" width="720" height="486" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/201612231052089-1.png 720w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/201612231052089-1-300x203.png 300w" sizes="(max-width: 720px) 100vw, 720px" />

<img class="alignnone size-full wp-image-951" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310531158-1.png" alt="CentOS7：firewall防火墙使用" width="724" height="432" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310531158-1.png 724w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310531158-1-300x179.png 300w" sizes="(max-width: 724px) 100vw, 724px" />

开启伪装功能，重启后依然生效：

firewalld防火墙的伪装功能实际就是SNAT技术，即让内网用户不必在公网中暴露自己的真实IP地址。

<img class="alignnone size-full wp-image-953" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310540249-700x500-1.png" alt="CentOS7：firewall防火墙使用" width="700" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310540249-700x500-1.png 700w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310540249-700x500-1-300x214.png 300w" sizes="(max-width: 700px) 100vw, 700px" />

将向本机888端口的请求转发至本机的22端口且重启后依然生效：

<img class="alignnone size-full wp-image-955" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310544629-694x500-1.png" alt="CentOS7：firewall防火墙使用" width="694" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310544629-694x500-1.png 694w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310544629-694x500-1-300x216.png 300w" sizes="(max-width: 694px) 100vw, 694px" />

过滤所有”echo-reply”的ICMP协议报文数据包，仅当前生效：

ICMP即互联网控制报文协议”**I**nternet **C**ontrol **M**essage **P**rotocol“，归属于TCP/IP协议族，主要用于检测网络间是否可通信、主机是否可达、路由是否可用等网络状态，并不用于传输用户数据。

<img class="alignnone size-full wp-image-956" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310554619-743x500-1.png" alt="CentOS7：firewall防火墙使用" width="743" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310554619-743x500-1.png 743w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310554619-743x500-1-300x202.png 300w" sizes="(max-width: 743px) 100vw, 743px" />

仅允许192.168.10.20主机访问本机的1234端口，仅当前生效：

富规则代表着更细致、更详细的规则策略，针对某个服务、主机地址、端口号等选项的规则策略，**优先级最高**。

<img class="alignnone size-full wp-image-959" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310563474-689x500-1.png" alt="CentOS7：firewall防火墙使用" width="689" height="500" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310563474-689x500-1.png 689w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310563474-689x500-1-300x218.png 300w" sizes="(max-width: 689px) 100vw, 689px" />

**查看网卡设备信息：**

<img class="alignnone size-full wp-image-960" title="CentOS7：firewall防火墙使用" src="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310571556-1.png" alt="CentOS7：firewall防火墙使用" width="733" height="423" srcset="https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310571556-1.png 733w, https://3mile.tophttps://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/media/2016122310571556-1-300x173.png 300w" sizes="(max-width: 733px) 100vw, 733px" />

firewall-config图形管理工具真的非常实用，很多原本复杂的长命令被用图形化按钮替代，设置规则也变得简单了，日常工作中真的非常实用。所以有必要跟读者们讲清配置防火墙的原则——只要能实现需求的功能，无论用文本管理工具还是图形管理工具都是可以的。

### 三、服务的访问控制列表

在Linux中不光可以使用iptables来做安全控制，其实简单的控制也可以使用tcp_wrappers来进行。

Tcp_wrappers(即Transmission Control Protocol(TCP)Wrappers)是一款基于IP层的ACL访问控制列表流量监控程序，它能够根据来访主机地址与本机目标服务程序做允许或拒绝规则，控制列表修改后会立即生效，系统将会先检查允许规则，如果匹配允许则直接放行流量，若拒绝规则中匹配则直接拒绝，都不匹配默认也会放行。

允许名单：/etc/hosts.allow

拒绝名单：/etc/hosts.deny

指定客户端的规则如下：

<table width="712">
  <tr>
    <td>
      客户端类型
    </td>
    
    <td>
      示例
    </td>
    
    <td>
      满足示例的客户端列表
    </td>
  </tr>
  
  <tr>
    <td>
      单一主机
    </td>
    
    <td>
      192.168.10.10
    </td>
    
    <td>
      IP地址为192.168.10.10的主机。
    </td>
  </tr>
  
  <tr>
    <td>
      指定网段
    </td>
    
    <td>
      192.168.10.
    </td>
    
    <td>
      IP段为192.168.10.0/24的主机。
    </td>
  </tr>
  
  <tr>
    <td>
      指定网段
    </td>
    
    <td>
      192.168.10.0/255.255.255.0
    </td>
    
    <td>
      IP段为192.168.10.0/24的主机。
    </td>
  </tr>
  
  <tr>
    <td>
      指定DNS后缀
    </td>
    
    <td>
      .linuxprobe.com
    </td>
    
    <td>
      所有DNS后缀为.linuxprobe.com的主机
    </td>
  </tr>
  
  <tr>
    <td>
      指定主机名称
    </td>
    
    <td>
      boss.linuxprobe.com
    </td>
    
    <td>
      主机名称为boss.linuxprobe.com的主机。
    </td>
  </tr>
  
  <tr>
    <td>
      指定所有客户端
    </td>
    
    <td>
      ALL
    </td>
    
    <td>
      所有主机全部包括在内。
    </td>
  </tr>
</table>

限制只有192.168.10.0/24网段的主机可以访问本机的sshd服务：

编辑允许规则：

<div id="crayon-5abdc6c5d74e6452947309" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74e6452947309-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74e6452947309-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74e6452947309-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-r">cat</span> <span class="crayon-o">/</span><span class="crayon-v">etc</span><span class="crayon-o">/</span><span class="crayon-v">hosts</span><span class="crayon-e">.allow</span>
            </div>
            
            <div id="crayon-5abdc6c5d74e6452947309-2" class="crayon-line">
              <span class="crayon-v">sshd</span><span class="crayon-o">:</span><span class="crayon-cn">192.168.10.</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

拒绝其他所有的主机：

<div id="crayon-5abdc6c5d74fa012080458" class="crayon-syntax crayon-theme-shell-default crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-always">
  <div class="crayon-plain-wrap">
  </div>
  
  <div class="crayon-main">
    <table class="crayon-table">
      <tr class="crayon-row">
        <td class="crayon-nums " data-settings="hide">
          <div class="crayon-nums-content">
            <div class="crayon-num" data-line="crayon-5abdc6c5d74fa012080458-1">
              1
            </div>
            
            <div class="crayon-num" data-line="crayon-5abdc6c5d74fa012080458-2">
              2
            </div>
          </div>
        </td>
        
        <td class="crayon-code">
          <div class="crayon-pre">
            <div id="crayon-5abdc6c5d74fa012080458-1" class="crayon-line">
              <span class="crayon-sy">$</span> <span class="crayon-r">cat</span> <span class="crayon-o">/</span><span class="crayon-v">etc</span><span class="crayon-o">/</span><span class="crayon-v">hosts</span><span class="crayon-e">.deny</span>
            </div>
            
            <div id="crayon-5abdc6c5d74fa012080458-2" class="crayon-line">
              <span class="crayon-v">sshd</span><span class="crayon-o">:</span><span class="crayon-o">*</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

PS：对于Firewall防火墙，后面持续增加内容……..