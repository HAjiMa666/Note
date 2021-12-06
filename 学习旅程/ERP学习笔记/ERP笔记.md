# 代码规范

## import位置

```js
// 第一层 导入模块

// 第二层 导入自己的组件

// 第三层 导入工具函数或者一些静态数据
```

## 在函数式组件中 各个部分存放的位置

```js
function Button(){
	// 最顶层放所有的Hook
    
    // 放props,如果有的话
    
    //放自定义函数
    
    //渲染组件
}
```

每一种要分类摆放 不要放到很散

# 工具操作

`npm ls 包名`:可以查看当前安装包的版本号

# CSS

如何让整个页面沾满整个屏幕高度

答: 设置当前页面的最小高度

```css
section{
    /* 设置最小高度为整个屏幕高度,这样在内容比较少的情况下 也能占满整个高度 */
	min-height: 100vh;
}
```

如果比最小高度大的话 那么就是根据内容的自适应来变化高度

这样子就完美解决了 这个问题

# Echarts

## 在项目中加载Echarts

```js
// 引入 echarts 核心模块，核心模块提供了 echarts 使用必须要的接口。
import * as echarts from 'echarts/core';
// 引入柱状图图表，图表后缀都为 Chart
import { BarChart } from 'echarts/charts';
// 引入提示框，标题，直角坐标系，数据集，内置数据转换器组件，组件后缀都为 Component
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  DatasetComponentOption,
  TransformComponent
} from 'echarts/components';
// 标签自动布局，全局过渡动画等特性
import { LabelLayout, UniversalTransition } from 'echarts/features';
// 引入 Canvas 渲染器，注意引入 CanvasRenderer 或者 SVGRenderer 是必须的一步
import { CanvasRenderer } from 'echarts/renderers';

// 注册必须的组件
echarts.use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  BarChart,
  LabelLayout,
  UniversalTransition,
  CanvasRenderer
]);

// 接下来的使用就跟之前一样，初始化图表，设置配置项
var myChart = echarts.init(document.getElementById('main'));
myChart.setOption({
  // ...
});
```

## 封装组件

在react中使用echarts 其实和普通组件没啥区别

只要和文档中的使用方法一样就行

然后根据自己的需求按需加载

然后对这个组件进行一个封装

将自己需要的属性暴露出去,自定义属性,这样就可以动态的生成一个组件了



# antd

## 嵌套子表格

> 最近在写项目遇到一个嵌套子表格的需求，所以我就找上了ａｎｔｄ中的嵌套子表格的样式
>
> 但是他有一个问题，就是数据源会造成所有的子表格都是一样的

我为了解决这个问题，查看了网上的一些解决方案，记录下自己切实可行的方案

首先嵌套的子表格的数据一定要有一个唯一的ｉｄ，嵌套子表格的所有数据首先使用对象进行一个存储，对象的ｋｅｙ需要使用唯一的，然后在嵌套子表格的数据源选择的时候，就可以根据对象的ｋｅｙ拿到不同的数据，这样嵌套子表格相同的问题就解决了

代码实现

- 数据存储使用redux

  ```js
  const getDevices = (groupCode) => {
      return (dispatch, getState) => {
          // 首先从redux中的store中取出devices的数据
          const devices = getState().getIn(["device", "devices"]);
          requestDevices(groupCode).then(res => {
              // 每次请求后 将得到的数据用剩余参数展开放进数组中
              const devicesArr = [...res.data.data];
              // 根据返回的结果的group_code 当做对象的唯一的id
              // 将得到的结果直接放入到我们从redux容器中取得数据devices中
              devices[res.data.data[0].group_code] = devicesArr;
              // 将新的devices通过actionp
              dispatch(getDevicesAction(devices));
          })
      }
  }
  ```

- 组件部分

  ```js
      const expandedRowRender = (record) => {
          //每次点击按钮的时候 会渲染当前父表格下的子表格
          //因为是根据唯一的id来选择对应的数据源
          //那么每个子表格被渲染的时候 就不会因为数据源相同而被同时xuan
          const data = [];
          devices && devices[record.deviceGroup].forEach((item) => {
              data.push({
                  key: item.groupCode,
                  name: item.name,
                  code: item.code,
                  groupCode: item.group_code,
                  state: item.state,
                  beginTime: item.begin_time,
                  monthTime: item.month_time,
                  monthErrorTime: item.month_stop_time,
                  finishTime: item.finish_time,
                  monthStopTime: item.month_stop_time,
                  Tape: item.det_eqp_type,
                  factory: item.factory,
              })
          })
          return <Table columns={props.subColumns} dataSource={data} pagination={true} />;
      };
  ```

  

# git操作

1. git reset . 撤销git add 提交记录
2. git log 查看所有提交记录
3. git show 查看最新提交记录
4. git show commitId 查看指定hashID的修改
5. git show commItId fileName 查看某个具体文件的修改

# React router

1. 注意嵌套关系

   1. 如果是要在主页面渲染登录和登录成功后的两个界面 那么可以在主路口设置两个父组件,登录成功后,进行一个重定向,指向那个登录成功后的界面

   2. 然后呢 就是要做路由嵌套的话 需要在URL上面标记下,举个例子

      我要进行一个模块的跳转 但是这个模块内有很多子路由

      父亲: /home

      儿子:就需要加上 /home的前缀  /home/son

      像上面这个样子的

2. 如果出现路由渲染不成功的话 那很有可能就是嵌套关系没有做好

3. 注意啊 如果我要渲染一个父亲 但是那个父亲里面有很多子路由 而那些子路由没有从父路由那继承过来 而是直接从 router中的配置 直接获取的话

   会是渲染不出来的 而且会无限循环 最后将页面卡死

# styled-components

## styled-components 安装

1. 安装

   `yarn add styled-components`

2. 为了保证版本一致,不会导致多个版本冲突,所以需要在`package.json`加上这一段

   ```json
   "resolutions": {
       "styled-components": "^5"
     }
   ```
## 基础用法

### 在js中写css

```js
import styled from "styled-components";

// 注意这里的命名一定要大写
// 这里本质上也是一个React组件
// React组件要求首字母大写
const Title=styled.h1`
	color:red;
`
// 将组件导出去
export {
	Title
}
```

```js
import Title from "./style.js"

render(
	<div>
    	<Title>
    		这就是使用方法
    	</Title>
    </div>
)
```



`styled`后面可以加上html的所有标签

## 在styeld-components引入属性,进行动态修改

```js
const Button = styled.button`
	// g
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    <Button primary>Primary</Button>
  </div>
);
```











