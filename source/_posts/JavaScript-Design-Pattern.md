---
title: JavaScript设计模式之单例模式
date: 2018-01-03 23:00:00
author: 
  nick: JQ_Chan
  link: https://www.github.com/jqchan
tags: [JS]
categories: 前端开发
subtitle: JavaScript设计模式
---

## JavaScript设计模式
设计模式分类：
* 创建型设计模式，如Constructor（构造器模式）、Factory（工厂模式）、Abstract（抽象模式）、Prototype（原型模式）、Singleton（单例模式）、Builder（建造者模式／生成器模式）
>特点：专注于处理对象创建机制，以适合给定的情况的方式来创建对象
* 结构型设计模式，如Decorator（装饰者模式）、Facade（外观模式／门面模式）、Flyweight（享元模式）、Adapter（适配器模式）、Proxy（代理模式）
>结构模式与对象组合有关，通常可以用于找出在不同对象之间建立关系的简单方法。
* 行为型设计模式，如Iterator（迭代器模式）、Mediator（中介者模式）、Observer（观察者模式）、Visitor（访问者模式）
>专注于改善或简化系统中不同对象之间的通信
