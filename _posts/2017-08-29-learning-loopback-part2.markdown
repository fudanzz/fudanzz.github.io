---
layout:     post
title:      "Learning LoopBack-Part2"
date:       2017-08-29 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

## Build your first Rest API


### Overview
LoopBack是一个优秀的开发rest api的node框架，在介绍它的特性之前，我们先看一下，在不依赖loopback的情况下，我们是如何开发一个rest API；完了我们在看基于loopback，我们如何开发一个rest api. 本章我们通过比较学习的方式，来学习loopback的开始方式有如何不同，以及它有哪些更优秀的特性，能帮助我们进行快速开发。

### Build Rest API without LoopBack
如果你已经在本地安装了node环境，那我们先从创建一个node项目开始。

首先创建一个项目目录

    mkdir restapp
    cd restapp

初始化你的node项目

    npm init

安装项目依赖的第三方库，这里我们会用到express

    npm install express --save


### Build Rest API with LoopBack
