---
title: JavaScript设计模式之构造器模式
date: 2019-01-03 23:00:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [JS]
categories: 前端开发
subtitle: JavaScript设计模式之构造器模式
---

## Constructor（构造器模式）

在ES6之前，JavaScript不支持class类的概念，但支持与对象一样用法的特殊constructor（构造器）函数。
通过在构造器前面加new关键字，告诉JavaScript像使用构造器一样实例化一个新对象，并且对象成员由该函数定义。
在构造器内，关键字this引用新创建的对象。
