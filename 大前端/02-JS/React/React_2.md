# ReactCSS样式编写

## 前言

> 整个前端已经是组件化的天下,而CSS的设计不是为组件化而生,所以在目前组件化的框架中都需要一种合适的CSS解决方案
>
> 在组件化选择合适的CSS解决方案应该符合以下条件
>
> 1. 可以编写局部CSS:css具备自己作用域,不会随意污染其他组件内的原生
> 2. 可以编写动态的css:可以获取当前组件的一些状态,根据状态的变化生成不同的CSS样式  
> 3. 支持所有的css特性:伪类,动画,媒体查询
> 4. 编写起来简洁方便,最好符合一贯的css风格特点

## 内联样式

![image-20210805091856953](https://gitee.com/IU_czx/images/raw/master/img/image-20210805091856953.png)

## 普通CSS

会有层叠问题,需要设置多层权重,才能识别,较为麻烦

## CSS Modules

![image-20210805093957679](https://gitee.com/IU_czx/images/raw/master/img/image-20210805093957679.png)

## CSS in JS

![image-20210805114429527](https://gitee.com/IU_czx/images/raw/master/img/image-20210805114429527.png)

![image-20210805114743756](https://gitee.com/IU_czx/images/raw/master/img/image-20210805114743756.png)

# 前端网络请求

## 前端网络请求的选择

1. 传统的Ajax,基于XMLHttpRequest(XHR)------------(不好用)
2. Jquery的请求
3. Fetch API
4. axios(最常用的)

## Axios的基本使用

1. 首先导入axios包,你可以在项目中使用npm或者yarn进行导入

2. 在使用的文件中导入包

3. 最基本的用法

   ```jsx
           axios({
               url: 'https://httpbin.org/get',
               params: {
                   name: 'why',
                   age: 18,
               }
           }).then(res => {
               console.log(res);
           }).catch((err) => {
               console.log(err);
           });
   ```

   axios.get()的用法:
   
   ```jsx
   axios.get("url地址",{你想传入的参数对象}).then('回调结果')
   ```
   
   axios.post的用法:
   
   ```jsx
   axios.post("url地址",{data对象}).then('回调结果')
   ```
   
   无论是什么请求,最终都是调用的axios中的request请求,可以通过查询源码查证
   
   axios.all()是对于请求的合并
   
## axios的配置信息

1. 请求配置信息(可以在coderwhy老师的公众号找到,或者官网)

2. 响应结构信息

3. 全局默认配置

   1. 可以在入口文件中导入axios包

   2. 然后在那里面写一些默认配置

   3. ```jsx
      import axios from 'axios';
      
      axios.defaults.baseURL='https://httpbin.org';
      axios.defaults.timeout='5000';
      axios.defaults.headers.common["token"]='';
      ```

   4. 创建多个实例

      ```jsx
              // 创建多个新的实例
              const instance = axios.create({
                  baseURL: '',
                  timeout: '',
              })
          }
      ```

## axios的拦截器

```jsx
        // 拦截器的使用(请求拦截和响应拦截)
        axios.interceptors.request.use(config => {
            // 一般会在什么地方使用拦截器呢
            // 1. 发送网络请求的时候,想弹出一个loading组件
            // 2. 某一些请求,要求用户携带token,如果没有登录,那么直接跳转到登录页面
            // 3. params/data进行序列化的操作
            return config;
        })

        axios.interceptors.response.use(res => {
            console.lo(res.data);
        }, err => {
            // if(err&)
        })
```

## 开发中实际使用的

> 一般要进行二次封装的,但为什么要进行二次封装呢,接下来来解释一下

1. 默认情况下我们是直接使用axios来进行开发的
2. 但是我们要考虑一个问题,假如有100多处中都直接依赖axios,突然间有一天axios出现了重大bug,并且该库已经不再维护,这个时候该如何处理呢
3. 大多数情况下,我们会寻找一个新的的网络请求库或者自己进行二次封装
4. 但是有100多处都依赖了axios,方便我们进行修改码,我们所有依赖的axios库的地方都要进行修改吗?这样太麻烦了

我们可以按以下方式去做

1. 在项目根目录下创建一个service文件夹
2. 在service文件下专门放一个请求的文件和一个基础配置文件
3. 如果后续开发中,出错的话,也只需要更新这一个文件即可

# React中的过渡动画

## React-transition-group介绍

1. 安装

   ```jsx
   npm install react-transition-group --save
   yarn add react-transition-group
   ```

2. 使用

   1. 主要包含四个组件
      1. Transition:该组件是一个和平台无关的组件(不一定和CSS结合),但一般是和CSS来完成的,比较常用的是CSSTransition
      2. CSSTransition
      3. SwitchTransition:两个组件显示和隐藏切换时,使用该组件
      4. TransitionGroup:将多个动画组件包裹在其中,一般用于列表中元素的动画

3. 详细介绍

   1. CSSTransition:

      1. 他在执行的时候,有三个状态:appear.enter,exit

         ![image-20210808103501916](https://gitee.com/IU_czx/images/raw/master/img/image-20210808103501916.png)

      2. 在这个组件中可以传递多个属性

         1. in:这个传递一个布尔值,true开始,false退出,动画的起点

         2. classNames:可以设置一个类名头,为上述三个状态添加头类名,这样你可以设置特定的过渡动画

         3. timeout:这个是过渡动画必加的一个属性,表示动画会在页面上显示多久

         4. unmountOnExit:表示在不显示的时候,会把当前元素移除DOM树

         5. appear:表示动画在开始时是否会执行

         6. 后面还可以接六个钩子函数,对于各个状态进行一些操作

            ```jsx
            					onEnter={el => { console.log('进入状态'); }}
                                onEntering={el => { console.log("正在进入状态"); }}
                                onEntered={el => { console.log('进入完成'); }}
                                onExit={el => { console.log("准备退出"); }}
                                onExited={el => { console.log("已经退出"); }}
                                onExiting={el => { console.log("正在退出") }}
            ```

         7. 当然,这个只是帮你加类名,真正的动画你还得在CSS样式中写,然后引用他.

   2. SwitchTransition

      1. 应用场景:主要就是对按钮的切换加一个过渡动画,他不是移除容器,而只是改变容器内的内容
      2. 在switchTransition中,也要包裹一层CSSTransition才行

   3. TransitionGroup

      1. 这个要注意了,这个只能包裹在列表元素的父元素上,一定要想下面这样包裹才行,不能在TransitionGroup下面在包裹一层

         ```jsx
         <TransitionGroup>
         	<CSSTransition>
             	"这里是列表元素"
             </CSSTransition>
         </TransitionGroup>
         ```

# JavaScript纯函数

> 函数式编程中有一个概念叫纯函数,JavaScript符合纯函数式编程的范式,所以也有纯函数的概念

一般定义:

![纯函数定义](https://gitee.com/IU_czx/images/raw/master/img/image-20210808164648876.png)

总结:

1. 确定的输入,一定会产生确定的输出
2. 函数在执行过程中,不能产生副作用

![image-20210808165819651](https://gitee.com/IU_czx/images/raw/master/img/image-20210808165819651.png)

# redux

> 1. JavaScript开发的应用程序,已经变得越来越复杂了
>
>    所以现在要管理的状态越来越多,越来越复杂
>
>    这些状态包括服务器返回的数据,缓冲数据,用户操作产生的数据,也包括一些UI的状态,比如某些元素是否被选中,是否显示加载特效,当前分页
>
> 2. 管理不断变化的state是非常困难的
>
>    1. 状态之间相互会存在依赖,一个状态的变化会引起另一个状态的变化,View页面也有可能引起状态的变化
>    2. 当应用程序复杂时,state在什么时候,因为什么原因而发生变化,发生了怎么样的变化,会变得相当难以控制和追踪
>    3. React在视图层帮助我们解决了DOM的渲染过程,但是state依然是留给我们自己来管理
>       1. 无论是组件定义自己的state,还是组件之间的通信通过props进行传递,也包括通过Context进行数据之间的共享
>       2. React主要负责帮助我们管理视图,state如何维护最终还是我们自己来决定
>
> 3. Redux就是一个帮助我们管理State的容器,Redux是JavaScript的状态容器,提供了可预测的状态管理
>
> 4. 除了React,也可以和其他界面库一起使用

## 核心理念

1. Store
2. Action
   * 所有的数据变化,必须通过派发(dispatch)action来进行更新
   * action是一个普通的JavaScript对象,用来描述这次更新的type和content
3. 定义纯函数reducer--->数据和action联系起来

## 三大原则

1. 单一数据源
   * 整个应用程序的state被存储到一颗object tree中,并且这个object tree只存储在一个store中
   * redux并没有强制让我们不能创建多个Store中,但是那样做并不利于数据的维护
   * 单一数据源可以让整个应用程序的state变得方便**维护,追踪,修改**
2. State是只读的
   * 唯一修改State的方法一定是触发action,不要试图在其他地方通过任何的方式来修改State
   * 这样就确保了View或网络请求都不能直接修改state,他们只能通过action来描述自己想要如何修改state
   * 这样可以保证所有的修改都被集中化处理,并且按照严格的顺序来执行,所以不需要担心race condition(竟态)的问题
3. 使用纯函数进行修改
   * 通过reducer将旧state和actions联系在一起,并且返回一个新的state
   * 随着应用程序的复杂度增加,我们可以将reducer拆分成多个小的reducers,分别操作不同的state tree的一部分
   * 但是所有的reducer都应该是纯函数,不能产生任何的副作用

## redux的目录结构

> redux在使用时一般要分开管理,将reducer,store,contants,action都分开管理,这样也方便我们维护

1. reducer:用于将action和state进行联系起来进行管理

   ```jsx
   import {
       INCREMENT,
       DECREMENT,
       ADD_NUMBER,
       SUB_NUMBER,
   } from "./constants.js";
   
   const initialState = {
       counter: 0
   }
   
   export default function reducer(state = initialState, action) {
       switch (action.type) {
           case INCREMENT:
               return { ...state, counter: state.counter + 10 };
           case DECREMENT:
               return { ...state, counter: state.counter - 5 };
           case ADD_NUMBER:
               return { ...state, counter: state.counter + action.num };
           case SUB_NUMBER:
               return { ...state, counter: state.counter - action.num };
           default:
               return state;
       }
   }
   ```

2. contants:用于管理你要进行操作的名字,设为常量,方便管理

   ```jsx
   export const INCREMENT = "INCREMENT";
   export const DECREMENT = "DECREMENT";
   export const ADD_NUMBER = "ADD_NUMBER";
   export const SUB_NUMBER = "SUB_NUMBER";
   ```

3. action:你想进行的状态改变行为,对于状态,你要进行什么操作使之改变

   ```jsx
   import {
       INCREMENT,
       DECREMENT,
       ADD_NUMBER,
       SUB_NUMBER,
   } from "./constants.js";
   
   export const incAction = () => ({
       type: INCREMENT,
   });
   
   export const decAction = () => ({
       type: DECREMENT,
   });
   
   export const addAction = num => ({
       type: ADD_NUMBER,
       num,
   });
   
   export const subAction = num => ({
       type: SUB_NUMBER,
       num,
   })
   ```

4. store:创建一个redux容器,将reducer传递进去,对于所有的状态进行一个管理

   ```jsx
   import { createStore } from "redux"
   import reducer from "./reducer.js";
   
   const store = createStore(reducer);
   
   export default store;
   ```

##  使用

> 将目录结构搭建好后,使用起来就比较方便了,只要在你所需要的组件引入store容器,将所需要使用的action进行一个派发,让reducer能辨别该执行什么操作,最后在挂载的时候,对于状态的改变进行订阅,这样数据发生改变后,就能重新执行render函数,重新渲染数据

## 将redux封装成通用的库

> 如果要想将这个包变成不需要依赖任何用户的库,其他小伙伴想要使用的话,只需要自己传入一个参数即可使用,我们还怎么做呢
>
> > 我们在这里使用context上下文来进行一个操作

### 第一步:创建一个context

创建一个context文件,里面放着我们的context

```jsx
import React from "react";

const StoreContext = React.createContext();

export { StoreContext };
```

### 第二步:在connect函数中进行一个引用

```jsx

import React, { Component } from 'react'
import { StoreContext } from './context';

// 首先我们使用高阶组件 来给我们的组件来传递函数
export default function connect(MapStateToProps, MapDispathToprop) {

    return function Enhanced(WrappedComponent) {
        return class EnhancedHOC extends Component {
            static contextType = StoreContext;
            constructor(props, context) {
                // 因为context在构造器中，一开始是没有值的，需要我们手动去给context赋值，从父类那继承下context，这样就相当于把从contextProvider中传递过来的值拿到并给到构造器中的context
                super(props, context);
                this.state = {
                    storeState: MapStateToProps(context.getState()),
                }
            }

            componentDidMount() {
                this.unSubscribe = this.context.subscribe(() => {
                    this.setState({
                        storeState: MapStateToProps(this.context.getState()),
                    })
                })
            }

            componentWillUnmount() {
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

### 第三步:在入口文件中引入context即可

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

### 最后一步:就是在组件中引入connect组件,进行action的派发

```jsx
import React from 'react';
import { addAction, subAction } from './store/createActions';
import connect from "./connect/connect(Wrapper)"

function App(props) {
    return (
        <div>
            <h1>计数器</h1>
            <h2>{props.counter}</h2>
            <button onClick={e => props.addFunction(5)}>增加</button>
            <button onClick={e => props.deFunction(10)}>减少</button>
        </div>
    )
}

const MapStateToProps = state => {
    return {
        counter: state.counter,
    }
};

const MapdispatchToProp = dispatch => {
    return {
        addFunction: function (num) {
            dispatch(addAction(num))
        },
        deFunction: function (num) {
            dispatch(subAction(num))
        }
    }

}


export default connect(MapStateToProps, MapdispatchToProp)(App);
```

## 组件的异步操作

![image-20210809192624314](https://gitee.com/IU_czx/images/raw/master/img/image-20210809192624314.png)

使用中间件进行网络请求

使用redux-thunk,他是如何发送异步请求呢,也可以使用redux-saga来进行异步操作

1. 我们知道,默认的情况下的dispatch(action),action需要是一个JavaScript对象
2. redux-thunk可以让dispatch(action函数),action可以是一个函数
3. 该函数会被调用,并且会传给这个函数一个dispatch函数和getState函数
   1. dispatch函数用于我们之后再次派发action
   2. getState函数考虑到我们之后的一些操作需要依赖原来的状态,用于我们可以获取之前的一些状态

## redux-saga

## 中间件的深入解析

## reducer的拆解

## React中的state如何管理

> 目前我学习了三种状态管理的方式
>
> 1. 组件中的state管理
> 2. 使用context数据共享状态
> 3. 使用redux管理应用状态
>
> 老师项目中采用的state管理方案
>
> * UI相关的组件内部可以维护的状态,在组件内部自己来维护
> * 大部分需要共享的状态,都交给redux管理
> * 从服务器请求的数据(包括请求的操作),交给redux管理

# React-Router的使用

## 前端路由的原理

> 1. 改变URL,但是页面不要进行强制刷新(例如a元素)
> 2. 自己来监听URL的改变,并且改变之后自己改变页面的内容

URL发生改变,同时不引起页面的刷新有两个办法

1. 通过URL的hash改变URL
2. 通过HTML5中的history模式修改URL

## URL的hash

1. URL的hash也就是锚点(#),本质上是改变window.location的href属性;
2. 我们可以通过直接赋值location.hash来改变href,但是页面不发生刷新

## HTML5的history

他是HTML5接口新增的,他有六种模式改变URL而不刷新页面:

1. replaceState:替换原来的路径
2. pushState:使用新的路径
3. popState:路径的回退
4. go:向前或向后改变路径
5. forward:向前改变路径
6. back:向后改变路径

## React-router基本使用



![image-20210810164614563](https://gitee.com/IU_czx/images/raw/master/img/image-20210810164614563.png)

## NavLink和Link

NavLink拥有exact属性,同时它可以为活跃的链接添加相对应的样式,活跃时他会自定义一个active的类名,你可以通过activeClassName来给它自定义类名

## Switch

可以实现排他操作,匹配到一个路由后,就不会匹配到其他路由

## Redirect

可以重定向到另外一个网站

[React Router: Declarative Routing for React.js](https://reactrouter.com/web/api/Redirect)

## 动态路由

可以通过match.params来拿取动态值

## 统一管理路由===>react-router-config

# Hook

## 前言

> 为什么需要**Hook**?
>
> 它可以让我们在不编写class的情况下使用state以及其他的react特性,例如生命周期
>
> **Class组件存在的问题**
>
> 1. 复杂组件变得难以理解:后期的逻辑设计的越来越复杂,不容易拆分
> 2. 难以理解的class:有时候很难搞清楚this的指向
> 3. 组件的复用状态很难

使用Hook有两个额外的规则

1. 只能在函数最外层调用Hook,不要在循环,条件判断或者子函数中调用
2. 只能在React的函数组件中调用Hook,不要在其他的JavaScript函数中调用

## 基本使用

> Hook:UseState
>
>   	本身是一个函数,来自React包
>												
>   	参数和返回值
>												
>   	参数:作用是给创建出来的状态一个默认值
>												
>   	返回值:数组
>
> ​	  元素一:当前state的值
>
> ​	  设置新的值时,使用到的一个函数

1. ***UseState***本身和之前的this.setState一样,可以传入一个函数,也可以直接传值,传入函数可以对之前的状态的进行一个累加操作,直接传值,则到最后面会合并

2. ***EffectHook***可以让我们实现类似于类组件中的生命周期函数功能

   1. 它在我们的状态发生改变时,就会执行useEffect中的回调函数

      ```react
      useEffect(() => {
          	//第一个回调函数时是相当于类组件中的componentdidMount()生命周期函数
              console.log("订阅");
      		//返回值是一个是一个函数,相当于类组件中的componentwillUnmount()生命周期函数
              return () => {
                  console.log("订阅取消");
              }
          }, [])
      //传入的第二个参数,是有关性能优化的
      //假如你要监听count的变化,你可以将count的值放进第二个参数数组中去,这样子的话,他就只会监听你的count的值,如果这个count的值不发生变化的话,那么不会触发useEffect()
      ```

   2. 可以使用多个useEffect函数,来进行多个操作,不用像类组件那样,全部放在一个生命周期函数

3. ***useContext***

   1. 它可以使用那些context共享出来的全局数据

4. useReducer:感觉和redux差不多,但是又没有redux便捷

5. UseCall:使用场景:在将一个组件中的函数，传递给子元素进行回调使用时，对useCallback对函数进行处理

6. useMemo:实际上也是为了性能优化,他针对的是返回值的优化

7. useRef:返回的是一个对象,并且返回的对象在整个生命周期不会变,可以用于保留上一次的值和这一次的值

   ![image-20210812104006508](https://gitee.com/IU_czx/images/raw/master/img/image-20210812104006508.png)

8. useImperativeHandle:让我们在使用ref的时候自定义暴露给父组件的实例值,意思就是,我想暴露给父组件什么属性

## 自定义Hook

看我代码

## fiber

> GUI渲染和JavaScript的代码执行是在一个线程, 他们都是单线程,所以他们都是互斥的
>
> 本来React的那些组件的渲染是在reconciliation中完成的,这些是耗时操作,但是react提出了fiber,将这些协同操作分成了许多多fiber,每一个fiber就相当于一个执行单元

# 网易云项目

## 项目规范

1. 文件夹,文件名称同意小写,多个单词以连接符(-)连接
2. Javascript变量采用小驼峰标识,常量全部使用大写字母,组件采用大驼峰
3. CSS采用普通CSS和styled-component结合来编写(全局采用普通CSS,局部采用styled-component);
4. 整个项目不再使用类组件,统一使用函数式组件,并且全面拥抱hooks
5. 所有的函数组件,为了避免不必要的渲染,全部使用memo进行包裹
6. 组件内部的状态,使用useState,useReducer;业务数据全部放在redux中进行管理
7. 函数组件内部基本顺序按照如下顺序编写代码
   1. 组件内部state管理
   2. redux的hooks代码
   3. 其他组件的hooks代码
   4. 其他逻辑代码
   5. 返回jsx代码
8. redux代码规范如下
   1. 每个模块有自己的reducer,通过combinReducer进行合并
   2. 异步请求代码使用redux-thunk,并且写在actionCreators中
   3. redux直接采用redux hook方式来进行编写,不再使用connect
9. 网络请求使用axios
   1. 对axios进行二次封装
   2. 所有的模块请求会放到一个请求文件中单独进行管理
10. 项目使用AntDesign
    1. 项目中某些AntDesign中的组件会被拿过来单独使用
    2. 但是多部分组件还是自己进行编写
11. 其他项目在开发中根据实际情况进行编写

## 步骤

### 1. 样式的初始化

1. 可以使用yarn或npm引入normalize.css包,或者你可以直接把normalize的文件下载下来,放进项目
2. 然后加入一些样式的重置,再设置一些全局样式

### 2. 给项目路径起别名

1. 如果你想给一些路径起别名,方便寻找,不需要根据相对路径一层层的往下找
2. 在React中安装@craco/craco这个包
3. 详细用法在我源代码中,写的很详细

### 3. 将公共组件头部和尾部完成

1. 对于在页面中进行切换的时候,使用路由,需要跳转到其他页面的话,使用a链接
2. 要想在styled-components中引入图片,要使用import引入

### 4. discover子路由模块地完成

1. 不要在父路由上加上exact属性,因为如果父路由精确匹配了,那么子路由就无法匹配到,那么,相对应的路由就无法显示出来

## 性能优化

### useSelector

> 在此之前,我们使用的是普通的redux管理,通过connect函数将组件和redux进行一个管理
>
> 但是这种方式在项目中,页面比较多显得比较麻烦,所以为了更方便进行一个管理,我们使用了Hook将redux和组件进行了一个管理
>
> 但是使用了Hook之后,还有一个有关性能的问题,那就是我们通过useSelector进行一个状态的获取,它所进行的状态比较是用'==='进行比较,而我们的这个函数每次返回的是一个新的对象字面量,所以不可能相等,所以我们在第二个参数那传递一个shallowEqual,来说明对他们进行一个**浅层比较**,这样的性能也会提升不少

### immutable.js

> 这个包也是用来帮助我们解决性能优化的
>
> 在项目中,reducer中,每个返回值都需要将之前的状态对象进行一个拷贝,在数量这么多,或者是状态对象十分庞大的情况下,性能会降低不少或显著减少,这个immutable包就是来帮助我们,它使用可持久化的数据结构,尽可能地帮助我们复用之前的对象,来帮助我们减少新对象在内存中的占用

## 项目笔记

### useRef的再学习

```jsx
import React, { memo } from 'react'
import { useRef } from 'react'

import resizeImg from "../../utils/resizeImg"

import { RankListWrapper } from "./styled"

export default memo(function RankList(props) {
    const { name, coverImgUrl, tracks } = props.rankInfo;
    const imgCover = resizeImg(coverImgUrl, 80)
    const iconRef = useRef();
    function iconDisplay() {
        iconRef.current.classList.add("icon-display");
    }
    function iconHide() {
        iconRef.current.classList.remove("icon-display");
    }
    return (
        <RankListWrapper>
            <div className="header">
                <a href="" className="cover"><img src={imgCover} alt="" /></a>
                <div className="headerRight">
                    <a className="rankName">{name}</a>
                    <div className="icon">
                        <a href="" className="play_icon"></a>
                        <a href="" className="collect_icon"></a>
                    </div>
                </div>
            </div>
            <div className="list">
                {
                    tracks.map((item, index) => {
                        if (index < 10) {
                            return (
                                <div className="list_content" id={item.name}
                                    onMouseOver={e => {
                                        console.log(iconRef);
                                        iconDisplay();
                                    }}
                                    onMouseLeave={e => {
                                        iconHide();
                                    }}
                                >
                                    <span className="No">{index + 1}</span>
                                    <a className="song text-nowrap">{item.name}</a>
                                    <div className="icon" ref={iconRef} id={item.name}>
                                        <a href="" className="play_icon"></a>
                                        <a href="" className="add_icon"></a>
                                        <a href="" className="collect_icon"></a>
                                    </div>
                                </div>
                            )
                        }
                    })
                }

            </div>
        </RankListWrapper >
    )
})


/**
 * 使用useRef的时候,他每次都是返回一个对象,而且是一样的
 * 所以像我上面这么写,是有问题的,你经过多少次循环,他也只会返回最后一次循环拿到的ref对象,所以也就造成了我把鼠标放上去,只有最后一个响应了我
 */
```

### 愚蠢的Undefined

这个问题确实很愚蠢,我真的没有想到,这个bug,我竟然会错在这里

本来在拿取数据的时候,第一次总会有undefined的值出现,我当时就想着,给他判断一下,只有不是undefined才能给它值,然后问题出现了,我给它的判断条件,它一次都没有生效,我还上网查了下,怎么判断undefined

经过我的种种查证,发现没有任何问题,当我快要崩溃的时候

发现比较undefined的值错了,在比较undefined的值的时候,一定要确认好哪个是表现出来undefined的值

### moment.js的相关使用

> 因为音乐播放,需要格式化他的播放时间,但是我又不想自己去封装一个函数,所以呢,我就想起了之前学习用到的moment.js库,所以我就去官网看着又重温复习一下,但是我觉得这样下去也不是事,所以我觉得还是要做笔记比较好,这里就记录我用到的,没用到的就不补充了,以后用到了 在回来补充

在React中使用这个包,就要进行下载

1. ```react
   yarn add moment
   yarn add moment-duration-format
   ```

2. 第一个包是moment主体,第二个包是我们对duration的一个格式化,这两个包都是我们这次用到的

3. 使用的话,就直接引入下面这两个就行,第二个包只要引入就行,你不用也可以

   ```jsx
   import moment from 'moment'
   import momentDurationFormatSetup from "moment-duration-format"
   ```

4. 接下来就直接贴我的使用代码了

   ```jsx
    const totalTime = moment.duration(songInfo.dt, "milliseconds").format("mm:ss");
   //这个参数就很明显了,就是传数据,第二个参数就是代表你传递的这个参数是什么单位
   //格式化:可以跟你想要格式化的样子
   //如果你想要这种初始没有值的话 也要显示00:00这种格式的
   //你可以使用trim这个属性,加上mid,这个代表的是即使没有值,也会取0
   //还有更详细的用法,我没用的,以后有需要了再去看
    const pTime = moment.duration(currentTime, "seconds").format("mm:ss", { trim: "mid" })
   ```

### 样式js怎么接受组件传递过来的信息

> 记住重要的一点,props是只有==自定义组件==才能传递的属性,像一般的html标签是无法传递props
>
> 在样式js中接收的话,就是用 ${props=>props.attribute}即可了

### 无限循环的值

> 起因是因为这段函数
>
> ```jsx
> const getNewArr = useCallback(() => {
>         let newArr = [];
>         for (let i = 0; i < 3; i++) {
>             newArr[i] = allRank[i] !== undefined && allRank[i].id;
>         }
>         return newArr;
>     }, [allRank])
> ```
>
> 因为我没有给函数加上useCallback,所以它每次渲染时都会调用这个函数,导致了我这个局面,所以我的newArr会无限次被创建出来,导致了我后面榜单数据显示不出来
>
> 为了性能优化,一定要记住,只有依赖的值变了,才能变,多多注意控制台输出的提醒,非常重要

## 项目部署

### 脚手架打包

只需要使用`yarn build`就能对使用脚手架的项目进行打包
