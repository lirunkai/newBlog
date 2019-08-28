## Redux

什么时候需要使用Redux？？

1. 组件的状态需要共享
2. 某个状态需要全局获取。 比如用户id

Redux: 状态管理器。类似vuex, 提供一个数据存储的地方, 方便所有组件获取和设置.



### store

数据保存的地方, 全局唯一.

#### 创建store

```react
import { createStore } from 'redux'
const store = createStore(fn)
```

**getState()** 获取state

**dispatch(action) ** 提交action到reducer

**subscribe(listener) ** 注册监听器

### state

整个应用的state被存储在一个Object tree中.  

特点: state 只读, 唯一改变state的方式是触发action,确保视图(view)和网络请求不能直接修改state

```react
const state = store.getState()	
```



### action 

**一个用于描述已发生事件的普通对象**, 需要通过action来改变state

```
const action = {
	type: 'addType',
	data: 'learn Redux'
}
```

### reducer 纯函数

描述action如何修改state tree。actions 只是描述了*有事情发生了*这一事实，并没有描述应用如何更新 state。

reducer接收 state 和 action，并返回新的 state 的函数

## React Redux

UI组件和容器组件

### connect()

用于从UI组件中生成容器组件

```
import { connect } from 'react-redux'
const VisibleTodoList = connect(
	mapStateToProps,
	mapDispatchToProps
)(TodoList)
```

### mapStateToProps

接受(state, props)作为参数.  将外部的state对象映射到UI组件的props，返回一个对象，里面的每个键值对就是一个映射

mapStateToProps返回的state会根据Store的变化来更新.

```
const mapStateToProps = (state, ownProps) => {
	return {
		stateOne: state.storeOne
	}
}
```

### mapDispatchToProps

用来建立UI组件到store.dispatch方法的映射. 

接受(dispatch, props)作为参数. 

```
const mapDispatchToProps = (dispatch, props) => {
	return {
		onClick: () => {
			dispatch({
				type: 'SET_STATE_ONE',
				data: data
			})
		}
	}
}
```

### Provider

Provider 让容器直接拿到state

```react
import {Provider, createStore} from 'react-redux'
function reducer(){}
let store = createStore(reducer)

function App(){
  return (
  	<Provider store={store}></Provider>
  )
}
```

