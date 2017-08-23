## Node.js Path模块

Node.js Path模块提供了一些用于处理文件路径的小工具，与物理文件系统无关，可通过以下方式引入该模块：

> var path=require("path");

#### 方法
|序号      |方法                 |描述                 |
|:----------|:------------------|:---------------------|
|1[1-3获取路径/文件名/扩展名]         |path.dirname(p)|返回路径中代表文件夹的部分，同 Unix 的dirname 命令类似|
|2           |path.basename(p[, ext])|返回路径中的最后一部分,ext为去掉的后缀名。同 Unix 命令 bashname 类似|
|3          |path.extname(p)|返回路径中文件的后缀名，即路径中最后一个'.'之后的部分。如果一个路径中并不包含'.'或该路径只包含一个'.' 且这个'.'为路径的第一个字符，则此命令返回空字符串|
|4[4-5路径组合]          |path.join([path1][, path2][, ...])|用于连接路径。该方法的主要用途在于，会正确使用当前系统的路径分隔符，Unix系统是"/"，Windows系统是"\"|
|5          |path.resolve([from ...], to)|将 to 参数解析为绝对路径。|
|6 [路径解析]        |path.normalize(p)   |规范化路径，注意'..' 和 '.'|
|7 [7-8文件路径分解/组合]          |path.parse(pathString)|返回路径字符串的对象|
|8          |path.format(pathObject)|从对象中返回路径字符串，和 path.parse 相反|
|9          |path.isAbsolute(path)|判断参数 path 是否是绝对路径。|
|10         |path.relative(from, to)|用于将相对路径转为绝对路径。|


#### 属性
|序号      |属性                 |描述                 |
|:----------|:------------------|:---------------------|
|1         |path.sep|平台的文件路径分隔符，linux上是'/' 或 windows上是 '\'|
|2         |path.delimiter|平台的分隔符, linux上是':'或 windows上是';'|
|3         |path.posix|提供上述 path 的方法，不过总是以 linux 兼容的方式交互|
|4         |path.win32|提供上述 path 的方法，不过总是以 win32 兼容的方式交互|

#### 方法实例
创建main.js,代码如下：
```javascript
var path=require("path");

//返回路径的最后一部分
console.console.log('basename：'+path.basename('/foo/bar/baz/asdf/test.html'));

//返回路径的名称  
console.log('dirname：'+path.basename('/foo/bar/baz/asdf/test.html'));

//返回路径的扩展名，从路径的最后一部分.如果没有，返回一个空字符串。
console.log('extname：'+path.basename('test.html'));

//把字符串组合成对象的格式
console.log('parse：'+path.parse('/home/user/dir/file.txt'));

//  格式化路径
console.log('normalization : ' + path.normalize('/test/test1//2slashes/1slash/tab/..'));

//连接路径
console.log('joint path : ' + path.join('/test', 'test1', '2slashes/1slash', 'tab', '..'));

// 转换为绝对路径
console.log('resolve : ' + path.resolve('main.js'));
```
代码执行结果如下：
> $ node main.js      
basename：test.html        
dirname：/foo/bar/baz/asdf    
extname：.html    
parse：{    
   root : "/",        
   dir : "/home/user/dir",       
   base : "file.txt",       
   ext : ".txt",      
   name : "file"       
   }     
normalization : /test/test1/2slashes/1slash    
joint path : /test/test1/2slashes/1slash        
resolve : /web/com/1427176256_27423/main.js

#### 属性实例
linux 上sep
>'foo/bar/baz'.split(path.sep)    
// Returns: ['foo', 'bar', 'baz']

windows上sep
> 'foo\\bar\\baz'.split(path.sep)    
// Returns: ['foo', 'bar', 'baz']

> path.win32.join('\temp','fuck')            
'\\temp\\fuck'

> path.win32.join('/temp', 'demo')    
'\\tmp\\demo'  

linux上的delimiter  
> console.log(process.env.PATH)      
// Returns: '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'

> process.env.PATH.split(path.delimiter)
// Returns ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']

windows上的delimiter
> console.log(process.env.PATH)
// Returns 'C:\Windows\system32;C:\Windows;C:\Program Files\node\'

> process.env.PATH.split(path.delimiter)
// Returns ['C:\\Windows\\system32', 'C:\\Windows', 'C:\\Program Files\\node\\']
