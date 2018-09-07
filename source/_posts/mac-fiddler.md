---
title: Mac安装Fiddler
date: 2018-09-07 08:00:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [Fiddler]
categories: 生活杂碎
subtitle: Mac安装Fiddler进行抓包
---
最近没工作，突然想做个小程序，并对一款以上线的小程序的一个功能非常感兴趣，但又不确定它是不是利用webview去做的，所以想抓包来看下。之前没接触过抓包工具，但面试的时候别人有问到前端用过哪些工具，表示只用过Postman去模拟请求，还有mock数据这些。所以百度了一下抓包工具，然后找了Fiddler的安装教程，可参考[《[微信开发利器]微信内移动前端开发抓包调试工具fiddler使用教程》](https://blog.csdn.net/gysea123321/article/details/51209564)以及[《使用Fiddler对移动设备上的HTTP/HTTPS抓包》](https://blog.csdn.net/awker/article/details/39079475)。

## Mono安装
Mac下需要使用.Net编译后的程序，需要用到跨平台的方案Mono（现阶段微软已推出跨平台的方案.Net Core，不过暂时只支持控制台程序）。安装程序可以从(http://www.mono-project.com/download/#download-mac)地址下载。

安装完后，在Terminal里执行以下命令，其中`<mono version>`替换成你所装的mono版本：
``` bash
/Library/Frameworks/Mono.framework/Versions/<mono version>/bin/mozroots --import --sync
```
此步是为了从Mozilla LXR上下载所有受信任的root证书，存于Mono的证书库里。root证书能用于请求https地址。

## Fiddler安装
从Fiddler官网(https://www.telerik.com/download/fiddler)下载fiddler-mac.zip的压缩包。解压到非中文字符的路径下即可。

## 运行Fiddler
在刚才fiddler-mac解压的文件夹下新建一个Terminal终端，执行命令
``` bash
sudo mono Fiddler.exe
```
在此过程中，启动Fiddler可能会报错（我的就报错了），如下：
``` bash
=================================================================
Got a SIGSEGV while executing native code. This usually indicates
a fatal error in the mono runtime or one of the native libraries 
used by your application.
=================================================================
```
**解决方案就是切换32bit-mono启动Fiddler**，可参考[《mac下Fiddler的安装-启动》](https://yq.aliyun.com/articles/443107)以及[《mac mono Fiddler.exe啟動失敗》](https://hk.saowen.com/a/8a726de5a45fb20a2591440689eb0509115eccdfd2d8de01072d3f11f4f21652?spm=a2c4e.11153940.blogcont443107.10.10a96998hWxqfu)。
``` bash
mono --arch=32 Fiddler.exe
```
启动过程中需要输入电脑使用者的密码

## 修改Fiddler配置
打开Fiddler后在菜单栏中点击 Tools - Options - Connections 中配置Allow remote computers to connect 以及点击隔壁的HTTPS配置Decrypt HTTPS Traffic，重启Fiddler

## 手机设置代理（手机和电脑必须在统一局域网）
我的手机还是老款的华为安卓机，不懂手机设置代理的可以百度一下。

打开Fiddler后右上角有个Online的，鼠标放上去或者点击一下就会显示Fiddler的IP地址，设置代理的时候输入这个IP就行了，默认端口可在上面**修改Fiddler配置**中的Connections中设置或者查看，默认为8888

## 最后
然后在手机端访问网页什么的就可以在Fiddler中看到请求啦，然后自己去找自己需要的东西吧，然后就没有然后了。
