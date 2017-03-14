#json-server
这是一个轻量级的restful风格的模拟服务器,通过不同的请求方法,可以对同一个url指向的数据库中的数据进行CRUD操作.

- 安装 `npm i json-server -g`

- 按照如下格式创建json文件,作为服务器的模拟数据库
```
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

- 运行服务器
`json-server --watch db.json --port 3004`

- 访问http://localhost:3004/posts,将显示所有posts集合


增删改查示例:
- get()查询
	- post()添加
	- put()更新
	- delete()删除
	
```
var axios = require('axios')

//查询操作
function getTest(url) {
    axios.get(url)
        .then(function (res) {
            console.log(res.data);
        })
}

getTest('http://localhost:3000/posts')

//添加操作
function postTest(url) {
  var obj = {"title": "react", "author": "facebook" }
  axios.post(url, obj)
      .then(function (res) {
        console.log(res.data);
      })
}

// postTest('http://localhost:3000/posts)

//更新操作
function putTest(url) {
  var obj = {"title": "angular", "author": "google" }
  axios.put(url, obj)
      .then(function (res) {
        console.log(res.data);
      })
}

// putTest('http://localhost:3000/posts/4')


//删除操作
function deleteTest(url) {
  axios.delete(url)
      .then(function (res) {
        console.log(res.data);
      })
}

// deleteTest('http://localhost:3000/posts/4')


```