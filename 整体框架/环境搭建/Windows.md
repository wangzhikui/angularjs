# Windows环境搭建



## 基础环境

1. Node：基础环境
2. Gulp：项目自动化管理工具
3. Bower：资源管理工具，如下载、卸载JS、CSS，类似于npm
4. Compass[或SASS]：css编译工具
5. Ruby：Compass是用Ruby语言开发的，所以安装它之前，必须安装Ruby环境
6. Yeoman：项目自动化生成工具

## 安装过程

1. 安装Node：（自带npm）
2. 安装bower ：npm install -g bower
3. 安装Gulp ：npm install -g gulp
4. 安装ruby ：http://rubyinstaller.org/downloads/
5. 安装Compass[或SASS]： gem install compass
6. 安装yo ：npm install -g yo

## 详细安装说明

### nodejs安装
```
运行：node-v5.10.1-x64.msi
下载地址：https://nodejs.org/en/
Nodejs安装完成后默认安装了npm
npm：https://www.npmjs.com/
运行：CMD或者powershell
输入：node –v  和  npm –v
可以查看当前nodejs的版本以及相应的npm的版本```

### 全局安装包管理工具bower

```说明：一个客户端技术的软件包管理器，它可用于搜索、安装和卸载如JavaScript、HTML、CSS之类的网络资源。
Bower安装包使用的是git命令从github上下载，所以需要在本地安装git环境。（查看之前git沙龙分享的资料）
运行CMD或powershell，执行：npm install –g bower
-g表示全局安装
**本地安装与全局安装**
**本地安装**
1. 将安装包放在 ./node_modules 下(运行npm时所在的目录)
2. 可以通过 require() 来引入本地安装的包
**全局安装**
1. 将安装包放在 /usr/local 下
2. 可以直接在命令行里使用
我们需要在命令行使用bower命令，所以这里选择全局安装
具体地址可查看安装结果
C:\Users\Administrator\AppData\Roaming\npm\node_modules
**安装过程**
运行命令安装完成后输入bower –v 查看版本
Bower简明入门教程：https://segmentfault.com/a/1190000002971135
官网：http://bower.io/```

### 全局安装gulp

npm install –g gulp
安装ruby
下载地址：http://rubyinstaller.org/downloads/
 
下载与操作系统相关版本，测试机器为win7 64所以下载的是
2.3.0（x64）
 
选中Add Ruby executables to yourPATH
安装完成后重开一个powershell或cmd输入命里gem –v
 
显示当前gem版本则表示安装成功
安装compass
安装成功ruby后再安装compass
执行命里：gem install compass
请阅读常见问题说明中gem使用

### 使用yeoman搭建项目


```使用npm安装yeoman命令行程序yo
运行：npm install –g yo
CMD或者powershell进入到项目目录运行命令：yo
 

选择生成器-webapp
 
这里去掉modernizr和sass，选择sass的会会安装未编译的sass版bootstrap回车即开始安装，安装过程需要一定的时间。
安装结束后主要目录说明
App：应用文件目录，html,js,css，image等
Bower_components:bower管理的包存放路径
Node_modules：yo构建项目时下载的外部模块（组件）
Test：测试逻辑存放目录
.bowerrc：bower管理的包存放路径配置文件
.bower.json：配置bower依赖关系配置文件
Gulpfile.js：构建工具gulp配置文件
Package.json：nodejs+npm配置文件

更改项目配置
经过上述操作，一个工程基本成型，更具实际需要做一些配置
更改bower管理的依赖包
构建的项目中bower_comonents中含有jquery包但是bower.json中没配置信息
更新jquery
打开cmd或者powershell
进入项目路径
 
执行命令：bower install jquery –save
重新安装一下jquery 并使用-save参数，将依赖信息保存到bower.json文件中或者直接修改bower.json
{
  "name": "umcdemo",
  "private": true,
  "dependencies": {
    "bootstrap-sass": "~3.3.5",
    "jquery": "^2.2.4"
  },
  
在dependencies中添加
“jquery”：“^2.2.4”
然后运行bower update
查看bootstrap包路径下的bower.json
"dependencies": {
  "jquery": ">= 1.9.0"
},
依赖的jquery版本需要>=1.9默认安装的是2.2.4版本，我们的项目使用1.x版本，
目前1.x版本最高为1.12.4某一个开源框架的版本可以使用命令bower info jquery
 
这里我们更改项目的bower文件
{
  "name": "umcdemo",
  "private": true,
  "dependencies": {
    "bootstrap-sass": "~3.3.5",
    "jquery": "^2.2.4"
  },
修改jquery版本为1.12.4
执行命里bower update
删除chai和mocha
我们这里并不需要chai和mocha所以执行命令卸载
bower uninstrall chai
bower uninstrall mocha
删除项目bower.json中
"devDependencies": {
  "chai": "^3.5.0",
  "mocha": "^2.5.3"
}```

### 安装angularjs和requirejs


```执行命里
bower install angulajs –save
bower install requires –save```

### 常见问题


```gem安装compass包括
由于天朝网络原因，连接不上默认的库https://rubygems.org/
可使用淘宝镜像，目前维护gem镜像的是ruby-china团队
使用如下命令
gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/
 
输入gem sources –l查看确保来源只有这一个
安装compass
gem install compass```

