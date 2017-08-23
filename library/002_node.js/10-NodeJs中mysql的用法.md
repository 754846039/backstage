## 简介和安装

Node.js与MySQL交互操作有很多库，具体可以在 https://www.npmjs.org/search?q=mysql  查看。

### 安装
通过以下命令进行mysql的安装：
> npm install mysql

### 进行mysql的测试
```javascript
var mysql  = require('mysql');  //调用MySQL模块

//创建一个connection
var connection = mysql.createConnection({     
  host     : '192.168.0.200',       //主机
  user     : 'root',               //MySQL认证用户名
  password : 'abcd',        //MySQL认证用户密码
  port: '3306',                   //端口号
});
//创建一个connection
connection.connect(function(err){
    if(err){        
          console.log('[query] - :'+err);
        return;
    }
      console.log('[connection connect]  succeed!');
});  
//执行SQL语句
connection.query('SELECT 1 + 1 AS solution', function(err, rows, fields) {
     if (err) {
             console.log('[query] - :'+err);
        return;
     }
     console.log('The solution is: ', rows[0].solution);  
});  
//关闭connection
connection.end(function(err){
    if(err){        
        return;
    }
      console.log('[connection end] succeed!');
});
```
代码执行结果：
> [connection connect] succeed!   
The solution is:2    
[connection end] succeed!   
[Finished in 0.3s]

说明我们的mysql安装成功

## 方法
### 1、createConnection(Object)方法
建立数据库连接
该方法接受一个对象作为参数，该对象有四个常用的属性host，user，password，database。与php中链接数据库的参数相同。
#### Connection Options参数
  |名称     |含义     |
  |:--------|:--------|
  | host:　　　　　|　 连接数据库所在的主机名. (默认: localhost)|
  | port: 　　　　　|　连接端口. (默认: 3306)|
  | localAddress: 　|　用于TCP连接的IP地址. (可选)|
  | socketPath: 　　|　链接到unix域的路径。在使用host和port时该参数会被忽略.|
  | user: 　　　　　　|　MySQL用户的用户名.|
  | password:　　　　 |　MySQL用户的密码.|
  | database: 　　　　|　链接到的数据库名称 (可选).|
  | charset: 　　　　　|　连接的字符集. (默认: 'UTF8_GENERAL_CI'.设置该值要使用大写!)|
  | timezone: 　　　　　|　储存本地时间的时区. (默认: 'local')|
  | stringifyObjects: 　|　是否序列化对象. See issue #501. (默认: 'false')|
  | insecureAuth: 　　　|　是否允许旧的身份验证方法连接到数据库实例. (默认: false)|
  | typeCast: 　　　　　|　确定是否讲column值转换为本地JavaScript类型列值. (默认: true)|
  | queryFormat: 　　　　| 自定义的查询语句格式化函数.|
  | supportBigNumbers:| 数据库处理大数字(长整型和含小数),时应该启用 (默认: false).|
  | bigNumberStrings: | 启用 supportBigNumbers和bigNumberStrings 并强制这些数字以字符串的方式返回(默认: false).|
  | dateStrings: | 强制日期类型(TIMESTAMP, DATETIME, DATE)以字符串返回，而不是一javascript Date对象返回. (默认: false)|
  | debug:| 是否开启调试. (默认: false)|
  | multipleStatements: | 是否允许在一个query中传递多个查询语句. (Default: false)|
  | flags: | 链接标志.|

### 结束数据库连接两种方法和区别
#### end()
end()方法在queries都结束后执行，end()方法接收一个回调函数，queries执行出错，仍然后结束连接，错误会返回给回调函数err参数，可以在回调函数中处理！

#### destory()
立即终止数据库连接，即使还有query没有完成，之后的回调函数也不会在触发。
