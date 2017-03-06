# 编译Bower
参见示例项目 gulp/bower.js，该段代码包含将Bower管理的库插入到HTML、复制Bower库到构建目录、清除构建目录中的Bower文件。

##示例代码
```
'use strict';

/**
 * 1. 将Bower管理的库插入到HTML
 */
var config = require("./conf");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var wiredep = require("wiredep").stream;


/**
 * 移动Bower管理的库到项目的生成目录下
 */
gulp.task("bower:move", ["bower:clean"], function(){
	gulp.src(path.join(config.paths.srcBower, "**/*"), {base : './'})
		.pipe(gulp.dest(config.paths.buildTmp));
});


/**
 * 插入Bower管理的库插入到HTML
 */
gulp.task("bower:insert", function(){
	gulp.src(config.paths.srcHtml)
		.pipe(wiredep({
	    	ignorePath: '../'
	    }))
		.pipe(gulp.dest(config.paths.src));
});


/**
 * 清除已移动的目录文件
 */
gulp.task("bower:clean", ["bower:insert"], function(cb){
	rimraf(config.paths.buildBower, cb);
});


/**
 * 定义对外暴漏的任务名
 */
gulp.task("bower", ["bower:move"]);

```