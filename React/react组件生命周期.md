#React组件生命周期

- `componentWillMount()`在组件调用render渲染之前调用
- `componentDidMount()`在组件第一次渲染之后调用,此时已经生成了真实DOM,可以通过this.getDOMNode()访问.此时可以进行一些准备工作,比如发送ajax请求,设置定时器等.
- `componentWillUnmount()`在卸载一个组件时,会调用该方法,此时可以执行一些收尾工作,比如回收变量,停止定时器等
- `componentWillReceiveProps()`当父组件向组件内传递一个新的prop时,会触发方法,第一次渲染不会调用这个方法内可以放置一些需要根据父组件状态变化而实时更新的数据
