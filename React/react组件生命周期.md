#React组件生命周期

组件在render之前会执行`componentWillMount()`方法
在render之后会执行`componentDidMount()`方法
以上两种方法在一个render之内只会执行一次,所以,一些准备工作可以放在里面执行,比如发送ajax请求.
在卸载一个组件时,也会触发`componentWillUnmount()`方法,此时可以执行一些收尾工作,比如回收变量,停止定时器等
当父组件向组件内传递一个新的prop时,会触发`componentWillReceiveProps()`方法,这个方法内可以放置一些需要根据父组件状态变化而实时更新的数据
