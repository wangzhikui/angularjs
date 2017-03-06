# 编译CSS

参见示例项目 gulp/css.js，该段代码包含SASS转义，CSS浏览器兼容前缀添加，构建文件清理，CSS文件监听。

##执行编译CSS命令
包含清除已构建CSS文件、构建CSS、监听CSS文件任务。
```
$ gulp css
```

##仅执行CSS构建命令
包含清除已构建JS文件、构建JS。
```
$ gulp css:build
```

##示例代码
```
'use strict';

/**
 * 1. 构建CSS文件
 * 	• 编译SASS文件
 *  • 自动为CSS添加浏览器兼容前缀
 *  • 压缩CSS
 * 2. 监听CSS文件变化并及时编译
 */

var config = require("./conf");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var $ = require("gulp-load-plugins")();

/**
 * 构建CSS文件
 */
gulp.task("css:build", ["css:clean"], function(){
	var cssFilter = $.filter("**/*.scss");
	gulp.src(config.paths.srcCss)
		.pipe($.sass({ outputStyle: 'expanded'}).on('error', $.sass.logError))
		.pipe($.autoprefixer({
			browsers : ["last 2 version", "Android >= 4.0", "Firefox >= 4.0", "Explorer >= 6"],
			cascade : true}))
		.pipe($.if(config.system.compresses, $.minifyCss()))
		.pipe(gulp.dest(config.paths.build));
});


/**
 * 清除已构建的CSS文件
 */
gulp.task("css:clean", function(cb){
	rimraf(config.paths.buildCss, cb);
});


/**
 * 兼容CSS文件的变化并及时重构
 */
gulp.task("css:watch", function(){
	gulp.watch(config.paths.srcCss, function(){
		$.runSequence("css:build", "serve:reload");
	});
})


/**
 * 定义对外暴漏的任务名
 */
gulp.task("css", ["css:build", "css:watch"]);

```