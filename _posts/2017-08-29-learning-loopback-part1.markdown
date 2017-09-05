---
layout:     post
title:      "Learning Loopback-Part1"
date:       2017-08-29 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

###Loopback Overview

#### Loopback introduction

虽然我不是Loopback的founder, 不了解Loopback创建时候的重重细节。但身处技术大潮之中，大概也能猜到一二。Loopback的兴起得益于两个大的时代背景：

* Javascript的大行其道
* Mobile/API经济

#### Javascript的大行其道

世界似乎已经无法阻止Javascript的脚步了.

在传统的前端领域,Javascript依旧大放异彩（angularJS,React,Vue），

另外你可以用Javascript来构建桌面应用(NW.js ，Electron );

你还可以用Javascript来构建跨平台的移动应用（Cordova,Ionic）

甚至在长久以来被JAVA占据的服务器端，你也可以用Javascript来搭建后端应用(node.js)

#### mobile/api 经济
随着智能手机，移动应用的普及，移动互联网已经渗透到我们生活中的点点滴滴滴。移动互联网的盛行，其背后很重要的一个技术推动力，便是API。很多技术大人已经意识到，API不光可以用来做应用之间的简单集成，API甚至可以作为一个产品，将企业的核心价值，或者说能力，通过API的方式，传播出去。

所以我们看到很多将API作为公司核心产品的公司，比如Twillo(https://www.twilio.com/),
这是一家提供短信服务的公司，消费这家公司短信服务的唯一方式，就是使用它对外提供的API。

在国内，比如中航信，国内四大航空公司都要依赖它提供的API的来进行航空票价的计算。

应该说，API作为企业能力的衍生，对外渠道的扩展，将扮演越来越重要的角色。

#### Loopback 功能简介

从功能维度讲，Loopback就是一个Express+ORM+REST API的结合体：

* Loopback基于express
* orm的方式访问后端数据
* 提供REST接口的暴露

所以Loopback是一个偏重后端的node开发开发框架。从这个角度讲，有点像java企业开发里面的spring framework. 其实把Loopback 比作node企业开发的"spring framwork"一点都不为过，许多著名的公司的都在使用Loopback作为企业的node开发框架，这其中包括Go Daddy,赛门铁克等公司。

如果你了解express的基础只是，上手Loopback会非常快，因为Loopback是基于express的构建的。

如果你习惯了ORM的方式访问后端数据，Loopback基于ORM,为你提供了丰富的后端连接器（connector）,这些连接器涵盖了目前主流的关系数据库（oracle,db2,mysql），非关系数据库(mongoDB,redis)，即使是传统的web service也可以轻松集成。

另外Loopback的REST API功能可以根据model自动生成CRUD REST API，这个大大减少重复代码，提高来开发效率。


#### Others
在上面的大背景下，node框架层出不穷,大家在选择的时候难免挑花了眼，下面的链接是目前市面上框架的分类以及一些比较，供参考:

* http://nodeframework.com
* http://Loopback.io/resources
* https://richardcooke.info/choosing-a-restful-api-node-js-framework-koa-vs-Loopback-vs-hapi
* https://strongloop.com/strongblog/compare-express-restify-hapi-Loopback

2015年，IBM公司收购了Loopback的母公司strongloop,并将Loopback整合进了其API旗舰产品API Connect. 同时Loopback仍将作为一个开源项目运行。相信在背靠大公司，获得充分的资金以及人力以后，Loopback能在企业NODE应用领域发展得更好。
