# cookie和session
必须写在\<html\>前
## cookie
### 什么是cookie
保存在客户端的用户的状态信息
### 语法
```php
// 创建cookie
setcookie(name, value, expire过期时间, path, domain);
// 取回 Cookie 的值
echo $_COOKIE["name"];
// 删除 Cookie (设置 cookie 过期时间为过去 1 小时)
setcookie("user", "", time()-3600);
```



### 加密
```php
md5("string");  把任何字符串转为32位的字符串
```


## session
- 在cookie中保存口令，比较安全 存在服务器
- session和cookie只能在同域名下访问
- session 前不能有任何输出，不是非得写在html前,一般会写在\<html\>前，如果不是会闪一下
### session语法
```php
// 开启session  把用户信息存储到 PHP session 中之前，首先必须启动会话
session_start();  
// 创建session,存储状态信息
$_SESSION["name"]="value";
// 检索
echo $_SESSION["name"];
// 销毁指定 Session
unset($_SESSION['name']);
// 销毁/重置 session  将失去所有已存储的 session 数据
session_destroy();
```




#### http协议   tcp/ip协议
- 无状态协议，只负责接受和响应用户的请求，不负责记录用户的状态，所以需要用到cookie来记录
w3c规范 协议  为了不同浏览器遵守同一规则
汽车 红绿灯指定规则 所有人都遵守这个规则


session是cookie的一种，cookie是服务器给客户端的礼物  4k,避免恶意操作大量写入cookie
cookie怎么保存信息？
- 服务器会给客户端保存在硬盘上一些指定的信息
- 客户端每一次想服务器发起请求的时候都会携带cookie
- 服务器会接收每一次客户端发送来的cookie值，然后来判断状态
session是一种特殊的cookie
存储位置不一样



cookie
带着钱1000一毛--去银行--银行开证明：张三有1000张一毛--带着钱和证明回去了，每花一毛钱就需要到银行重新开证明
session
带着钱1000一毛--去银行--存到银行，给了你一张银行卡/口令--带着卡回去了


光有http完不成状态存储
所以需要记录状态
cookie记录用户的状态 存在客户端
session 记录用户的状态  存在服务器，留下一个指令
