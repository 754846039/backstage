> 1. [HTTP简介](#HTTP简介 "HTTP简介")
1. [技术架构](#技术架构 "技术架构")
1. [HTTP头域](#HTTP头域 "HTTP头域")
1. [工作原理](#工作原理 "工作原理")
1. [HTTP协议的主要特点](#HTTP协议的主要特点 "HTTP协议的主要特点")
1. [Node.js中的http模块](#Node.js中的http模块 "Node.js中的http模块")
1. [一、http服务器](#一、http服务器 "一、http服务器")
1. [二、http客户端](#二、http客户端 "二、http客户端")

## HTTP简介
>  超文本传输协议(HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个规定。设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。

## 技术架构
> HTTP是一个客户端和服务器端请求和应答的标准（TCP）。客户端是终端用户，服务器端是网站。通过使用WEB浏览器、网络爬虫或其他的工具，客户端发起一个到服务器上指定端口（默认端口为80）的HTTP请求。

## HTTP头域
> HTTP的头域包括通用头，请求头，响应头和实体头四个部分。

###  (一)通用头域
通用头域包含请求和响应消息都支持的头域，通用头域包含Cache-Control、Connection、Date、Pragma、Transfer-Encoding、Upgrade、Via。
> 1.Cache-Control头域：指定请求和响应遵循的缓存机制。     
  Public指示响应可被任何缓存区缓存。      
  Keep-Alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive功能避免了建立或者重新建立连接。     

> 2.Date头域：表示消息发送的时间。

> 3.Pragma头域：用来包含实现特定的指令，最常用的是Pragma:no-cache。在HTTP/1.1协议中，它的含义和Cache-Control:no-cache相同。  

### (二)请求消息
> 1、Host头域：指定请求资源的Intenet主机和端口号。     
2、Referer头域：允许客户端指定请求url的资源地址，是个相对地址。    
3、Range头域：可以请求实体的一个或多个子范围。   
4、User-Agent头域：内容包含发出请求的用户信息。

### (三)响应消息
> 1、Location响应头：用于重定向接收者到一个新URI地址。    
2、Server响应头：包含处理请求的原始服务器的软件信息。

### (四)实体信息
请求消息和响应消息都可以包含实体信息，实体信息一般由实体头域和实体组成。
> 1.Content-Type实体头：用于向接收方指示实体的介质类型，指定HEAD方法送到接收方的实体介质类型，或GET方法发送的请求介质类型      
2.Content-Range实体头：用于指定整个实体中的一部分的插入位置，他也指示了整个实体的长度。    
3.Last-modified实体头：指定服务器上保存内容的最后修订时间。

## 工作原理
> HTTP操作过程分为四步：   
（一）客户机与服务器建立连接

> （二）建立连接后，客户机发送一个请求给服务器，请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容。

>（三）服务器接到请求后，给予相应的响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容。

> （四）客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器断开连接。

## HTTP协议的主要特点
* 1.**支持客户/服务器模式。**

* 2.**简单快速：**    
   客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。每种方法规定了客户与服务器联系的类型不同。由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。

* 3.**灵活：**    
  HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。

* 4.**无连接：**    
   无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。

* 5.**无状态：**   
   HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

## Node.js中的http模块
传统的HTPP服务器会由Aphche、Nginx、IIS之类的软件来担任，但是nodejs并不需要，nodejs提供了http模块，自身就可以用来构建服务器，而且http模块是由C++实现的，性能可靠。

使用http模块时，需要通过以下方法来引入：
> var http=require('http')。

接下来通过一个简易的http服务器来作为开头的学习，就像下面这个例子
```javascript
var http=require("http");        
http.createServer(function(request,response){       
response.writeHead(200,{'Content-Type':'text/html;charset=utf8'});  //发送http头部   
response.end('Hello world\n');   //发送响应数据   
}).listen(8888);
```
使用node命令执行以上代码
打开浏览器输入localhost:8888,我们可以看到屏幕上的hello nodejs了，这表明这个最简单的nodejs服务器已经搭建成功了。
##### 以上代码分析
* 使用require指令来载入Node.js自带的http模块，并将实例化的http赋值给变量http
* 调用http模块提供的createServer函数，该函数会返回一个对象，这个对象上有一个listen方法，这个方法有一个数值参数，用来指定服务器监听的端口号

**nodejs中的http模块中封装了一个HTPP服务器和一个简易的HTTP客户端**

> http.Server是一个基于事件的http服务器，http.request则是一个http客户端工具，用于向http服务器发起请求。  

在上面的例子中，createServer方法中的参数函数中的两个参数req和res则是分别代表了请求对象和响应对象。其中req是http.IncomingMessage的实例，res是http.ServerResponse的实例

## 一、http服务器
文章开头使用的createServer方法返回了一个http.Server对象，这其实是一个创建http服务的捷径，如果我们用以下代码来实现的话，也将一样可行

```javascript
var http=require("http");
var server=new http.Server();

server.on("request",function(req,res){
    res.writeHead(200,{
        "content-type":"text/plain"
    });
    res.write("hello nodejs");
    res.end();
});
server.listen(3000);
```

上代码我们通过直接创建一个http.Server对象，然后为其添加request事件监听，其实也就说createServer方法其实本质上也是为http.Server对象添加了一个request事件监听

### http.Server的事件
http.Server是一个基于事件的服务器，她是继承自EventEmitter，事实上，nodejs中大部分模块都继承自EventEmitter，包括fs、net等模块，这也是为什么说nodejs基于事件驱动（关于EventEmitter的更多内容可以在官方api下的events模块找到），http.Server提供的事件如下：

> * request：当客户端请求到来时，该事件被触发，提供两个参数req和res，表示请求和响应信息，是最常用的事件

* connection：当TCP连接建立时，该事件被触发，提供一个参数socket，是net.Socket的实例

* close：当服务器关闭时，触发事件（注意不是在用户断开连接时）

正如上面我们所看到的request事件是最常用的，而参数req和res分别是http.IncomingMessage和http.ServerResponse的实

### http.IncomingMessage

http.IncomingMessage是HTTP请求的信息，一般由http.Server的request事件发送，并作为第一个参数传递，http请求一般可以分为两部分：请求头和请求体;其提供了3个事件，如下

> * data：当请求体数据到来时，该事件被触发，该事件提供一个参数chunk，表示接受的数据，如果该事件没有被监听，则请求体会被抛弃，该事件可能会被调用多次（这与nodejs是异步的有关系）

* end：当请求体数据传输完毕时，该事件会被触发，此后不会再有数据

* close：用户当前请求结束时，该事件被触发，不同于end，如果用户强制终止了传输，也是用close

**http.IncomingMessage的属性如下：**  

|名称     |含义       |
|:--------|:----------|
|complete|客户端请求是否已经发送完成|
|httpVersion|http协议版本   |
|method|http请求方法，如：GET、POST、PUT等|
|url|原始的请求路径|
|headers| http请求头|
|trailers|http请求尾(一般不常见)|
|connection|当前http连接套接字，为net.Socket的实例|
|socket|connection属性的别名|
|client|client属性的别名|

### http.ServerResponse
http.ServerResponse是返回给客户端的信息，决定了用户最终看到的内容，一般也由http.Server的request事件发送，并作为第二个参数传递，它有三个重要的成员函数，用于返回响应头、响应内容以及结束请求

* res.writeHead(statusCode,[heasers])：向请求的客户端发送响应头，该函数在一个请求中最多调用一次，如果不调用，则会自动生成一个响应头

* res.write(data,[encoding])：想请求的客户端发送相应内容，data是一个buffer或者字符串，如果data是字符串，则需要制定编码方式，默认为utf-8，在res.end调用之前可以多次调用

* res.end([data],[encoding])：结束响应，告知客户端所有发送已经结束，当所有要返回的内容发送完毕时，该函数必需被调用一次，两个可选参数与res.write()相同。如果不调用这个函数，客户端将用于处于等待状态


## 二、http客户端
http模块提供了两个函数http.request和http.get，功能是作为客户端向http服务器发起请求。

### http.request(options,callback)

options是一个类似关联数组的对象，表示请求的参数，callback作为回调函数，需要传递一个参数，为http.ClientResponse的实例，http.request返回一个http.ClientRequest的实例。

options常用的参数有host、port（默认为80）、method（默认为GET）、path（请求的相对于根的路径，默认是“/”，其中querystring应该包含在其中，例如/search?query=byvoid）、headers（请求头内容）

如下实例：
```javascript
var http=require("http");

var options={
    hostname:"cn.bing.com",
    port:80
}

var req=http.request(options,function(res){
    res.setEncoding("utf-8");
    res.on("data",function(chunk){
        console.log(chunk.toString())
    });
    console.log(res.statusCode);
});
req.on("error",function(err){
    console.log(err.message);
});
req.end();
```

运行这段代码我们在控制台可以发现，对应首页的html代码已经呈现出来了。

### http.get(options,callback)

这个方法是http.request方法的简化版，唯一的区别是http.get自动将请求方法设为了GET请求，同时不需要手动调用req.end()，但是需要记住的是，如果我们使用http.request方法时没有调用end方法，服务器将不会收到信息。因为http.get和http.request方法都是放回一个http.ClientRequest对象

### http.ClientRequest

http.ClientRequest是由http.request或者是http.get返回产生的对象，表示一个已经产生而且正在进行中的HTPP请求，提供一个response事件，也就是我们使用http.get和http.request方法中的回调函数所绑定的对象，我们可以显式地绑定这个事件的监听函数

```javascript
var http=require("http");

var options={
    hostname:"cn.bing.com",
    port:80
}

var req=http.request(options);
req.on("response",function(res){
        res.setEncoding("utf-8");
    res.on("data",function(chunk){
        console.log(chunk.toString())
    });
    console.log(res.statusCode);
})

req.on("error",function(err){
    console.log(err.message);
});
req.end();
```

http.ClientRequest也提供了write和end函数，用于向服务器发送请求体，通常用于POST、PUT等操作，所有写操作都必须调用end函数来通知服务器，否则请求无效。此外，这个对象还提供了abort()、setTimeout()等方法，具体可以参考文档

### http.ClientReponse

与http.ServerRequest相似，提供了三个事件，data、end、close，分别在数据到达、传输结束和连接结束时触发，其中data事件传递一个参数chunk，表示接受到的数据。其属性如下

|名称| 含义  |
|statusCode  |http状态吗|
|httpVersion|http协议版本|
|headers|http请求头|
|trailers|http请求尾(不常见)|

此外，这个对象提供了几个特殊的函数

* response。setEncoding([encoding])：设置默认的编码，当data事件被触发时，数据将会以encoding编码，默认值是null，也就是不编码，以buffer形式存储

* response.pause()：暂停结束数据和发送事件，方便实现下载功能

* response.resume()：从暂停的状态中恢复

最后我们做一个简单的爬虫练习：通过http模块将中山大学里学院的名称都扒下来：
```javascript
var cheerio=require("cheerio");
var http=require("http");
var fs=require("fs");

var options="http://www.sysu.edu.cn/2012/cn/jgsz/yx/index.htm";
var htmlData=""
var req=http.request(options,function(res){
    res.on("data",function(chunk){
        htmlData+=chunk;
    });
    res.on("end",function(){
        var $=cheerio.load(htmlData);
        var textcontent=$("tr").text();
        fs.writeFile("./school.txt",textcontent,"utf-8")
    });
});
req.end();
```
之后我们就可在school.txt文件中看到所有的学院了
这里用了一个外部的模块cheerio，这个模块可以让我们像jquery一样操作html代码
