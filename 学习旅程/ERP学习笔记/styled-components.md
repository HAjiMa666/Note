# styled-components 安装

1. 安装

   `yarn add styled-components`

2. 为了保证版本一致,不会导致多个版本冲突,所以需要在`package.json`加上这一段

   ```json
   "resolutions": {
       "styled-components": "^5"
     }
   ```

   

# 基础用法

## 在js中写css

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



