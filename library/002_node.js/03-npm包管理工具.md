>1. [npm包管理工具](#npm包管理工具 "npm包管理工具")
1. [npm升级](#npm升级 "npm升级")
1. [使用npm命令来安装模块](#使用npm命令来安装模块 "使用npm命令来安装模块")
1. [全局安装与本地安装](#全局安装与本地安装 "全局安装与本地安装")
1. [使用package.json](#使用package.json "使用package.json")
1. [Package.json 属性说明](#Package.json 属性说明 "Package.json 属性说明")
1. [模块卸载](#模块卸载 "模块卸载")
1. [模块更新](#模块更新 "n模块更新")
1. [模块搜素](#模块搜素 "模块搜素")
1. [模块创建](#模块创建 "模块创建")
1. [发布代码](#发布代码 "发布代码")
1. [版本号](#版本号 "版本号")
1. [npm常用命令](#npm常用命令 "npm常用命令")
1. [自定义命令](#自定义命令 "自定义命令")
1. [淘宝NPM镜像](#淘宝NPM镜像 "淘宝NPM镜像")

## npm包管理工具
#### npm是个同Node.js一起安装的包管理工具，解决了Node.js代码部署上很多的问题。用于Node.js包的发布、传播、依赖控制

#### npm常见的使用场景：

* 允许用户从NPM服务器下载别人编写的第三方包到本地使用

* 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用

* 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用

新版的nodejs已经集成了npm，所以之前npm也一并安装好了。这里可以通过"npm -v"命令来检测是否安装成功。命令如下：    
> $ npm -v  
3.10.10  
出现npm当前的版本号即安装成功

## npm升级
npm升级也可以通过npm命令
**Window系统下**
> npm install npm -g

**Linux系统下**
> $ sudo npm install npm -g

使用淘宝镜像的命令  【注】 淘宝镜像详情看下 [淘宝NPM镜像](#淘宝NPM镜像 "淘宝NPM镜像")
```
> cnpm install npm -g
```
## 使用npm命令来安装模块
npm安装Node.js模块语法格式如下：   
> npm install 模块名

以下实例使用Node.js常用的web框架模块 **express** 为例：
> $ npm install express

安装成功以后，**express** 包就放在了工程目录下的 node_modules 目录中，因此在代码中只需要通过 require('express') 的方式就好，无需指定第三方包路径。
```
var express =require ('express');
```

## 全局安装与本地安装
通过npm进行的包安装分为本地安装（local）、全局安装（global）两种  
* 本地安装将安装包放在./node_modules下（运行npm命令时所在的目录），若没有node_modules目录，会在当前执行npm命令的目录下生成node_modules目录。
* 全局安装会将安装包放在/usr/local或者你的node安装目录下，能够直接在命令行使用。

        npm install express    //本地安装    
        npm install express -g    //全局安装

若出现以下错误：
> npm err! Error: connect ECONNREFUSED 127.0.0.1:8087  

解决办法为：  
> $ npm config set proxy null

实例：使用全局方式安装express
> npm install express -g

安装过程输出如下：
```
 express@4.13.3 node_modules/express     //本行输出了express模块的版本号及安装位置     
├── escape-html@1.0.2       
├── range-parser@1.0.2       
├── merge-descriptors@1.0.0       
├── array-flatten@1.1.1       
├── cookie@0.1.3       
├── utils-merge@1.0.0       
├── parseurl@1.3.0       
├── cookie-signature@1.0.6       
├── methods@1.1.1       
├── fresh@0.3.0       
├── vary@1.0.1       
├── path-to-regexp@0.1.7       
├── content-type@1.0.1       
├── etag@1.7.0       
├── serve-static@1.10.0       
├── content-disposition@0.5.0       
├── depd@1.0.1       
├── qs@4.0.0       
├── finalhandler@0.4.0 (unpipe@1.0.0)       
├── on-finished@2.3.0 (ee-first@1.1.1)       
├── proxy-addr@1.0.8 (forwarded@0.1.0, ipaddr.js@1.0.1)       
├── debug@2.2.0 (ms@0.7.1)       
├── type-is@1.6.8 (media-typer@0.3.0, mime-types@2.1.6)       
├── accepts@1.2.12 (negotiator@0.5.3, mime-types@2.1.6)       
└── send@0.13.0 (destroy@1.0.3, statuses@1.2.1, ms@0.7.1, mime@1.3.4, http-errors@1.3.1)       
```

**使用如下命令查看所有全局安装的模块**
> npm ls -g  

## 使用package.json
package.json 位于模块的目录下，用于定义包的属性。接下来让我们来看下 express 包的 package.json 文件，位于 node_modules/express/package.json 内容：
```
{
  "name": "express",
  "description": "Fast, unopinionated, minimalist web framework",
  "version": "4.13.3",
  "author": {
    "name": "TJ Holowaychuk",
    "email": "tj@vision-media.ca"
  },
  "contributors": [
    {
      "name": "Aaron Heckmann",
      "email": "aaron.heckmann+github@gmail.com"
    },
    {
      "name": "Ciaran Jessup",
      "email": "ciaranj@gmail.com"
    },
    {
      "name": "Douglas Christopher Wilson",
      "email": "doug@somethingdoug.com"
    },
    {
      "name": "Guillermo Rauch",
      "email": "rauchg@gmail.com"
    },
    {
      "name": "Jonathan Ong",
      "email": "me@jongleberry.com"
    },
    {
      "name": "Roman Shtylman",
      "email": "shtylman+expressjs@gmail.com"
    },
    {
      "name": "Young Jae Sim",
      "email": "hanul@hanul.me"
    }
  ],
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/strongloop/express.git"
  },
  "homepage": "http://expressjs.com/",
  "keywords": [
    "express",
    "framework",
    "sinatra",
    "web",
    "rest",
    "restful",
    "router",
    "app",
    "api"
  ],
  "dependencies": {
    "accepts": "~1.2.12",
    "array-flatten": "1.1.1",
    "content-disposition": "0.5.0",
    "content-type": "~1.0.1",
    "cookie": "0.1.3",
    "cookie-signature": "1.0.6",
    "debug": "~2.2.0",
    "depd": "~1.0.1",
    "escape-html": "1.0.2",
    "etag": "~1.7.0",
    "finalhandler": "0.4.0",
    "fresh": "0.3.0",
    "merge-descriptors": "1.0.0",
    "methods": "~1.1.1",
    "on-finished": "~2.3.0",
    "parseurl": "~1.3.0",
    "path-to-regexp": "0.1.7",
    "proxy-addr": "~1.0.8",
    "qs": "4.0.0",
    "range-parser": "~1.0.2",
    "send": "0.13.0",
    "serve-static": "~1.10.0",
    "type-is": "~1.6.6",
    "utils-merge": "1.0.0",
    "vary": "~1.0.1"
  },
  "devDependencies": {
    "after": "0.8.1",
    "ejs": "2.3.3",
    "istanbul": "0.3.17",
    "marked": "0.3.5",
    "mocha": "2.2.5",
    "should": "7.0.2",
    "supertest": "1.0.1",
    "body-parser": "~1.13.3",
    "connect-redis": "~2.4.1",
    "cookie-parser": "~1.3.5",
    "cookie-session": "~1.2.0",
    "express-session": "~1.11.3",
    "jade": "~1.11.0",
    "method-override": "~2.3.5",
    "morgan": "~1.6.1",
    "multiparty": "~4.1.2",
    "vhost": "~3.0.1"
  },
  "engines": {
    "node": ">= 0.10.0"
  },
  "files": [
    "LICENSE",
    "History.md",
    "Readme.md",
    "index.js",
    "lib/"
  ],
  "scripts": {
    "test": "mocha --require test/support/env --reporter spec --bail --check-leaks test/ test/acceptance/",
    "test-ci": "istanbul cover node_modules/mocha/bin/_mocha --report lcovonly -- --require test/support/env --reporter spec --check-leaks test/ test/acceptance/",
    "test-cov": "istanbul cover node_modules/mocha/bin/_mocha -- --require test/support/env --reporter dot --check-leaks test/ test/acceptance/",
    "test-tap": "mocha --require test/support/env --reporter tap --check-leaks test/ test/acceptance/"
  },
  "gitHead": "ef7ad681b245fba023843ce94f6bcb8e275bbb8e",
  "bugs": {
    "url": "https://github.com/strongloop/express/issues"
  },
  "_id": "express@4.13.3",
  "_shasum": "ddb2f1fb4502bf33598d2b032b037960ca6c80a3",
  "_from": "express@*",
  "_npmVersion": "1.4.28",
  "_npmUser": {
    "name": "dougwilson",
    "email": "doug@somethingdoug.com"
  },
  "maintainers": [
    {
      "name": "tjholowaychuk",
      "email": "tj@vision-media.ca"
    },
    {
      "name": "jongleberry",
      "email": "jonathanrichardong@gmail.com"
    },
    {
      "name": "dougwilson",
      "email": "doug@somethingdoug.com"
    },
    {
      "name": "rfeng",
      "email": "enjoyjava@gmail.com"
    },
    {
      "name": "aredridel",
      "email": "aredridel@dinhe.net"
    },
    {
      "name": "strongloop",
      "email": "callback@strongloop.com"
    },
    {
      "name": "defunctzombie",
      "email": "shtylman@gmail.com"
    }
  ],
  "dist": {
    "shasum": "ddb2f1fb4502bf33598d2b032b037960ca6c80a3",
    "tarball": "http://registry.npmjs.org/express/-/express-4.13.3.tgz"
  },
  "directories": {},
  "_resolved": "https://registry.npmjs.org/express/-/express-4.13.3.tgz",
  "readme": "ERROR: No README data found!"
}
```
## Package.json 属性说明
* **name** - 包名。
* **version** - 包的版本号。
* **description** - 包的描述。
* **homepage** - 包的官网 url 。
* **author** - 包的作者姓名。
* **contributors** - 包的其他贡献者姓名。
* **dependencies** - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
* **repository** - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
* **main** - main 字段是一个模块ID，它是一个指向你程序的主要项目。就是说，如果你包的名字叫 express，然后用户安装它，然后require("express")。
* **keywords** - 关键字

## 模块卸载
使用以下命令来卸载express模块

> npm uninstall express

卸载后，可以到/node_modules/目录下查看包是否还存在，或者通过npm命令   
> $ npm ls  

## 模块更新
使用以下命令更新模块

> npm update express

## 模块搜素
使用以下命令进行模块搜素

> npm search less

## 模块的创建
创建模块，package.json 文件是必不可少的。
>在命令行输入：```npm init```     
  会在当前目录下生成一个package.json文件，该文件用于定义包的属性。
  >> $ npm init  //配置文件      
This utility will walk you through creating a package.json file.     
It only covers the most common items, and tries to guess sensible defaults.

  >> See `npm help json` for definitive documentation on these fields
and exactly what they do.

  >> Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

>> Press ^C at any time to quit.      
name: (node_modules) mc                   # 模块名      
version: (1.0.0)                          # 版本名      
description: Node.js 测试模块              # 描述       
entry point: (index.js)      
test command: make test      
git repository: https://github.com/runoob/runoob.git  # Github 地址     
keywords:      
author:     
license: (ISC)     
About to write to ……/node_modules/package.json:      # 生成地址   

> {
  "name": "mc",      
  "version": "1.0.0",         
  "description": "Node.js 测试模块",       
  ……
}


> Is this ok? (yes) yes

以上相关信息根据自己的需要进行设置，最后输入“yes”会生成package.json文件

## 发布代码

**步骤一：**       
    在命令行输入：```npm addUser```    
    进行npm用户注册，注册成功以后登录  
> $ npm adduser   
Username: mc   
Password:        
Email: (this IS public) mcmohd@gmail.com   


**步骤二：**    
   在命令行输入：```npm publish```    
   可以将自己编辑的代码上传    
   相反的若要撤销发布 ```npm unpublish```
> npm publish    

**步骤三：**          
    上传成功以后，可以输入: ```npm install``` 包名称   进行下载
> npm install mc

## 版本号
使用NPM下载和发布代码时都会接触到版本号。NPM使用语义版本号来管理代码，这里简单介绍一下。  
语义版本号分为X.Y.Z三位，分别代表主版本号、次版本号和补丁版本号。当代码变更时，版本号按以下原则更新。  
* 如果只是修复bug，需要更新Z位。
* 如果是新增了功能，但是向下兼容，需要更新Y位。
* 如果有大变动，向下不兼容，需要更新X位。

## npm常用命令
npm提供了很多命令，使用npm help可以查看所有的命令。此处列举几个常用的命令
* npm help，查看所有的命令
* npm help <命令名>，查看某条命令详细帮助
* npm install和npm uninstall，进行包的安装和卸载
* npm ls，进行已经安装了的包的查看
* npm update <包名>，把当前目录下node_modules子目录里边的对应模块更新至最新版本
* npm update <包名> -g，把全局安装的对应命令行程序更新至最新版。
* npm search <包名>，进行模块搜素
* npm cache clear，可以清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人。
* npm unpublish <包名>@<版本号>，可以撤销发布自己发布过的某个版本代码。

## 自定义命令
我们通过以下一个简单的例子来实现下：
**步骤一**
创建一个"pack.js"的文件，内容如下：
```javascript
console.log('我是自定义命令');
```

**步骤二**
在指定的文件"pack.js"文件下通过"npm init"命令生成一个package.json文件，具体内容如下：
```javascript
{
  "name": "pack",
  "version": "1.0.0",
  "description": "",
  "main": "pack.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

各属性描述参见上边    [Package.json 属性说明](#Package.json 属性说明 "Package.json 属性说明")

**步骤三**
在package.json文件中创建指定命令
```javascript
"bin":{    
    "yxc":"./pack.js"   
  }  
```
**步骤四**
在指定运行的文件（pack.js）里加入 ```#!/user/local/bin/node```(node的安装目录)，指定该文件运行要调用的程序   
```javascript
#!E:\node\node.exe
console.log('我是自定义命令');
```
**步骤五**
在终端 cd 进去该目录，运行```npm install -g```将该模块打包到全局环境下面

> npm install -g

通过 ```npm link```也可以，此处可以省略第五步，会生成一个快捷方式
> npm link   //功能：在本地包和全局包之间穿件符号连接。

**后期包的更新**
只需要在package.json文件中修改version字段，然后重新使用npm publish命令就行了

## 淘宝NPM镜像
国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。   
淘宝 NPM 镜像是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。
你可以使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

> $ npm install -g cnpm --registry=https://registry.npm.taobao.org

或者直接通过添加 **npm** 参数 **alias** 一个新命令
```
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"

# Or alias it in .bashrc or .zshrc
$ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```
安装成功后就可以使用cnpm命令安装模块了

> $ cnpm install express

更多详情查阅：http://npm.taobao.org/
