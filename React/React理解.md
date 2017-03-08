#React

这个框架专注于使用纯js语法写页面,为此,他们发明了一套可以在js代码中写<标签>的jsx语法;
同时为了提升框架的效率问题,react设计了虚拟DOM这一概念;
>虚拟DOM与真实DOM之间存在映射关系,当虚拟DOM状态(setState)改变,将会创建新的虚拟DOM树,经过新旧之间的diff算法比较差异之后,局部刷新页面中的对应元素
>>*真实DOM是拥有很多属性的重对象,虚拟DOM则只包含用户需要的属性*

react同时也是面向组件的框架,使用组件将页面切分为一个个功能区块,组件间相对较为独立,父子组件之间使用`props`和`state`通信,兄弟组件之间依靠父组件通信;

<br>
##语法详解

在ES6语法中,使用`class...extends`语句创建一个继承`React.Component`对象的react组件

```
class App extends React.Component{
	render(){			//改写Component内的render()方法
		retrun <h1>Hello React!</h1>
	}
}
```
使用以下代码将组件渲染生成的组件插入指定容器元素中;
```
ReactDOM.render(<Person />, document.getElementById('example'))
```
<br>
---
如果需要向组件内传递数据,在渲染时,添加属性并赋值,在组件内部使用`this.props.propName`获取传递进来的数据;

```
class App extends React.Component{
	render(){
		let {msg} = this.props			//ES6解构赋值
		retrun <h1>{msg}</h1>		
	}
}

ReactDOM.render(	
	<Person msg={'Hello React!'}/>, 	//添加msg属性
	document.getElementById('example')
)
```
---<br>

子组件更改父组件state
```
class Parent extends React.Component{
	constructor(props){
		super(props)
		this.state = {
			msg: ''
		}
	}
	render (){
		return <Child flag={this.state.flag}/>
	}
}

class Child extends React.Component{
	setMsg(){
		
	}

	render(){
		<input type='text' ref='msgInput' onChange={this.setMsg}/>
		<p ref='shower'>
	}
	
}

```
