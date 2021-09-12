# 前言

> `call`,`apply`,`bind`
>
> 实际上是用C++来写的,我这次是用JS来模拟实现

# 手写`Call`

```js

Function.prototype.zxCall = function (thisArg, ...restArg) {
    var fn = this;
    thisArg = (thisArg !== undefined && thisArg !== null) ? Object(thisArg) : window
    thisArg.fn = fn;
    var result = thisArg.fn(...restArg);
    delete thisArg.fn;
    return result
}


const obj = {
    num: 1,
    name: "czx",
}

function foo() {
    console.log("函数被执行", this);
}

function sum(n1, n2, n3, n4) {
    var sum = n1 + n2 + n3 + n4;
    return sum;
}


var result = sum.zxCall(obj, 1, 2, 3, 4);
console.log(result)


/**
 * 1. 在函数的原型上加上我们手写的call,使其具有通用性
 * 2. 通过隐式绑定 我们可以拿到调用它的this对象
 * 3. 在传入的绑定对象中,在它的基础上加上一个fn属性,用于将this赋予它
 * 4. 这样我们可以直接在内部对这个函数进行一个调用,完成第一步
 * 5. 对于thisArg进行一个判断
 *      1. 传入的必须得是对象,使用Object()对thisArg进行一个包裹
 *      2. 对于传入的thisArg如果是0,null,undefined进行一个详细判断
 *      3. 不能直接判断 thisArg ? : 这么写,如果传入的是0的话,那么会造成一个小bug,this变成window
 * 6. 接下来解决传递参数的问题,作为函数,那么必然是要传递参数的,但是参数的数量我们其实是不确定的
 *    这时候我们可以使用剩余参数来做接收参数,无论参数有多少个,都能够接收
 *      1. 将剩余参数传入给函数,然后执行
 *      2. 将执行完的结果进行返回
 *      3. 这样我们需要函数返回结果的时候,也能拿到结果了
 *
 */
```

# 手写`apply`

```js
Function.prototype.zxApply = function (thisArg, argArr) {
    var fn = this;
    thisArg = (thisArg !== undefined && thisArg !== null) ? Object(thisArg) : window
    thisArg.fn = fn;

    // 第一种写法
    // if (argArr !== undefined) {
    //     var result = thisArg.fn(...argArr);
    // } else {
    //     var result = thisArg.fn();
    // }

    // 第二种写法
    // argArr = argArr || [];
    // var result = thisArg.fn(...argArr);

    // 第三种写法
    argArr = argArr ? argArr : [];
    var result = thisArg.fn(...argArr);


    delete thisArg.fn;
    return result
}


const obj = {
    num: 1,
    name: "czx",
}

function foo() {
    console.log("函数被执行", this);
}

function sum(...arg) {
    console.log(...arg);
}


var result = sum.zxApply(obj, [1, 2, 3]);
sum.apply(obj, [1, 2, 3])
```

这个写法大致与Call类似,唯一不同的是传递的参数不同,appl要求传递的是一个数组

所以呢在apply传递参数的时候,要对传递的参数进行一个判定,判断是或否为空

还有一个点就是 传入String类型的数据 也可以 这是一个小bug

如果需要做改进的话 就要对String类型的参数 进行一个判断

# 手写`bind`

```js
Function.prototype.zxBind = function (thisArg, ...arg) {
    var fn = this;
    thisArg = (thisArg !== undefined && thisArg !== null) ? thisArg : window;
    function proxyFn(...restArg) {
        thisArg.fn = fn;
        var result = thisArg.fn(...[...arg, ...restArg]);
        delete thisArg.fn;
        return result;
    }
    return proxyFn;
}


const obj = {
    name: "czx",
}

function foo() {
    console.log(this);
}

function sum(...arg) {
    console.log(...arg);
    const newArr = [...arg];
    let sum = 0;
    newArr.map(item => sum += item)
    return sum;
}

var newSum1 = sum.zxBind(obj, 1, 2, 3);
var newSum2 = sum.bind(obj, 1, 2, 3);

console.log(newSum1(6, 7, 8));
newSum2(2, 3, 5);
```

# 认识`arguments`

> 长得像数组,本质上是一个对象,是一个`类数组`(array like)
>
> 他是存在在`AO`当中的

常见的三种操作

1. 获取参数的长度
2. 根据索引值获取某一个参数
3. `arguments.callee`:获取当前arguments所在的函数

将`arguments`转换为数组

1. 自己进行遍历

2. 扩展操作符

3. `Array.prototype.slice.call(arguments)`

   这个是我们要去借用数组的`slice`方法

   通过数组原型上的方法,去给这个arguments遍历,然后拿到一个数组数据

4. `Arrar.from()`这个方法也能将arguments转换为数组

箭头函数中没有`arguments`

* 箭头函数同样的会去找上层作用域,如果上层作用域有,那么他就能找到,浏览器中是一定没有arguments,找到浏览器,也就是最顶层,就会报错
* 在node环境中,是有arguments的

# 手写Slice

```js
Array.prototype.zxSlice = function (start, end) {
    arr = this;
    start = start || 0;
    end = end || arr.length;
    var newArr = [];
    for (var i = start; i < end; i++) {
        newArr.push(arr[i]);
    }
    console.log(newArr);
}


function sum(n1, n2) {
    console.log(arguments);
    Array.prototype.zxSlice.call(arguments, 1, 3);
}

sum(1, 2, 3, 4, 5)
```

数组中slice的重写,实现核心都是要拿到调用它的`this`,方便我们后续操作

