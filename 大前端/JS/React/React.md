# 前言

> 特点:
>
> 1. 声明式编程
> 2. 组件化开发
> 3. 多平台适配

开发React需要依赖三个库

1. react:包含react所必须的核心代码
2. react-dom:react渲染在不同平台所需要的核心代码
   1. web端会将jsx渲染成原生DOM
   2. 移动端会渲染成移动端的UI
3. babel:将jsx转换成React代码的工具  

# 认识JSX

## 01--案例1--电影列表

```jsx
<script type="text/babel">
        class  App extends React.Component {
            constructor(){
                super();
                this.state={
                    message:"无证之罪",
                    movies:['大话西游','流浪地球','星际穿越','盗梦空间'],
                }
            }
            render() {
                const liArr=[];
                for (let movie of this.state.movies){
                    liArr.push(<li>{movie}</li>);
                }

                return (
                    <div>
                        <h1>电影列表一(第一种方法渲染)</h1>
                    <ul>
                        {liArr}
                    </ul>
                        <h1>电影列表二(第二种方法渲染)</h1>
                        <ul>
                            {
                                this.state.movies.map((items)=>{
                                    return <li>{items}</li>;
                                }) 
                            }
                        </ul>
                    </div>
                    
                );
            }
        }

        ReactDOM.render(<App/>,document.querySelector(".app"))
    </script>

```

## 02--案例二---简单计数器

```jsx
<script type="text/babel">
        class  App extends React.Component {
            constructor(props){
                super(props);
                this.state={
                    counter:2
                }
            }
            render() { 
                return ( 
                    <div>
                        <h2>当前计数:{this.state.counter}</h2>
                        <button onClick={this.increment}>+1</button>
                        <button onClick={this.decrement.bind(this)}>-1</button>    
                    </div>
                );
            }
            increment=()=>{
                console.log(this);
                this.setState({
                    counter:this.state.counter+1,
                })
            }
            decrement(){
                this.setState({
                    counter:this.state.counter-1,
                })
            }
        }
         
        ReactDOM.render(<App/>,document.querySelector(".app"));
</script>
```

## 03---认识JSX语法

```jsx
  <script type="text/babel">

        /**
         * jsx实际上是嵌入到JavaScript中的一种结构语法
         * JSX的书写规范
         * 1. JSX的顶层只能有一个根元素,很多时候会在外层包裹一个div原生,也可以使用后面会学到的Fragment
         * 2. 为了方便阅读,通常在jsx的外层包括一个小括号(),这样可以方便阅读,并且jSX可以进行换行书写
         * 3. JSX的标签可以是单标签,也可以是双标签
         *    注意:如果是单标签,必须以/>结尾
         * 
        */


        const element=<h1>nihao</h1>
        ReactDOM.render();
    </script>
```

## 04---JSX注释

```jsx
    <script type="text/babel">
        class  extends React.Component {
            constructor(){
                super();
                this.state={
            
                }
            }
            render() { 
                return ( 
                    <h1>
                        {/* 这里面中写注释*/}
                        Hello World
                    </h1>
                );
            }
        }
         
        ReactDOM.render();
    </script> 
```

## 05--JSX嵌入数据

```jsx
    <script type="text/babel">
        class  extends React.Component {
            constructor(){
                super();
                this.state={
                    name:'CodeSpirit',
                    age:18,
                    age:[1,2,3,4],

                    /**
                    下面在{}什么都不显示
                    为什么React不让他们显示
                    因为有些时候会在{}做判断,如果判断为真或者为假,可能会有让他们显示为null或							undefined,这样子的话,就可以让内容不进行渲染在页面上
                    但如果要显示他们的话,可以将他们转换为字符串
                   	转换为字符串的三种方法
                   	*/
                    1. String();
                    2. 利用字面量 后面加上 "",用这个比较方便
                    3. 利用toString方法,并不是所有属性都有这个方法,谨慎使用
                    test:null,
                    test2:undefined,
                    test3:true,

                    // React中不能将对象作为参数传入JSX中
                    friend:{
                        name:"jiji",
                        age:19,
                    }
                }
            }
            render() { 
                return ( 
                <div>

                </div>
                );
            }
        }
         
        ReactDOM.render(<App/>,document.querySelector(".app"));
    </script>
```

## 06---JSX嵌入表达式

1. 运算表达式
2. 三元运算符
3. 执行一个函数

```jsx
    <script type="text/babel">
        class App extends React.Component {
            constructor(){
                super();
                this.state={
                    firstName:"czx",
                    lastName:"henbang",
                    isLogin:false,
                }
            }
            render() { 
                // 解构赋值
                const {firstName,lastName,isLogin}=this.state;
                console.log(firstName);
                return ( 
                <div>
                    {/* 运算表达式*/}
                    <h1>{firstName+lastName}</h1>
                    {/*三元表达式*/}
                    <h2>{isLogin ? "欢迎登录":"请先登录"}</h2>
                    {/*可以进行函数的调用*/}
                    <h2>{this.getFullName()}</h2>
                    {/*只要是JavaScript中的逻辑表达式都能使用*/}
                </div>
                );
            }
            
            getFullName(){
                return this.state.firstName+this.state.lastName;
            }
        }

         
        ReactDOM.render(<App/>,document.querySelector(".app"));
    </script>
```

## 07---JSX属性嵌入

```jsx
    <script type="text/babel">
        class App extends React.Component {
            constructor(){
                super();
                this.state={
                    title:'我是标题',
                    active:true,
                }
            }
            
            render() { 
                const {title,active}=this.state;
                return ( 
                    <div>
                    <h1 title={title}>Hello World</h1>
                    {/*像class,for这种javaScript的预留字,直接这么写是会出警告的,对于不同的预留字有不同的写法*/}
                    {/*1.class=>className 2.for=>htmlFor*/}
                    {/*绑定普通属性*/}
                    <h2 className={title}>1</h2>
                    {/*绑定class*/}
                    <h2 className={"box title "+(active?"active":"")}>2</h2>
                    {/*绑定内联样式*/}
                    <div style={{color:"red"}}>看我绑定内联样式</div>
                    </div>
                );
            }
        }
         
        ReactDOM.render(<App/>,document.querySelector(".app"));
    </script>
```

1. 像class,for这种javaScript的预留字,直接这么写是会出警告的,对于不同的预留字有不同的写法
   1. class=>className 
   2. for=>htmlFor
2. 当绑定内联样式的是时候,style要写{{}}这种格式,里面的{}是JSX语法

## 08---绑定事件--this处理

```jsx
    <script type="text/babel">
        class App extends React.Component {
            constructor(props){
                super(props);
                this.state={
                    
                }
                // 在构造器方法中,初始化的时候先进行调用,将bind先绑定,在后续中就把不需要连环绑定
                this.btnClick=this.btnClick.bind(this);
            }
            render() { 
                return ( 
                <div>
                    {/*第一种绑定的方法(显式绑定)*/}
                    <h1 onClick={this.btnClick}>Hello World</h1>
                    {/*第二种方式,箭头函数*/}
                    {/*方法三(推荐使用这个方法) 在语法中直接定义函数  或直接在函数中调用其他定义函数*/}
                    <button onClick={()=>{this.btnClick2()}}>点我</button>
                    <button onClick={this.btnClick3}>箭头函数测试</button>
                </div>
                );
            }

            btnClick(){
                console.log("我被点击了");
            }
            btnClick2(){
                console.log("我被点击了");
            }

            btnClick3=()=>{
                console.log("我被点击了",name);
            }
        }
         
        ReactDOM.render(<App/>,document.querySelector(".app"));
    </script>
```

总共有三种绑定事件

1. 通过bind来做一个显示绑定
2. 通过箭头函数,因为箭头函数自身不会绑定this,会寻找上下文
3. 通过箭头函数来调用其他普通函数,==推荐使用这种==
   * 因为调用的普通函数,传递参数非常方便
   * 如果只用箭头函数,不方便传递参数

## 09---绑定事件---传递参数

```jsx
    <script type="text/babel">
        class App extends React.Component {
            constructor(){
                super();
                this.state={
            
                }
            }
            render() { 
                return ( 
                    <div>
                        <button onClick={this.btnOnClick.bind(this)}>点击</button>
                        <button onClick={(e)=>{this.btnOnClick(e)}}>点击</button>
                    </div>
                );
            }
            btnOnClick(event){
                // 这个event是react自己合成的,不是原生的  
                console.log('我发生了点击',event);
            }
        }
         
        ReactDOM.render(<App/>,document.querySelector(".app"));
    </script>
```

1. 如果是不通过箭头函数调用,而是通过普通函数调用,会用Call(undefined,event)传递参数,所以在显式绑定之后,可以看到event
2. 如果是通过箭头函数的话,因为箭头函数不绑定this,所以call,apply,bind对于它无效,但是会传递event事件过来,

# JSX本质

## 01---JSX本质

1. 实际上,jsx仅仅只是React.createElement(Component,props,...children)函数的语法糖
   - 所有的jsx最终都会被转换成React.creatElement的函数调用
   - 第二个参数props是标签属性
2. React.createElement()的位置可以在源码中查看,主要看react文件夹中的入口文件index.js
   1. 他需要传递三个参数
      1. 参数一:type
         - 当前的ReactElement的类型
         - 如果是标签元素,那么就使用字符串表示div
         - 如果是组件元素,那么就使用组件的名称
      2. 参数二:config
         - 所有的jsx的属性都在config中以对象的属性和值的形式进行存储
      3. 参数三:children
         - 存放在标签中的内容,以children数组的方式进行存储
         - 如果是多个元素

```jsx
<h1 name="czx" age={18}>
  <h2></h2>
  <h2></h2>
</h1>
/*-------------------代码转换过程------------------------*/
/*#__PURE__*/
React.createElement("h1", {
  name: "czx",
  age: 18
}, /*#__PURE__*/React.createElement("h2", null), /*#__PURE__*/React.createElement("h2", null));
```



## 02---虚拟DOM的创建过程

1. 我们通过React.createElement最终创建出一个ReactElement对象
2. 为什么要创建一个ReactElement对象
   - 因为React利用ReactElement对象组成了一个JavaScript的对象树
   - JavaScript的对象树是大名鼎鼎的虚拟DOM
   - 频繁操作DOM树,效率是会比较低的,所以才会出现虚拟DOM这个概念
3. ==jsx->reactElement对象->通过render函数在将树结构的JavaScript对象(对象的多重嵌套)->渲染成真实的DOM树==

## 03--为什么要用虚拟DOM

1. 很难跟踪到状态发生的改变:原有的开发模式,我们很难跟踪到状态发生的改变,不方便针对我们的应用程序进行调试
2. 操作真实DOM的性能比较低:传统的开发模式会进行频繁的DOM操作,而这一做法的性能非常的低
   1. 首先 document.createElement本身创建出来的就是一个非常复杂的对象
   2. 其次,DOM操作会引起浏览器的回流和重绘. 

![image-20210731191859198](https://gitee.com/IU_czx/images/raw/master/img/image-20210731191859198.png)

声明式编程

1. 虚拟DOM帮助我们从命令式编程转到了声明式编程
2. React官方说法:Virtul DOM是一种编程理念
   1. 在这个理念中,UI以一种理想化或者虚拟化的方式保存在内存中,并且是一个简单的JavaScript对象
   2. 我们可以通过ReactDOM.render让虚拟DOM和真实DOM同步起来,这个过程叫做协调(reconcilition)
3. 这种编程方式赋予了React声明式的API
   1. 你只需要告诉React希望让UI是什么状态
   2. react来确保DOM和这些状态是匹配的
   3. 你不需要直接进行DOM操作,就可以从手动更改DOM,属性操作,事件处理中解放出来

# React脚手架

 ## 01---前端工程的复杂化

![image-20210801081453300](https://gitee.com/IU_czx/images/raw/master/img/image-20210801081453300.png)

## 02---脚手架

> 传统的脚手架是建筑学的一种结构:在搭建楼房,建筑物时,临时搭建出来的一个框架

编程中提到的脚手架(Scaffold),其实是一种工具,帮助我们快速生成项目的工程化结构

1. 每个项目做出来的效果不同,但是他们的基本工程化结构是相似的
2. 既然相似,没有必要从0开始搭建,完全可以使用一些工具,帮助我们生成基本的工程化模板
3. 不同的项目,在这个模板的基础之上进行项目开发或者进行一些配置的简单修改即可
4. 这样也可以间接保证项目的基本结构一致性,方便后期的维护

**总结**

> 脚手架让项目从搭建到开发,再到部署,整个流程变得快速和便捷

## 03---npm和yarn命令对比

![image-20210801083036030](https://gitee.com/IU_czx/images/raw/master/img/image-20210801083036030.png)

## 04---cnpm

> 如果安装某些东西安装不下来,选择淘宝的镜像,来进行安装

npm install -g cnpm --registry=https://registry.npm.taobao.org

## 05---packge.json和yarn.lock

1. package.json中存放的是依赖,依赖前面加上^这个的,说明如果更新了小版本之后,package.json的版本也会随之更新
2. yarn.lock里面存放的是真实版本,就是当前实际安装的是什么版本

## 06---目录结构分析

![image-20210801090240348](https://gitee.com/IU_czx/images/raw/master/img/image-20210801090240348.png)

## 07---了解PWA

1. PWA全称Progress Web App,即渐进式WEB应用
2. 一个PWA应用首先是一个网页,可以通过Web技术编写出一个网页应用
3. 随后添加上App Manifest和Service Worker来实现PWA的安装和离线等功能
4. 这种Web存在的形式,我们称之为WebApp

**PWA解决了那些问题**

1. 可以添加至主屏幕,点击主屏幕图标可以实现启动动画以及隐藏地址栏
2. 实现离线缓冲功能,即使用户手机没有网络,依然可以使用一些离线功能
3. 实现了消息推送
4. 等等一系列类似于Native App相关的功能

## 08---Webpack

> 他是一个现代JavaScript应用程序的静态模块打包器(Module bundler)
>
> 当webpack处理应用程序时,他会递归地构建一个依赖关系图(dependecy graph),其中包含应用程序需要的每个模块,然后将所有这些模块打包成一个或多个bundle

![image-20210801091840239](https://gitee.com/IU_czx/images/raw/master/img/image-20210801091840239.png)

# React组件化开发

## 前言

> 分而治之的思想

## 01-React的组件化

1. 组件化思想的应用:
   * 有了组件化的思想,我们在之后的开发中就要充分的利用它
   * 尽可能的将页面拆分成一个个小的,可复用的组件
   * 这样让我们的代码更加方便组织和管理,并且扩展性页更强
2. React的组件相对于Vue的更加灵活和多样,按照不同的方式可以分成很多组件类
   * 根据组件的定义方式,可以分为,
     1. <span style="color:skyBlue">函数组件(Functional Component)</span>
     2. <span style="color:skyBlue">类组件(Class Component);</span>
   * 根据组件内部是否有状态需要维护,可以分为:
     1. <span style="color:skyBlue">无状态组件(Stateless Component)</span>
     2. <span style="color:skyBlue">有状态组件(Stateful Component);</span>
   * 根据组件的不同职责,可以分成
     1. <span style="color:skyBlue">展示性组件(Presentation Component)</span>
     2. <span style="color:skyBlue">容器性组件(Container Component)</span>

## 02-类组件

定义类组件的要求

* 组件的名称是大写字符开头(无论类组件还是函数组件)
* 类组件需要继承自React.Component
* 类组件必须实现render函数

## 03-render函数的返回值

1. React元素
2. 数组或fragment元素
3. Portals(入口,大门):可以渲染子节点到不同的DOM树上去
4. 字符串或数值类型:他们在DOM中被渲染成文本节点
5. 布尔型或null:什么都不渲染

## 04-认识生命周期

> React组件也有自己的生命周期,了解组件的生命周期可以让我们在最合适的地方完成自己想要的功能

生命周期和生命周期函数的关系

1. 生命周期是一个抽象的概念,在整个生命周期的整个过程,分成了很多阶段
   1. 装载阶段(Mount),组件在第一次在DOM树上被渲染的过程
   2. 更新阶段(Update),组件状态发生变化,重新更新渲染的过程
   3. 卸载阶段(UnMount),组件从Dom树种被移除的过程
2. React内部为了告诉我们当前处于那些阶段,会对我们组件内部实现的某些函数进行回调,这些函数就是生命周期函数(类,普通函数没有)
   1. 比如实现componentDidMount函数:组件已经挂载到DOM上,就会回调
   2. 比如实现componentDidUpdate函数:组件发生更新时,就会回调
   3. 比如实现componentWillUnmount函数:组件即将被移除时,就会回调
   4. 我们可以在这些回调函数种编写自己的逻辑代码,来完成自己的需求功能

![image-20210801164849218](https://gitee.com/IU_czx/images/raw/master/img/image-20210801164849218.png)

## 05-生命周期函数

**Constructor**

* 如果不初始化state或不进行方法绑定,则不需要为React组件实现构造函数
* constructor通常只做两件事情:
  * 通过给this.state赋值对象来初始化内部的state
  * 为事件绑定实例(this);

**componentDidMount**

* componentDidMount()会在组件挂载后(插入DOM树中)立即调用
* componentDidMount中通常在哪里进行操作呢
  * 依赖于DOM的操作可以在这里进行
  * 在此处发送网络请求的最好的地方
  * 可以在此处添加一些订阅

**componentDidUpdate**

* 他会在更新后立即被调用,首次渲染不会执行此方法
* 当组件更新后,可以在此处对DOM进行了操作
* 如果你对更新前后的props进行了比较,也可以选择在此处进行网络请求;(例如,当props未发生变化时,则不会执行网络请求)

**componentWillUnmount**

* componentWillUnmount()会在组件卸载即销毁之前直接调用
* 在此方法中执行必要的清理操作
* 例如,请求timer,取消网络请求或清除,在component中创建订阅

## 06-组件的嵌套

![image-20210801211753376](https://gitee.com/IU_czx/images/raw/master/img/image-20210801211753376.png)

 ## 07-组件的通信

> 组件的通信非常重要

父传子的通信

下面是父亲

> 通过props属性来进行通信

```js
export default class App extends Component {
    render() {
        return (
            <div>
                <Children name='CodeSpirit' age='18'/>
            </div>
        )
    }
}
```

下面是儿子(函数组件)

```js
export function Children(props) {
    const {name,age}=props;
    return (
        <div>
            {name}
            <p>{age}</p>
        </div>
    )
}
```

下面是儿子的类组件形式

```js
export class Children extends Component{
	//其实下面涉及到一些高级的东西了,我们怎么搞懂的,目前先记住吧
    // 但是为什么可以不经过constructor就能引用props呢
    // answer:他默认就是通过这种构造方式进行构造的
    render(){
    const {name,age}=this.props;
        return (
            <h1>我是{name},今年{age}岁</h1>
        );
    }
}
```



## 08-propTypes

> 数据类型验证

现在不默认引进,要想使用的话,得自己引入包

```js 
import PropTypes from 'prop-types';
```

**使用方法:**

下面这个只是示例

对你要验证的属性设定想要传递的类型

```js
Children.propTypes={
    name:PropTypes.string,
    age:PropTypes.number,
    names:PropTypes.array,
}
```

你也可以这么使用

```js
// 这也是ES6中的classfiled
export  class Test extends Component {
    static propTypes={
        // 在这里面也可以设置数据类型验证
    }

    static defaultProps={
        name:"CodeSpirit",
         //在这里面可以设置props默认的值 
    }
}

```

## 09-子组件传递父组件

> 在某些情况下,我们需要子组件向父组件传递消息:
>
> 在vue中通过自定义事件来完成的
>
> 在React中同样通过props传递消息,只是让父组件给子组件传递一个回调函数,在子组件中调用这个函数即可

## 10-实现类似于Vue中Slot插槽的两种方式

1. 通过this.props.children来实现
   1. 这种呢一般是用于只插入一个东西比较好
   2. 传入多个元素,顺序不能出错,不灵活
2. 通过this.props来实现,比较灵活了
3. 上面两种方式都实现了,具体看我代码

```js
import React, { Component } from 'react'
import NavBar from './01-NavBar';
import NavBar2 from './02-NavBar2';
export default class App extends Component {
    render() {
        return (
            <div>
                {/* 第一种办法,采用双标签 this.props.children */}
                <NavBar>
                    <div>我是左边</div>
                    <div>我是中间</div>
                    <div>我是右边</div>
                </NavBar>
                <hr/>
                <NavBar2    leftSlot={<div>我是左边</div>}
                            centerSlot={<div>我是中间</div>} 
                            rightSlot={<div>我是右边</div>}/>
            </div>
        )
    }
}
```

```js
import React, { Component } from 'react'

export default class NavBar extends Component {
     
    render() {
        return (
            <div className='navbar'>
                <div className='LeftSlot'>  {this.props.children[0]}</div>
                <div className='CenterSlot'>{this.props.children[1]}</div>
                <div className='RightSlot'> {this.props.children[2]}</div>
            </div>
        )
    }
}

```

```js
import React, { Component } from 'react'

export default class NavBar extends Component {
    render() {
    const {leftSlot,centerSlot,rightSlot}=this.props;
        return (
            <div className='navbar'>
                <div className='LeftSlot'>  {leftSlot}</div>
                <div className='CenterSlot'>{centerSlot}</div>
                <div className='RightSlot'> {rightSlot}</div>
            </div>
        )
    }
}

```

## 11-跨组件通信

### 1. 层层传递

第一种方法:一层一层传递,每一层传递到下一层,简化-->可以在中间传递层使用JSX的语法:属性展开

### 2.context传递

1. 非父子组件数据的共享
   1. 在开发中,比较常见的是数据传递方式是通过props属性自上而下(由父到子)进行传递
   2. 但是对于有一些场景:比如一些数据需要在多个组件中进行共享(地区偏好,UI主题,用户登录状态,用户信息)
   3. 如果我们在顶层的App中定义这些信息,之后一层层传递下去,对于一些中间层不需要数据的组件来说,是一种冗余的操作
2. React提供了一个API:Context
   1. React.createContext
      1. 创建一个需要共享的Context对象
      2. 如果一个组件订阅了Context,那么这个组件会从离自身最近的那个匹配的Provider中读取到context值
      3. defaultValue是组件在顶层查找过程中没有找到对应的Provider,那么就使用默认值
   2. Context.Provider
      1. 每个Context对象都会返回一个provider React组件,它允许消费组订阅context的变化
      2. provider接受一个value属性,传递给消费组件
      3. 一个Provider可以和多个消费组件有对应关系
      4. 多个provider也可以嵌套使用,里层的会覆盖外层的数据
      5. 当Provider的Value值发生变化时,它内部的所有消费组件都会重新渲染
   3. Class.contextType
      1. 挂载在class上的contextType属性会被重赋值为一个由React.createContext()创建的Context对象
      2. 这能让你使用this.context来消费最近Context的值
      3. 你可以在任何生命周期函数中访问到它,包括render函数

### 3. 使用方法

1. 通过props来进行层层传递一个特定的值

```js
import React, { Component } from 'react';

function ProfileHeader(props) {
  return (
    <div>
      <h2>用户昵称: {props.nickname}</h2>
      <h2>用户等级: {props.level}</h2>2
    </div>
  )
}

function Profile(props) {
  return (
    <div>
      {/* <ProfileHeader nickname={props.nickname} level={props.level}/> */}
      <ProfileHeader {...props}/>
      <ul>
        <li>设置1</li>
        <li>设置2</li>
        <li>设置3</li>
        <li>设置4</li>
      </ul>
    </div>
  )
} 

export default class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      nickname: "kobe",
      level: 99
    }
  }

  render() {
    // const {nickname, level} = this.state;

    return (
      <div>
        <Profile {...this.state}/>
      </div>
    )
  }
}

```

> 这种方法比较麻烦,因为需要层层传递,对于传递的中间件来讲,根本就用不到传过来的数据,会显得非常冗余,所以为了解决这个问题,有了Context的出现

2. 针对类组件的使用方法

```js
import React, { Component } from 'react'

//1.第一步:首先声明一个Context对象,这个对象是全局共享的
const UserContext=React.createContext({
    //补充:这个下面的值是默认值,如果没有找到相对应要共享的值,这个值会成为默认值
    name:'CodeSpirit',
    age:18,
})



export class ProfileHeader extends Component{
    /**第三步:指定contextType读取我们定义的USerContext
    *  React会往上找到最近的UserContext的Provider,然后使用它的值
    */
    static contextType=UserContext;
    render(){
        console.log(this.context);
        return (
            <div>
            //然后就可以根据this.conText中的值拿到向对应的值
            <div>{this.context.name}</div>
            <div>{this.context.age}</div>
            </div>
        );
    }
}

export class Profile extends Component{
    render(){
        return (
            <div>
                <ProfileHeader/>
                <ul>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                </ul>
            </div>
        )
    }
} 

export default class App extends Component {
    constructor(props){
        super(props)
        this.state=({
            name:'我是CodeSpirit',
            age:18,
        })
    }
    render() {
        return (
            <div>
        //第二步:你要在父组件中使用Context.Provider标签将子组件包裹起来,这样profile中的组件及profile		     中的子组件都成为了Context中的全局值,在Provider中通过value传值.
                <UserContext.Provider value={this.state}>
                    <Profile/>
                </UserContext.Provider>
            </div>
        )
    }
}

```

3. 针对函数组件的使用方法

> 其实使用方法差不多,它用了UserContext.Consumer来取值

```js
import React, { Component } from 'react'

const UserContext=React.createContext({
    name:'CodeSpirit',
    age:18,
})




// 函数组件要使用UserContext.Consumer
function ProfileHeader(){
    return (
        //不同的地方就在这下面,使用Consumer标签包裹,然后可以拿到之前Provider的值,就能使用了
        <UserContext.Consumer>
        {
            value=>{
                return (
                    <div>
                    <div>{value.name}</div>
                    <div>{value.age}</div>
                    </div>
                )
            }
        }
        </UserContext.Consumer>
    )
}

export class Profile extends Component{
    render(){
        return (
            <div>
                <ProfileHeader/>
                <ul>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                </ul>
            </div>
        )
    }
} 

export default class App extends Component {
    constructor(props){
        super(props)
        this.state=({
            name:'我是CodeSpirit',
            age:18,
        })
    }
    render() {
        return (
            <div>
                <UserContext.Provider value={this.state}>
                    <Profile/>
                </UserContext.Provider>
            </div>
        )
    }
}

```

4. 多个Context的通信方式

> 这样的方法会显得比较复杂,这是后面要学的redux的内容,可以解决这种问题,好好学啊!!!

```js
import React, { Component } from 'react'

const UserContext=React.createContext({
    name:'CodeSpirit',
    age:18,
})
const ThemeContext=React.createContext({
    color:'red',
})



// 函数组件要使用UserContext.Consumer
function ProfileHeader(){
    return (
        //在这下面也是如此,要想拿到值,就要嵌套包裹
        <UserContext.Consumer>
        {
            value=>{
                return (
                   <ThemeContext.Consumer>
                       {
                           theme=>{
                               return(
                                <div>
                                <div>{value.name}</div>
                                <div>{value.age}</div>
                                <p style={{color:theme.color}}>看我颜色变了没</p>
                                </div>
                               )
                           }
                       }
                   </ThemeContext.Consumer>
                )
            }
        }
        </UserContext.Consumer>
    )
}

export class Profile extends Component{
    render(){
        return (
            <div>
                <ProfileHeader/>
                <ul>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                    <li>1</li>
                </ul>
            </div>
        )
    }
} 

export default class App extends Component {
    constructor(props){
        super(props)
        this.state=({
            name:'我是CodeSpirit',
            age:18,
        })
        this.theme=({
            color:"red",
        })
    }
    render() {
        return (
            //多个COntext的时候,要用Provider嵌套包裹起来
            <div>
                <UserContext.Provider value={this.state}>
                    <ThemeContext.Provider value={this.theme}>
                    <Profile/>
                    </ThemeContext.Provider>
                </UserContext.Provider>
            </div>
        )
    }
}

```

## 事件总线

> 如果在开发中有跨组件之间的事件传递,可以用==事件总线==
>
> 使用
>
> `yarn add events`
>
> 常用API
>
> - 创建EventEmitter对象：eventBus对象；
> - 发出事件：`eventBus.emit("事件名称", 参数列表);`
> - 监听事件：`eventBus.addListener("事件名称", 监听函数)`；
> - 移除事件：`eventBus.removeListener("事件名称", 监听函数)`；

## 12-SetState详解

### 为什么要使用SetState

1. 要想修改数据渲染到页面上去，就必须使用setState才能进行修改
2. 为什么我们可以使用这个方法，因为这是继承过来的

### setState异步更新

为什么setState要设置成异步更新：

官方回答：https://github.com/facebook/react/issues/11527

老师总结：

1. setState设计为异步，可以显著的提高性能
   1. 如果每次调用setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的
   2. 最好的办法应该是获取到多个更新，之后进行批量更新
2. 如果同步更新了state，但是还没有执行render函数，那么state和props不能保证同步
   1. state和props不能保持一致型，会在开发中产生很多问题

setState可以传递两个参数，第二个参数是结果的回调函数

### setState同步情况

1. 放在定时器内 
2. 放在原生监听中

### 数据合并

在源码中，有一个object.assign(),把要修改的数据覆盖到this.state,进行一个数据的合并

### setState（Updater|stateChange,[CallBack]）

> 在setState中，我们第一个参数传递的是Updater或stateChange

1. 如果你想基于之前的状态中的值进行一个累计操作的话，使用updater函数

   1. 他是一个带有形式参数的updater函数（state，props）=>statechange

   2. **state**是之前的状态的应用（他不应该直接被修改😉),应该使用基于state和props构建的新对象来表示变化

   3. updater 函数中接收的 `state` 和 `props` 都保证为最新。updater 的返回值会与 `state` 进行浅合并。

   4. ```js
      this.setState((state,props)=>{
          return {counter:state.counter+props.step};
      })
      ```

2. 对于第二个callback回调函数,如果你想要立马拿到state更新完后的值,可以在这个callback函数上拿到这个值，==官方建议==：推荐在componentDidUpdate()中代替此方式

3. 当然你也可以在第一个参数中传递一个对象类型的数据,他会将传入的对象==浅层合并==到新的state中,因为他是通过object.assign()来进行对象的赋值的,如果多次调用这个的话,值只会加一次,因为后面的值会覆盖前面的值

## 13-React更新机制

![image-20210803102257110](https://gitee.com/IU_czx/images/raw/master/img/image-20210803102257110.png)

<h2><Strong>1. 情况一</Strong></h2>

1. 当节点为不同元素的时候,React会拆卸掉原来的树,并且建立新的元素

   1. 当卸载一颗树的时,对应的DOM节点会被销毁,并且执行componentwillUnmount()方法

   2. 当建立一颗新的树的时候,对应的节点会被创建以及插入到DOM中,组件实例将执行compnentWillMount()方法,紧接着componentDidMount()方法

   3. ```jsx
      <div>
      	<Componnet/>    
      <div>
          
      <Span>
          <Component/>
      </Span>
      ```

      > 上面两个是不会复用的,因为节点元素不一样,会被销毁重建

<h2><Strong>情况二
</h2>

![image-20210803103745993](https://gitee.com/IU_czx/images/raw/master/img/image-20210803103745993.png)

<h2><Strong>情况三

![image-20210803104015449](https://gitee.com/IU_czx/images/raw/master/img/image-20210803104015449.png)

## 14-Key的优化

> 在我们前面遍历列表时,总是会提示一个警告,让我们加入一个keyt属性

1. 方式一:在最后位置中插入数据,有无key影响不大
2. 方式二:在前面插入数据,在没有key的状况下,所有的li都要进行修改,
3. 当子元素上有key时,React使用key来匹配原有树上的子元素以及最新树上的子元素
4. 不要使用index作为key,因为在前面插入,index依然会变,对于性能没有任何优化

## 15-Render函数的调用

> 减少render的调用,性能优化,能解决类组件的调用

1. shouldComponentUpdate()
2. pureComponent()  

> 函数组件的性能优化,memo

```js
import React, {PureComponent,memo } from 'react'


// memo的用法
// 用memo包裹住函数组件,会生成一个新的函数,这个函数就是我们想要的函数组件了
const MemoHeader=memo(
function MemoHeader(){
    console.log('memoHeader被调用');
    return (
        <div>
            memoHeader
        </div>
    )
}
)
// 使用PureComponent节省性能
export  class Header extends PureComponent {
    render() {
        console.log("Header 被调用");
        return (
            <div>
                Header
            </div>
        )
    }
}


export  class Content extends PureComponent {
    render() {
        console.log("Context 被调用");
        return (
            <div>
                Content
            </div>
        )
    }
}


export default class App extends PureComponent {
    constructor(props){
        super(props);
        this.state=({
            counter:1,
        })
    }
    render() {
        console.log('App render被调用');
        return (
            <div>
                <MemoHeader/>
                <Header/>
                <Content/>
                <span>{this.state.counter}</span>
                <button onClick={e=>{this.increment()}}>+1</button>
            </div>
        )
    }

    // 要想阻止render函数执行,可以使用下面这个生命周期函数
    // shouldComponentUpdate(){
    //     return false;
    // }

    increment(){
        this.setState({
            counter:this.state.counter+1,
        })
    }
}

```

上面有函数组件和类组件的使用方法

## 16-全局事件传递events

> 安装:yarn add events

```js
import React, { PureComponent } from 'react'
// 1.导入包
import EventEmitter from 'events';

// 2.构造对象
const evnetBus=new EventEmitter();

class Home extends PureComponent{
    componentDidMount(){
        //4.在挂载完成时添加监听事件
        evnetBus.addListener ("SayHello",this.handlerHelloListener)
    }
    componentWillUnmount(){
        //5.在即将卸载时卸载监听
        evnetBus.removeListener("SayHello".this.handlerHelloListener)
    }

    handlerHelloListener(...args){
        const arr=[...args];
        console.log(arr);
        console.log(...args);
    }
    render(){
        return (
            <div>
                Home
            </div>
        )
    }
}
class Profile extends PureComponent{
    render(){
        return (
            <div>
                profile
                <button onClick={e=>this.emmitEvent()}>点击</button>
            </div>
        )
    }
    
    emmitEvent(){
        //3. 使用emit进行事件传递
        evnetBus.emit('SayHello',123,'Home');
    }
}

export default class App extends PureComponent {
    render() {
        return (
            <div>
                <Home/>
                <Profile/>
            </div>
        )
    }
}
```

![image-20210803165725420](https://gitee.com/IU_czx/images/raw/master/img/image-20210803165725420.png) 

## 17-setState传递的数据最好不可变

首先来看代码

```jsx
import React, { Component } from 'react'
// import PropTypes from 'prop-types'



export default class App extends Component {
    constructor(props){
        super(props);
        this.state=({
            students:[  {name:'czx',age:18},
                        {name:'qwe',age:19},
                        {name:'小林',age:20},
                        {name:'小妹',age:21},
                    ]
        })
    }

    shouldComponentUpdate(newProps,newStates){
        if(this.state.students!==newStates){
            return true;
        }
        return false;
    }

    render() {
        return (
            <div>
                <ul>
                    {
                        this.state.students.map((item,index)=>{
                            const {name,age}=item;
                            return (
                                <div>
                                <li key={item}>name:{name} age:{age}</li>
                                <button onClick={e=>this.increment(index)}>增加年龄1岁</button>
                                </div>
                            )
                        })
                    }
                </ul>
                <button onClick={e=>this.addNewStudent()}>增加新学生</button>
            </div>
        )
    }

    increment(index){
        let {students}=this.state;
        students[index].age+=1;
        this.setState({
            students:students,
        })
    }
    addNewStudent(){
        const newStudents=[...this.state.students]
        newStudents.unshift({name:'曹志贤',age:18});
        this.setState({
            students:newStudents,
        })
    }
}
// App.propTypes={
//     students:PropTypes.any.isRequired
// }

```

> 来讲解一下浅拷贝的事情，如果在修改setState中的值时，直接对this.state进行一个修改，那么对于用shouldComponentUpdate而言，是没有任何性能优化的

如果你想要添加数据的时候,使用的是这种方法,就是我上面说的,没有任何性能优化,我们通过一张图来讲解一下

```js
const students=this.state.students
students.push(新对象)
```

![image-20210803154528405](https://gitee.com/IU_czx/images/raw/master/img/image-20210803154528405.png)

这张图也是很好的解释了浅拷贝的原理,只复制了表面一层,在数组中对对象的引用仍然是原来的没有变

## 18-如何使用ref

> 在React的开发模式中,通常情况下,不建议直接操作原生DOM,但是某些特殊情况下,确实需要获取到DOM进行操作:
>
> 1. 管理焦点
> 2. 触发强制动画
> 3. 继承第三方DOM库

如何创建refs来获取对应的DOM呢,目前有三种方式

```js
import React, { Component,createRef } from 'react'

export default class App extends Component {
    constructor(props){
        super(props);

        this.title=createRef();
        this.titleEl=null;
    }
    render() {
        return (
            <div>
                {/* 第一种方式:通过ref属性传递字符串拿到DOM元素 */}
                <h1 ref='title'>Hello React!</h1>
                {/* 第二种方式:传递一个对象 (目前React推荐的方式)*/}
                <h1 ref={this.title}>传递一个对象</h1>
                {/* 第三种方式:传递一个回调函数 */}
                <h1 ref={(arg)=>{this.titleEl=arg}}>传递一个对象</h1>
                <button onClick={e=>this.getContext()}>获取</button>
            </div>
        )
    }

    getContext(){
        console.log(this.refs.title);
        this.refs.title.textContent='Hello! CodeSpirit'
        // 推荐使用下面这种方式进行原生操作
        console.log(this.title.current);
        // 第三种方式:传递回调函数
        console.log(this.titleEl);
    }
}

```

## 19-ref的类型

1. 当ref对象在组件上的时候,拿到的对象就是组件对象,也可以调用组件对象的方法
2. 不能在函数式组件使用ref,因为函数组件没有实例

## 20-受控组件

> 在react中,HTML表单的处理方式和普通的DOM元素不太一样,表单元素通常会保存在一些内部的state上

![image-20210804081419010](https://gitee.com/IU_czx/images/raw/master/img/image-20210804081419010.png)

```js
import React, { Component } from 'react'

export default class App extends Component {
    constructor(props){
        super(props);
        this.state={
            username:'',
            password:'',
            email:'',
            selected:'banana',
        }
    }
    render() {
        return (
            <div>
                <form onSubmit={e=>this.handlerChange(e)}>
                    <label htmlFor="username">
                        用户名
                        {/* 通过onchange进行监听状态改变 */}
                        <input type="text" name="username" id="username" onChange={e=>{this.handlerChange(e)}} value={this.state.username}/>
                    </label>
                    <label htmlFor="password">
                        密码
                        <input type="text" name="password" id="password" onChange={e=>{this.handlerChange(e)}} value={this.state.password}/>
                    </label>
                    <label htmlFor="email">
                        邮箱
                        <input type="text" name="email" id="email" onChange={e=>{this.handlerChange(e)}} value={this.state.email}/>
                    </label>
                    {/* select要在selected中使用value获取选中的值 */}
                    <select name="selected" value={this.state.selected} onChange={e=>{this.handlerChange(e)}}>
                        <option value="apple">苹果</option>
                        <option value="banana">香蕉</option>
                        <option value="pear">梨</option>
                    </select>
                </form>
            </div>
        )
    }

    handlerChange(e){   
        this.setState({
            // Es6中的新语法----计算属性名
            [e.target.name]:e.target.value,
        })  
    }
}

```



## 21-非受控组件

> 交给ref,通过ref使用原生DOM来拿取数据,这样子react无法对他进行管控,不方便管理
>
> 官方推荐使用受控组件,某些特殊情况下使用受控组件

```js
import React, { Component, createRef } from 'react'

export default class App extends Component {
    constructor(props){
        super(props);
        this.username=createRef();
    }
    render() {
        return (
            <div>
                <form onSubmit={e=>this.handlerChange(e)}>
                    <label htmlFor="username">
                        用户名
                        <input type="text" name="username" id="username" ref={this.username}/>
                    </label>
                </form>
            </div>
        )
    }

    handlerChange(e){   
        e.preventDefault();
        console.log(this.username.current.value);
    }
}
```

## 22-高阶组件

> 首先来回顾一下什么是高阶函数
>
> 高阶函数需要满足以下两个条件
>
> 1. 接受一个或多个函数作为输入
> 2. 输出一个函数
>
> 比如:filter,map,reduce都是高阶函数
>
> 好,现在我们在来看下高阶组件
>
> 1. 高阶组件的英文是Higher-Order Component,简称HOC
> 2. 官方定义:高阶组件是参数为组件,返回值为新组件的函数

### 高阶组件的基本用法:

```js
import React, { Component, PureComponent } from 'react'

class App extends Component {
    render() {
        return (
            <div>
                你好 {this.props.name}
            </div>
        )
    }
}

function enhanced(App){
    class NewComponent extends PureComponent {
        render(){
            return <App {...this.props}/>;
        }
    }
    // 你可以给每个组件设置你自己想要的名字
    NewComponent.displayName='CodeSpirit';
    return NewComponent;
}

const EhanceComponent=enhanced(App);
export default EhanceComponent;

```

### 高阶组件的props增强用法

```jsx
import React, { Component, PureComponent } from 'react'

class Home extends PureComponent{
    render(){
        return (
            <div>
            <h2>Home</h2>
            <h3>{`昵称:${this.props.nickname}`}</h3>
            <h3>{`等级:${this.props.level}`}</h3>
            <h3>{`中国:${this.props.region}`}</h3>
            </div>
        )
    }
}

function EnhanceRegionProps(App){
    return props=>{
        return <App {...props} region='中国'/>;
    }
}


export default class App extends Component {
    render() {
        return (
            <div>
                App
                {/* 假设有很多相同组件,我们要对这个组件加上某个特定属性,如果直接在组件上加属性传递,无疑会浪费很多时间
                    而且这会修改我们放在这里组件的结构,为了不这么做,我们可以在定义一个高阶组件
                */}
                <Home nickname='CodeSpirit' level={99}/>
                <EnhancedHome nickname='CodeSpirit' level={99}/>
            </div>
        )
    }
}

// 你可以使用默认导出这个组件,使用我们定义的高阶函数,来使得他返回一个新的组件
// export default EnhanceRegionProps(Home);


// 你也可以使用以下方法,
// 使用这种方法,返回的新组件,要在父组件中对引用的组件名进行一个修改
const EnhancedHome=EnhanceRegionProps(Home);

```

### 高阶组件通过Context的使用方法

```jsx
import React, { Component, createContext, PureComponent } from 'react'


// 第三种版本:创建一个高阶组件
function withUSer(App){
    return props=>{
        console.log(props);
        return (
            <UserContext.Consumer>
                {
                    user=>{
                        console.log(props);
                        console.log(user);
                        return <App {...props}{...user}/>
                    }
                }
            </UserContext.Consumer>
        )
        
        
    }
}

// 创建一个context
const UserContext=createContext({
    nickname:'默认',
    level:-1,
    region:'中国,'
})

// 第一个版本
class Home extends PureComponent{
    static contextType=UserContext;
    render(){
        return (
            <div>
            <h2>Home</h2>
            <h3>{`昵称:${this.context.nickname}`}</h3>
            <h3>{`等级:${this.context.level}`}</h3>
            <h3>{`中国:${this.context.region}`}</h3>
            </div>
        )
    }
}

// 第二个版本
class Home2 extends PureComponent{
    render(){
        return (
            <UserContext.Consumer>
                {
                    user=>{
                       return(
                       <div>
                            <h2>Home</h2>
                            <h3>{`昵称:${user.nickname}`}</h3>
                            <h3>{`等级:${user.level}`}</h3>
                             <h3>{`中国:${user.region}`}</h3>
                               
                        </div>
                       )
                }
                 }
            </UserContext.Consumer>
        )
    }
}

// 第三个版本:使用高阶组件
// 使用这种方式的话呢,可以节省一部分的冗余代码,如果不把consumer提取出来的话,
// 每引用一次provider就要在这个组件内重新写入一个consumer,太浪费时间,用高阶组件给他返回一个包裹的Consumer会更便捷
class Home3 extends PureComponent{
    render(){
        return (
                       <div>
                             <h2>Home---{this.props.name}</h2>
                             <h3>{`昵称:${this.props.nickname}`}</h3>
                             <h3>{`等级:${this.props.level}`}</h3>
                             <h3>{`中国:${this.props.region}`}</h3>
                        </div>
                )
    }
}
const EnhanceHome3=withUSer(Home3);

export default class App extends Component {
    render() {
        return (
            <div>
                <UserContext.Provider value={{nickname:'CodeSpirit',level:99,region:'中国江西省'}}>
                    <h1>第一个版本---contextType版本</h1>
                    <Home/>
                    <h1>第二个版本-----consumer</h1>
                    <Home2/>
                    <h1>第三个版本------高阶组件版本</h1>
                    <EnhanceHome3 name='曹志贤'/>
                </UserContext.Provider>
                
            </div>
        )
    }
}
```

### 渲染判断鉴权

>  在开发中,我们可能遇到这样的场景
>
> 1. 在某些页面时必须用户登录才能成功进入
> 2. 如果用户没有登录成功,那么直接跳转到登录页面

原理和之前一样,对于要鉴权的页面进行一层验证包裹

### 生命周期劫持

> 可以计算一下渲染时间

### ref转发

```js
import React, { createRef, PureComponent,forwardRef } from 'react'

/**
 * 如果想往函数式组件添加ref的话,就得使用forwardRef这个高阶函数,
 * 传进去的函数会多出一个参数---ref
 * 这样就函数组件就能使用ref
 */

const Profile=forwardRef(
    function(props,ref){
        return <div ref={ref}>你好啊</div>
    }
)



class Home extends PureComponent{
    render(){
        return (
            <div>
            <h2>Home</h2>
            <h3>{"昵称:"}</h3>
            <h3>{"等级"}</h3>
            <h3>{`中国`}</h3>
            </div>
        )
    }
}


export default class App extends PureComponent {
    constructor(props){
        super(props);
        this.title=createRef();
        this.Profile=createRef();
    }
    render() {
        return (
            <div>
                <Profile ref={this.Profile}/>
                <Home ref={this.title}/>
                <button onClick={e=>this.getRef()}>提取ref</button>
            </div>
        )
    }
    getRef(){
        console.log(this.title);
        console.log(this.Profile.current);
    }

}
```

### Portals的使用

> 要想使用Portals,首先要从react-dom中导入ReactDom包，才能进行使用

用法：

```jsx
ReactDom.createPortal(child,container)
```

1. 第一个参数（child）是任何可渲染的React子元素，例如一个元素，字符串或fragment
2. 第二个参数（container）是一个DOM元素

我们接下来来看下我写的这段代码,能更加清晰地了解他是怎么运转地

```jsx
import React, { PureComponent } from 'react'
1.我们首先引用了ReactDom这个包
import ReactDom from 'react-dom';

2.在定义了这个Model类组件时,我们在渲染地时候,使用了portal
class Model extends PureComponent{
    render(){
        return (
            3.可以看到第一个参数是我们传递地那个子组件
            4.第二个参数是拿取到文档中的节点,即想把这个子组件要渲染去哪的地方
            ReactDom.createPortal(this.props.children,document.getElementById("model"))
        )
    }
}

export default class App extends PureComponent {
    render() {
        return (
            <div>
                Home
                {首先,我们定义了一个Model组件,在Model组件中传递了一个子组件,也就是`我在中间`}
                <Model>
                    <div>我在中间</div>
                </Model>
            </div>
        )
    }
}
```

应用场景:比如要在视窗上给个提示,让元素跳出来提示东西

## fragment

```jsx
import React, { Component,Fragment } from 'react'

export default class App extends Component {
    render() {
        return (
            <div>
                {/* Fragement可以写成下面这种短语法,也可以完整的写 */}
                {/* 如果你想添加key的话,就得使用完整标签 */}
                <>
                    <h1>1</h1>
                    <h2>2</h2>
                </>
            </div>
        )
    }
}
```

## StrictMode

> 严格模式是一个用来突出显示应用程序潜在问题的工具
>
> 与Fragment一样,StrictMode不会渲染任何可见的UI
>
> 他为其后代元素触发额外的检查和警告
>
> 严格模式检查仅在开发模式下运行,他们不会影响生产构建;
>
> 要在React包中引入StrictMode

检查什么:

1. 不安全的生命周期
2. 使用过时的ref API
3. 检查意外的副作用
   1. 这个组件的constructor会被调用两次
   2. 这是严格模式下故意进行的操作,让你来查看在这里写的一些逻辑代码被调用多次时,是否会产生一些副作用
   3. 在生产环境中,是不会被调用两次的

