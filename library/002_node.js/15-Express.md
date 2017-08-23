## Express简介
Express 是一个基于 Node.js 平台的极简、灵活的 web 应用开发框架，它提供一系列强大的特性，帮助你创建各种 Web 和移动设备应用。

使用 Express 可以快速地搭建一个完整功能的网站。

Express 框架核心特性：
* 可以设置中间件来响应 HTTP 请求。
* 定义了路由表用于执行不同的 HTTP 请求动作。
* 可以通过向模板传递参数来动态渲染 HTML 页面。

## Express的安装

安装 Express 并将其保存到依赖列表中：
> $ npm install express --save

安装 Node 模块时，如果指定了 --save 参数，那么此模块将被添加到 package.json 文件中 dependencies 依赖列表中。 然后通过 npm install 命令即可自动安装依赖列表中所列出的所有模块。

## 创建一个Express实例

**1、为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。**
```
$mkdir myapp
$ cd myapp
```

**2、通过 npm init 命令为你的应用创建一个 package.json 文件**
```
$ npm init
```

**3、安装 Express 并将其保存到依赖列表中**
```
$ npm install express --save
```

 **4、进入 myapp 目录，创建一个名为 app.js 的文件,内容如下：**

 ```javascript
 var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!');
});

var server = app.listen(3000, function () {
  var host = server.address().address;
  var port = server.address().port;

  console.log('Example app listening at http://%s:%s', host, port);
});
```
将对所有 (/) URL 或 路由 返回 “Hello World!” 字符串。对于其他所有路径全部返回 404 Not Found。

## Express 应用生成器
通过应用生成器工具 express 可以快速创建一个应用的骨架。

**1、全局安装express-generator**

> npm install -g express-generator

**2、创建名为worker的骨架**

> express worker

**3、安装所应用依赖包**

> cd worker   
npm install

**4、启动应用**

> npm start

然后在浏览器中打开 http://localhost:3000/ 网址就可以看到这个应用了。

通过 Express 应用生成器创建的应用一般都有如下目录结构：
```
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.jade
    ├── index.jade
    └── layout.jade
```

## 请求和响应
Express 应用使用回调函数的参数： request 和 response 对象来处理请求和响应的数据。

**request** 和 **response** 对象的具体介绍：

### Request 对象
request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。常见属性有：
1. req.app：当callback为外部文件时，用req.app访问express的实例
1. req.baseUrl：获取路由当前安装的URL路径
1. req.body / req.cookies：获得「请求主体」/ Cookies
1. req.fresh / req.stale：判断请求是否还「新鲜」
1. req.hostname / req.ip：获取主机名和IP地址
1. req.originalUrl：获取原始请求URL
1. req.params：获取路由的parameters
1. req.path：获取请求路径
1. req.protocol：获取协议类型
1. req.query：获取URL的查询参数串
1. req.route：获取当前匹配的路由
1. req.subdomains：获取子域名
1. req.accepts()：检查可接受的请求的文档类型
1. req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
1. req.get()：获取指定的HTTP请求头
1. req.is()：判断请求头Content-Type的MIME类型

### Response 对象
response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。常见属性有：
1. res.app：同req.app一样
1. res.append()：追加指定HTTP头
1. res.set()在res.append()后将重置之前设置的头
1. res.cookie(name，value [，option])：设置Cookie
1. opition: domain / expires / httpOnly / maxAge / path / secure / signed
1. res.clearCookie()：清除Cookie
1. res.download()：传送指定路径的文件
1. res.get()：返回指定的HTTP头
1. res.json()：传送JSON响应
1. res.jsonp()：传送JSONP响应
1. res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
1. res.redirect()：设置响应的Location HTTP头，并且设置状态码302
1. res.send()：传送HTTP响应
1. res.sendFile(path [，options] [，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
1. res.set()：设置HTTP头，传入object可以一次设置多个头
1. res.status()：设置HTTP状态码
1. res.type()：设置Content-Type的MIME类型


## Express路由
路由（Routing）是由一个 URI（或者叫路径）和一个特定的 HTTP 方法（GET、POST 等）组成的，涉及到应用如何响应客户端对某个网站节点的访问。

每一个路由都可以有一个或者多个处理器函数，当匹配到路由时，这个/些函数将被执行。

路由的定义由如下结构组成：app.METHOD(PATH, HANDLER)。其中，app 是一个 express 实例；METHOD 是某个 HTTP 请求方式中的一个；PATH 是服务器端的路径；HANDLER 是当路由匹配到时需要执行的函数。

实例：
```javascript
// 对网站首页的访问返回 "Hello World!" 字样
app.get('/', function (req, res) {
  res.send('Hello World!');
});

// 网站首页接受 POST 请求
app.post('/', function (req, res) {
  res.send('Got a POST request');
});

// /user 节点接受 PUT 请求
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user');
});

// /user 节点接受 DELETE 请求
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user');
});
```

### 中间件
Express 是一个自身功能极简，完全是由路由和中间件构成一个的 web 开发框架：从本质上来说，一个 Express 应用就是在调用各种中间件。

中间件（Middleware） 是一个函数，它可以访问请求对象（request object (req)）, 响应对象（response object (res)）, 和 web 应用中处于请求-响应循环流程中的中间件，一般被命名为 next 的变量。

中间件的功能包括：
* 执行任何代码。
* 修改请求和响应对象。
* 终结请求-响应循环。
* 调用堆栈中的下一个中间件。

实例：
基于express框架专门处理session的中间件
```javascript
var session = require('express-session')
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))
```

## 静态文件
Express 提供了内置的中间件 express.static 来设置静态文件如：图片， CSS, JavaScript 等。

你可以使用 express.static 中间件来设置静态文件路径。例如，如果你将图片， CSS, JavaScript 文件放在 public 目录下，你可以这么写：
```javascript
app.use(express.static('public'));
```

我们可以到 public/images 目录下放些图片,如下所示：
```javascript
node_modules
server.js
public/
public/images
public/images/logo.png
```

实例：
```javascript
var express = require('express');
var app = express();

app.use(express.static('public'));

app.get('/', function (req, res) {
   res.send('Hello World');
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port

})
```  
执行效果如下：   
![wd！](amWiki/images/wd.jpg "wd！")  


## GET 方法
以下实例演示了在表单中通过 GET 方法提交两个参数，我们可以使用 server.js 文件内的 **process_get** 路由器来处理输入：
index.htm 文件代码如下：
```html
<html>
<body>
<form action="http://127.0.0.1:8081/process_get" method="GET">
First Name: <input type="text" name="first_name">  <br>

Last Name: <input type="text" name="last_name">
<input type="submit" value="Submit">
</form>
</body>
</html>
```

server.js 文件代码如下:
```javascript
var express = require('express');
var app = express();

app.use(express.static('public'));

app.get('/index.htm', function (req, res) {
   res.sendFile( __dirname + "/" + "index.htm" );
})

app.get('/process_get', function (req, res) {

   // 输出 JSON 格式
   response = {
       first_name:req.query.first_name,
       last_name:req.query.last_name
   };
   console.log(response);
   res.end(JSON.stringify(response));
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port

})
```
运行效果：   
![gif！](amWiki/images/gif.gif "gif！")  


## POST 方法
以下实例演示了在表单中通过 POST 方法提交两个参数，我们可以使用 server.js 文件内的 **process_post** 路由器来处理输入：
index.htm 文件代码修改如下：
```html
<html>
<body>
<form action="http://127.0.0.1:8081/process_post" method="POST">
First Name: <input type="text" name="first_name">  <br>

Last Name: <input type="text" name="last_name">
<input type="submit" value="Submit">
</form>
</body>
</html>
```

server.js 文件代码修改如下:
```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');

// 创建 application/x-www-form-urlencoded 编码解析
var urlencodedParser = bodyParser.urlencoded({ extended: false })

app.use(express.static('public'));

app.get('/index.htm', function (req, res) {
   res.sendFile( __dirname + "/" + "index.htm" );
})

app.post('/process_post', urlencodedParser, function (req, res) {

   // 输出 JSON 格式
   response = {
       first_name:req.body.first_name,
       last_name:req.body.last_name
   };
   console.log(response);
   res.end(JSON.stringify(response));
})

var server = app.listen(8081, function () {

  var host = server.address().address
  var port = server.address().port

  console.log("应用实例，访问地址为 http://%s:%s", host, port)

})
```

执行效果:   
![gif7！](amWiki/images/gif7.gif "gif7！")  

## Cookie 管理
使用中间件向 Node.js 服务器发送 cookie 信息，以下代码输出了客户端发送的 cookie 信息：

```javascript
var express      = require('express')
var cookieParser = require('cookie-parser')

var app = express()
app.use(cookieParser())

app.get('/', function(req, res) {
  console.log("Cookies: ", req.cookies)
})

app.listen(8081)
```
