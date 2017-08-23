>1. [Window 上安装Node.js](#Window 上安装Node.js "Window 上安装Node.js")
1. [Linux 上安装Node.js](#Linux 上安装Node.js "Linux 上安装Node.js")
1. [Mac 上安装Node.js](#Mac 上安装Node.js "Mac 上安装Node.js")
1. [有关Node.js的升级](#有关Node.js的升级 "有关Node.js的升级")
1. [nodejs运行环境的配置](#nodejs运行环境的配置 "nodejs运行环境的配置")
1. [Node.js的运行](#Node.js的运行 "Node.js的运行")

### Node.js安装包及源码下载地址： https://nodejs.org/en/download/

![NodeJs安装包！](amWiki/images/download.png "NodeJs安装包！")  

你可以根据不同的平台系统选择你需要的Node.js安装包。详情如下：

## **[注意]**
**在相应的平台下，下载相应的版本(一个是长期维护版本，一个是最新版本)。**       
**学习或者实验可以用最新版本，项目上线要用长期维护版。**                      
**一般的偶数版本是稳定版，奇数版本是实验版。**      

## Window 上安装Node.js    
安装包中包含有node.exe,npm包，一些nodejs运行必备的环境组件。   
你可以采用以下两种方式来安装  

### 1、Windows安装包(.msi)
> 32位安装包下载地址：https://nodejs.org/dist/v6.9.5/node-v6.9.5-x86.msi            
> 64位安装包下载地址：https://nodejs.org/dist/v6.9.5/node-v6.9.5-x64.msi

本文实例以v0.10.26版本为例，其他版本类似，安装步骤如下：     
步骤1：双击下载后的安装包v0.10.26，如下：      
![双击下载后的安装包v0.10.26！](amWiki/images/windows-step1.png "双击下载后的安装包v0.10.26！")     

步骤2：点击以上的Run运行，将出现如下界面：      
![点击以上的Run运行！](amWiki/images/windows-step2.png "点击以上的Run运行！")      

步骤3：勾选接受协议选项，点击next(下一步)按钮：     
![勾选接受协议选项！](amWiki/images/windows-step3.png "勾选接受协议选项！")     

步骤4：Node.js默认安装目录为 "C:\Program Files\nodejs\" , 你可以修改目录，并点击 next（下一步）：    
![Node.js默认安装目录！](amWiki/images/windows-step4.png "Node.js默认安装目录！")     

步骤5: 点击树形图标来选择你需要的安装模式，要选择add to path将node.exe自动添加到全局路径下 , 然后点击下一步 next（下一步）：   
![安装模式！](amWiki/images/windows-step5.png "安装模式！")     

步骤6：点击 Install（安装） 开始安装Node.js。你也可以点击 Back（返回）来修改先前的配置。 然后并点击 next（下一步）：        
![Install！](amWiki/images/windows-step6.png "Install！")     

安装过程如下：          
![安装过程！](amWiki/images/windows-step7.png "安装过程！")     

点击 Finish（完成）按钮退出安装向导。      
![完成！](amWiki/images/windows-step8.png "完成！")     

安装成功以后检测PATH环境变量是否配置了Node.js    
> 点击“开始”=>"运行"=>输入"cmd"=>输入命令"path"

输出结果如下：    
```
PATH=C:\oraclexe\app\oracle\product\10.2.0\server\bin;C:\Windows\system32;    
C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;     
c:\python32\python;C:\MinGW\bin;C:\Program Files\GTK2-Runtime\lib;    
C:\Program Files\MySQL\MySQL Server 5.5\bin;C:\Program Files\nodejs\;     
C:\Users\rg\AppData\Roaming\npm
```
我们可以看到环境变量中已经包含了C:\Program Files\nodejs\    
检查Node.js版本    
![版本！](amWiki/images/node-version-test.png "版本！")     

### 2、Windows二进制文件安装(.exe)
> 32位安装包下载地址：https://nodejs.org/dist/v6.9.5/node.exe          
> 64位安装包下载地址：https://nodejs.org/dist/v6.9.5/x64/node.exe

安装步骤如下：   
步骤1： 双击下载的安装包 Node.exe ，将出现如下界面 :     
![Node.exe！](amWiki/images/exe-windows-step1.png "Node.exe！")     

步骤2：点击 Run（运行）按钮将出现命令行窗口：   
![Run！](amWiki/images/exe-windows-step21.png "Run！")     

版本测试：   
进入node.exe所在的目录，如下所示：    
![测试！](amWiki/images/node-version.png "测试！")     

安装成功以后需要手动配置环境变量         

我的电脑 -> 右键选择属性-> 高级系统设置 -> 高级 -> 环境变量        
![环境1！](amWiki/images/hj1.png "环境1！")     

进入环境变量对话框，选择 -> 系统变量 -> Path 进行编辑，将之前node.js的安装地址加进去 ，点击 “确定” 完成配置     
![环境2！](amWiki/images/hj2.png "环境2！")     

配置完后，我们安装个module进行一下测试，以我们常用的express为例  
> npm install express -g      //-g就是全局安装的意思

运行效果如下：   
![环境3！](amWiki/images/hj3.png "环境3！")     



## Linux 上安装Node.js
1、下载源码，在 https://nodejs.org/en/download/ 下载最新的Nodejs版本

>  cd /usr/local/src/    
wget http://nodejs.org/dist/v0.10.24/node-v0.10.24.tar.gz

2、解压源码

> tar zxvf node-v0.10.24.tar.gz

3、编译安装

> cd node-v0.10.24    
./configure --prefix=/usr/local/node/0.10.24              
make           
make install

4、配置NODE_HOME，进入profile编辑环境变量

> vim /etc/profile

设置nodejs环境变量，在 export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL 一行的上面添加如下内容:

> #set for nodejs            
export NODE_HOME=/usr/local/node/0.10.24           
export PATH=$NODE_HOME/bin:$PATH

:wq保存并退出，编译/etc/profile 使配置生效

> source/etc/profile   

验证是否安装配置成功

> node -v

输出版本号v0.10.24表示配置成功    

npm模块安装路径

> /usr/local/node/0.10.24/lib/node_modules/

## Mac 上安装Node.js
1、下载源码，在 https://nodejs.org/en/download/ 下载最新的macOS版本

2、下载之后点击安装即可。它将在我们的计算机上安装node.js和npm

3、打开终端进行测试是否安装成功，如下会成功返回当前版本号：  
> localhost:~ binxu$ node -v  //进行版本的查看
v6.9.1  

npm安装的检测，同样会成功返回当前版本号：  
> localhost:~ binxu$ npm -v
3.10.8

这就安装成功了  


## 有关Node.js的升级
### windows系统下

方法一：   
> 下载.msi的安装包，放在之前的node.exe存放目录下进行安装即可

方法二：   
在终端通过指令进行升级：node有一个模块叫n，专门用来管理NOde.js版本的  
> npm install -g n    //首先安装n模块  
n stable     //升级node.js到最新版。n后面也可以跟随版本号，如 n v6.9.5   

此方法同样适用于Mac系统

### Linux系统下
> 1、npm install -g n
  2、n stabal

## nodejs运行环境的配置
**以phpstorm为例**

> * 打开phpstorm的配置项(setting)
* 打开Plugins -> 仓库中搜素nodejs,install进行安装，安装完成后重启编译器
* 打开配置项 -> frameswork下能找到node and npm，已经安装成功
* 让它可用，设置作用区间以及能够自动提示的语言。


**webstorm中天然支持nodejs**

## Node.js的运行
### 交互的方式运行

> - cmd -> node 回车 -> 进入nodejs的编译环境
- 在这个环境下，只要你输入符合nodejs语法规范的代码，回车后会立即得到相应的结果，所以称为交互型

### 编译型运行

> - 创建一个js的文件
- cd进去nodejs所在的文件夹目录  -> node node.js       
**注** 对js文件进行解析和执行，如果说想在命令行看到结果，必须手动输出
