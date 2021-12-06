# 错误处理方案

## throw

> 通过 throw抛出一个错误信息,抛出后,后续代码不会再执行

- 通过 throw抛出一个对象是比较常见的,因为对象可以表达更多的信息
- 创建类.并且创建这个类对应的对象
- 使用 JS提供的 Error 类,可以自定义自己的错误

```js
function bar() {
    throw new Error("I'm a error");
}

// 1. 第一种是不处理,bar函数会继续将是收到的异常向外抛出 直到最顶层的demo调用 将错误展示出来
// 2. 使用 try catch捕获异常 正确处理异常后 程序就不会崩掉 (ES10之后 可以将catch的err省略掉)
// 3. finally 再try catch的最后面执行 无论发生什么 finally是一定会执行的

function foo() {
    bar();
}

function test() {
    foo();
}

function demo() {
    test();
}

demo();
```



# 模块化

> ES6推出的模块化 
>
> 重点: CommonJS和ES6

## node common.js原理

```js
const info = {
    name: "czx",
    age: 18,
}


// 通过 module.exports进行一个导出
// 在后面的文件 就可以通过require进行一个接收
// require 本质上就是通过文件路径找到这个文件
// 然后返回module.exports的值
// 这次返回的是info这个对象
// 并且在源文件进行改动 引用的文件中的module也会发生改变
module.exports = info
```

## exports原理

```js
const name = "czx";
const age = 18;


// 在源码中 node做了这样的一个操作
// module.exports={};
// exports=module.exports
// 做了这样一个赋值操作
// 所以我们可以看出 像我下面这样的操作是没有任何问题的
// 最后还是加到了 module.exports的那个空对象中的
exports.name = "czx222";
exports.age = 18;
```

## CommonJs的优缺点

![image-20211130082729164](https://gitee.com/IU_czx/images/raw/master/img/commonjs%E7%9A%84%E6%9C%89%E7%BC%BA%E5%97%B2.png)

## require细节

> require是一个函数,可以帮助我们引入一个模块

![image-20211130082938115](https://gitee.com/IU_czx/images/raw/master/img/require%E6%9F%A5%E6%89%BE%E7%BB%86%E8%8A%82-1.png)

![image-20211130083010588](https://gitee.com/IU_czx/images/raw/master/img/require%E6%9F%A5%E6%89%BE%E7%BB%86%E8%8A%822.png)

## 模块的加载过程

1. 模块在第一次加载的时候,会被执行一次
2. 模块被多次引入的时候,会缓存,最终只加载一次
3. ![image-20211130085120546](https://gitee.com/IU_czx/images/raw/master/img/%E6%A8%A1%E5%9D%97%E5%8A%A0%E8%BD%BD%E7%9A%84%E5%BE%AA%E7%8E%AF%E5%BC%95%E7%94%A8.png)

## ES-Module

### 两个关键字

`import` 和 `export`

1. 导出的时候可以起别名
2. 导入的时候可以起别名
3. 导入的时候可以将所有的内容放到一个标识符中

导入和导出可以结合使用

引入并导出

```js
export {} from "XX.js"
export * from "XX.js" // 更加简洁,在写工具库函数更加方便
```

### default的用法

默认导出的方法

```
export {
	name as default
}
```

```js
export default name
```

named exports (命名导出)

- 在导出export时指定了名字
- 在导入import时需要知道具体的名字

default exports(默认导出)

- 默认导出export时 可以不需要指定名字
- 在导入的时候不需要使用 {},并且可以自己来指定名字
- 他也方便和我们现有的commonJS等规范相互操作

```js
import ...
//后续的代码必须要等到 import 的文件解析完成后 才会执行
```

如果我们不想要等待前面引入文件解析完成 可以使用 `import()`函数

import函数返回的是一个 promise对象

ES11 新增的特性

meta属性本身也是一个对象: `{url:"当前模块所在的路径"}`

### ES-module的解析过程

 #### 构建

- 根据地址查找js文件,并且下载,将其解析成模块记录(Module Record);

  ![image-20211130101315093](https://gitee.com/IU_czx/images/raw/master/img/ESModule%E7%9A%84%E8%A7%A3%E6%9E%90%E8%BF%87%E7%A8%8B.png)

#### 实例化(Instantiation)

- 对模块记录进行实例化,并且分配内存空间,解析模块的导入和导出语句,把模块执行对应的内存地址

#### 运行赋值(Evaluation)

-  运行代码,计算值,并且将值填充到内存地址中

![image-20211130101408333](https://gitee.com/IU_czx/images/raw/master/img/ES-Module%E7%9A%84%E8%A7%A3%E6%9E%90%E8%BF%87%E7%A8%8B-2.png)

- 导出的模块可以修改值 但是在导入时,导入的模块是不能修改其模块的值

