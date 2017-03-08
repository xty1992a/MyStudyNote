##pubsub-js
自定义事件
发布(触发)
订阅(绑定监听)
1. 安装并引入
	`npm install pubsub-js`
	`import PubSub from 'pubsub-js'`
2. 订阅消息
```
PubSub.subscribe('said', (msg, data)=> {
	console.log(data)
});
```

3. 发布消息
```
PubSub.publishSync('said', 'hello pubsub is work !')
```

这个插件可用于react组件之间直接通信使用,不受组件之间的阻隔.

