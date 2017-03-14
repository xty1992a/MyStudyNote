#Restful API与Restless API

Restful意为`表现层状态转译`,这是一种软件架构风格
**将网页视为一个软件,将url视为资源的路径,将请求方法视为对资源的CRUD方法;**
在这种视角看来,url(路径)是不应该具有行为数据的,它应该仅仅标记一个资源的路径,而不必在路径中添加动词,声明对这个资源的操作方式,这项工作应该由请求方法决定;
即,真正的贯彻`get();post();put();delete()`方法的真正含义,正确的使用不同的请求方法,而不是get,post包办一切.
这样做的目的有利于简化网络请求,显得更有层次更加明了;

url示例:

```
//动物园的所有动物名单
www.zoos.com/animals
//所有鸟类名单
www.zoos.com/animals/birds
//指定鸟类的数据
www.zoos.com/animals/birds/1
```
restful风格的操作,一下示例为`json-server`模拟服务器
```
//获取,指定标识 id:1
axios.get(www.zoos.com/animals/birds/1)
	.then(res => {
		console.log(res.data)
	})
//增加,往birds集合中添加
axios.get(www.zoos.com/animals/birds, {an bird info})
	.then(res => {
		console.log(res.data)//返回新添加的对象数据
	})

//更新,修改指定标识的数据
axios.get(www.zoos.com/animals/birds/1, {new bird info})
	.then(res => {
		console.log(res.data)//返回新添加的对象数据
	})


//删除,删除指定标识的数据
axios.get(www.zoos.com/animals/birds/1)
	.then(res => {
		console.log(res.data)
	})

```