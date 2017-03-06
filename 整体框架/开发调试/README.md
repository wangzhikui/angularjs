# 开发调试

##启动服务
服务启动文件为gulpfile.js，内部还导入了其他需要执行的任务，其他任务位于gulp目录下。
```
$ gulp
```
此步命令会执行bower库插入、编译JS、编译CSS、编译HTML任务，然后启动服务器。
##单独编译JS
```
$ gulp js
```
##单独编译CSS
```
$ gulp css
```
##单独编译HTML
```
$ gulp html
```

##单独进行Bower构建
```
$ gulp bower
```

##单独启动服务器
```
$ gulp serve
```