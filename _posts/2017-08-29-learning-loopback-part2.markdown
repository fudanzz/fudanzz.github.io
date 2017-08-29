---
layout:     post
title:      "Learning LoopBack-Part2"
date:       2017-08-29 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

## Build your first Rest API

LoopBack是一个优秀的开发rest api的node框架，在介绍它的特性之前，我们先看一下，在不依赖loopback的情况下，我们是如何开发一个rest API；完了我们在看基于loopback，我们如何开发一个rest api. 本章我们通过比较学习的方式，来学习loopback的开始方式有如何不同，以及它有哪些更优秀的特性，能帮助我们进行快速开发。

### Sample Rest API Project
这里的samle project会演示如何将一张用户表的增删改查操作暴露为相应的rest api。后端的数据存储使用mongoDB,同时简单起见，这张用户表只有两个字段：用户名和密码。

### Build Sample Rest API without LoopBack

如果你已经在本地安装了node环境，那我们先从创建一个node项目开始。

1.首先创建一个项目目录

    mkdir restapp
    cd restapp

2.初始化你的node项目

    npm init

3.安装项目依赖的第三方库，这里我们会用到express

    npm install express morgan body-parser cors mongoose lodash --save

4.接下来我们会创建一个简单的目录结构，创建完之后，项目目录结构如下：

    index.js
    node_modules
    package.json
    server
      api
      middleware
      util

项目目录说明：

  server/api : 这个目录用来存放项目里面api的定义

  server/config :这个目录用来存放项目的配置信息

  server/middleware :这个目录用来存放项目用到的middleware定义


5.定义项目的配置信息
在server/config目录下，创建一个config.js文件。目前我们只需保存需要用到的mongoDB的链接信息。
```javascript
    module.exports = {
    db: {
        url: 'mongodb://localhost/nodedb'
    }
    };
```
备注：例子中mongoDB跑在本地，使用默认监听端口27017,数据库名nodedb

6.定义项目用到的middleware
在server/middleware目录下，创建一个appMiddlware.js文件。这里我们需要定义项目用到的middleware.
```javascript
    var morgan = require('morgan');
    var bodyParser = require('body-parser');
    var cors = require('cors');

    // setup global middleware here

    module.exports = function (app) {
        app.use(morgan('dev'));
        app.use(bodyParser.urlencoded({
            extended: true
        }));
        app.use(bodyParser.json());
        app.use(cors());
    };
``
7.api定义
首先我们要在api目录里面创建一个入口文件api.js.作为整个项目api的入口，这里用到了express的Router组件。
```javascript
    var router = require('express').Router();

    // api router will mount other routers
    // for all our resources
    router.use('/users', require('./user/userRoutes'));

    module.exports = router;
```
接着我们需要在api目录下面创建一个user目录。在这个user目录下，创建一下三个文件：

* userModel.js

* userController.js

* userRoutes.js  

userModel.js 用来定义user的数据模型：

```javascript
    var mongoose = require('mongoose');
    var Schema = mongoose.Schema;

    var UserSchema = new Schema({
        username: {
            type: String,
            required: true,
            unique: true
        },

        // dont store the password as plain text
        password: {
            type: String,
            required: true
        }
    });

    module.exports = mongoose.model('user', UserSchema);
```
userController.js用来定义真正的增删改查操作：

```javascript
var User = require('./userModel');
var _ = require('lodash');

exports.params = function (req, res, next, id) {
    User.findById(id)
        .select('-password')
        .exec()
        .then(function (user) {
            if (!user) {
                next(new Error('No user with that id'));
            } else {
                req.user = user;
                next();
            }
        }, function (err) {
            next(err);
        });
};

exports.get = function (req, res, next) {
    User.find({})
        .select('-password')
        .exec()
        .then(function (users) {
            res.json(users.map(function (user) {
                return user.toJson();
            }));
        }, function (err) {
            next(err);
        });
};

exports.getOne = function (req, res, next) {
    var user = req.user.toJson();
    res.json(user.toJson());
};

exports.put = function (req, res, next) {
    var user = req.user;

    var update = req.body;

    _.merge(user, update);

    user.save(function (err, saved) {
        if (err) {
            next(err);
        } else {
            res.json(saved.toJson());
        }
    })
};

exports.post = function (req, res, next) {
    var newUser = new User(req.body);

    newUser.save(function (err, user) {
        if (err) {
            return next(err);
        }

        res.json(user.toJson());
    });
};

exports.delete = function (req, res, next) {
    req.user.remove(function (err, removed) {
        if (err) {
            next(err);
        } else {
            res.json(removed.toJson());
        }
    });
};

```

userRoutes.js 用来user rest api的定义:

```javascript
var router = require('express').Router();
var controller = require('./userController');

// setup boilerplate route jsut to satisfy a request
// for building
router.param('id', controller.params);

router.route('/')
    .get(controller.get)
    .post(controller.post)

router.route('/:id')
    .get(controller.getOne)
    .put(controller.put)
    .delete(controller.delete)

module.exports = router;

```

8. Put All Together

在index.js文件里面，我们需要前面定义的middlware,config以及user api的定义串联起来，并定义一个全局的异常处理：

```javascript
var express = require('express');
var app = express();

var config = require('./server/config/config');
var api = require('./server/api/api');

// db.url is different depending on NODE_ENV
require('mongoose').connect(config.db.url);


// setup the app middlware
require('./server/middleware/appMiddlware')(app);

// setup the api
app.use('/api', api);

// set up global error handling
app.use(function (err, req, res, next) {

    console.error(err.stack);
    res.status(500).send('Oops');
});

app.listen(config.port);
console.log('server is listening on http://localhost:' + config.port);


```
9.Test Drive

最后我们在本地启动这个express,并进行一些简单的测试：

    node index.js

接下来我们用curl命令来测试暴露的user rest api

创建用户

    curl -X POST -H "Content-Type: application/json" -d  '{"name":"","password":"12345"}' http://localhost:3000/api/users

获取用户

    curl -X GET http://localhost:3000/api/users/59a504539a8e4d43e2bb484b

获取所有用户

    curl -X GET http://localhost:3000/api/users

修改用户

    curl -X PUT -H "Content-Type: application/json" -d  '{"name":"phil","password":"77777"}' http://localhost:3000/api/users/59a50aee9ecb82447d1f72be

删除用户

    curl -X PUT http://localhost:3000/api/users/59a504539a8e4d43e2bb484b


如果上述测试返回正常，那这样一个标准的rest api的例子我们就做完了，希望没有花费大家很多时间 ：）接下来我们就来看一下如何基于loopback构建上述的user rest api

### Build Rest API with LoopBack
