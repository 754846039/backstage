
>1. [Node.js全局对象的定义](#Node.js全局对象的定义 "Node.js全局对象的定义")
1. [NodeJs全局变量](#NodeJs全局变量 "NodeJs全局变量")
1. [NodeJs全局对象global的方法](#NodeJs全局对象global的方法 "NodeJs全局对象global的方法")
1. [魔术常量](#魔术常量 "魔术常量")

## Node.js全局对象的定义
> JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。   

所有全局变量（除了 global 本身以外）都是 global 对象的属性。在 Node.js 我们可以直接访问到 global 的属性，而不需要在应用中包含它。
> * javascript里面的全局对象  window   
* node.js里面的全局对象  global  

global最根本的作用是作为全局变量的宿主，据ECMAScript的定义，满足以下条件的变量都是全局变量
> * 在最外层定义的变量
* 全局对象的属性
* 隐式定义的变量
在Node.js中不可能在最外层定义变量，因为所有用户代码都是属于当前模块的，而模块本身不是最外层上下文。

## NodeJs全局变量

[注:]   全局空间可以访问console,process,buffer等模块，不需要require

### Buffer类
用于处理二进制数据。详见 buffer 章节

### console模块
console模块是Node提供的核心模块，提供基本的输出功能
console对象的方法如下：
> 1. console.log()    在控制台输出。【类似的还有2-4，格式有%s,%d,%j(json格式)】
1. console.info()     返回信息行消息
1. console.error()    在控制台输出一个错误的消息
1. console.warn()     输出警告消息
1. console.dir(object)       利用util.inspect()输出对象的分析
1. onsole．time()     在程序运行之前调用、记录当前的时间信息
1. console.timeEnd()  配合 onsole．time()，在程序运行完成之后调用，记录程序完成后的时间信息（即间隔的时间）
1. consle.trance()    追踪情况。
1. console.assert(expr,msg)   用于判断某个表达式或变量是否为真。若expr为假，则输出msg

演示代码如下：    

**(一)log err warn info有如下同样的用法**

```javascript
console.log('%s,%d,%j','hello world',1000,{name:'Bill Gate',Sexy:'Male',age:18,product:['xp','win7','win8']});
```

输出如下：   
>  hello world,1000,{"name":"Bill Gate","Sexy":"Male","age":18,"product":["xp","win7","win8"]}

**(二)dir：输出对象分析**
```
var Person = function(name,age)       
{       
  this.name=name;      
  this.age=age;      
};       

var p = new Person('Jobs',23);  

console.dir(p);  
console.dir(Person);
```
输出如下：   
> { name: 'Jobs', age: 23 }     
[Function]

**(三)time、timeEnd 输出间隔时间，assert 判断表达式真假，trance追踪情况**
```javascript
console.time('timer1');       
for(var i=0;i<10000000;i++)       
{      
    if(i%2==0)     
    {      
    }      
}      
console.timeEnd('timer1');        
try     
{      
  console.assert(1==22,'if equal are wrong');      
}     
catch(err)     
{     
  console.log('%s,%s',err.name,err.message);      
}       

console.trace('trace');      
```

输出结果如下：  
```
timer1: 169ms     
AssertionError,if equal are wrong     
Trace: trace      
    at Object.<anonymous> (/home/aaaa/nodejs/stdio.js:36:9)     
    at Module._compile (module.js:449:26)     
    at Object.Module._extensions..js (module.js:467:10)     
    at Module.load (module.js:356:32)     
    at Function.Module._load (module.js:312:12)     
    at Module.runMain (module.js:492:10)      
    at process.startup.processNextTick.process._tickCallback (node.js:244:9)       
```

### process

process是一个全局变量，即global对象的属性，它用来操作或者是获取或者查看当前进程的相关信息。
> 1. process.argv()    是用来获取或查看当前进程的相关信息。
1. process.cwd()       查看当前进程的工作目录
1. process.chdir()     更改当前进程的工作目录
1. process.stdin()     标准的输入流
1. process.stdout()    标准的输出流
1. process.emit()      主动触发自定义事件
1. process.pause()     进程暂停
1. Process.resume()    进程重启

**4、module和exports**         
module.exports===exports分配所需出口。   
   能够将当前模块下的值发射出去，让引用的模块来获取相应的值。     
	因为module.exports 和 exports 是引用关系，如果直接赋值，会导致这个对象的联系断开。  

## NodeJs全局对象global的方法
**1、setInterval(fn,ms)**
> 全局函数在指定的毫秒(ms)数后执行指定的函数fn，重复执行

**2、setTimeout(fn,ms)**
> 全局函数在指定的毫秒(ms)数后执行指定的函数fn，只执行一次

**3、clearTimeout()**
> 全局函数用于停止一个之前通过setTimeout()创建的定时器

**4、require();**
> 引入其他模块
  **4.1、require.cache()**
  > 记录当前目录下的所有模块信息
  **4.2、require.resolve()**
  > 将引用的模块转化为

## 魔术常量
### _filename
_filename表示当前正在执行的脚本的文件名。
输出文件所在位置的绝对路径。若在没空看中，返回模块文件的路径

例子，从 /Users/mjr 运行 node example.js：

```
console.log(__filename);
// 输出: /Users/mjr/example.js
```

__filename 实际上不是一个全局变量，而是每个模块内部的。

### _dirname
_dirname表示当前执行脚本所在的目录

例子，从 ```/Users/mjr``` 运行 ```node example.js```：

```
console.log(__dirname);    
// 输出: /Users/mjr
```

```__dirname``` 实际上不是一个全局变量，而是每个模块内部的。

例子，给出两个模块：a 和 b，其中 b 是 a 的一个依赖，目录结构如下：

* /Users/mjr/app/a.js
* /Users/mjr/app/node_modules/b/b.js

b.js 的 __dirname 返回 /Users/mjr/app/node_modules/b，而 a.js 的 __dirname 返回 /Users/mjr/app。
