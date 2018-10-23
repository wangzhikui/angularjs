# 基于requireJS和angularJS的前端技术架构

1、概要描述  
1.1、angularJS描述:angularJS是可以用来构建WEB应用的，WEB应用中的一种端对端的完整解决方案。通过开发者呈现一个更高层次的抽象来简化应用的开发。最适合的就是用它来构建一个CRUD应用，它提供了非常方便的且统一高效的解决方案，其数据绑定、基本模版标识符、表单验证、路由、深度链接、组件重用、依赖注入、以及HTML标记等，最受欢迎的莫过于它的双向数据绑定。

1.2、requireJS描述:requireJS是来解决传统的页面加载script标记操作，通过其初始化配置实现按需、并行、延时的载入js库，声明不同js文件之间的依赖关系，它是遵循前端AMD规范\(异步模块加载\)。js代码可以以模块化的方式进行组织\(模块化编程\)。模块化的意义就是通过代码逻辑表明模块之间的依赖关系和执行顺序，按照模块逻辑来分解代码，起到配合mvc框架架构项目的作用。

1.3、整合：使用requireJS模块化定义模块质检的依赖关系，打包不需要文件挨个对照，很方便。将script脚本从模版页面中抽离出来，通过js当前模块加载需要依赖的js模块。按需加载。路由更加方便。

2、设计思想  
2.1、思想：效仿后端MVC架构的基本思想，采用MVVM模式，脱离传统的前后端耦合度太紧思想，采用前后端分离开发的方式，使其维护成本减少开发效率提高。让前端开发人员只需去关注数据和页面的交互，后端人员只需提供数据。

2.2、Rest：rest指的是一组架构约束条件和原则，满足这些约束条件和原则的应用程序或设计就是RestFul。Rest原则就是客户端和服务器之间的交互在请求之间是无状态的，还有一个重要的原则就是分层系统，表示组件无法了解它与之交互的中间层以外的组件。通过将系统知识限制在单个层，可以限制整个系统的复杂性，促进了底层的独立性。rest是一个轻量级的webservice的架构风格，目的就是为了降低开发的复杂性，提高系统的伸缩性。

2.3、原理：angularJS和requireJS集成、其运行原理步骤如下：

基于requireJS和angularJS的前端技术架构 - cl\_xia\_yong - 攻城师

1、初步加载初始页面如index.html，首先加载样式文件，再加载requireJS配置文件和源文件。

2、通过requireJS配置的data-main主函数入口，加载angularJS和应用依赖的js源文件。

3、通过ng.bootstrap\(document, \['app'\]\)手动初始化静态页面使其支持angularJS，ng.resumeBootstrap\(\)延迟引导。

4、经index.html页面配置布局指令,加载smart-device-detect、  smart-fast-click、smart-layout、smart-page-title处理页面以及整体规划布局。

5、通过index.html指定的属性ui-view，通过angularJS的ui-router 插件来动态的切换路由。

6、通过主函数入口main.js注册的应用app.js来注册整个应用程序的各个模块，每个模块中定义各自的路由。

7、定义一个全局依赖的模块如includes.js文件，装载全局应用程序用到的服务、指令以及组件。

8、定义相应的拦截机处理http请求的异常统一操作，如是否登陆，是否拥有该操作权限等。

9、由各自定义的路由去加载相应的模版，相应的controller处理数据提供到模版上显示。

3、设计优缺点  
3.1、优点

3.1.1、angularJS是一种MVVM前端框架,这样就可以完全脱离于后端程序的耦合度，可以完全脱颖而出，前端和后端可以分开部署，分开开发。

3.1.2、angularJS的模块化解决了代码逻辑的耦合性，通过依赖注入使其耦合性很散，从而可以很方便的拆分组合。

3.1.3、模版功能强大丰富，自带丰富的angular指令，也可以自定义指令。

3.1.4、前端的MVVM框架，包含了模版、数据双向绑定，路由，模块化，服务，过滤器，依赖注入等所有功能,前端处理方便。

3.1.5、模块化,维护性高、灵活架构焦点分离、方便模块间组合，分解，单个模块功能调试，升级。

3.1.6、可测试性，可以进行单元测试。

3.1.7、js/css、图片文件压缩合并，提高用户体验。

3.2、缺点

3.2.1、验证功能错误信息显示比较薄弱。

3.2.2、第三方库一起使用不是很便利，需要手动的包装directive。

3.2.3、不适合于频繁操作DOM。

3.2.4、版本升级兼容性不是很好，高版本未能很好的兼容低版本。

3.2.5、系统分层，调用链增长，模块间通信损耗性能。

4、架构实现  
4.1、整体架构说明

```
        该架构采用javascript脚本技术实现，系统架构图如下：
```

基于requireJS和angularJS的前端技术架构 - cl\_xia\_yong - 攻城师

4.2、项目环境搭建

```
       前端完全无需任何依赖工具，一个记事本编辑器即可。需配合后端java开发的 话只需按照java的开发环境建立一个web项目即可，将前端框架搭建好的webapp目录拷贝到web项目的webRoot下面就可以开始开发了。开发完成后采用grunt构建工具打包压缩webapp的js文件。
```

4.3、技术应用

基于requireJS和angularJS的前端技术架构 - cl\_xia\_yong - 攻城师

```
        1、angularJS、整体框架支持者，MVVM模式架构。

        2、requireJS、模块化以及按需加载js文件。

        3、require-domready、采用回调的方式让页面加载完成后运行requireJS。

        4、bootstarp、采用bootstrap样式库。

        5、jquery、jquery文件库，操作DOM元素。

        6、angular-route、路由控制，通过hash和history两种方式实现。

        7、angular-couch-potato、配合ui-router来实现延时按模块加载。

        8、angular-animate、实现动画效果的angular插件。

        9、angular-sanitize、实现html净化的angular插件。

        10、以上为框架的主要源文件，还有大量的插件和组件以及自定义组件等。
```

4.4、框架搭建步骤

```
      1、新建一个webapp的文件夹，在其下面建好对应的文件夹，如api、app、plugin、styles、vendor和入口地址index.html。

     2、准备好angular和require以及所需的插件源文件，存放到vendor目录 下面,最好按功能区分来设置不同的文件夹。通过config.js配置应用依赖的js文件。

     3、定义app所需的功能，建立相应的文件夹，如auth、components、dashboard、layout、modules。定义应用的主函数和应用文件，如main.js、app.js以及抽离的配置文件config.js、includes.js文件。

     4、开始编写index.html，采用标准的html5规范，导入应用需用的样式文件、定义script脚本加载requireJS文件。

     5、定义整体应用的布局，通过angularJS的指令和路由操作。

     6、定义requireJS的配置文件，配置整个应用的依赖关系。

     7、编写主函数入口文件main.js，加载应用程序，启动angular。

     8、编写应用主文件app.js，定义应用的模块，加载模块。配置拦截机。

     9、配置应用的全局依赖includes.js。

     10、规划整体应用的模块、布局以及相关组件和互相的依赖关系。

     11、拦截机验证用户信息，权限信息。

         具体目录说明如图：
```

基于requireJS和angularJS的前端技术架构 - cl\_xia\_yong - 攻城师

4.5、模块开发步骤

```
  1、规划模块的设计，定义前后端套接的数据结构。

  2、在app的modules目录下面定义一个模块如system,然后到system定义一个module.js，定义模块的路由，启动该模块。

  3、定义相应的controller、views、services、directives以及filters。  

  4、到system模块定义views需要的模版文件。

  5、开发system解析模版的controller，后端提供需要的json接口的数据。

  6、如需用到自定义指令和数据过滤器到相应的文件夹下面定义开发。在 module.js文件的路由中指定其依赖的指令和过滤器。

 7、前后端开始数据对接，权限验证。
```

5、构建和压缩  
5.1、Grunt构建工具

5.1.1、简介：Grunt是一个基于任务的JavaScript应用的命令行的自动化的构建工具。它可以用来做压缩、编译、单元测试、代码检查以及打包发布的任务。更智能、更省事，不需重复的进行，特别是大项目中，只需配置好要做的任务即可。

5.1.2、如何构建：Grunt是要配合Node.js一起使用，具体步骤如下：

1、下载nodeJS Server，安装到本地电脑。

2、安装grunt的命令行界面grunt-cli，sudo npm install grunt-cli -g。

3、在应用中建立一个grunt的文件夹，并且配置好一份package.json和 Gruntfile文件。

4、安装grunt模块插件，常用模块有：npm install grunt --save-dev

```
  检查js语法 ： npm install grunt-contrib-jshint --save-dev

  合并文件 ：    npm install grunt-contrib-concat --save-dev

  压缩文件 ：    npm install grunt-contrib-uglify --save-dev

  监控文件 ：    npm install grunt-contrib-watch --save-dev

  删除文件 ：    npm install grunt-contrib-clean --save-dev

  复制文件 ：    npm install grunt-contril-copy --save-dev

  图像压缩 ：    npm insatll grunt-contril-imagemin --save-dev

  压缩合并CSS ： npm install grunt-contril-cssmin --save-dev

save-dev :自动将其添加到devDependencies配置段中，遵循tilde version range格式。
```

5、到应用工程目录下的grunt目录，运行grunt命令。

6、注意事项  
6.1、各模块注入某个服务或某块插件的时候，要注意是否配置了其对应的源文件， 否则会报注入失败。

6.2、angular插件服务的注入名称到各个源文件中可以找到，如源文件中  angular.module\(‘xxx’\)，其中xxx就是服务名称。

