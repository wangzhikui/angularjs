#Gulp构建

下面演示如何使用Gulp进行项目构建，构建代码已存在于示例项目中。

##整体目录结构
```
—— gulpfile.js
—— /gulp
  —— conf.js     // 构建配置信息
  —— js.js       // JS构建
  —— css.js      // CSS构建
```

##JS构建示例(js.js)
```
var config = require("./conf");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var $ = require("gulp-load-plugins")();


gulp.task("js", ["clean:js"], function(){
	gulp.src(config.paths.srcJs)
		.pipe($.babel({
				presets: ['es2015']
			}))
		.pipe($.if(config.system.compressed, $.uglify()))
		.pipe(gulp.dest(config.paths.build));
});


gulp.task("clean:js", function(cb){
	rimraf(config.paths.buildJs, cb);
});


gulp.task("watch:js", function(){
	gulp.watch(config.paths.srcJs, ["js"]);
});


gulp.task("build:js", ["js", "watch:js"]);
```

##CSS构建示例(css.js)
```
var config = require("./conf");
var path = require("path");
var gulp = require("gulp");
var rimraf = require("rimraf");
var $ = require("gulp-load-plugins")();


gulp.task("css", ["clean:css"], function(){
	var cssFilter = $.filter("**/*.scss");
	gulp.src(config.paths.srcCss)
		.pipe($.sass({ outputStyle: 'expanded'}).on('error', $.sass.logError))
		.pipe($.autoprefixer({
			browsers : ["last 2 version", "Android >= 4.0", "Firefox >= 4.0", "Explorer >= 6"],
			cascade : true}))
		.pipe($.if(config.system.compresses, $.minifyCss()))
		.pipe(gulp.dest(config.paths.build));
});


gulp.task("clean:css", function(cb){
	rimraf(config.paths.buildCss, cb);
});


gulp.task("watch:css", function(){
	gulp.watch(config.paths.srcCss, ["css"]);
})


gulp.task("build:css", ["css", "watch:css"]);
```


##配置文件示例(conf.js)
```
exports.paths = {
	src : "app"						// 源文件目录
	,build : "build"				// 构建目录
	,srcCss : "app/**/*.scss"		// CSS文件路径
	,buildCss : "build/**/*.css"	// CSS构建路径
	,srcJs : "app/**/*.js"			// 源JS文件路径
	,buildJs : "build/**/*.js"		// JS构建路径
}

exports.system = {
	debug : true,		// 是否是调试状态
	compressed : false	// 是否压缩JS、CSS、HTML
}
```

##入口文件(Gulpfile.js)
```
'use strict';

var css = require("./gulp/css");
var js = require("./gulp/js")
var gulp = require("gulp");

gulp.task("default", ["build:js", "build:css"]);
```