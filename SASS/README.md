# SASS简介

教程地址：[http://www.w3cplus.com/sassguide/](http://www.w3cplus.com/sassguide/)


##node-sass安装问题
安装node-sass时，遇到的错误MSBUILD: error MSB3428 
可以通过下面的方式解决：
使用cnpm来安装node-sass
$ npm install cnpm -g --registry=https://registry.npm.taobao.org
$ cnpm install node-sass --registry=https://registry.npm.taobao.org

# Sass 学习

### SASS是一种CSS的开发工具，提供了许多便利的写法，大大节省了设计者的时间，使得CSS的开发，变得简单和可维护


### SASS是Ruby语言写的，但是两者的语法没有关系。不懂Ruby，照样使用。只是必须先安装Ruby，然后再安装SASS



### Rudy安装

 * 下载地址：http://rubyinstaller.org/downloads/
 * ruby -v  查看版本
   
### Sass安装
   安装命令：gem install sass
   
   安装成功
  scss文件转css
  sass style.scss style.css
  --watch监听某个文件或目录一旦源文件有变动，就自动生成编译后的版本
  sass --watch app/sass:public/stylesheets

  css转sass/scss
  http://css2sass.herokuapp.com/
  scss转css
  http://www.sassmeister.com/
  
  Compass是Sass的工具库，Compass在它的基础上，封装了一系列有用的模块和模板，补充Sass的功能
  compass使用方法：
  安装：gem install compass
  创建项目：compass create myproject(项目名称)
  编译：compass compile(需要到根目录下)
       compass compile --output-style compressed(生产压缩后的css)
       compass compile --force
       Compass只编译发生变动的文件，如果你要重新编译未变动的文件，需要使用--force参数。
       compass compile --force
       compass watch 运行该命令后，只要scss文件发生变化，就会被自动编译成css文件
  参考地址：
  http://www.ruanyifeng.com/blog/2012/11/compass.html
  
  sass 有两种后缀名文件：一种后缀名为 sass，不使用大括号和分号；另一种后缀为scss 的文件，这种和我们平时写的 css 文件格式差不多，使用大括号和分号。在此也建议使用后缀名为 scss 的文件，以避免 sass 后缀名的严格格式要求报错。
  
## Sass特性
*
###  使用变量
sass使用$符号来标识变量
变量可以在css规则块定义之外存在
变量值也可以引用其他变量
反复声明一个变量，只有最后一处声明有效且它会覆盖前边的值
默认变量 !default
$link-color: blue;
$link-color: red !default;
a {
color: $link-color;//blue
}
如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中
$side : left;
.rounded {
　　border-#{$side}-radius: 5px;
}
### CSS嵌套
选择器嵌套
*#content {*
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}

 /* 编译后 */
*#content article h1 { color: #333 }
*#content article p { margin-bottom: 1.4em }
*#content aside { background-color: #EEE }

既可以像普通的CSS那样包含属性，又可以嵌套其他规则块
*#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
 * #content aside { background-color: #EEE }*
}

 /* 编译后 */
*#content article h1 { color: #333 }*
*#content article p { margin-bottom: 1.4em }
*#content aside { background-color: #EEE }

父选择器&
article a {
  color: blue;
  &:hover { color: red }
}
/* 编译后*/
article a { color: blue }
article a:hover { color: red }

属性嵌套
nav {
  border: 1px solid #ccc {
  left: 0px;
  right: 0px;
  }
}
编译后
nav {
  border: 1px solid #ccc;
  border-left: 0px;
  border-right: 0px;
}

###计算功能
SASS允许在代码中使用算式：
body {
　　margin: (14px/2);
　　top: 50px + 100px;
　　right: $var * 10%;
}

### 注释
SASS共有两种注释风格。
标准的CSS注释 /* comment */ ，会保留到编译后的文件。
单行注释 // comment，只保留在SASS源文件中，编译后被省略。
在/*后面加一个感叹号，表示这是"重要注释"。即使是压缩模式编译，也会保留这行注释，通常可以用于声明版权信息
/*! 。。。*/

### 导入SASS文件
sass:@import规则在生成css文件时就把相关文件导入进来,import的导入文件可以不写后缀
sass 使用@import "foo.css";等同于css的import
嵌套导入
.blue-theme {@import "blue-theme"}
下列三种情况下会生成原生的CSS@import，尽管这会造成浏览器解析css时的额外下载
1. 被导入文件的名字以.css结尾；
2. 被导入文件的名字是一个URL地址（比如http://www.sass.hk/css/css.css），由此可用谷歌字体API提供的相应服务；
3. 被导入文件的名字是CSS的url()值
解决方法可以直接把css后缀改成scss


### 继承

SASS允许一个选择器，继承另一个选择器
.class1 {
　　　　border: 1px solid #ddd;
　　}
 .class2 {
　　　　@extend .class1;
　　　　font-size:120%;
　　}

### Mixin混合器
混合器使用@mixin标识符定义
@mixin left {
　　　　float: left;
　　　　margin-left: 10px;
　　}
  使用@include命令，调用这个mixin。
  div {
　　　　@include left;
　　}
  mixin的强大之处，在于可以指定参数和缺省值
  @mixin left($value: 10px) {
　　　　float: left;
　　　　margin-right: $value;
　　}
  使用的时候，根据需要加入参数：
  div {
　　　　@include left(20px);
　　}
  
### 自定义函数
SASS允许用户编写自己的函数
　@function double($n) {
　　　　@return $n * 2;
　　}
　*　#sidebar {
　　　　width: double(5px);
　　}






参考地址：http://www.ruanyifeng.com/blog/2012/06/sass.html
         http://www.sasschina.com/guide/
         http://www.w3cplus.com/sassguide/debug.html
         http://www.sass.hk/sass-course.html
         http://www.w3cplus.com


