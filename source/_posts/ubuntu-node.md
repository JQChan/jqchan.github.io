---
title: Ubuntu安装node
date: 2018-09-06 20:45:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [Node]
categories: Node杂想
subtitle: Ubuntu安装node学习
---

由于4月份买了3年的阿里云云服务器ECS，想着自己接触一下Linux，然后顺便接触一下Node.js。

我的ESC服务器使用的是Ubuntu 16.04的系统，百度了下怎样在Ubuntu中安装Node，最后参考了CSDN上的一篇文章————[《Ubuntu环境下安装nodejs和npm》](https://blog.csdn.net/wangtaoking1/article/details/78005038)，成功地在Ubuntu上安装了Node。（还有一篇文章介绍了在Ubuntu上安装Node的多种方法，详见[《在Ubuntu下安装Node.JS的不同方式》](https://yq.aliyun.com/articles/87706?spm=5176.10695662.1996646101.searchclickresult.61e46f17ivNa1W)）在此过程中遇到了一个报错：*sudo: unable to resolve host xxxx*，解决方法参考[《Ubuntu 报错 sudo: unable to resolve host xxxx 解决方法》](https://blog.csdn.net/a1007720052/article/details/79804098)

**Ubuntu命令采用apt-get，CentOS采用yum**