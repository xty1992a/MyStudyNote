##AMD规范
AMD(Asynchronous Module Definition 异步模块定义)是用于在浏览器端异步加载模块的规范,它具体实现是Require.js;

以下例子遵循如下文件结构
```
  |-js
    |-libs
      |-require.js
    |-modules
      |-alerter.js
      |-msgData.js
    |-main.js
  |-index.html
```
<br>

**定义模块**
	模块内容全部写在全局函数define()中,使用return暴露方法;
	defined()函数的参数为一个回调函数或者一个依赖包的数组,视具体情况决定
- 无依赖包:
```
//msgData.js
define(function(){
	let msg = 'hello world'
	function getMsg(){
		return msg.toUpperCase()
	}
	retrun {getMsg}	//ES6语法
})
```
- 有依赖包
```
//alerter.js
define(['msgData'], function(msgData){
	let name = 'tom'
	function showMsg(){
		alert(name + ' say: ' + msgData.getMsg())
	}
	retrun {showMsg}
	})
```
<br>

**主文件设置**
	这是一个IIFE自调用匿名函数;
	在主文件中,首先需要设置模块映射,然后再引入模块;
	`如果主文件与模块文件在同一文件夹,可以不需要设置模块映射`
```
//main.js
(function () {
//配置
require.config({
  //基本路径
  baseUrl: "js/",
  //模块标识名与模块路径映射
  paths: {		//基于基本路径定位
    "alerter": "modules/alerter",		//require.js会自动添加'.js',如果加上会报错
    "dataService": "modules/dataService",
  }
})

//引入使用模块
require( ['alerter'], function(alerter) {
  alerter.showMsg()
})
})()
```
- 建立模块名映射
	使用require.config()方法设置配置对象,将其作为参数传入;
	该对象中,使用`baseUrl`设置基本路径,该路径将作为后续所有模块定位位置;
	使用`paths`对象设置各模块名,与其对应的路径;
- 引入模块
	使用`require()`方法引入模块,第一个参数为模块数组,该数组将作为形参传入第二个参数,一个回调函数中,位置必须一一对应,在回调函数中,模块将被作为对象使用
	`模块数组的顺序不作要求,require.js会自动处理它们的依赖关系`
<br>

**页面引入**

依照AMD规范定义好模块之后;使用`<script>`标签引入require.js.`data-main`属性指向模块的主文件.
```
<script data-main="js/main" src="js/libs/require.js"></script>
<script type="text/javascript">
    seajs.use('./js/modules/main');
</script>

```
<br><br><br>
----
<br>
**引入第三方框架**

- 基于AMD规范的库文件,如:jQuery
	- 将jQuery文件引入项目
	`js/libs/jquery-1.10.1.js`
	- 在主文件main.js中配置jquery路径
```
paths:{
	'jquery':'libs/jquery-1.10.1'
}
```
	- 在alerter.js中使用jQuery
```
//alerter.js
define(['msgData', 'jquery'], function(msgData){
	let name = 'tom'
	function showMsg(){
		$('body').css({background, 'red'})		//使用jquery语法
		alert(name + ' say: ' + msgData.getMsg())
	}
	retrun {showMsg}
	})
```
	*注意事项:jquery内部有检测当前是否是AMD环境,已经对AMD环境进行了模块引入,名为jquery,所以必须使用`jquery`*

- 不基于AMD规范的库,如:angular及其插件
	- 首先导入angular文件
 		`js/libs/angular.js`
    	`js/libs/angular-messages.js`

	- 配置main.js
		- 配置paths
```
paths:{
	'angular': 'libs/angular',
	'angular-messages': 'libs/angular-messages'
}
```		
		- 包装不兼容AMD的模块
```
shim:{
	'angular': {
		exports: 'angular'		//指定导出模块名
	},
	'angular-messages': {
		exports: 'angular-messages',
		deps: ['angular']		//指定所依赖模块的数组
	}
}
```
		- 引入模块
```
require( ['alerter', 'angular', 'angular-messages'], function(alerter, angular) {
    alerter.showMsg()
    angular.module('myApp', ['ngMessages'])
    angular.bootstrap(document,["myApp"])
  })
})()
```
<br><br><br>