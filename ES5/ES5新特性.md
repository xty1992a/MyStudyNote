##ES5扩展

###Object的静态方法,常用的有两个,都是对Object本身的扩展
---

- Object.create(prototype[,descriptors])
	参数一,指定新建对象的原型对象
	参数二,一个对象,属性为对某个属性的配置项
```
var obj = {n:1}
var obj1 = Object.create(obj,{
		m:{
			value:value,
			writable:true		//是否可修改,默认为true
			get:fun()			//在读取m时触发
			set:fun()			//在对m赋值时触发
		}
	})
```

- Object.defineProperties(obj, descriptors)
	为指定对象定义扩展多个属性	
```
var p = {
	firstName: 'tom',
	lastName: 'peter'
}

	Object.defineProperties(p, {
		funllName:{
			get: function(){		//读取funllName时触发
				return this.firstName + ' ' + this.lastName
			},
			set: function(value){	//对fullName赋值时触发
				var names = value.split(' ');
				this.firstName = names[0];
				this.lastName = names[1];
			}
		}	
	})
```


###Array.prototype.function()
---
对所有数组添加的方法:

- indexOf(value)	//获取数组中第一个等于这个值的下标
- lastIndexOf(value)//获取数组中最后一个等于这个值的下标
- forEach(fun(item, index))	//遍历数组
- map		//遍历一个数组并返回新数组
- filter 	//遍历一个数组并根据条件返回新数组

```
let arr = [2,3,4,5,6,7]

//将所有item加10
var newArr = arr.map(function(item){
	return item += 10
});

//筛选出索引大于5的数组
var smallArr = arr.filter(item){
	return item > 5
}

```
		

###Function.prototype.bind(obj)
---
为所有function添加的方法,类似于call()
同样能指定函数中的this;
区别在于,call()/apply()将会立即执行
bind()则将函数返回
```
    var a = 'aaa';
    var obj = {
        a : 'bbb'
    };

    setTimeout(function () {
        console.log(this.a);
    }.call(obj), 2000)	//立即执行,不延迟

    setTimeout(function () {
        console.log(this.a);
    }.bind(obj), 2000)	//延迟执行
	
```
	