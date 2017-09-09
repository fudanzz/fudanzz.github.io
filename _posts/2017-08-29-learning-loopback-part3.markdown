---
layout:     post
title:      "Learning LoopBack-Part3"
date:       2017-08-29 12:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### LoopBack Core Concept

这一章节我们会重点讲述loopback的几个核心概念，为熟练掌握loopback这个框架以及后面学习一些loopback的高级特性打下坚实基础。

#### create loopback project

在讲核心概念之前，我们先讲一下如何创建一个loopback项目。
命令行的方式是最为简单的方式，为此你需要先全局安装一个loopback命令行工具
```javascript
$ npm install -g loopback-cli
```

执行一下命令来创建loopback项目：
```javascript
$ lb app <project-name>
```
上面的这个命令类似项目脚手架工具，会为你创建下面基本的项目目录结构：

* client目录 ：存放前端相关的内容
* common目录 ：存放前后端公共的model定义文件和js
* server ： 存放服务器端的内容
  * server.js : 应用入口文件
  * config.json ： 应用主配置文件
  * model-config.json ： 应用model配置文件
  * datasources.json ： 应用datasources配置文件
  * middleware.json ： 应用middleware配置文件
  * component-config.json ： loopback组件配置文件

#### Core Concept

掌握loopback框架,需要了解下面几个重点概念:
* component-config.json
* model
* data source ／connector
* routing and middleware


#### Model

Model是loopback框架里头最核心的概念，后面会讲到的data source以及connector都会围绕着model展开。Model本质上是一个javascript对象，是对后端的业务数据或者业务逻辑进行的抽象封装。通过操作model，可以实现相关的业务逻辑或者与后端系统的交互，比如数据校验或者实现数据库表的增删改查操作。

loopback框架里面提供一些了内建的model，比如用户，角色以及应用，你可以根据需要直接使用这些model，也可以基于现有的model来进行扩展；当然大部分情况下，我们会根据特定应用需求来定义自己的model。

你可以通过下面这几种方式来自定义model：

* LoopBack model generator
* model discovery
* instance introspection
* programing with loopback API

**LoopBack model generator** 是推荐的创建model的方式，你可以通过命令行交互的方式创建你需要的model.

下面是如何使用这个命令行工具的示例：
在项目的根目录下，运行下面的命令创建一个account model. （这里默认你已经使用 lb project-name 生成了你的项目目录结构了）

```javascript
$ lb model account
? Enter the model name: account
? Select the datasource to attach account to: db (memory)
? Select models base class PersistedModel
? Expose account via the REST API? Yes
? Custom plural form (used to build REST URL):
? Common model or server only? common
Lets add some account properties now.

Enter an empty property name when done.
? Property name: accountName
   invoke  loopback:property
? Property type: string
? Required? No
? Default value[leave blank for none]:

Lets add another account property.
Enter an empty property name when done.
? Property name:
```

Model创建成功之后，这个命令行工具会在项目目录创建以下文件：
* /common/models/account.json 这是一个model定义文件，里面包含这个model的详细定义，比如字段名，属性，继承的父类等信息
* /common/models/account.js 这是model Javascript文件，你可以在添加相关的业务逻辑或者对这个model进行扩展。

除了上面两个新生成的文件，新加的model也会被添加到下面的文件中：
* /server/model-config.json 这个是整个项目的model配置文件

除了通过命令行的方式来创建model，loopback还提供了model discovery和 instance introspection的方式来创建model. 如果你的数据表已经有了，或者数据模型早就已经定义好了，那你可以考虑使用上面这两种方式来创建model. 关于这两种方式的详细描述，我们会在后面章节提到。

最后loopback还提供了api的方式来创建model,下面是一个简单示例：
```javascript

var loopback = require('loopback');
var app = loopback(); // Create an instance of LoopBack
// Create an in memory data source
var ds = loopback.createDataSource('memory');

// Create a open model that doesn't require predefined properties
var FormModel = ds.createModel('form');

// Expose the model as REST APIs
app.model(FormModel);
app.use(loopback.rest());

// Listen on HTTP requests
app.listen(3000, function () {
    console.log('The form application is ready at http://127.0.0.1:3000');
});

```
上述代码仅仅创建了一个开发的model,即我们没有定义任何的字段，你可以为这个model添加任何的字段； 当然你也可以定义model的字段，并且添加强约束检查.


需要说明的，这里演示编程的方式创建model,是为了让大家对model有一个更为直观的感受，通过api的方式创建model不是常用的功能，另外API的方式，不会生成model定义文件，这对项目的后期维护可能会有一些影响。

通过上面几种方式的演示，我们可以发现，一旦model定义好，相关的rest api就会自动暴露，省去了重复繁琐的工作，大大提升了开发效率。

如果要进一步了解loopback model为何能够如此神奇的暴露rest API接口，我们需要了解data source 以及 connector.

#### Data Source / Connector

下面这张图解释了model与datasource以及connector之间的关系：

![Image of explorer](https://raw.githubusercontent.com/fudanzz/fudanzz.github.io/master/img/post/dsource-connector.png)

Datasource 抽象了后端系统，比如数据库，REST API, SOAP API等。于这些后端系统的交互，都通过datasouce这个抽象层来交互。你可能已经注意到，前面我们在定义model的时候，都需要绑定一个datasource.

而datasource本身则通过不同的connector与后端系统交互。比如我要访问后端的mysql数据库，则需要一个mysql的connector. connector封装了与后端系统交互的细节，比如针对数据库表的增删改查。

datasource/connector本质上一个ORM/ODM框架，无论后端系统是数据库，还是其它类型的服务，通过这个ORM/ODM 层，我们都可以方便的，通过操作对象的方式，来实现后端系统的访问。

正因为datasource抽象了后端系统的访问，所以当我们把一个model与datasource绑定起来的时候，这个model具备了对后端系统增删改查的能力。

下面我们看一下如何创建datasource 和 connector.












为了进一步了解model，datasouce以及connector之间的关系，我们这里继续演示一下代码的方式来创建
```javascript
"initial:before": {
  "loopback#favicon": {}
},
```
```javascript
"initial:before": {
  "loopback#favicon": {}
},
```
```javascript
"initial:before": {
  "loopback#favicon": {}
},
```
```javascript
"initial:before": {
  "loopback#favicon": {}
},
```













至此，你应该对loopback最核心的三个概念：model, datasource和connector有了初步的了解，接下来我们看一下loopback框架另外一个重要的概念：Routing.

#### Routing /middleware

前面我们已经提到过，loopback基于express框架的，所以loopback的routing概念和express的routing包括middlware概念是一致的。

另外loopback的routing又做了自己的扩展。大家知道在申明express的middleware的时候，是要考虑顺序的，如果不注意，这个比较容易出问题。loopback在这里引入了"phase"的概念。即通过显式的方式定义middleware的触发顺序。phase在这里可以理解为阶段的意思，loopback启动或者应用响应请求有不同的阶段，阶段是有顺序的，你可以在为不同的阶段申请不同的middleware,从而达到精确控制middleware的触发顺序。

如果你通过前面命令行方式已经创建了loopback应用，在server目录下面有个middleware.json文件，这里面定义loopback的各个预设的phase,以及默认的middlewares申明。

middleware.json文件里面的预设的phase名字是不能改的，不然会导致意外的问题。每个phase阶段的middleware定义是可以根据应用需要配置的。

我们先来看看有哪些预设的phase:

1, initial - 初始阶段是middleware可以运行的起点

2, session - 这个阶段用来初始化会话

3, auth - 这个阶段用来定义认证以及授权的动作

4, parse - 解析http body

5, routes - 这个阶段可以用来执行你定义的各种routes,包括你直接用express api定义的各种middleware;这里需要注意，你需要用loopback的API,才可以定义middleware在哪个phase执行，xpress api定义的各种middleware，默认只能在routes阶段被触发。

6,files - 处理静态内容

7,final - 定义全局错误处理的逻辑

另外每个phase都有两个子阶段：
* phase before
* phase after

让你可以对每个phase做到更细粒度的控制。

回过头来，我们在看middleware.json里面的默认middleware定义：

在initial before阶段，我定义个favicon middleware, 这里的loopback#favicon会被解析为：require('serve-favicon')

```javascript
"initial:before": {
  "loopback#favicon": {}
},
```
在initial阶段，我们看到compression,cors,helmet 这个几个middleware被依次申明：

```javascript
"initial": {
   "compression": {},
   "cors": {
     "params": {
       "origin": true,
       "credentials": true,
       "maxAge": 86400
     }
   },
   "helmet#xssFilter": {},
   "helmet#frameguard": {
     "params": [
       "deny"
     ]
   },
   "helmet#hsts": {
     "params": {
       "maxAge": 0,
       "includeSubdomains": true
     }
   },
   "helmet#hidePoweredBy": {},
   "helmet#ieNoOpen": {},
   "helmet#noSniff": {},
   "helmet#noCache": {
     "enabled": false
   }
 },
```
在routes阶段，loopback自带的rest middleware 会被加载。这里的${restApiRoot}，引用的是定义在config.json里面的属性值。

```javascript
"routes": {
  "loopback#rest": {
    "paths": [
      "${restApiRoot}"
    ]
  }
},
```
最后在final阶段，我们看到urlNotFound和strong-error-handler这两个用来做异常处理的middleware被注册进来

```javascript
"final": {
  "loopback#urlNotFound": {}
},
"final:after": {
  "strong-error-handler": {}

```


#### Summary

通过学习上面loopback的核心概念，我们应该可以对loopback有了一个初步的了解。loopback本质上是结合了express,ORM 以及REST API的特性，使得我们开发一个企业node后端应用变得方便简单。
