---
layout:     post
title:      "Learning LoopBack-Part3"
date:       2017-08-29 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### LoopBack Core Concept
这一章节我们会重点讲述loopback的几个核心概念，为数量掌握loopback这个框架以及后面学习一些loopback的高级应用打下坚实的基础。

#### Core Concept
掌握loopback,需要了解下面几个重点概念:
* model
* data source ／connector
* router


#### Model
Model是loopback框架里头最核心的概念，后面会讲到的data source以及connector都会围绕着model展开。Model本质上是一个javascript对象，是对后端的业务数据或者业务逻辑进行的抽象封装。通过操作model，实现与后端系统的交互，比如实现数据局的增删改查操作。

loopback框架里面提供一些自带的model，比如用户，角色以及应用，你可以根据需要直接使用这些model，也可以基于现有的model来进行扩展；当然大部分情况下，我们会根据特定应用需要来定义自己的model。

有下面几种方式来自定义model：
* LoopBack model generator
* model discovery
* instance introspection
* programing with loopback API

LoopBack model generator是推荐的创建model的方式，你可以通过命令行交互的方式创建你的model.



通过上面几种方式的演示，我们可以看到loopback model强大的地方是说
提供多样的创建方式，一旦model定义好，相关的rest api就会自动暴露，省去了重复繁琐的工作，大大提升开发效率

如果要进一步了解loopback model为何能够如此神奇的暴露rest API接口，我们需要了解data source 以及 connector.


#### Data Source /Connector


#### Routing

#### Summary
