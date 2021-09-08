## 00-前言

这里存放一些React的面试题集合

| [必须要会的 50 个React 面试题 - SegmentFault 思否](https://segmentfault.com/a/1190000018604138) |
| ------------------------------------------------------------ |
|                                                              |
|                                                              |
|                                                              |



## 01-什么是JSX

1. JSX是一种JavaScript的语法扩展(extention),也被称为JavaScriptXML
2. 它用于描述我们的UI界面,并且可以和JavaScript融合在一起使用

## 02-什么是声明式编程

1. 声明式编程就是只关心结果,不关心执行过程

   就比如 我告诉你 去把菜买回来,我只要你把菜带会来,但是我不关心你是走的哪条路去买的,也不关心你是在哪个地方买的菜

2. 命令式编程 就是 你做的每一步都是我下达指令的

   还是拿买菜来讲,你去买菜,我告诉你出门该怎么走,然后拿多少钱去什么地方买什么菜,最后再按我的路线把菜拿回来

## 03-setState什么时候是异步什么时候是同步的

> 简单描述一下
>
> 1. 在组件生命周期或React合成事件中，setState是异步；
> 2. 在setTimeout或者原生dom事件中，setState是同步；
>
> 下面是讲的很好的一篇博客
>
> [深入 setState 机制 · Issue #26 · sisterAn/blog (github.com)](https://github.com/sisterAn/blog/issues/26)
>
> 也可以看why老师讲的深入了解setState这门课

如果setState是异步的话,那我们怎么拿到数据呢,有两种方式

1. 通过setState({},callback);

   setState可以传递第二个参数,第二个参数是一个回调函数,可以拿到setState更新后的值

2. 通过生命周期函数componentdidUpdate()

   在这个函数内也是可以取到更新完之后的值

## 04-为什么setState设计成异步的

> 这里贴一篇React官方的回答
>
> [RFClarification: why is `setState` asynchronous? · Issue #11527 · facebook/react (github.com)](https://github.com/facebook/react/issues/11527)

## 05-React组件如何性能优化

> React进行性能优化的手段

<h3>1. 在类组件中
1. 使用shoulComponentUpdate

   使用他比较之前的值和最新的值(依赖),来判断当前组件是否需要渲染

2. 使用PureComponent

   使用继承自PureComponent的,React会帮助我们自动的去判断,哪个组件相对应的依赖发生改变,进行重新渲染

<h3>2.在函数中

1. 使用函数或者函数组件的时候,建议都包裹上一层memo函数,功能和类组件中的两个功能类似,都是判断依赖是否改变,需不需要重新变化
2. Hook的出现,让函数组件又一次迸发了活力
   1. useMemo
   2. useCalback

## 06-为什么UseState使用数组而不使用对象

> useState使用到了JavaScript解构赋值的思想

数组和对象结构赋值的区别

|               数组               |                  对象                   |
| :------------------------------: | :-------------------------------------: |
|          元素按次序排列          |           对象的属性没有次序            |
| 解构时变量取值由数组元素位置决定 | 解构时变量名必须与属性同名,才能正确的值 |
|         变量名可以任意取         |          变量名必须与属性同名           |

我们也可以得出一个结论,使用数组会更灵活,可以任意命名state和修改state和修改state的方法名

内部原理是把state声明成了一个数组,由于一个组件可以使用多个useState,为了避免冲突并确保state的准确性,useState要使用数组而不是对象

## 07-react事件绑定原理

1. React并不是将事件绑定在div的真实DOM上,而是在document出监听所有支持的事件,当事件发生并冒泡至doucment的时候,React将事件内容封装并交由真正的处理函数运行.这样的方式减少了内存消耗,还能在组件挂载销毁时统一订阅和移除事件.
2. 冒泡到document的事件并不是原生事件,而是React的合成事件,这样做有助于在多个浏览器上保持一致性,如果要阻止这个事件的话,得用`event.preventDefault`来进行阻止

![image-20210906105515415](https://gitee.com/IU_czx/images/raw/master/img/React%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%B5%81%E7%A8%8B.png)

![image-20210906105839212](https://gitee.com/IU_czx/images/raw/master/img/%E8%AF%A6%E7%BB%86%E6%B5%81%E7%A8%8B.png)

