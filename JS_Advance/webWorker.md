由于js是单线程运行,所以如果在主线程进行长时间的运算就会阻塞主线程的运行,表现就是页面卡死,不再响应用户的操作,此时可以使用webworkerAPI,将大运算量的任务交由分线程运算.
*分线程不具有操作页面的权限,必须将结果交还主线程,由主线程处理后续操作*

分线程即另一个js文件,在这个js内,全局对象不再是window,而是当前js内的worker对象,这个对象内有onmessage事件和postMessage()函数,用于接受主线程的数据和返回处理后的数据
```
var onmessage = function(ev){
	var data = ev.data			//通过event.data获得数据
		data = data.toUpperCase()
	postMessage(data)
}
```