# redux

## 什么是redux

- redux是一种使用`action`的事件进行管理和更新应用状态的模式和库
- 它是作为一个应用的全局中心容器,使用规则确保状态的变化在一个可预测的状态下

## 什么时候该使用redux

1. app在许多地方都有大量的状态
2. app的状态更新的比较频繁
3. app更新的逻辑比较复杂
4. 这个app有中等或巨大的代码库,并且很有可能被许多人所使用

## redux的库和工具

> redux是一个独立的js库,常与以下的包一起使用

- React-Redux(redux提供的官方的包,结合react一起使用非常方便)

- Redux-Toolkit

  是官方推荐的写redux逻辑的方法,包含了redux官方认为构建一个redux app所必须的工具,redux-toolkit是以他们实践出来的最佳实践所得,简化了大部分的redux任务,避免了一些比较普遍容易犯的错误,使得更加容易写redux应用

- Redux DevTools Extension

  是一个可以监听redux状态变化的插件,非常好用,还可以根据时间回到之前的某个状态

## redux术语和概念

```js
function Counter() {
  // State: a counter value
  // 状态
  const [counter, setCounter] = useState(0)

  // Action: code that causes an update to the state when something happens
  // 行为
  const increment = () => {
    setCounter(prevCounter => prevCounter + 1)
  }

  // View: the UI definition
  // 视图  
  return (
    <div>
      Value: {counter} <button onClick={increment}>Increment</button>
    </div>
  )
}
```

It is a self-contained(完备) app with the following parts:

- state:值得信赖的源驱动我们的app
- view:基于当前状态的一个声明式描述UI
- actions:基于用户的输入和触发更新而改变状态的事件

这也构成了一个单向数据流(one-way data flow)

- state描述了我们的app在某一个特定的状态的情况
- UI基于状态进行渲染
- 当一些改变状态的操作发生时,UI会基于当前新的状态进行一个重新渲染

![单向数据流](https://redux.js.org/assets/images/one-way-data-flow-04fe46332c1ccb3497ecb04b94e55b97.png)

在react中,这很有可能会被破坏掉,当我们在一个app中有许多组件需要共享相同的状态(state)的时候,尤其是这些组件都定位在app的不同位置的时候,这个可以使用状态提升(父传子)解决一部分问题,但是有时候也不能解决问题

一种解决办法就是把共享state抽取出来,放在组件树之外的一个中心容器进行管理,然后任何组件就可以使用这个状态或者触发行为,这也是redux的核心思想

### 不变性

> 变化意味着多变,而如果一个事情是不可变的,那么他就永远不可变

JS的对象和数组就是可变的,因为他们是引用类型数据,我们可以改变其中的内容,但是他们的引用却不会变,这就是可变化

在redux中,为了不变化的更新值(**update values immutably**),你的必须复制现有的对象或者数组,然后修改这个备份.

### 术语

- Actions:是一个原生的JS对象,拥有`type`field(type字段),你可以认为一个action是一个描述应用中会发生的某些事情

  我们通常会划分成两个部分`domain/HAPPENING`

  第一个部分`domain/`告诉我们这个action是属于哪个部分

  第二个部分`HAPPENING`告诉我们这个部分发生了什么事情

  下面是一个典型的action

  ```js
  const addTodoAction = {
    type: 'todos/todoAdded',
    payload: 'Buy milk'
  }
  ```

- Action Creators

  它是一个函数,用于创造和返回一个action对象

  我们通常使用下面这个形式,而不必每次手动创建一个action对象

  ```js
  const addTodo = text => {
    return {
      type: 'todos/todoAdded',
      payload: text
    }
  }
  ```

- Reducers

  它是一个用于将当前`state`和`action`对象进行联系起来的一个函数,决定在什么时候更新状态并返回一个新的状态`(state, action) => newState`

  Reducers有以下规则

  - 只应该基于`state`,`action`计算新的状态
  - 不允许修改已经存在的状态,需要copy他们产生备份,在进行修改
  - 不允许做任何异步操作,计算随机值,或者造成其他副作用
  - 总而言之,reducer就是一个纯函数

  ```js
  const initialState = { value: 0 }
  
  function counterReducer(state = initialState, action) {
    // Check to see if the reducer cares about this action
    if (action.type === 'counter/increment') {
      // If so, make a copy of `state`
      return {
        ...state,
        // and update the copy with the new value
        value: state.value + 1
      }
    }
    // otherwise return the existing state unchanged
    return state
  }
  ```

- Store

  存储所有共享状态的容器

  `store`通过传递一个`reducer`创建,并且有一个方法`getState`可以返回当前的state

  ```js
  import { configureStore } from '@reduxjs/toolkit'
  
  const store = configureStore({ reducer: counterReducer })
  
  console.log(store.getState())
  // {value: 0}
  ```


- dispatch(事件): 将`action`进行派发,reducer(类似于监听器)会根据派发的`action`进行一个状态的更新

  ```js
  const increment = () => {
    return {
      type: 'counter/increment'
    }
  }
  
  store.dispatch(increment())
  
  console.log(store.getState())
  // {value: 2}
  ```

  

- selectors(这个概念有点蒙,感觉类似于useSelector这个Hook)

  是一个可以从store容器中提取出特定的值的函数

  帮助避免了重复的逻辑,当不同的部分需要读取相同的数据时



## redux的数据流

![redux流程图](https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)



针对redux,我们可以将这些步骤划分成更多细节

- 初始设置
  - redux的store使用总的reducer创建
  - store每回调一次这个`root reducer`,就会存储这个回调值作为他的初始`state`
  - 当这个UI第一次被渲染,UI组件使用当前`store`中的`state`,并且使用这个数据去决定渲染什么,他们也可以订阅未来的`store`更新,如果这个`state`发生变化后,他们可以知道'
- 更新
  - 在app中发生某些事情,比如用户点击一下按钮
  - 这个app代码`dispatch`了一个`action`到redux的容器中,比如`dispatch({type: 'counter/increment'})`
  - `store`会再次运行这个`reducer`,使用之前的状态和当前的状态,并且保留返回值作为最新的`state`
  - `store`会提醒所有订阅的组件
  - 每个需要数据的UI组件会从`store`检查他们需要的`state`是否发生变化
  - 每个组件看见他们需要的数据发生变化,会强制使用新数据进行渲染,也因此可以更新屏幕上的新内容

