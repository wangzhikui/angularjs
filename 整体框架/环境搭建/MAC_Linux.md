# MAC Linux环境搭建
##1.基础环境
```
Node               //基础环境
Gulp		       //项目自动化管理工具
Bower		       //资源管理工具，如下载、卸载JS、CSS，类似于npm
Compass[或SASS]    //css编译工具
Yeoman		       //项目自动化生成工具[使用示例项目，可以省略]
```


##2.安装过程

```
1. 安装或升级Node
2. 安装Gulp
    npm install -g gulp
3. 安装bower
    npm install -g bower
4. 安装Compass[或SASS]
    gem install compass
5. 安装yo [使用示例项目，该步骤可省略]
    npm install -g yo
    5.1安装angular生成器
        npm install -g generator-angular
```

##3.创建项目

###3.1使用示例项目
[示例项目](https://qiyeyun.gitbooks.io/angular/content/%E6%95%B4%E4%BD%93%E6%A1%86%E6%9E%B6/Gulp%E9%A1%B9%E7%9B%AE%E6%9E%84%E5%BB%BA/%E7%A4%BA%E4%BE%8B%E9%A1%B9%E7%9B%AE.html)

###3.2使用Yeoman创建项目
```
1.选择项目目录
    $ mkdir web && cd web
2.yo创建项目
    $ yo
3.更改项目目录结构
    按项目模块化更改目录结构
4.更改package.json并初始化
    更改需要的Gulp构建插件
5.更改bower.json并初始化
    更改需要的组件依赖
6.执行项目
    $ gulp
```
##4.常见问题

```
1. compass无法找到
    切换gem源
        gem sources --add http://gems.ruby-china.org/ --remove https://rubygems.org/
        gem sources -l
        gem install compass
```
	