##Node的模块实现
####require()的运行机制
required()可以识别两种模块;
- 官方提供的核心模块
	- node运行时已经加载进内存,加载速度最快
- 用户编写的文件模块
	- 以. .. / 开头的标识符
		会将标识符转换为真实路径进行查找,找到则引入,次快
		tips:加上文件扩展名有助于加快速度,没有扩展名的文件,node会用fs模块依次以.js,.json,.node进行尝试
	- npm安装的包
		在当前目录下的node_modules寻找;
		未找到则到父级目录,直至根目录,找到则引入,最慢
	
require()执行时会首先在缓存中查询,(node会把引入过的模块都以对象的形式进行缓存,但是对核心模块的缓存检查会优先于文件模块).
未找到再去具体目录找,对于自定义模块则会去当前目录直至根目录依次寻找node_modules;
```
tip:
如果require的结果是一个文件夹,node会将其视为一个包处理,寻找package.json文件,并使用JSON.parse()进行解析.
然后根据main的值进行定位,如果没有package.json,则会将index作为引入对象,依次查找index.js;index.json;index.node;
```

####模块编译
当引入一个文件,node会在当前创建一个模块对象,将引入的文件执行之后的对象与模块对象相绑定,对于不同的文件,有不同的编译方式
- .js文件,通过fs模块同步读取后直接编译
- .node文件,node是用c/c++写的,通过dlopen()方法加载
- .json文件, 通过fs读取之后用JSON.parse()解析

编译过程中,node对引入的js文件进行了包装,会将其放入一个function内部运行,该function的形参有exports,require等,所以这些方法和属性无需定义就能使用;
```
(function (exports, require, module, __filename, __dirname) { 
	var math = require('math'); 
		exports.area = function (radius) { 
		return Math.PI * radius * radius; 
	}; 
}); 
```
```
tips:
不能对exports直接赋值的原因是exports是一个形参,对形参的直接修改不能改变实参,只有修改module的属性exports才能真正改变exports;
```

<br>








		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
			
			