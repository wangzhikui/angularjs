# 编译JS

参见示例项目 gulp/js.js，该段代码包含ES6转义，JS压缩，构建文件清理，JS文件监听。

##执行编译JS命令
包含清除已构建JS文件、构建JS、监听JS文件任务。
```
$ gulp js
```

##仅执行JS构建命令
包含清除已构建JS文件、构建JS任务。
```
$ gulp js:build
```

##示例代码
```
'use strict';

/**
 * 1. 构建JS文件
 * 	• 编译JS
 *  • 压缩JS
 * 2. 监听JS文件变化并及时编译
 */

var config = require("./conf");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var $ = require("gulp-load-plugins")();


/**
 * 构建JS文件
 */
gulp.task("js:build", ["js:clean"], function(){
	gulp.src(config.paths.srcJs)
		.pipe($.babel({
				presets: ['es2015']
			}))
		.pipe($.if(config.system.compressed, $.uglify()))
		.pipe(gulp.dest(config.paths.build));
});


/**
 * 清除已构建的JS文件
 */
gulp.task("js:clean", function(cb){
	rimraf(config.paths.buildJs, cb);
});


/**
 * 1. 监听JS文件变化并及时重构
 * 2. 重启静态服务器
 */
gulp.task("js:watch", function(){
	gulp.watch(config.paths.srcJs, function(){
		$.runSequence("js:build", "serve:reload");
	});
});

/**
 * 定义对外暴漏的任务名
 */
gulp.task("js", ["js:build", "js:watch"]);

```