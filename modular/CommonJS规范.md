##模块化

开发过程中,如果代码全部写在一个文件里,阅读体验很差,而且不便于维护,所以引入了模块化的概念,即:
将一个高耦合的长文件拆分为多个功能模块,分头开发不同的功能,然后通过约定的规范合并到一起共同实现工程需求.
*CommonJS是一套js的模块化规范;*

***概论***
CommonJS规范中,将每个文件作为一个模块,每个模块都有自己的作用域,内部的数据都是私有的.
```
tip:使用`global.warning = true`会暴露整个模块,将其挂载为全局变量
```

CommonJS规定,`module`变量代表当前模块,这个变量是一个对象,它的`exports`属性是对外的接口,加载某个模块,实际上是加载该模块的exports属性.

使用`require()`方法加载模块

```
tips:
> 模块内代码运行在模块作用域,不会污染全局
> 模块可以多次加载,但只会在第一次运行一次,然后引擎会将其缓存,再加载会直接读取缓存
> 模块加载顺序,按其在代码中出现的顺序
```
CommonJS还有另一个重要组成部分,即package.json文件;该文件是对工程的描述,及一些npm命令的封装

CommonJS规范适用于服务器(node.js)及浏览器(browserify);
- 在服务器端,模块会同步动态加载,当require一个包时,node会首先在缓存中找,如果没有再去指定目录找,如果是第三方模块则在当前node_module文件夹下寻找,如果没有则在上一层试图找node_module文件夹,一直找到根目录为止;

- 在浏览器端,不能直接使用CommonJS语法,需要使用browserify将多个模块重新打包为一个js文件,然后再提供给浏览器;

***基本语法***
* **package.json**
	package.json是对包的描述文件
	```
	name:"myProject",		  //指定包的名字,
	version: "1.0.0",		  //指定包的版本;	//这两项即可定位一个包,确定一个包的标识;
	
	script:  {				 //值为一个'对象',封装了一些npm指令
		"start":"node ./bin/app.js"		//使用npm run start 即可使用node调用app.js
	}			
	```


* **node**
node.js是CommenJS的具体实现,模块间使用`module.exports`,`exports.name`暴露方法,使用`require('./module.js')`引入模块;
这种方式是同步进行的,所以不适用于浏览器端
`*当执行到某个功能需要引用某个模块,如果临时请求该模块,等待模块功能返回期间的白屏是不能接受的`
	- 暴露方法
	```
	//module.js
	module.exports = {
		foo:function(){
			console.log('foo()')
		},
		bar:function(){
			console.log('bar()')
		}
	}
	```

	- 引入模块
	```
	var module = require('./module/module.js')
	
	module.foo()
	module.bar()
	```


* **browserify**

	1.安装browserify
	`npm install browserify -g`或`npm install browserify --save-dev`

	2.使用npm命令,合并模块组为一个主文件js(使用browserify 读取js/src/app.js,输出为js/dist/bundle.js)
	`browserify js/src/app.js -o js/dist/bundle.js		//-o output`
	
	3.页面使用`<script>`标签引入js/dist/bundle.js即可
```
tip:
	简单来说,browserify就是一个用于打包遵循commonJS规范的模块化工程的工具,可以生成一个单独的主程序js文件
```

	browserify文件结构
	```
	  |-js
	    |-dist //打包生成文件的目录
	    |-src //源码所在的目录
	      |-module1.js
	      |-module2.js
	      |-module3.js
	      |-app.js //应用主源文件
	  |-index.html
	  |-package.json
	    {
	      "name": "browserify-test",
	      "version": "1.0.0"
	    }
	```