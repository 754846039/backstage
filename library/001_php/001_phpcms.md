# phpcms
[phpcms下载地址     http://bbs.phpcms.cn/thread-936338-1-1.html](http://bbs.phpcms.cn/thread-936338-1-1.html)<br>
[phpcms帮助文档  http://v9.help.phpcms.cn/](http://v9.help.phpcms.cn/)<br>
[phpcms安装文档  http://v9.help.phpcms.cn/html/install/](http://v9.help.phpcms.cn/html/install/)

- phpcms、phpAdmin基于php开发的
- phpcms账号：15935487645 密码123456
- PHPCMS V9采用PHP5+MYSQL作为基础进行开发

## 安装
- www目录下新建一个项目
- 将其中 install_package文件夹中的内容剪切到项目目录下
- 在地址栏打开安装程序`localhost/项目文件夹名称/install`
- 创建数据库
- 安装配置
  - 选择模块-->全新安装（包含PHPSSO）
  - 端口：3306不改
  - 数据库账号：root
  - 数据库密码：空  
  - 数据库名称：已创建好的数据库名
  - phpcms账号：admin
  - phpcms密码：名字
- 安装完毕请登录后台生成首页，更新缓存
- 默认phpcms管理员密码与phpsso管理员密码相同
- 为了您站点的安全，安装完成后即可将网站根目录下的“install”文件夹删除。


  admin.php后台管理系统
  index.php网站入口

## 主要目录结构
- caches(缓存)
  - configs
    - system.php(站点配置)
    - database.php(数据库配置)
- phpcms(网站核心内容)
  - libs(框架主类库、主函数库目录)
- phpcms(网站核心内容)
  - templates(存放所有模板)
  - default>content>html
- statics(静态文件)
  - css
  - images
  - js


## 后台数据管理
[后台网址：http://localhost/gs-phpcms/install_package/admin.php](http://localhost/gs-phpcms/install_package/admin.php)
- 内容
  - 管理栏目
    - 添加栏目（可设置是否在导航显示，缩略图为唯一的）
  - 管理内容
    - 添加文章

## 整站
### 网页的逻辑结构
- 首页-->导航-->列表-->详情
- 首页-->一级导航-->二级导航-->列表-->详情

### 步骤
> 一级导航点击进入category页面，二级导航点击进去list页面，继续点击进入show页面

1. 首先将网页拆分成头部和底部，头部包含所有网页中头部公共部分，底部包含所有网页中底部公共部分，同时把相对应的js,css,html分开
2. 引入头部和尾部

引入头部 `{templates "content","header"}`<br>
引入底部 `{templates "content","footer"}`

3. 静态常量
- 在static中的css/js/images文件中新建mycss/myjs/myimg
  - `{CSS_PATH}mycss/...` 默认CSS路径（设置-->基本设置-->路径）
  - `{JS_PATH}myjs/...`
  - `{IMG_PATH}myimg/...`

4. 更换地址：用到静态常量
```html
{pc:content  action="category" catid="0" num="10" siteid="$siteid" order="listorder ASC" moreinfo="1"}
{loop $data $v}
<a href="$v[url]" class="{if $catid==$v[catid]}show{/if}">{$v[catname]}</a>
{/loop}
{/pc}
```

### 语法
#### pc标签的作用：定义要操作的事情
- action：决定获取的内容是栏目 category表导航，lists表列表页
- catid：要操作的栏目id(0代表首页，$catid表示当前页)
- num：决定最大的单页输出个数
- siteid：操作的站点（一般是一个网站，站点就是当前的站点）
- order：排序规则  
  - listorder ASC（以取出来的列表顺序排列，以升序排列）
  - listorder DESC（以取出来的列表顺序排列，以降序排列）
- moreinfo="1"：可以在非show页面获取内容

#### loop作用是循环输出
- $data	保存所有取回的数据，会有很多行，同时也决定了循环次数
- $v	每次进行loop输出的时候，当前行的数据保存在 $v这个变量上
- $n	默认变量，记录第几次输出
>loop标签中间的内容(html)会每次循环输出

#### {if}{else}{/if}
```html
<a class="{if $catid==0}active{/if}">
<div class="">
{if $catid==10} 1 {elseif $catid==11} 2 {else} 3 {/if}
</div>
```

#### 获取上上级父元素
- 上上级栏目名称<br>
`{$CATEGORYS[$CATEGORYS[$CAT[parentid]][parentid]][catname]}`
- 上上级栏目链接<br>
`{$CATEGORYS[$CATEGORYS[$CAT[parentid]][parentid]][url]}`

#### 取父级栏目的信息
- 栏目名字<br>
`{$CATEGORYS[$top_parentid][catname]}`
- 栏目图片<br>
`{$CATEGORYS[$top_parentid][image]}`
- 栏目地址<br>
`{$CATEGORYS[$top_parentid][url]}`
- 栏目栏目id<br>
`{$CATEGORYS[$top_parentid][catid]}`

#### 当前栏目的上级栏目id
- `{$CAT[parentid]}`
- `{$top_parentid}`
- `{$CATEGORYS[$catid][parentid]}`
- `{$CATEGORYS[$top_parentid][catid]}`

#### 取当前栏目的信息
- 当前栏目描述<br>
`{$CATEGORYS[$catid][description]}`
- 当前栏目链接<br>
`{$CATEGORYS[$catid][url]}`
- 当前栏目名称<br>
`{$CATEGORYS[$catid][catname]}或{$catname}`
- 当前栏目目录名<br>
`{$CATEGORYS[$catid][catdir]}`
- 当前栏目的点击数<br>
`{$CATEGORYS[$catid][hits]}`
- 当前栏目id<br>
`{$catid}`
- 当前站点<br>
`{$siteid}`

#### 获取某个指定栏目的信息
- `{$CATEGORYS[指定栏目的id][url]}`
- `{$CATEGORYS[指定栏目的id][catname]}`

#### 取show页面的信息
- 当前文章题目<br>
`{$title}`
- 当前文章内容<br>
`{$content}`
- 当前文章来源<br>
`{$copyfrom}`
- 当前文章发布时间<br>
`{$inputtime}`
- 当前文章作者<br>
`{$username}`
- 当前文章描述<br>
`{$discription}`
- 当前文章缩略图<br>
`{$thumb}`

#### 其他
- 回到首页<br>
`<a href="{siteurl($siteid)}"></a>`
- 输出内容<br>
`<?php var_dump($r) ?>`
- 定义变量<br>
`{php $i=0}（html可以嵌套php）`
- 在非show页面获取内容时,需在pc标签里设置<br>
`moreinfo="1"`
- 发表时间的格式化<br>
`{date('Y-m-d H:i:s',$r[inputtime])}`
- 获取栏目图片（保存在一级导航唯一的图片）,CSS中背景图只能是相对路径，且不能从数据库获取，如果背景图要使用栏目图片，需要写在行内样式中<br>
`style="background：url('{$CATEGORYS[$top_parentid][image]}')"`
- 面包屑导航<br>
`{catpos($catid)}如果要更改，可以修改源代码（php）或者通过JS更改`
- 分页<br>
`{$pages}在pc标签里设置page="$page"`
- 总点击排行榜：<br>
```html
{pc:content  action="hits" catid="$catid" num="10" order="views DESC" cache="3600"}
{loop $data $v}
<a href="$v[url]" class="{if $catid==$v[catid]}show{/if}">{$v[catname]}</a>
{/loop}
{/pc}
```

- 月点击排行榜<br>
`order="monthviews DESC"`
- 上一篇 下一篇<br>
```html
<strong>上一篇：</strong><a href="{$previous_page[url]}">{$previous_page[title]}</a><br />
<strong>下一篇：</strong><a href="{$next_page[url]}">{$next_page[title]}</a>
```

- PC嵌套取二级栏目
```
{pc:content action="category" catid="0" num="10"}
{php $i=0}
{loop $data $r}
{pc:content action="category" catid="$r[catid]" num="10"}
{loop $data $v} {/loop}
{/pc}
{/loop}
{/pc}
```

* 架构、接口、前后端分离
