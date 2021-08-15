# 前言

> 1. Node.js
> 2. express
> 3. MoonDB

1. 静态网页
   * HTML CSS JS组成的页面
2. 动态网页
   * 有数据库交互的

# Node基础

1. __filename:当前文件的所在位置
2. __dirname:当前所处的文件夹的位置

## 制作自己的模块

1. 先在自己的js文件中定义一个函数

   ```js
   function greeting(name){
       console.log("Hello!  "+name);
   }
   exports.greeting=greeting;
   ```

2. 然后你可以在另外一个js文件中调用它

   ```js
   require("你js文件所在的位置")
   ```

3. 然后你就可以调用之前js中的函数功能了

4. 后面如果js文件比较多的话,如果你想要调用一个文件的话

5. 在文件夹中定义一个index.html文件,加上而类似与这种格式的内容,就可以调用整个文件夹了

   ```js
   let try1=require("./try1");
   let try2=require("./try2");
   exports.greeting=try1.greeting;
   exports.intro=try2.intro;
   ```

## 引用内置模块

1. path

   1. basename:

      ```js
      根据__filename或者___dirname来获取当前的名字
      ```

   2. extname

      `同上,不过获取的是后面的扩展名`

2. url

3. fs

## 剩下的看我写的代码笔记

# Express

## 前言

> 他是一个module
>
> 他是一个Node框架
>
> 帮助我们写node.js更快捷

## 基本使用

```js
const express=require("express");
const app=express();

app.get("/",function(req,res){
    res.send("You are on the homepage")
});

app.listen(3000,()=>{
    console.log("Server is running on port 3000");
});
```

### HTTP Requests

* get:获得一些请求
* post:给什么东西
* put
* patch
* Delete

### 剩下的看我代码笔记

### HTTP状态码

![image-20210717204307811](https://gitee.com/IU_czx/images/raw/master/img/image-20210717204307811.png)

# EJS

> 可以用js写HTML
>
> 看我写的代码模板

#　SQL

1. DBMS
2. RDBMS
3. CRUD(Create,Remove,update,Delete)
4. SQL:和NoSQL

## Key

* primary key:主键
* Foreign key
* Natural key
* Surrogate key
* Composite key

## SQL Data Types

1. INT:整型
2. DECIMAL(p,s):-----p total digits, s digits after the dot
3. VARCHAR(M) ------20 characters
4. DATE -------"YYYY-MM-DD

## MongoDB

1. show dbs:显示你有什么数据库
2. db:目前你所处的数据库
3. use 数据库:你想要使用的数据库,没有这个数据库的话,就会创建这个数据库
4. show collections:显示当前所处的数据库中的所有数据集合
5. MongoDb的shell也就是Javascript的shell

### CRUD

1. insert

   1. db.dbname.insertOne();

   2. ~.insertMany():放入一个数组集合

2. find

3. update:和insert一样,只是insert换成了update

### 基本使用方法

```js
const express = require("express");
const app = express();
const ejs = require("ejs");
const monggose = require("mongoose");
app.use(express.static("public"));

// 连接数据库  
monggose.connect("mongodb://localhost:27017/exampleDB", {
    useNewUrlParser: true,
    useUnifiedTopology: true,
}).then(() => {
    console.log("Connect to MongoDB");
}).catch((err) => {
    console.log("connected failed");
    console.log(err);
})

/**
 * 接下来讲解如何在node中使用mongoose
 * 1. 首先要有一个schema(架构) 
 * 2. 接下来创建一个Model
 * 3. 创建一个对象并且存储到数据库中
 */

// 创建一个schema
const studentSchema = new monggose.Schema({
    name: String,
    age: Number,
    major: String,
    scholarship: {
        merit: String,
        other: Number,
    },
});
// 使用instance method来创建一个属于自己的处理函数
studentSchema.methods.countMerit=function(){
    return this.scholarship.merit;
}
// // 创建一个model 必须要求为单数,且第一个字母大写,他会自动转换为students
const Student = monggose.model("Student", studentSchema);


Student.findOne({name:"h"}).then((data)=>{
    let result=data.countMerit();
    console.log(result);
}).catch(e=>{
    console.log("erro!!!!");
    console.log(e);
})


// 更新 update-----updateOne和updateMany
// Student.updateOne({name:"Jhon"},{name:"Coder"}).then((msg)=>{
//     console.log(msg);
// })

/**
 * find和findOne的区别
 * find找到的数据无论是一个还是多个,返回的都是一个数组
 * findOne返回的是第一个找到的
 */
// Student.findOne({name:"Coder"}).then(data=>{
//     console.log(data);
// })
// Student.find().then((data)=>{
//     console.log(data);
// });

// findOneAndUpdate
// Student.findOneAndUpdate({name:"Coder"},{name:"Coders"}).then((data)=>{
//     console.log(data);
//     console.log("更新成功");
// });
// 创建一个对象
// const John = new Student({
//     name: "h",
//     age: 25,
//     major: "computer",
//     scholarship: {
//         merit: 2300,
//         other: 1300
//     }
// });
// // 存入DataBase
// John.save().then(()=>{
//     console.log("Save Successfully");    
// }).catch((e=>{
//     console.log("error happend");
//     console.log(e);
// }))


app.get("/", (req, res) => {
    res.render("index.ejs");
    console.log(e);
})
app.listen(3000, (req, res) => {
    console.log("server is running on port 3000");
})


/**
 * Schema Type validators
 * 可以看文档
 * eg:
 *  name{
 *  type:String;
 *  你可以根据你设置的数据类型 设置相对应的验证方式 
 * }
 * 常用的是
 * String:
 * 1. enum
 * 2. minlength
 * 3. maxlength
 * Number:
 * 1. min
 * 2. max
 * 3. enum
 * 要想在更新的时候也能进行验证的话,就要设置runvalidator这个属性,为true则会验证
 */
```

# AJAX

> sync code:同步
>
> async code 异步

在以前的时候,如果使用异步的话,可能会造成异步的函数还没执行,但是需要它的结果去输出的同步代码,这样会造成结果未定义,当时的解决办法就是在函数定义的时候加个回调函数,这样就能解决问题了,但是这样随着代码变多,就会变成 CallBack Hell

## Promise

现在可以用Promise来解决这个问题

有两种办法来获取值

1. 用`then`,`catch`
2. 用`async`:这个是用在定义函数名之前的,`await`用在要使用的函数名之前,捕获异常的话是用try和catch

# Restful API

> 使用基于HTTP语法的restful routing去控制crud operations
>
> 数据发送用send,提示信息用{message:""}

# Middlewares and Error Handling

## Express JS Life Cycle(生命周期)

 req--->middleware----->route---->res

## Middleware

1. middleware:实质上是函数,在客户端发送请求到服务器上,在req和res之间有某些函数需要执行的,这些函数就称为中间件

2. 它可以用来指定特定的一些用法

   语法:`app.use((req,res,next)=>{你自己想要用的内容})`,当然你也可以像使用app.use("/resource",(req,res,next)),这样使用,可以帮助你在指定的资源下,执行某些特定的操作,==注意:next()是必不可少的,如果少了这个,它将不会执行接下来的中间件==

3. 除了放在req和res之间,也可以放在res route上,`app.get("",(req,res,next){},(req,res){})`

4. 不过一般不这么用,一般是在req和res之间定义几个中间件函数,然后再route上调用,可以无限装入中间件

## Error Handling

[Express error handling (expressjs.com)](https://expressjs.com/en/guide/error-handling.html)

一般的错误处理用err就行

如果遇到异步中发生的错误,需要用try,catch

验证器的错误必须被.catch抓到

如果是用 findOneAndUpdate再await中有一个(err,doc)错误处理方式

# Cookies and Sessions

## Coookies

> 可以用来存储本地用户的数据

## Sessions

> 1. 比较安全,不会被黑客攻击
> 2. 存储容量比较大

## flash

> 他是Session的一个小部分,可以借助这个来提示一些登录信息

# 验证和密码学

## 密码学的应用

1. 帮助密码加密
2. 网上的信息加密

3. 用hash加密,salting可以使得即使是相同的密码,看上去也不同,salting几乎不可逆的