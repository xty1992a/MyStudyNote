#ES6规范化模块
<br><hr><br>

前端js的模块化主流规范是AMD和CMD,及兼容CMD和AMD的UMD;
ES6中,对模块化进行了规范化,但由于浏览器对ES6的支持还不够,所以使用ES6的规范对代码进行模块化处理之后,还需要使用工具(babel)转为遵循ES5语法的模块,然后再使用Browserify合并为一个js主文件实际使用;

***ES6模块化语法***
ES6使用两个关键字`export`,`import`对模块进行引入和暴露;
配合ES6的其他新语法,比如解构赋值,对象省略属性名等可以十分简洁的模块化编写工程;

- **export暴露**
	- 分次暴露(内联导出)
	```
	export function foo(){
		console.log('foo()')
	}
	export let msg = 'hello world'
	let data = 'fuck off'
	export {data}
	```	
	
	- 一次暴露
	```
	function foo(){
		console.log('foo()')
	}
	let arr = [1,2,3,4,5]
	
	export {foo, arr}
	```

	- 导出时重命名
	```
	function foo(){...}
	export { foo as bar }		//引入时如果使用bar才能找到foo()
	```

	- 默认导出(引入时不必加{})	
	```
	function foo(){}
	function bar(){}
	
	export default foo
	//or
	export {foo as default }
	//混合导出
	export {foo as default ,bar}
	```

	- 从其他模块导出
	```
	export {foo, bar} from './bar.js'
	export * from './bar.js'
	export {foo as FOO, bar as BAR} from './bar.js'
	```
<br>

- **import导入**
	- 默认使用`{}`引入其他模块暴露的export对象,`{}`内列举需要使用的命名对象;
	- default对象不需要加`{}`;
	- 没有被列举的对象不会被导入,如果需要导入模块所有对象,使用`*`
	`import引入的模块会被提升,类似var`
```
import foo from './foo.js'
import {foo, bar} from './foo.js'
import * as fooMod from './foo.js'  
import {defult as foo, bar} from './foo.js'
```

<br><br>

***转译为ES5语法并合并***
- 使用babel工具将ES6语法转译为ES5
	1. 安装babel-cli,babel-preset-es2015以及下一步需要使用的browserify;
	babel主体程序`npm install babel-cli browserify -g`
	babel插件,用于转译ES6`npm install babel-preset-es2015 --save-dev`
	```
	tip:
		cli:command line interface
		preset:预设,包含插件,用于将ES6语法转译为ES5
	```
	2. 定义`.babelrc`文件(rc意为:runtime control),该文件遵循json格式;
	```
	{
		"presets": ["es2015"]
	}
	```
	3. 使用npm命令,抓取指定文件夹下的js文件,转换为es5语法,添加到指定文件夹
	`babel js/src -d js/lib`

- 使用browserify将多个模块合并为一个主文件
	1. 安装browserify,上一步已经安装,如果不成功,也可以单独安装
	`npm install browserify -g`
	2. 使用npm命令,将指定模块组转换为单个js文件(工具会自动根据模块内部的导入导出关系将其合并)
	`browserify js/lib/app.js -o js/lib/bundle.js`

- 在页面内引入bundle.js
```
<script type="text/javascript" src="js/lib/bundle.js"></script>
```




















<br><br><br>