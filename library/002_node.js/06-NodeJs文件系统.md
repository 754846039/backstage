## fs模块

文件 I/O 是由简单封装的标准 POSIX 函数提供的。 通过 ```require('fs') ```访问该模块。
> 所有的方法都有异步和同步的形式。    

异步形式始终以完成回调作为它最后一个参数。 传给完成回调的参数取决于具体方法，但第一个参数总是留给异常。 如果操作成功完成，则第一个参数会是 ```null``` 或 ```undefined```。

当使用同步形式时，任何异常都会被立即抛出。 可以使用 ```try/catch``` 来处理异常，或让它们往上冒泡。

## Node.js的异步编程和同步编程

### Node.js的异步编程

**Node.js异步编程的直接体现就是通过回调函数来实现**
> **[注意]**   异步编程依赖于回调来实现，但不代表使用了回调函数程序就异步化了

非阻塞代码的实现，即异步编程    
创建example.txt文件，如下：
> 异步和同步

创建main.js文件，如下：
```   
var fs=require("fs");  
fs.readFile("example.txt","utf-8",function(error,data){   
   if(err) throw err;  
   console.log(data.toString());  
});
console.log("end");
```

执行结果如下：
> $ node main.js   
end  
异步和同步

### Node.js的同步编程

```
var fs=require("fs");  
var con=fs.readFileSync("input.txt");   
console.log(con.toString());   
condole.log("end");
```
执行结果如下：
> $ node main.js   
异步和同步  
end

以上例子第一个实例不需要等待文件读取完成，就可以在读取文件的同时执行接下来的代码，大大提高了程序的性能。   
第二个例子在文件读取完成之后才执行完程序。

故：阻塞代码是按照顺序依次执行的，而非阻塞的代码不需要按顺序，所以如果需要处理回调函数的参数，就需要写在回调函数内。


##### 文件的操作：打开、读取、修改、关闭、删除、拷贝
##### 文件夹的操作：创建、删除、修改、遍历
---

## fs.access(path[, mode], callback)
**测试**

> * path 指定的文件或目录的用户权限。
* mode 是一个可选的整数，指定要执行的可访问性检查。
   mode可能的值
   * fs.constants.F_OK - path 文件对调用进程可见。 这在确定文件是否存在时很有用，但不涉及 rwx 权限。 如果没指定 mode，则默认为该值。
   * fs.constants.R_OK - path 文件可被调用进程读取。
   * fs.constants.W_OK - path 文件可被调用进程写入。
   * fs.constants.X_OK - path 文件可被调用进程执行。 对 Windows 系统没作用（相当于 fs.constants.F_OK）。
* callback 是一个回调函数，会带有一个可能的错误参数被调用。 如果可访问性检查有任何的失败，则错误参数会被传入。

实例：检查 /etc/passwd 文件是否可以被当前进程读取和写入。
```javascript
fs.access('/etc/passwd', fs.constants.R_OK | fs.constants.W_OK, (err) => {
  console.log(err ? 'no access!' : 'can read/write');
});
```

**同步调用方法：fs.accessSync(path[, mode])**
如果有任何可访问性检查失败则抛出错误，否则什么也不做。

## fs.open(path,flags[,mode],callback(err,fd))
(async)   
**打开文件**  
> * path -文件的路径
* flags -文件打开的方式 r w a
* mode -设置文件模式(权限)，文件创建默认权限为0666(可读，可写)
* callback -打开完成后执行的函数，带有两个参数：callback(err,fd)

flags参数可以是一下值：
|Flag       |描述        |
|-----------|:----------:|
|r          |以读取模式打开文件，如果文件不存在抛出异常|
|r+         |以读写模式打开文件，如果文件不存在抛出异常|
|rs         |以同步的方式读取文件|
|rs+        |以同步的方式读取和写入文件|
|w           |以写入模式打开文件，如果文件不存在则创建|
|wx          |类似'w'，但是如果文件路径存在，则文件写入失败|
|w+          |以读写模式打开文件，如果文件不存在则创建|
|wx+          |类似'w+'，但是如果文件路径存在，则文件读写失败|
|a          |以追加模式打开文件，如果文件不存在则创建|
|ax          |类似'a'，但是如果文件路径存在，则文件追加失败|
|a+          |以读取追加模式打开文件，如果文件不存在则创建|
|ax+          |类似'a+'，但是如果文件路径存在，则文件读取追加失败|

[注意]：fs.open() 某些标志的行为是与平台相关的。 因此，在 OS X 和 Linux 下用 'a+' 标志打开一个目录（见下面的例子），会返回一个错误。 与此相反，在 Windows 和 FreeBSD，则会返回一个文件描述符。    
```javascript
// OS X 与 Linux
fs.open('<directory>', 'a+', (err, fd) => {
  // => [Error: EISDIR: illegal operation on a directory, open <directory>]
});

// Windows 与 FreeBSD
fs.open('<directory>', 'a+', (err, fd) => {
  // => null, <fd>
});
```

**同步调用方法：fs.openSync(path, flags[, mode])**
返回一个表示文件描述符的整数。

## fs.stat(path,callback(err,stats))
(async)
**读取文件的元信息**   

> * path -文件的路径
* callback:读取完信息以后要执行的函数,返回两个参数（err, stats）
* stats：是fs.Stats的一个对象,返回有关文件的一些信息。

```javascript
var fs = require('fs');
var root = __dirname;
fs.stat(root + '/duang.txt', '666', function( err, stats ) {
    if (err) throw err;
    console.log( stats );
});
```

**同步调用方法为：fs.statSync( path )**
返回一个 fs.Stats 实例。

## fs.read(fd,buffer,offset,length,position,callback)
**从fd文件中中读取数据。**

> * fd:打开文件的编码
* buffer:数据将被写入到的 buffer。
* offset:buffer 中开始写入的偏移量。
* length：是一个整数，指定要读取的字节数。
* position:为一个整数变量，标识从哪个位置开始读取文件。如果pisition的参数为null，数据将从文件的当前位置开始读取。
* callback：读取完成后执行的回调函数。回调了三个参数 (err, bytesRead, buffer).

## fs.write(fd,buffer,offset,length[,position],callback())
**将buffer缓冲器内容写入fd指定的文件。**    

> * fd：打开文件编码
* buffer:要写入的数据
* offset:要写入的数据的位置
* length:要写入的数据的长度
* position:指明将数据写入文件从头部算起的偏移位置。如果把pisition设置为null, 那么数据将从当前位置开始写入。
* callback:接受两个参数（err, written）, 其中written标识有多少字节的数据已经写入。

> buffer这个参数可以通过Node.js Buffer API的new Buffer创建。

## fs.writeFile(file,data[,options],callback())
**异步地写入数据到文件，如果文件已经存在，则替代文件**

> * file：文件的名字
* data：写入的内容
* options：设置选项
* callback：写入完成后执行的回调函数

## fs.appendFile(file,data,[,options],callback())
**向文件追加内容,如果文件不存在则创建文件**   

> * file:要操作的文件
* data:要追加的内容
* options:指定选项
* callback

实例：
```javascript
fs.appendFile('message.txt', 'data to append', (err) => {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
```
如果 options 是一个字符串，则它指定了字符编码。例如：
```javascript
fs.appendFile('message.txt', 'data to append', 'utf8', callback);
```

*注意：如果文件存在，往里追加内容；若不存在，和writeFile（）一样*

**同步调用方法：fs.appendFileSync(file, data[, options])**
返回 undefined。

## fs.readFile(file[,options],callback(error,data))
**异步的读取一个文件的全部内容**

> * 要读取的文件
* 设置选项
* 读取完成后执行的回调函数,回调有两个参数 (err, data)，其中 data 是文件的内容。
* data.toString()读取文件里内容

实例：
```javascript
fs.readFile('/etc/passwd', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

如果字符编码未指定，则返回原始的 buffer。

如果 options 是一个字符串，则它指定了字符编码。 例子：
```javascript
fs.readFile('/etc/passwd', 'utf8', callback);
```

**同步读取：fs.readFileSync('filename')**
返回 file 的内容。  
如果指定了 encoding 选项，则该函数返回一个字符串，否则返回一个 buffer。

## fs.rename(oldPath,newPath,callback)
**修改文件名字**

> * olaPath：原来的名字
* newPath：新的名字
* callback：修改完成后执行的回调函数

实例：
```javascript
var fs = require('fs');
var root = __dirname;
fs.rename(root + 'oldername.txt', root + 'newname.txt', function() {
    if (err) throw err;
    console.log('rename complete');
});
```

代码执行结果
> 被指定的文件被重命名为newname.txt

**同步调用方法：fs.renameSync(oldPath, newPath)**
返回 undefined。

## fs.unlink(path,callback)
**删除文件**

> * path：要删除的文件的名字
* callback：删除完成后执行的回调函数

```javascript
var fs = require('fs');
var root = __dirname;
fs.stat(root + 'duang.txt', function( err ) {
    if (err) throw err;
});
```

**同步调用方法：fs.unlinkSync(path)**
返回 undefined。

## 文件的复制
需要自定义，如下：
```javascript
 function copy(filename){     
    var index=filename.indexOf(".");     
    var basename=filename.slice(0,index)+"(1)";     
    var lastname=filename.slice(index);     
    var newname=basename+lastname;     
    fs.readFile(filename,function(err,data){     
        fs.writeFile(newname,data,function(){     
            console.log("done");     
        })     
    })     
}     
```

## fs.chmod(path, mode, [callback])
**修改文件权限。**

```javascript
var fs = require('fs');
var root = __dirname;
fs.chmod(root + '/duang.txt', '666', function( err ) {
    if (err) throw err;
    console.log('chmod complete');
});
```

代码执行结果如下：
> 代码执行前，文件duang.txt的权限不是666。但是当脚本执行完之后该文件的权限就被修改为666了。

**对应同步调用接口为： fs.chmodSync( path, mode );**

## 有关目录的操作

### fs.mkdir(path,[mode],callback)
**创建一个目录**

> * path：创建的目录
* mode：目录的模式
* callback：回调函数

### s.rmdir(path,callback)
> **删除目录f**
* path：要删除的目录
* callback：删除后执行的回调函数

**同步调用方法：fs.rmdirSync(path)**

### 创建深层次的目录及文件
需要自定义，如下：
```javascript
 function makedir(path){       
    var arr=path.split("/");       
    var path="";       
    arr.forEach(function(name,val){       
       path+=name+"/";       
        if(name.indexOf(".")>-1){       
            fs.writeFileSync(path.slice(0,-1),"<html>\n\f</html>>");        
        }else{       
            fs.mkdirSync(path);       
        }        
    })       
}     
```  

#### 更多详情参见nodejs API https://nodejs.org/dist/latest-v7.x/docs/api/fs.html
