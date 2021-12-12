# Redux使用指南

## 00-简介

本文主要是用来记录Redux结合React的使用过程,帮助大家在使用Redux的时候,能够更好的理解Redux,从而更好地使用它

## 01-为什么需要Redux

1. JavaScript的应用程序越来越复杂了,需要管理的状态也越来越多了

   这些状态包括服务器返回的数据,缓存数据,用户操作产生的数据,也包括一些UI的状态

2. 我们要管理不断变化的状态是非常困难的

   状态之间会互相依赖,一个状态的变化会引起另一个状态的变化,view页面的变化也可能会引起状态的变化

   如果我们想要去追踪一个状态的变化是非常难的,因为我们不知道状态在什么时候发生了变化,因为什么原因发生了变化

3. React在视图层帮助我们解决了DOM的渲染过程,但是State依然是交给我们自己来进行管理的

   例如组件自己定义的state,父子组件通过props传递信息,亦或是通过context进行全局共享状态

   React的核心思想`UI=render(state)`

4. 说到底,Redux是一个帮助我们管理状态的容器,我们可以将需要管理的状态放进这个容器中,这个容器给我们提供了可预测的状态管理功能

## 02-Redux的核心理念

1. store
2. action
3. reducer

* Store:它是Redux提供给我们存储所有状态的容器,这也是我们寻找状态的地方

* action:它是一个JS对象类型的数据,是用来定义状态的变化行为,主要由type和数据组成

  ```js
  const changeStateAction={type:"CHANGESTATE",state:state}
  const IncrementAction={type:"INCREMENT"}
  ```

  可以看到 type是用来定义状态发生改变的原因的,state就是你想要改变的状态数据,这个state可加可不加,看自己的需求

  这样子使用action,我们可以很明确的知道,状态改变的原因是什么,方便我们跟踪状态和预测状态

  在Redux中,**所有的action都是需要通过dispatch进行更新数据的**,这一定请大家牢记

* reducer:这是Redux关键的一个地方,它是负责将action和state联系起来的一个**纯函数**

  它可以将state和action结合起来生成一个新的state

## 03-Redux的三大原则

1. 单一数据源

   * 整个应用程序的state被存储在一棵object tree中,并且这个Object Tree只存储在一个Store中

   * 单一数据源可以让整个应用程序的state变得方便维护,追踪和修改

2. State是只读的

   * 唯一修改state的途径就是通过dispatch action,不要使用其他的方法去修改state

   * 这样子的好处就是 我们可以对状态进行集中管理修改,并且会按照严格的顺序执行,不需要担心 race condition(竞态)问题

   * 这里解释一下竞态的概念

     竞态:对于同样的输入，程序的输出有时候正确而有时候却是错误的。这种一个计算结果的正确性与**时间有关**的现象就被称为**竞态（RaceCondition）**

3. 使用纯函数来执行修改

   只执行修改应该修改的状态,不会修改其他地方的状态,非常安全,修改状态不用担心会影响其他的地方

   我来解释一下纯函数的概念
   
   > 先来看下维基百科的定义
   > * 在程序设计中，若一个函数符合一下条件，那么这个函数被称为纯函数：
   >1. 此函数在相同的输入值时，需产生相同的输出。函数的输出和输入值以外的其他隐藏信息或状态无关，也和由I/O设备产生的 外部输出无关.
     2. 该函数不能有语义上可观察的函数副作用，诸如“触发事件”，使输出设备输出，或更改输出值以外物件的内容等。 n 当然上面的定义会过于的晦涩，所以我简单总结一下： p 确定的输入，一定会产生确定的输出； p 函数在执行过程中，不能产生副作用；
   
   总结
   
   1. 确定的输入有确定的输出
   2. 在执行过程中,不会产生副作用.举个例子,俗话说的好,是药三分毒,吃药虽然能治病,但是或多或少会影响我们身体的其他地方,这就是副作用.纯函数就像吃药不会对身体产生任何不好影响,100%有益,大家可以这么理解这句话🌺

## 04-在项目中使用Redux

需要安装以下包

1. redux
2. react-redux
3. redux-thunk
4. immutable
5. redux-immutable

---

前三个包是肯定要安装的,4,5你们可以自己选择,4,5是用来对状态存储的结构进行一个优化的,可以对项目起到一个优化的作用

这些包我现在就不再说了,后面用到了再和你们细讲

## 05-redux的目录结构

![image-20211004153642148](https://gitee.com/IU_czx/images/raw/master/img/redux%E7%9A%84%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84.png)



1. actionCreators:用来创建action的地方的
2. constants:用来记录action中的type常量的,统一管理
3. reducer:负责将action和state联系起来
4. index.js 容器创建的地方

## 06-redux的最基本使用

> 针对比较简单的程序,你们可以只使用一个reducer,这里也是讲一个reducer的情况,后面会讲到reducer拆分的情况

1. 🍔创建一个store容器,定义存储状态的地方

   ```js
   import { createStore} from "redux"
   import reducer from './reducer.js';
   const store = createStore(reducer);
   export default store;
   ```

2. 🥓创建`constants`,定义好状态改变的类型

   ```js
   const ADDNUM="ADDNUM";
   const SUBNUM="SUBNUM";
   export {
   	ADDNUM,
       SUBNUM,
   }
   ```

3. 🍗创建actionCreators,定义好需要改变状态的行为

   ```js
   import {ADDNUM,SUBNUM} from "./constants"
   //这里写成一个函数,是为了方便dispatch的时候,方便传值的
   //最后返回的是一个action对象
   const addNumAction=(num)=>{
       return {
           type:ADDNUM,
           //这里其实可以直接写num,而不用写 num:num
           //这是js的一个特点,对象名和传递的参数相同,可以直接省略掉后面的参数的
           num:num,
       }
   };
   const subNumAction=(num)=>{
       return {
           type:SUBNUM,
           num:num,
       }
   }
   
   export {
   	addNumAction,
       subNumAction,
   }
   ```

4. 🥗定义reducer,将action和state联系起来

   ```js
   import {ADDNUM,SUBNUM} from "./constants"
   //初始化state的值
   const defaultValue={
       num:0,
   }
   //reduce接收state和action两个值
   //state=defaultValue,是把默认值给state
   const reducer=(state=defaultValue,action)=>{
       //根据action的type类型来判断该执行什么样的操作
       //没有找打对应的类型就会返回state,不执行任何操作
       switch(action.type){
           case ADDSUM:
               return {...state,num:state.num+action.num}
           case SUBNUM:
               return {...state,num:state.num-action.num}
           default:
               return state
       }
   }
   export default reducer
   ```

5. 在组件中使用

   test.js

   ```js
   import React, { memo } from 'react'
   import { connect } from "react-redux"
   
   import {
       addNumAction,
       subNumAction,
   } from "../store2/actionCreators"
   
   //下面这步大家可能不理解 为啥可以拿到现在组件没有的值
   //实际上 我们是先让这个组件拿到加强版组件的属性
   //因为加强后,这个原来组件的一切会被加强版组件继承过去 到那个时候 就有这些属性
   //请结合我下面 connect函数详解 这一节 来好好理解下
   const Test = memo(function Test(props) {
       return (
           <div>
               <h1>当前计数{props.num}</h1>
               <button onClick={e => props.addNum()}>加5</button>
               <button onClick={e => props.subNum()}>减5</button>
           </div>
       )
   })
   
   const mapStateToprops = state => {
       return {
           num: state.num
       }
   }
   
   const mapDispatchToprops = dispacth => {
       return {
           addNum: function () {
               dispacth(addNumAction(5));
           },
           subNum: function () {
               dispacth(subNumAction(5));
           }
       }
   }
   
   export default connect(mapStateToprops, mapDispatchToprops)(Test);
   ```

   index.js

   ```js
   import React from 'react';
   import ReactDOM from 'react-dom';
   
   import store from './store2';
   
   import { Provider } from 'react-redux';
   
   import Test from './pages/test';
   
   ReactDOM.render(
     <Provider store={store}>
       <Test />
     </Provider>,
     document.getElementById('root')
   );
   ```

   在组件中使用有几个注意事项

   1. 在入口文件index.js中,首先从react-redux引入Provider,这是负责将我们创建的store容器,通过context共享出去,这里注意一下,这个Provider是react-redux内部实现的,但本质上是context,最后会转换为context
   2. 在test.js中有三个关键的地方
      1. mapStateToProps:负责将状态映射到组件的属性上
      2. mapDispatchToprops:负责将dispatch的action映射到属性上,进行数据的更改
      3. connect:负责将1,2传入到test中,形成一个新的组件,这里用到了高阶组件的方法,待会会细讲
      4. 这几个的核心思想是 将disptch的行为,和我们需要的状态映射到组件上,这样子组件能通过props拿到这些值和行为,从而自己进行相对应的操作和数据展示

## 07-connect函数详解

> 我们这次来自己实现一下connect函数,看看react-redux究竟做了怎样的一个操作

### 01-创建一个context

创建一个context文件,里面放着我们的context 

这一步的操作是模仿react-redux所提供的Provider,因为它的核心机制是context

```jsx
import React from "react";

const StoreContext = React.createContext();

export { StoreContext };
```

### 02-在connect函数中进行一个引用

```jsx

import React, { Component } from 'react'
import { StoreContext } from './context';

// 首先我们使用高阶组件 来给我们的组件来传递函数
export default function connect(MapStateToProps, MapDispathToprop) {
    // 返回值是一个函数 这个函数接收一个组件
    // 这个函数的返回值是一个类组件  这个类组件是对之前传进来的组件的一个加强版 
    return function Enhanced(WrappedComponent) {
        return class EnhancedHOC extends Component {
            static contextType = StoreContext;
            constructor(props, context) {
                // 因为context在构造器中，一开始是没有值的，需要我们手动去给context赋值，从父类那继承下context
                //这样就相当于把从contextProvider中传递过来的值拿到并给到构造器中的context
                super(props, context);
                //这一步是将容器中的state放入到 当前组件中的state中
                this.state = {
                    storeState: MapStateToProps(context.getState()),
                }
            }
		   //需要更改的值 在生命周期函数componentDidMount()中完成
            componentDidMount() {
                // 订阅store容器中的状态变化 监听到变化后,使用setState进行一个修改
                // store.subscribe的返回值就是取消订阅状态变化
                this.unSubscribe = this.context.subscribe(() => {
                    this.setState({
                        storeState: MapStateToProps(this.context.getState()),
                    })
                })
            }

            componentWillUnmount() {
                //在卸载组件的时候 将取消订阅
                this.unSubscribe();
            }

            render() {
                return (
                    <WrappedComponent
                        {...this.props}
                        {...MapStateToProps(this.context.getState())}
                        {...MapDispathToprop(this.context.dispatch)} />
                )
            }
        }
    }
}
```

### 03-在入口文件中引入context即可

在这里将store作为参数传给context

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

import store from './store';
// import { StoreContext } from './connect/context';

// 使用react-redux所需要引入的报
import { Provider } from 'react-redux';
import App from './App3';

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>
    , document.getElementById('root'));
// <StoreContext.Provider value={store}>
//     <App />
// </StoreContext.Provider>
```

### 04-图解

> 防止大家不明白,我画了图供大家理解

![image-20211004180808072](https://gitee.com/IU_czx/images/raw/master/img/connect%E5%87%BD%E6%95%B0%E5%9B%BE%E8%A7%A3.png)

## 08-react-redux中Hook的使用和reducer的拆分

> 不知道大家在看完以上的介绍会不会觉得这样用太麻烦了,用起来比较繁琐
>
> 接下来我要给大家介绍下React在16.8版本新推出的Hook,有了Hook这个跨世纪的发明,React编写起来也更加方便了
>
> 而React-redux也是大量用到了Hook这个新特性,结合着使用,比之前快了不知道多少倍
>
> 接下来 我举得例子都是我写的网易云项目中 我是怎么组织redux的,大家主要看思想即可,里面一些我定义的变量不要过于计较了
>
> 主要是学习这个用法和思想

### 01-在根目录下创建store文件夹

> 实际在写项目的时候,各个页面的状态和行为是比较多的,这时候就需要我们去拆分reducer,让每个页面去管理自己的reducer,最后在这个主目录下进行一个合并,一起放到store容器中

index.js

```js
import { createStore, applyMiddleware} from "redux"

//为了在redux中进行异步请求,使用redux-thunk
import reduxThunkMiddleWare from "redux-thunk";
import zReducer from "./reducer";

//为了使用redux-thunk 需要从redux中引入applyMiddleware(中间件)
const storeEnhancer = applyMiddleware(reduxThunkMiddleWare);

// 在引用中间件后,在状态容器中,你得使用composeEnhancers将应用的中间件进行一个包裹,再往里面传递,在这个函数的定义内,第二个参数传递就是composeEnhancers
const store = createStore(zReducer, composeEnhancers(storeEnhancer));

export default store;
```

1. 创建一个redux容器,容器是唯一的,虽然redux没有规定必须一个,但是唯一的容器,方便我们追踪状态和查找
2. 为了进行异步请求,使用redux-thunk,应用中间件
3. 我怕还有小伙伴不知道该怎么使用redux-thunk,我还是简单的介绍下redux-thunk的使用步骤
   1. 下载redux-thunk这个包
   2. 引入redux-thunk,并从redux中引入applyMiddlware
   3. 将redux-thunk放入applyMiddleware
   4. 在创建容器的时候,用composeEnhancers对applyMiddleWare进行包裹传入,其实这也是高阶组件的用法,大家感兴趣可以翻读下源码

reducer.js

```js
// import { combineReducers } from 'redux';
import { combineReducers } from 'redux-immutable';

import { reducer as recommendReducer } from "../pages/discover/children_Pages/recommend/store";
import { reducer as songPlayer } from "../pages/player/store";
import { reducer as albumReducer } from "../pages/discover/children_Pages/album/store"

const zReducer = combineReducers({
    recommend: recommendReducer,
    player: songPlayer,
    album: albumReducer,
})

export default zReducer
```

1. 因为我在项目中使用的是immutable.js这个包,改变了我的数据存储结构,所以是在redux-immutable引入的combineReducer中

2. 这个combineReducer是用来帮助我们合并之前拆分的reducer的

3. combineReducer是传入一个对象的

4. 对象中的每个值代表着我们每个拆分的reducer

可能有小伙伴一头雾水,请接着往下看,到后面所有东西就都会串联起来

---

### 02-每个页面有自己的Store

> 网页应用有很多个页面,我们拆分reducer的准则是每个页面配备一个store
>
> 具体我们看实例  接下来的实例是音乐播放栏  我们看下目录结构

![image-20211005174001233](https://gitee.com/IU_czx/images/raw/master/img/reducer%E6%8B%86%E5%88%86.png)

大家看到这个结构是不是很熟悉呢,与我们之前讲的部分的结构划分是一摸一样的

与之前不同的是 index.js文件中的内容变了,不再是创建容器了,而是负责将reducer导出去,然后在主目录下的容器中引入合并reducer

`reducer.js`

```js
//引入immutable 改变数据结构
import { Map } from "immutable"

import {
    GETSONG, CURRENTSONGINDEX
} from "./constatnts"
//使用map对这个对象进行包裹
const defaultState = Map({
    playList: [],
    currentSongIndex: 0,
})

function reducer(state = defaultState, action) {
    switch (action.type) {
        case GETSONG:
            return state.set("playList", action.playList);
        case CURRENTSONGINDEX:
            return state.set("currentSongIndex", action.currentSongIndex);
        default:
            return state;
    }
}
export default reducer;
```

`index.js`(大家可以看到 index没有创建容器了,而是导出reducer了)

```js
import reducer from "./reducer";
export {
    reducer
};
```

`actionCreators.js`

```js
//这是我们定义的网络请求
import {
    requestLyric,
} from "../../../service/player"

import * as actionType from "./constatnts"

const changeLyricAction = (lyric) => ({
    type: actionType.GET_LYRIC,
    lyric,
})

//因为引入了redux-thunk这个中间件,所以可以在redux中进行网络请求
//我们需要请求数据的时候,使用这个行为进行派发即可
const getSongLyric = (id) => {
    return (dispatch, getState) => {
        const lyrics = getState().getIn(["player", "lyrics"]);
        const songInfo = getState().getIn(["player", "songInfo"]);
        const newLyrics = [...lyrics];
        const songIndex = songInfo.findIndex(item => item.id === id);
        requestLyric(id).then(res => {
            if (songIndex === -1) {
                newLyrics.push(res.data.lrc.lyric);
                //拿到数据后 可以对我们定义的行为进行派发
                dispatch(changeLyricAction(newLyrics));
            } else {
                dispatch(changeLyricAction(newLyrics));
            }
        })
    }
}
export {getSongLyric}
```

### 03-组件中使用

```js
import React, { memo, useEffect } from 'react'
import { shallowEqual, useSelector,useDispatch } from 'react-redux'
import {getSongLyric} from "./store/actionsCreators"

export default memo(function ZXPlayer() {
    const dispatch=useDispatch();
    const { lyrics, currentSongIndex } = useSelector(state => ({
        //因为我们使用了immutable 所以我们取数据的时候得使用 getIn()
        //shallowEqual是提升性能的一个方案,防止redux一直对我们的对象继进行深层比较,消耗性能
        lyrics: state.getIn(["player", "lyrics"]),
        currentSongIndex: state.getIn(["player", "currentSongIndex"]),
    }), shallowEqual);
    useEffect(()=>{
        dispatch(getSongLyric(id))
    },[])
    return <div>测试</div>
})

```

1. 在组件中使用 我们引入了两个Hook,这个是react-redux中所添加的 分别是useSelector和useDispatch
2. useSelector:负责拿到我们存储在容器中的状态 对应的是mapStateToProps
3. useDispatch:负责从容器中拿到dispatch这个行为  对应的是 mapDispatchToProps 不同的是这次没有把行为添加进去,行为是由我们自己来控制派发的,hook只是帮助我们拿到了dispatch这个函数而已
4. 我们在看了这个后,可以很明白的知道相比之前简单了不是一点半点
5. 以前我们需要自己定义state和需要派发的dispatch
6. 现在我们只需要useSelector和useDispatch,就可以非常轻松的拿到state和dispatch,省去了一大笔麻烦

## 09-收尾

讲的这,其实redux的使用就这么多了,redux的使用难度我个人觉得并没有很难,重点是去理解redux的工作原理是什么,

connect函数是如何将state和dispatch组合到原来的组件上到,这个我觉得是重点,大家要好好理解connect函数的执行逻辑是什么

文章后面讲的Hook的使用,也只是帮助我们更简单的使用redux而已,但是其核心是没变的

好,这次我们就讲的这吧,大家如果还有什么不明白的欢迎留言,我看到就会回复大家的







