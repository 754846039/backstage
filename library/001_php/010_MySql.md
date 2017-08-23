# MySQL 关系型数据库
## 通过命令行操作数据库
- mysql添加到环境变量 `C:\wamp\bin\mysql\mysql5.6.17\bin`
- 命令行打开 `mysql`
- 语句结束后要加分号
- 两次 ctrl+c 退出
- mysql -hlocalhost -uroot -p   “host、用户、密码”
- 回车  输入密码  默认空 换行即可
- 就有权限操作数据库


## apache如何解析php代码
- 查看文件名 默认找index
- 查看文件后缀名（默认index.html，其次index.php，再之后是index.php3）
- 读取到html文件后，会不进行解析，因为浏览器认识html,所以直接丢给浏览器去解析,但是浏览器不识别php语法，所以不会解析htmlz中的php语句
- 读取到php文件后，寻找标签对<?php ?>进行解析，遇到html代码会直接丢给浏览器


## 数据库简介
- mysql精准度高，中小型项目
- oracle对大型数据进行处理，加快检索速度
- 做数据库要备份，淘宝无时无刻不在备份
- 存储数据可以用文件（读取速度慢）、缓存（清理缓存就没了）、数据库
- 数据库可以将数据快速存储在硬盘中


## 命令行操作数据库
#### 数据库连接
- mysql -hlocalhost -uroot -p   “host、用户、密码”
#### 查询
- show databases;
  - 查看数据库表
- use 数据库名;
- show tables;

#### 创建
- create database w1701;创建库
- create if not exists database w1701
- create table stu(
    id int(10) primary key auto_increment,
    name varchar(20),
    sex varchar(10),
    age int(10)
  ) default charset=utf8;
#### 删除
- drop database 数据库名
- drop 表名
- use w1701;
#### 数据操作
- SELECT 列名称 FROM 表名称
- INSERT INTO 表名 (列1, 列2,...) VALUES (值1, 值2,....)
- UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
- DELETE FROM 表名称 WHERE 列名称 = 值
#### 排序
- desc 表名;
- asc 表名;

## 数据库语言
数据库 --> 表 --> 字段（约束）

主键
创建一套机制，使得检索速度
AJ自增

## PHP操作数据库
```
//创建数据库连接 实例化一个对象，都要遭函数的参数是。。。
$db=new mysqli("localhost","root"," ","数据库名");

//为了让你的网页能在更多的服务器上正常地显示，不会乱码，告诉mysql和它通信的是utf8编码
//1.告诉mysql server ,客户端（php程序）提交给它的编码是什么
//2.告诉mysql server ,客户端需要的结果的编码是什么
$db->query("set names urf8");

//设置sql语句
$sql="select * from 表名";
$sql="insert into stu (name,age,sex) values ('{$name}','{$age}','{$sex}')";//值为字符串，必须加引号

//发送sql语句，返回对应数据，得到一个结果集
$result=$db->query($sql);

//函数从结果集中取得一行作为关联数组，返回根据从结果集取得的行生成的关联数组，如果没有更多行，则返回 false
//每一行的信息，从结果集中把数据一条一条抽取出来
$rows=$resut->fetch_assoc();

//判断数据库是否操作成功
$db->affected_rows>0  影响的行数大于0

//函数返回结果集中行的数目,仅对select有效
mysql_num_rows()

//返回json形式的字符串
json_encode()

//在前台把json格式的字符串转成json数据
JSON.parse()
```

#### 案例
```html
<body>
  <?PHP
    $db=new mysqli("localhost","root"," ","wui1701");
    $db->query("set names urf8");
    $sql="select * from stu";
    $result=$db->query($sql);
    while($row=$result->fetch_assoc()):
  ?>
  <div class=""><?php echo $row["name"]?></div>
  <div class=""><?php echo $row["sex"]?></div>
  <div class=""><?php echo $row["age"]?></div>
  <div class=""><a href=<?php echo "del.php?id=".$roe?>></a></div>
  <?php  endwhile;?>
</body>
```


## 前后台交互方式
- get 通过地址栏传参,明文的方式  不安全、数据量有限4k
- post 通过加密的方式传递参数，数据量没有限制
- $\_REQUEST get\post都可以接收


## 前后台验证
- 前台：方便用户
- 后台：为了安全性
