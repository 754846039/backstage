>1. [Node.js Stream](#Node.js Stream "Node.js Stream")
1. [Stream的作用](#Stream的作用 "Stream的作用")
1. [Node.js中有四种基本的流类型](#Node.js中有四种基本的流类型 "Node.js中有四种基本的流类型")
1. [Buffer](#Buffer "Buffer")
1. [readStream 读取流](#readStream 读取流 "readStream 读取流")
1. [writeStream 写入流](#writeStream 写入流 "writeStream 写入流")
1. [stream.Duplex  读写流](#stream.Duplex  读写流 "stream.Duplex  读写流")
1. [stream.Transform  读写流](#stream.Transform  读写流 "stream.Transform  读写流")
1. [Transform和Duplex的区别](#Transform和Duplex的区别 "Transform和Duplex的区别")
1. [管道流](#管道流 "管道流")


## Node.js Stream [☝](#Node.js Stream "Node.js Stream")
Stream是Node.js中处理数据的抽象接口，Node中有很多对象实现了这个接口。
例如：对http服务器发起请求的request对象就是一个Stream,还有stdout(标准输出)

该stream模块可以使用访问：
```javascript
const stream = require('stream');
```

## Stream的作用 [☝](#Node.js Stream "Node.js Stream")
传统程序在执行过程中,会边读边写，读写的速度不一样会导致数据丢失；且内存受限，读取存取速度有限。采用流以后程序会读一部分写一部分，保障数据不缺失。  
故：**Stream的作用如下：**
> * 保证程序运行效率
* 防止数据丢失
* 防止内存的溢出  

## Node.js中有四种基本的流类型  [☝](#Node.js Stream "Node.js Stream")
> *  Readable - 读取流 （例如 fs.createReadStream()）
* Writable - 写入流  （例如写 fs.createWriteStream()）
* Duplex - 写流(即双工流)  (例如 net.Socket)
* Transform - 读写流(操作被写入数据，然后读出结果)   (例如 zlib.createDeflate())

## Buffer
Readable和Writable能够在内部缓冲器中进行数据的存储，被用来检索writable._writableState.getBuffer()或 readable._readableState.buffer的分别。   

潜在缓冲的数据的量取决于highWaterMark传递到流构造选项。对于正常的流，所述highWaterMark 选项指定的字节的总数。在对象模式操作的流，所述highWaterMark指定对象的总数。

一旦内部读缓冲器的总大小达到由指定的阈值highWaterMark，则流将暂时停止从基础资源读取数据直到当前缓冲可消耗（数据流将停止调用内部readable._read()方法，用于填充读缓冲区）。

## readStream 读取流
> * **fs.createReadStream(path,[opts]);  创建可读流**  
>> **path:**	创建读取流指定的文件路径    
>> **opts：**  
     * flags   
     * encoding   
     * fd   
     * mode   
     * autoClose   
     * start   
     * end   
     * highWaterMak  
{"encoding":"utf-8","start":0,"end":2,"highWaterMark":4}

> * **事件**  
>> **data:**	当数据读取的时候
>> **end:**	没有更多的数据可读时触发    
>> **close：**  当数据读完的时候

> * **方法**  
>> **pause()**	读取数据暂停(什么时候暂停？读入流大于写入流调用)
>> **resume(0)**	继续读取数据
>> **pipe()**		管道 由读取流安全的传输到下一个流

## writeStream 写入流
> * **fs.createWriteStream(path,[opts]);  创建一个可写入流**  

> * **事件**  
>> **drain**	当前内存数据完全都写入流的时候触发   
>> **close：**  当数据全部都写完后触发

> * **方法**  
>> **write(chunk,[encoding],[callback])** 要往写入流写入数据的时候触发

## stream.Duplex  读写流
```
duplex2._read=function(data,encoding,callback){
}
duplex2._write=function(data,encoding,callback){
    this.push(data.toString().toUpperCase());
    callback();
}
```
## stream.Transform  读写流
方法：
> tranform_transform=function(data,encoding,callback){
}

## Transform和Duplex的区别
> duplex 在写入前必须定义读取流，读流里为空，而transform中用_transform这个方法不需要读写这么麻烦，已经分装好了读写，只要操作数据就可以了。

## 管道流
管道提供了一个输出流到输入流的机制。通常用于从一个流中获取数据并将数据传送到另外一个流中。

**方法**
> fs.createReadStream().pipe(fs.createWriteStream());

#### 更多详情查看 https://nodejs.org/dist/latest-v7.x/docs/api/stream.html
