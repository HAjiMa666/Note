# 序

> 用面向过程的方法写出来的是一份蛋炒饭,而用面向对象写出来的程序是一份盖浇饭

# ES6中的类和对象

> 面向对象的思维特点:
>
> 1. 抽取对象公用的属性和行为组织(封装)成一个类(模板)
> 2. 对类进行实例化获取类的对象
> 3. 我们需要不断的创建对象,指挥对象做事情

> 对象由属性和方法组成
> 类抽象了对象的公共部分,泛指某一个大类
> 对象特指某一个,通过类实例化一个具体的对象

## 类

```js
class star{
    constructor(uname){
        this.name=uname;
    }
}

var star=new star("曹志贤");
```

![image-20210522060850723](https://gitee.com/IU_czx/images/raw/master/img/image-20210522060850723.png)

## 类的继承

> extend只能继承方法

> super关键字能继承父类的构造函数
>
> super.say()就是调用父类中的普通函数say()

1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,有就执行子类的方法
2. 如果子类中没有,就会去查找父类有没有这个方法,有就执行父类的方法

==注意==

1. super要放在子类this之前

2. 在ES6中类没有变量提升,必须先定义类,才能通过类实例化对象
3. 类里面的共有属性和方法一定要加this使用
4. constructor里面的this指向实例对象,方法里面的this指向这个方法的调用者

## 面向对象的版tab栏切换

* 看我博客

# 构造函数和原型对象

* 构造函数用于创建某一类对象,首字母要大写
* 要和new一起使用才有意义

new在执行时会做四件事情

1. 在内存中创建一个新的空对象
2. 让this指向这个新的对象
3. 执行构造函数里面的的代码,给这个新对象添加属性和方法
4. 返回这个新对象,所以构造函数里面不需要return

静态成员和实例成员的区别

* 静态成员是在构造函数上添加的成员称为静态成员,只能由构造函数本身来访问
* 实例成员:在构造函数内部创建的对象成员称为实例成员,只能由实例化的对象进行访问

问题

* 存在浪费内存的问题

原型可以解决这一问题

* 构造函数通过原型分配的函数是所有对象共享的

* prototype 在这个构造函数的这个属性上加上要用的公共方法,就能实现共享方法,而不会向之前一样,每实例化一个对象,公共方法就开辟一次内存空间

* 实例化的对象上也有一个

  ```js
  _proto_方法
  ```

  ![image-20210523065139899](https://gitee.com/IU_czx/images/raw/master/img/image-20210523065139899.png)

![image-20210523065631583](https://gitee.com/IU_czx/images/raw/master/img/image-20210523065631583.png)

![image-20210523065806773](https://gitee.com/IU_czx/images/raw/master/img/image-20210523065806773.png)

![image-20210523070140090](https://gitee.com/IU_czx/images/raw/master/img/image-20210523070140090.png)

![image-20210523073805805](https://gitee.com/IU_czx/images/raw/master/img/image-20210523073805805.png)

`原型对象的this指向对象:指向的都是实例对象`

==注意==数组和字符串内置对象不能给原型对象覆盖操作Array.prototype={},只能是Array.prototype.xxx=function{}的方式

# CALL

> 改变this的指向

```js
    <script>
        function fn(x, y) {
            console.log(this);
        }

        var o = {
            name: "czx"
        }
        console.log(fn.call(o));
    </script>
```

参考以上例子

![image-20210523082556931](https://gitee.com/IU_czx/images/raw/master/img/image-20210523082556931.png)

# ES5新增的方法

## 数组方法

迭代遍历方法:

* foreach()
* map()
* filter()
* some()
* every()

![image-20210523082945910](https://gitee.com/IU_czx/images/raw/master/img/image-20210523082945910.png)

![image-20210523083311516](https://gitee.com/IU_czx/images/raw/master/img/image-20210523083311516.png)

![image-20210523083645683](https://gitee.com/IU_czx/images/raw/master/img/image-20210523083645683.png)

找到符合条件的就直接返回,不执行后面操作

![image-20210523090643688](https://gitee.com/IU_czx/images/raw/master/img/image-20210523090643688.png)

## 字符串方法

* trim():去除字符串两边空格,但是不会去除字符串之间的空格

## 对象方法

* Object.keys():用于获取自身所有的属性名,返回一个由属性名组成的数组
* Object.defineProperty()

![image-20210523093517220](https://gitee.com/IU_czx/images/raw/master/img/image-20210523093517220.png)

# 函数高阶技巧

> 导读

![image-20210523100232840](https://gitee.com/IU_czx/images/raw/master/img/image-20210523100232840.png)

## 函数的定义和调用

```js
//第一种
function fn(){}
//第二种
var fun=function(){}
//第三种,必须要字符串格式
var f=new Function('参数1','参数2','函数体');
//所有的函数是Function的实例(对象)

```

* 函数也属于对象

![image-20210523101428957](https://gitee.com/IU_czx/images/raw/master/img/image-20210523101428957.png)

函数的调用方法

![image-20210523101722714](https://gitee.com/IU_czx/images/raw/master/img/image-20210523101722714.png)

![image-20210523101806416](https://gitee.com/IU_czx/images/raw/master/img/image-20210523101806416.png)

## 函数内部this的指向问题

![image-20210523101907415](https://gitee.com/IU_czx/images/raw/master/img/image-20210523101907415.png)

```js
    <button class="btn"></button>

    <script>
        // 普通函数的this的指向,它的对象是window
        function fn() {
            console.log(this);
        }
        fn();
        // 对象的方法,指向的是Object
        var obj = {
            sayHi: function () {
                console.log("对象的方法的" + this);
            }
        }
        obj.sayHi();
        // 构造函数 里面的this指向的是我们实例化的这个对象,原型指向的也是这个实例对象
        function star(uname, age) {
            this.uname = uname;
            this.age = age
        }
        var str = new star("czx");
        console.log(star.prototype);
        // 绑定事件函数 指向的是调用这个事件
        var btn = document.querySelector(".btn");
        btn.addEventListener("click", function () {
            console.log("绑定事件函数的this:" + this);
        })
        // 定时器函数 指向的也是window
        setTimeout(function () {
            console.log("定时器函数" + this);
        });
        //立即执行函数 指向的也是window
        (function () {
            console.log("立即执行函数" + this);
        })()
    </script>
```

## 改变函数内部this指向

* call()
  * 第一个可以调用函数
  * 第二个可以改变函数内的this指向
  * 主要作用是用来继承
* apply()
  * 也是调用函数
  * 可以改变this的指向
  * 它的参数必须是数组
  * apply的主要应用 可以利用apply借助于数学内置对象求最大值
  * ![image-20210523142000914](https://gitee.com/IU_czx/images/raw/master/img/image-20210523142000914.png)
* ==bind()==
  * 不会调用函数,能改变this的指向
  * 返回的是原函数改变this之后产生的新函数

![image-20210523143613379](https://gitee.com/IU_czx/images/raw/master/img/image-20210523143613379.png)

## 严格模式

> * 在脚本开头加上'use strict'开启严格模式
>
> * 在某个函数开启严格模式
>
> ```js
> function fn(){
>     'use strict';
> }
> ```
>
> 

### 变量规定

1. 变量必须先声明再使用
2. 不能随便删除已经命名好的元素
3. 全局作用域指向的是undefined
4. 构造函数下不加new调用,this会报错
5. 事件,对象还是指向调用者

### 函数变化

1. 函数名里面不允许重名
2. 函数必须声明在顶层,不允许在非函数块中声明函数

## 高阶函数

> Concept:高阶函数是对其它函数进行操作的函数,他**接受函数作为参数或将函数作为返回值输出**

## 闭包

> 闭包是有权访问另一个函数作用域中的变量的==函数==

主要是衍生了变量的作用范围

```js
    <script>
        window.addEventListener("load", function () {
            var lis = document.querySelector("ul").querySelectorAll("li");
            for (var i = 0; i < lis.length; i++) {
                (function (i) {
                    lis[i].onclick = function () {
                        console.log(i);
                    }
                })(i);
            }
        })
    </script>
```

* 立即执行函数也称为小闭包

## 递归

> 自己调用自己就是递归函数

* 容易发生栈溢出
* 记得加计数器退出循环

## 浅拷贝和深拷贝

> 浅拷贝:只是拷贝一层,更深层次对象级别的只会拷贝引用
>
> 深拷贝:拷贝多层,每一级别的数据都会拷贝

浅拷贝:

1. for(k in obj):将所有属性都拿到
2. 也可以用Object.assign(o,obj);
3. 更推荐用第二种
4. 更深层次的对象只是拷贝了地址

# 正则表达式

## 概述

* 正则表达式是用于匹配字符串中字符组合的模式,在javaScript,正则表达式也是对象

特点:

1. 灵活性强,逻辑性和功能性非常的强

2. 迅速的使用简单的方式达到字符串的控制

   ## JavaScript使用

   ```js
       <script>
           //1. 利用 RegExp 对象来创建正则表达式
           var regep = new RegExp(/123/);
           // 2.利用字面量创建正则表达式
           var rg = /123/;
           // 利用test()来做测试
           console.log(rg.test("13"));
           console.log(rg.test("abc"));
       </script>
   ```

## 正则表达式的字符

* 查看文档
* [正则表达式 | jQuery API 3.2 中文文档 | jQuery API 在线手册 (cuishifeng.cn)](https://jquery.cuishifeng.cn/regexp.html)
* 正则表达式不需要加引号,不管是数字型还是字符串型

> /abc/:包含就行
>
> /^abc/:必须要这个开头
>
> /^abc$/以这个开头,以这个结尾才行
>
> 在[^]加上这个符号,说明是取反

## 正则表达式的替换

* /表达式/[switch]
* g:全局匹配
* i:忽略大小写
* gi:全局匹配并忽略大小写

# ES6

## 新增赋值方法

1. let

   * 只有使用它声明的变量只在所处于的块级有效
   * 块级作用域可以防止循环变量变成全局变量
   * 不存在变量提升,只能先声明再使用
   * 暂时性死区,如果在块级作用域,如果有一个全局变量和let申明的块级作用域的变量同名,在块级作用域中先使用再声明,会报未定义的错误

![image-20210528102223821](https://gitee.com/IU_czx/images/raw/master/img/image-20210528102223821.png)

![image-20210528102355559](https://gitee.com/IU_czx/images/raw/master/img/image-20210528102355559.png)

2. const
   * 同样具有块级作用域,声明常量,常量是值(内存地址)不能变化的量
   * 声明常量必须赋值
   * 常量赋值后,值不能修改,如果是简单类型的,是不能修改的,如果是复杂类型的,内部的值能改,但是不允许重新赋值,不允许更改地址

![image-20210528103147070](https://gitee.com/IU_czx/images/raw/master/img/image-20210528103147070.png)

## 解构赋值

> ES6允许从**数组**中提取值,按照对应位置,对变量赋值,**对象**也可以实现解构

![image-20210528103615680](https://gitee.com/IU_czx/images/raw/master/img/image-20210528103615680.png)

![image-20210528103937344](https://gitee.com/IU_czx/images/raw/master/img/image-20210528103937344.png)

## 箭头函数

> ()=>{}
>
> const fn=()=>

* 如果形参只有一个,小括号可以省略掉,返回值只有一个,大括号也能省略掉

* 箭头函数
  * 它不绑定this关键字,指向的是函数定义位置的上下文this

## 剩余参数

![image-20210528193819063](https://gitee.com/IU_czx/images/raw/master/img/image-20210528193819063.png)

## 扩展运算符

> 扩展运算符可以将数组或者对象转为用逗号分隔的参数序列

应用:

1. 可以合并数组

   ```js
       <script>
           let arr1 = [1, 2, 3];
           let arr2 = [4, 5, 6];
           // 第一种方法,将数组合并
           let arr3 = [...arr1, ...arr2];
           console.log(...arr3);
           // 第二种方法
           let arr4 = [];
           arr4.push(...arr1, ...arr2, ...arr3);
           console.log(...arr4);
       </script>
   ```

2. 利用扩展符可以将伪数组转换为数组

   > 可以使用数组的方法

## Arrary的扩展方法

### 构造函数方法:Array.from()

> 将类数组或可遍历对象转换为真正的数组

```js
       // 通过Array.from方法
        // // let arr = Array.from(lis);
        // arr.push("a");
        // console.log(arr);
        var obj = {
            "0": 0,
            "1": 1,
            "2": 2,
            "3": 3,
            "4": 4,
            // 下面一定要给长度
            "length": 5
        }
        let arr = Array.from(obj, items => items * 2)
        console.log(arr);
```

Array种from后面还可以跟一个参数

### FIND()

```js
  var obj = [{
            id: 1,
            name: "czx"
        }, {
            id: 2,
            name: "zsw"
        }]
        let target = obj.find(item => item.name === "czx");
        console.log(target);
```

### findIndex()

> 只找到第一个符合条件的索引,和find的方法一样

### includes()

> 表示某个数组中有没有这个参数,有的话就返回true,没有就返回false

## 模板字符串

```js
`模板字符串`
```

* 模板字符串可以解析变量
* 它可以进行换行
* 还可以调用函数

```js
        // 第一个特点:可以解析变量
        let str = `这是一个模板字符串`;
        console.log(`后面是我拼接的${str}`);
        var obj = {
            id: 1,
            name: "czx"
        }
        // 第二个特点:可以换行显示
        console.log(`
            <span>${obj.id}</span>
            <span>${obj.name}</span>
        `);
        // 第三个特点,再模板字符串中可以调用函数
        const fn = () => "hhhhhhhh";
        let line = `${fn()}哈哈哈哈哈哈`;
        console.log(line);
```

### StartWith和endsWith

> 可以检查字符串中是否已这个开始或结尾

### repeat()

> 字符串的重复输出次数

## set数据结构

> 类似于数组,但是成员的值是唯一的,没有重复的值
>
> 本身是一个构造函数,用来生成set数据结构

实例方法:

1. add(value):添加某个值,返回Set结构本身
2. delete(value):删除某个值,返回一个布尔值
3. has(value):返回一个布尔值,表示该值是否为Set的成员
4. clear():清除所有成员,没有返回值

### 从set结构中取值

> 用forEach这个函数

```js
    <script>
        const arr = new Set([1, 2, 3, 4, 5, 1, 2, 3, 4, 5]);
        console.log(arr);
        console.log(...arr);
        arr.add("a").add("b");
        console.log(...arr);
        arr.delete(1);
        console.log(...arr);
        arr.has(10);
        console.log(...arr);
        // forEach遍历Set结构中的数据
        arr.forEach(value => console.log(value));
    </script>
```

