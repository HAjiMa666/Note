# promise的诞生

```js
// 以前都是通过回调函数来进行异步请求的

// 弊端:
// 1. 没有一个规范,使用别人封装好的请求函数时,使用成本很高
// 为了解决这个弊端 推出了Promise
// 解决了规范问题 大家都按这个规范去开发 大大减少学习成本

function requestUrl(url, succes, fail) {
    // 模拟网络请求
    setTimeout(() => {
        if (url === "spirit") {
            succes("请求成功");
            return "请求成功";
        } else {
            fail("请求失败");
            return "请求失败";
        }
    }, 1000);
}

function success(res) {
    console.log(res);
    return res;
}
function fail(res) {
    console.log(res);
    return res;
}

requestUrl("spirit", success, fail)
console.log(result);
```

# Promise的基本使用

1. promise传入一个executor,这个executor接收两个参数 分别是resolve和rejected

   ```js
   const promise = new Promise((resolve, rejected) => {
       // 异步请求在这里写
       //成功使用   resolve();
       //失败使用   rejected();
   })
   ```

   

2. promise有三个状态

   1. pending 
   2. fulfilled
   3. rejected

   ```js
   const promise = new Promise((resolve, rejected) => {
       // 没有resolve或rejected之前 状态为pending状态 
       //成功使用   resolve();==> fulfilled
       //失败使用   rejected();==> rejected状态
   })
   ```

3. promise自身有两个方法接收resolve的结果和rejected的结果

   ```js
   const promise=new Promise((resolve,rejected)=>{
   	resolve("aaa");
       rejected("ccc");
   })
   
   promise.then((res)=>{
       console.log(res) // aaa
   },(err)=>{
   	console.log(err); // ccc
   })
   ```

4. then方法

   ```js
   // then方法本身可以接收两个回调函数 分别代表为 resolve的结果和rejcted的结果
   promise.then((res)=>{},(err)=>{})
   // 为了美观 出现了catch这个语法糖 效果和上面一样
   promise.then(()=>{
       
   }).catch(()=>{
       
   })
   // then方法的返回结果是返回一个Promise对象 也就是说Promise的链式调用是因为then方法自身是会返回一个Promise对象
   promise.then(()=>{
       return "aaa"; // 这个返回值会被包裹为Promise对象
       return {
           then: (resolve,rejected)=>{}  // 在对象内实现了then方法 这种叫thenable方法 
       }
       return new Promise(); // 返回Promise对象
       //没有返回结果 则会在接下来的then返回undefined
   }).then((res)=>{
   	//res的结果
       //1. 如果是返回一个普通的值 那么会直接变为resolve 在res上输出
       //2. 如果返回的是一个thenable 那么结果是根据then方法的结果决定的 如果是resolve则是fulfilled 如果是rejectd则是rejected
       //3. 如果传入Promise对象的话 结果由Promise的结果所决定的
   })
   ```
# Promise的方法

1. `finally()`:无论promise的状态 都会去执行finally();

   下面是 Promise的方法

2. `resolve()`:可以直接将对象或一个值转换为Promise对象 其实和Promise的resolve方法一样

3. `rejected()`对应Promise中的rejected方法

4. `all()`可以传入一个数组,数组中的所有Promise对象执行完毕时,才会输出结果,如果有一个失败,则会返回失败,输出结果的顺序是根据数组的顺序来输出的

5. `allSettled()`:可以将所有的结果返回 ,返回结果是一个对象 每个对象存着每个执行状态和执行结果

6. `race()`:看谁执行的快,如果先resolve,则会输出fulfilled的结果,如果rejected,则会输出rejected的结果

7. `any()`:any方法会等到一个fullfilled状态,才会决定新Promise的状态

   ​			如果所有的Promise都是reject的,那么也会等到所有的Promise都变成rejected状态

