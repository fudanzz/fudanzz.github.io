---
layout:     post
title:      "Top Five JavaScript Pattern"
date:       2016-09-02 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### Overview

Heroku是业界流行的PAAS平台，你可以在上面部署运行java,node等程序，本文主要介绍如何在上面运行node程序。

### Setup Your Heroku
* 注册一个免费的Heroku账号
* 安装Heroku toolbelt客户端

验证：Heroku登录

    heroku login


### Build Node application
利用express搭建一个最简单的REST服务：

    npm init
    npm install --save express

创建一个server.js（详细代码见参考链接）

    var server = app.listen(process.env.PORT || 3000, function () {
    console.log('listening on port %d', server.address().port);
    });


创建一个Procfile文件：

    web: node server.js

验证：启动REST服务

### Deploy to Heroku

初始化本地git库

    git init
    git add .
    git commit -m 'first commit'


创建Heroku应用


    heroku create

    Creating app... done, ⬢ stormy-ravine-93117


添加Heroku远程Git


     heroku git:remote -a stormy-ravine-93117


部署应用


     git push heroku master

验证：

     heroku open

### 附录1
如果你的node应用采用Gulp打包，你也可以通过以下命令于Heroku集成：

    heroku create --buildpack https://github.com/timdp/heroku-buildpack-nodejs-gulp.git
    heroku config:set NODE_ENV=production

同时添加一个production task在你的build文件中：

    gulp.task('heroku:production', function () {
    console.log('production build');
    })

其它步骤跟上面是一样的。

### 附录2

如果你的node应用基于strongloop框架，你需要修改server.js里面的默认端口监听：

    return app.listen(process.env.PORT || 5000, function () {...

### 参考链接

1. <a href="https://github.com/fudanzz/nodeapp1">node application build wiht gulp and  heroku </a>

2. <a href="https://github.com/fudanzz/nodeapp2">node application based on strongloop with heroku Deploy</a>
