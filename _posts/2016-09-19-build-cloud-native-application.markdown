---
layout:     post
title:      "Build Cloud Native Application"
date:       2016-09-19 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

## Overview
在云计算的大背景下，越来越多的企业拥抱云计算，越来愈多的应用计划迁移或者已经部署到了云平台上，这里就要求我们的应用设计人员，或是开发人员，要开始考虑如何构建面向云端的应用（cloud native application）。

## Benefit
首先我们连看云端应用能给我们带来哪些好处：

* speed
* safety
* scale
* mobile/diversity

## Characteristic

* visibility
* fault tolerance
* micro-service architecture
* self-service(PAAS)
* API for collaboration

## Changes

* 文化改变  （continue delivery, agile）
* 组织改变   (devops)
* 技术改变  （微服务的方式，容器技术等等，去soa中心化）

## Key Technology & Pattern

### 微服务架构1：

如何从单一服务到微服务：
* new feature with micro-service
* integrate micro-service with existing service
* identify bounded service and extract service

### 分布式系统设计：
* 分布式配置信息／版本（spring cloud config/ zookeeper/spring cloud bus）
* 服务注册／发现 （spring netflix, eureka,ribbon）
* 容错 （hystrix/turbin）
* API gateway or edge service

## 其它

* 应用设计不要依赖于特定部署拓扑，比如单一结点，主机名等等，尽量保持应用无状态
* 最好不要依赖本地文件系统，比如读写临时信息到文件系统使用sql或者nosql数据库
* 尽量不要应用里面会话信息，最好使用分布式缓存
* 不要写日志到本地文件系统，采用分布式日志系统 Apache Flume
* 不要hardcode任何环境特定依赖，比如后台服务IP地址，而应采用服务注册，或者虚拟名字
* 不要在代码里使用操作系统特性

## 参考链接

1. http://www.ibm.com/developerworks/websphere/techjournal/1404_brown/1404_brown.html

2. https://www.oreilly.com/ideas/migrating-to-cloud-native-application-architectures

3. http://ryanjbaxter.com/2015/09/14/building-cloud-native-apps-with-spring-part-1/

4. http://www.redbooks.ibm.com/redpieces/abstracts/sg248275.html?Open

5. http://www.ben-morris.com/category/soa/

6. http://martinfowler.com/articles/microservice-testing/
