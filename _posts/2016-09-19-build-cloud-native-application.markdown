---
layout:     post
title:      "Build Cloud Native Application"
date:       2016-09-19 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

## Overview
云端架构：

1， 能力：

- 1,speed
- 2, safety
- 3, scale
- 4, mobile/diversity

2，特性：

- 1，visibility
- 2，fault tolerance
- 3， 微服务应用架构
- 4， self-service(PAAS)
- 5,   API for collabration

3，实施路径：

- 1，文化改变 （continue delivery, agile）
- 2，组织改变   (devops)
- 3，技术改变  （微服务的方式，容器技术等等，去soa中心化）

4， 关键技术／模式

微服务
微服务组成：
resource+service logic+domain+http client
如何从单一服务到微服务：
1，new feature with micro-service
2，integrate micro-service with monoligh
3,  identify bounded service and extract service

分布式系统设计：
1， 分布式配置信息／版本（spring cloud config/ zookeeper/spring cloud bus）
2,    服务注册／发现 （spring netflix, eureka,ribbon）
3,   容错 （hystrix/turbin）
4,   API gateway or edge service

5， 其它注意事项

- 1,  应用设计不要依赖于特定部署拓扑，比如单一结点，主机名等等，尽量保持应用无状态
- 2，最好不要依赖本地文件系统，比如读写临时信息到文件系统使用sql或者nosql数据库
- 3，尽量不要应用里面会话信息，最好使用分布式缓存
- 4，不要写日志到本地文件系统，采用分布式日志系统 Apache Flume
- 5，不要hardcode任何环境特定依赖，比如后台服务IP地址，而应采用服务注册，或者虚拟名字
- 6， 不要在代码里使用操作系统特性
