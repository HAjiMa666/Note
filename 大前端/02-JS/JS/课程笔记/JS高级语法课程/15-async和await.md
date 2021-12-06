# 异步函数 async   function

> async: asynchronous的缩写 代表异步
>
> sync: synchronous的缩写 代表同步

## 异步函数与同步函数的区别

### 异步函数的返回值

```js
// 异步函数的返回值一定是 Promise
async function foo() {
    console.log("Start");
    console.log("End");
    // 第一种返回值 如果没有返回值 那么直接返回undefined
    // return "I'm return value";
    // 第二种返回值 返回thenable 对象
    // return {
    //     then: function (resolve, rejected) {
    //         resolve("I'm thenale object");
    //     }
    // }
    // 第三种返回值 返回Promise对象
    return new Promise((resolve, reject) => {
        resolve("I'm promise object");
    })
}

const promise = foo();
promise.then(res => {
    console.log("result", res);
})
```

### 异步函数的异常处理

```js
// 普通函数开始执行错误函数
// function foo() {
//     console.log("Start exec err");
//     throw new Error("I'm a error");
// };

// // 普通函数开始执行 错误函数 错误函数执行完错误后 在函数后面的语句就不会再执行了
// console.log("Start");
// foo();
// console.log("End");


// 异步函数执行错误函数
async function bar() {
    console.log("async function start exec error");
    throw new Errow("I'm a error");
}

console.log("Start");
bar().catch(err => {
    console.log("codeSpirit err", err);
});
console.log("End");

```

### 异步函数的await的关键字

```js
function foo() {
    // return 1234556;
}

function requestData() {
    return new Promise((resolve, rejected) => {
        setTimeout(() => {
            // resolve("I'm promise resolve object");
            rejected("I'm a err");
        }, 1000);
    })
}

/**
 *  1.await后面可以接函数 函数的返回值是awiat的结果
 *  2.如果返回的是promise对象 那么resolve的结果就是await的结果,并且后面的执行代码会变成then方法的部分,加入到微任务队列中
 *  3.如果返回的promise对象 是rejected 出来的 那么await的结果是这个异步函数的返回值的rejected结果
 *     同时await后面的函数不会再执行,reject的结果需要使用catch捕获
 *  4.await后面可以跟普通值 会直接返回
 *  5.await后面可以跟 promise对象或者thenable对象 处理方法和函数中有promise处理是一样的
 * 
 */

async function test() {
    // const result = await requestData();
    const result = await {
        then: function (resolve, rejected) {
            resolve("q12");
        }
    }
    console.log("我是结果", result);
}

test().catch(err => {
    console.log(err);
});
console.log("我是不是先被执行了");
```

# 事件循环

## 进程和线程

官方解释:

- 进程:计算机已经运行的程序,是操作系统管理程序的一种方式

- 线程:操作系统能够运行运算调度的最小单位,通常情况下它被包含在进程中

老师解释

- 进程: 我们可以认为,启动一个应用程序,就会默认启动一个进程(也可能是多个进程)

- 线程:每一个进程中,都会启动至少一个线程用来执行程序中的代码,这个线程被称为主线程

- 所以我们也可以说进程是线程的容器
- 操作系统类似一个大工厂
- 工厂中里有很多车间,这个车间就是进程
- 每个车间可能有一个以上的工人在工厂,这个工人就是线程

## 操作系统的工作方式

![image-20211126161201536](https://gitee.com/IU_czx/images/raw/master/img/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%B7%A5%E4%BD%9C%E6%96%B9%E5%BC%8F.png)

## 浏览器中的JS线程

1. js是单线程的,但是js的线程应该有自己的容器进程: 浏览器或者node

2. 浏览器是一个进程 它里面只有一个线程嘛?

   答:不是的 在浏览器中 打开一个页面就是一个进程,是为了防止一个页面卡死而造成所有页面无法响应,整个浏览器需要强制退出

   而每个进程又有很多的线程,其中包括执行JS代码的线程

3. JS的代码执行是在一个单独的线程中执行的

   - 这就说明 JS在同一个时刻只能做一件事情
   - 如果这件事情是非常耗时的,这就意味着当前的线程就会被阻塞

4. 真正耗时的操作,实际上并不是由JS线程来执行的

   1. 浏览器中每个进程是多线程的,那么其他线程可以来完成这个耗时的操作
   2. 例如 网络请求,定时器,只需要在特定的时候来执行应有的回调即可

## 浏览器的事件循环

事件循环图解

![image-20211126211609633](https://gitee.com/IU_czx/images/raw/master/img/%E4%BA%8B%E4%BB%B6%E5%BE%AA%E7%8E%AF.png)

微任务和宏任务

- 宏任务:`setTimeout`,`ajax`,`DOM回调`,`UI Rendering`
- 微任务:`Promise then`,`queueMicrotask`,`Mutation Observer API`
- **规范** :宏任务在执行前 一定要把微任务清空完 才能执行宏任务

面试题一

```js
setTimeout(function () {
    console.log("setTimeout1");

    new Promise(function (resolve) {
        resolve();
    }).then(function () {
        new Promise(function (resolve) {
            resolve();
        }).then(function () {
            console.log("then4");
        });
        console.log("then2");
    });
});

new Promise(function (resolve) {
    console.log("promise1");
    resolve();
}).then(function () {
    console.log("then1");
});

setTimeout(function () {
    console.log("setTimeout2");
});

console.log(2);

queueMicrotask(() => {
    console.log("queueMicrotask1")
});

new Promise(function (resolve) {
    resolve();
}).then(function () {
    console.log("then3");
});


```

面试题二

```js
async function async1() {
  console.log('async1 start')
  // await异步函数的返回结果 resolve的结果会作为整个异步函数的promise的resolve结果
  // await后面的执行代码 就会变成.then后面的执行函数
  // 也就是说  console.log('async1 end') 这一段是相当于then方法内的 会被加入微任务中
  await async2();
  console.log('async1 end')
}

async function async2() {
  console.log('async2')
}

console.log('script start')

setTimeout(function () {
  console.log('setTimeout')
}, 0)

async1();

new Promise(function (resolve) {
  console.log('promise1')
  resolve();
}).then(function () {
  console.log('promise2')
})

console.log('script end')


```

面试题三

````js
Promise.resolve().then(() => {
  console.log(0);
  return new Promise((resolve, rejected) => {
    console.log("我是宏任务");
    resolve(4);
    console.log("我执行了嘛");
  })
}).then((res) => {
  console.log(res)
})


Promise.resolve().then(() => {
  console.log(1);
}).then(() => {
  console.log(2);
}).then(() => {
  console.log(3);
}).then(() => {
  console.log(5);
}).then(() => {
  console.log(6);
})
````

这里记两个结论

1. 返回值是 thenable 对象 微任务推迟一次
2. 返回值是 Promise.resolve 微任务推迟两次

## node的事件循环

 浏览器的事件循环是 根据 HTML5 的规范来实现的

Node是由libuv实现的

![image-20211128154109795](https://gitee.com/IU_czx/images/raw/master/img/image-20211128154109795.png)

node的事件循环事件阶段

一次的完整的事件循环`Tick`分成很多个阶段

- 定时器:本阶段执行已经被`setTimeOut`,`setInterval()`的调度回调函数
- 待定回调(pending Callback):对某些系统操作(如TCP错误类型)执行回调,比如TCP连接时接收到ECONN REFUSED
- idle,prepare: 仅系统内部使用
- 轮询(poll):检索新的I/O事件;执行I/O相关的回调
- 检测(check): setTmmediate() 回调函数在这里执行
- 关闭的回调函数:一些关闭的回调函数,如socket.on("close"….);

![image-20211128154030681](https://gitee.com/IU_czx/images/raw/master/img/node%E7%9A%84%E5%BE%AE%E4%BB%BB%E5%8A%A1%E5%92%8C%E5%AE%8F%E4%BB%BB%E5%8A%A1.png)

node面试题

![image-20211128160503882](https://gitee.com/IU_czx/images/raw/master/img/node%E9%9D%A2%E8%AF%95%E9%A2%98.png)

