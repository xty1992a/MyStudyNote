#buffer注目

读取非UTF8编码的网页时,如果使用如下方式接受数据,很容易出现问题;
```
var html = ''
res.on('data', function(chunk){
	html += chunk
})
res.on('end', function(){
	fs.writeFile('1.txt', html, function(e){})	
})

```
实际上chunk并非字符串,而是buffer,如果使用一个字符串与它相加,实际上是使用一个字符串与chunk.toString()相加,这个过程中原网页的原始编码已经被改变,极有可能出现乱码问题

所有应该使用如下方式
```
var bufArr = []
res.on('data', function(chunk){
	bufArr.push(chunk)
})
res.on('end', function(){
	var bigBuf = Buffer.concat(bufArr)
	//然后再对该Buff进行操作	
})

```
可以使用第三方插件比如`iconv-lite`,`encoding`等
以encoding为例
```
var encoding = require('encoding')
res.on('end', function(){
	var bigBuf = Buffer.concat(bufArr)
	//convert(文件,'tocharset', 'fromcharset')
	var utfStr = encoding.convert(bigBuf, 'utf8', 'gbk')	
})
```


