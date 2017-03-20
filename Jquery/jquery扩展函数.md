#对jquery核心函数的扩展

- $.extend()方法
	该方法是直接为$添加扩展方法,参数为一个对象,该对象上为名值对,值为一个函数.
```
$.extend({
	sing: function(){
		alert('i'm sing!')
	}
})

$.sing() //弹出`i'm sing!`
```

- $.fn.extend()方法
	该方法是为$()对象添加方法,实际上在源码中,$.fn就是$.prototype,所有jquery对象---也就是$核心函数的实例们,都将拥有新添加的方法.
	fn.extend()参数为一个带方法的对象.
	
```
$.fn.extend({
	sayName:function(){
		console.log(this)	//jquery对象打印自己
	}
})
```