>1. [模块的概念](#模块的概念 "模块的概念")
1. [模块的创建](#模块的创建 "模块的创建")
1. [Node.js中require方法中的文件查找策略](#Node.js中require方法中的文件查找策略 "Node.js中require方法中的文件查找策略")
1. [模块的分类](#模块的分类 "模块的分类")
1. [如何使用模块](#如何使用模块 "如何使用模块")

## 模块的概念

为了让Node.js的文件可以相互调用，Node.js提供了一个简单的模块系统
> * 模块是nodejs区别于javascript最重要的一个概念
* 模块是Node.js 应用程序的基本组成部分，它把每一个文件都当做一个独立的作用域，每一个文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。
* 在当前模块下定义的所有的变量\函数，都是属于这个模块的，如果想要定义全局变量，必须通过global.定义。那么在模块下定义的变量它的作用范围只是当前模块。而通过global定义的变量，那么它具有全局的作用范围

*引申：模块是node.js与javascript区别*

## 模块的创建

**（一）Node.js 提供了exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。**

创建一个hello.js文件，如下：
> exports.world=function(){    
 console.log('Hellow World!');   
}

在上述例子中通过exports对象把world作为模块的访问接口

创建一个main.js文件，如下：
> var hello=require('./hello');
hello.world()

在上述例子中通过require()加载这个模块，就能直接访问hello.js中exports对象的成员函数了。

**（二) 把一个对象封装到模块中**

创建一个hello.js文件,如下：
> function hello(){      
   this.say=function(){      
     console.log('Hello');    
 }   
}   
module.exports=hello;

创建一个main.js文件，如下：
> var hello=require('./hello');    
Hello=new hello();        
Hello.say();    

(一)和(二)的区别：使用module.exports=hello代替了exports.world=function(){}。
  在外部引用该模块时其接口对象输出的hello对象本身，而不是exports。

## Node.js中require方法中的文件查找策略
由于Node.js中存在四类模块（原生模块和3种文件模块），尽管require方法极其简单，但是内部的加载却是十分复杂的，其加载优先级也各自不同。如下图所示：     

![require！](amWiki/images/require.jpg "require！")     

### 从文件模块缓存中加载
尽管原生模块与文件模块的优先级不同，但是都不会优先于从文件模块的缓存中加载已经存在的模块。

### 从原生模块加载
原生模块的优先级仅次于文件模块缓存的优先级。require方法在解析文件名之后，优先检查模块是否在原生模块列表中。以http模块为例，尽管在目录下存在一个http/http.js/http.node/http.json文件，require("http")都不会从这些文件中加载，而是从原生模块中加载。    
原生模块也有一个缓存区，同样也是优先从缓存区加载。如果缓存区没有被加载过，则调用原生模块的加载方式进行加载和执行。

## 从文件加载
当文件模块缓存中不存在，而且不是原生模块的时候，Node.js会解析require方法传入的参数，并从文件系统中加载实际的文件，加载过程中的包装和编译细节在前一节中已经介绍过，这里我们将详细描述查找文件模块的过程，其中，也有一些细节值得知晓。

require方法接受以下几种参数的传递：
* http、fs、path等，原生模块。
* ./mod或../mod，相对路径的文件模块。
* /pathtomodule/mod，绝对路径的文件模块。
* nmod，非原生模块的文件模块。

## 模块的分类

模块（指定的是一个文件）分为三部分：
> * 1>核心模块（即node.js自带模块，如http模块）  

#### Node.js中核心模块主要内容包括：
*  全局对象   [详情查看章节NodeJs全局对象]
* 常用工具    
* 事件机制  
* 文件系统    [详情查看章节NodeJs文件系统]
* HTTP
> * 2>自定义模块（即用户自己写的模块）   

> * 3>外部模块    包（又称文件夹，可在npm官网进行下载）   
引入外部模块时，会先在核心文件中进行查找，再到node_modules

#### node.js中的模块[参见手册](https://nodejs.org/dist/latest-v6.x/docs/api/)
**【注】** nodejs方法的稳定等级（6种）

|等级       |描述         |应用时注意事项|
|-----------|:----------:|-------:|
|0          |废弃        |已废弃，不能使用|
|1          |试验        |正在试验阶段，不及建议使用|
|2          |不稳定      |在某些平台可以，并且不稳定，不建议使用，时刻关注最新|
|3          |稳定       |进入稳定阶段，即使改动也是改动底层的接口和性能，不影响使用|
|4          |冻结       |已经非常稳定，可以投入项目中使用|
|5          |锁定       |很长时间内不会升级/迭代，不接受修改（除非发生重大bug）|

## 如何使用模块
### 1、使用核心模块
> 举例：引入http模块 require("http");

### 2、使用自定义模块
> 举例：require("./bb.js")   
*引入自定义模块一定要加路径（可以是绝对路径，可以是相对路径）*

### 3、使用外部模块（又称作包）
> 举例：引入模块less require("less");   
*引入的优先级：1、核心文件，2.node_modules下的less包*
