# 编译HTML
参见示例项目 gulp/html.js，该段代码包含HTML复制到构建目录、构建文件清理，HTML文件监听。

##构建HTML命令
包含复制到构建目录、构建文件清理，HTML文件监听任务。
```
$ gulp html
```

##仅执行HMTL构建命令
包含清除已构建JS文件、构建JS。
```
$ gulp html:build
```
##示例代码
```
'use strict';

/**
 * 1. 复制HTML文件到build目录
 * 2. 监听HTML文件变化并及时编译
 */

var config = require("./conf");
var serve = require("./serve");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var $ = require("gulp-load-plugins")();


/**
 * 复制HTML文件
 */
gulp.task("html:build", ["html:clean"], function(){
	gulp.src(config.paths.srcHtml)
		.pipe(gulp.dest(config.paths.build));
});


/**
 * 清除已构建的HTML文件
 */
gulp.task("html:clean", function(cb){
	rimraf(config.paths.buildHtml, cb);
});


/**
 * 监听HTML文件变化并及时重构
 */
gulp.task("html:watch", function(){
	gulp.watch(config.paths.srcHtml, function(){
		$.runSequence("html:build", "serve:reload");
	})
});


/**
 * 定义对外暴漏的任务名
 */
gulp.task("html", ["html:build", "html:watch"]);
```
