---
layout:     post
title:      "Difference between Transpiling and Polyfill"
date:       2016-09-01 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

## Overview
<p>在我们学习前端技术或者框架的时候，**Polyfill** (aka shims) 和 **Transpiler**
是两个我们经常会碰到的词。对于非native speaker而言，单看字面意思还是蛮难区分的 (某种墙面填料品牌叫Polyfill)。比较实际的办法，还是从具体使用上区分.</p>

首先使用polyfill 和transpiler的背景是大致一样的，即当我们想使用新的语言特性，比如使用ES6的新语法或者API, 但是目标运行环境当前尚未支持的时候，我们可以有下面两种选择：

* Polyfill: 模拟出类似的API，达到旧的目标环境支持新的API的效果
* Transpiler: 将你的代码转换成目标环境支持的，可以运行的的代码

## Transpiler

比方说你想使用ES6的语法，例如箭头函数，但是目标环境（比如浏览器）当前还不支持该ES6的语法，你旧可以使用转换编译器(比如Babel)，把如下的箭头函数：

    [1,2,3].map(n => n + 1);

转换为如下代码：

    [1,2,3].map(function(n) {
    return n + 1;
    });

从而达到你的代码能够在旧的运行环境执行的效果。

## Polyfill

并不是所有的es6的特性都需要transpiler, 有些时候你需要。
举个例子

## Summary

>A polyfill will emulate certain APIs, whereas a transpiler will convert your code so it can be run with an older system

在前端技术日新月异的大背景下，已经成为新常态。当然你也可以等到浏览器全部支持这些新特性的时候，但是可能你会发现，
