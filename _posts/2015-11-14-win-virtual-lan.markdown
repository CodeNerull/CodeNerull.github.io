---
layout: post
title:  "Winodws 虚拟WIFI"
date:   2015-11-14 11:47
categories: winodws
tags: [winodws,技巧,网络]
---

**这一段纯属废话，要想快速配置请看下一段。**这几天由于一些特殊原因不能使用路由器了。就用笔记本共享网络。然后百度一下WIFI，随便找了个WIFI共享软件。下载->安装->运行->共享 无任何问题。感觉这个世界太完美了*^_^*。但在第二天以后电脑频繁连不上网。然后继续百度解决办法，搜到了虚拟WIFI，经过简单的配置网络共享成功后终于过上WIFI稳定的生活。
<!-- more -->

打开命令提示符（win+R -> 输入 -> cmd -> 回车）  
输入以下命令（ssid为WIFI名称，key为WIFI密码）：  
{% highlight bash %}
netsh wlan set hostednetwork mode=allow ssid=mywifi key=wifi0123
netsh wlan start hostednetwork
{% endhighlight %}
![wifiallow]({{site.ASSET_PATH}}/img/posts/win-virtual-lan/wifi-01.jpg) 

打开网络共享中心–>更改适配器设置,选择要共享的网络->右键->属性->共享  
选择`允许其他网络用户通过此计算机的 Internet 连接来连接`  
`在家庭网络连接`中选择要你创建的网络  
![wifiselect]({{site.ASSET_PATH}}/img/posts/win-virtual-lan/wifi-02.jpg) 

然后打开手机去连接WIFI吧  
![wifiselect]({{site.ASSET_PATH}}/img/posts/win-virtual-lan/wifi-04.jpg) 

关闭WIFI：  
{% highlight bash %}
netsh wlan stop hostednetwork
{% endhighlight %}

然后到这还没有连接成功的小伙伴建议你**重新拨号**连接网络或**重启电脑**  

创建开启/关闭WIFI的快捷方式

在记事本(cmd+R -> notepad)中输入以下文字，然后保存成.bat类型文件(保存类型选择`所有文件(*.*)`文件名为`开启WIFI.bat`)
{% highlight bash %}
netsh wlan set hostednetwork mode=allow ssid=mywifi key=wifi0123
netsh wlan start hostednetwork
{% endhighlight %}

同理在新的记事本中以下文字，然后保存成.bat类型文件(保存类型选择`所有文件(*.*)`文件名为`关闭WIFI.bat`)
{% highlight bash %}
netsh wlan stop hostednetwork
{% endhighlight %}