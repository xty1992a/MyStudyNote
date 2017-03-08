##CMD规范

**概论**
CMD可说是AMD与CommenJS的糅合,相当于在浏览器端使用类似AMD的方式创建了一个可以使用CommenJS规范的环境;

它同样也是专门用于浏览器端,异步加载模块的模块规范,它相对于AMD规范的特点还在于它的模块不会立即执行,而是只有被调用时才会执行;

CMD的具体实现是Sea.js

以下示例文件结构如下
```
|-js
|-libs
  |-sea.js
|-modules
  |-module1.js
  |-module2.js
  |-module3.js
  |-module4.js
  |-main.js
|-index.html
```
1.首先将sea.js引入项目;
`js/libs/sea.js`

**2.基本语法**
sea.js同样使用defined()包裹整个模块,参数为一个回调函数;

- 模块定义
	
	函数的参数为`require`,`exports`,`module`;
	这三个对象将用于引入和暴露模块,是用于模块间通信的桥梁;
	函数内部语法十分类似CommenJS,同样使用require引入模块,使用exports和module.exports暴露方法;
	同时,require增加了一个用于异步引入模块的.async()方法,参数一为模块路径,参数二为回调函数,形参将会引入模块,回调函数内部可以调用该模块
	```
	define(function (require, exports, module) {
	  //引入依赖模块(同步)
	  var module2 = require('./module2')
	
	  function show() {
	    console.log('module4 show() ' + module2.msg)
	  }
	
	  exports.show = show
	  //引入依赖模块(异步)
	  require.async('./module3', function (m3) {
	    console.log('异步引入依赖模块3  ' + m3.API_KEY)
	  })
	})
	```
- 主文件设置
	与模块设置基本相同,只是主文件不需要向外暴露,回调函数只需要一个require参数即可
```
    define(function (require) {
      var m1 = require('./module1')
      var m4 = require('./module4')
      m1.show()
      m4.show()
    })
```

- 页面内引入
	引入sea.js,创建模块运行环境,提供全局函数,全局变量等;
	使用seajs变量调用use()方法,参数为主文件路径
```
  <script type="text/javascript" src="js/libs/sea.js"></script>
  <script type="text/javascript">
    seajs.use('./js/modules/main')
  </script>
```

