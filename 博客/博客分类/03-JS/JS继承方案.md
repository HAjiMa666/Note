# JavaScript中实现继承的6种方案

## 01-原型链的继承方案

```js
function Person(){
    this.name="czx";
}
function Student(){}
var p1=new Person();
Student.prototype=p1;
var student1=new Student();
console.log(student1); // Person{}
console.log(student1.name); // czx
```

这是最简单的一种方案,同时也是弊端最多的方案,我们来分析下他的弊端

1. 如果直接打印Student的实例对象,打印出来是这样

   ![image-20210928104131722](https://gitee.com/IU_czx/images/raw/master/img/%E5%8D%9A%E5%AE%A2-%E7%BB%A7%E6%89%BF01.png)

   为啥不是打印出来的Student呢,我们先得了解一个东西,打印出来的这个名称是由`constructor`决定的

   我们直接将Person的实例对象赋值给Student的`prototype`,Student原来的prototype就被覆盖了
   而Person的实例对象的隐式原型是指向Person的`prototype`的

   而Person的prototype中是有`constructor`的,`constructor`是指向Person本身的
   你们可以这么理解,Person.prototype,那么constructor就是指向Person,Object.prototype中的`constructor`就是指向Object

   所以,Student1没找到自己的constructor,沿着原型链往上找,找到了Person的`constructor`,所以就是Person

2. 通过这种方式继承过来,打印学生的实例对象,继承过来的属性是看不见的

3. 如果在父类Person上添加引用类型的数据,如果我们创建多个学生对象实例,修改了引用类型的数据,那么父类中的数据也是会被改变的,那么实例的对象,相互之间就不是独立的,可以看下下面这段代码

   ```js
   function Person(){
       this.friends=[];
   }
   function Student(){}
   var p1=new Person();
   Student.prototype=p1;
   var student1=new Student();
   var student2=new Student();
   student1.friends.push("czx");
   console.log(student2.friends); // ["czx"]
   ```

4. 无法传递参数

   细心的同学可能就会发现,我这样写是无法传递参数的.那以后我们要传递参数的话,就会相当麻烦

   🎈所以,接下来我们看第二种方式

   ---

## 02-借用构造函数实现继承

这个方案的核心就是 `call`

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}


// 第一个弊端: Person执行了两次
// 第一次是new出来的,第二次是call执行的
// 第二个弊端是 在new的时候,会往student上加上一些不必要的属性,会把继承的属性加到了Student上面,这是没必要的
Student.prototype = new Person();
Student.prototype.studying = function () {
    console.log(this.name + "再学习");
}
function Student(name, age, sno) {
    Person.call(this, name, age);
    this.sno = sno;
}

let stu1 = new Student("czx", 18, 180047101);
stu1.studying();
console.log(stu1);

```

这个方案解决了第一种方案的(2),(3),(4)弊端

1. 这两个放的顺序一定不能放错了

   ```js
   Student.prototype = new Person();
   Student.prototype.studying = function () {
       console.log(this.name + "再学习");
   }
   ```

   顺序放错的话 `studying`那个函数加在了`Student`原来的原型上,而后又把`Person`的实例对象覆盖了`Student`的原型,那么在我们调用的话,就找不到了

2. 我们来看下这一段

   ```js
   function Student(name, age, sno) {
       Person.call(this, name, age);
       this.sno = sno;
   }
   ```

   因为在我们内直接使用call调用了Person并执行了,那么Person的属性也都可以在Student里面使用,这也能使的我们可以传递属性,可以复用父类中定义的属性.并且在我们打印的时候,也能把属性全部打印出来,大家可以自己试试

3. 这个方案说实话已经很不错了,解决了大部分问题,如果简单使用也是可以的,但是这种方案就没有弊端吗?
   答案是有的,我们现在来看下它的弊端

   1. 第一个弊端: Person执行了两次
   2. 第一次是new出来的,第二次是call执行的
   3. 第二个弊端是 在new的时候,会往student上加上一些不必要的属性,会把继承的属性加到了Student上面,这是没必要的,我们只需要在call的时候,调用Person,并且把属性放到Student上面去就行了
   4. 第一种方案的第一个弊端也没有解决

🎆我们现在来看下一种方案

---

## 03-直接继承父类的原型

```js
function Person(name) {
    this.name = name;
}
Person.prototype.running = function () {
    console.log(this.name + " is running");
}

function Teacher(name, career) {
    Person.call(this, name);
    this.career = career;
}
function Student(name, age) {
    Person.call(this, name);;
    this.age = age;
}

// 这种方法可不可行呢?
// 答案是不行
// 我们看下面的例子
// 我明明是给学生单独加的属性,但是teacher也可以共用它,这是不合理的
// 我们需要的是学生和老师自己的原型上是属于自己独一无二的属性
// 这样子可复用性才会高
Student.prototype = Person.prototype;
Teacher.prototype = Person.prototype;
Student.prototype.studying = function () {
    console.log(this.name + " is learning");
}

var s1 = new Student("czx", 18);
var t1 = new Teacher("teacher", "math");
console.log(s1);
s1.running()
s1.studying();
t1.studying();
```

这种方案是基于第二种方案的一个改版,但是我们看下这种方案可不可行

看完代码,大家也知道不行了,我在代码上也有详细的注释

1. 我明明是给学生单独加的属性,但是teacher也可以共用它,这是不合理的,这是因为我们加的方法都是直接加在了父类的原型上
2. 我们需要的是学生和老师自己的原型上是属于自己独一无二的属性
3. 这样子可复用性才会高

🎇接下来会介绍基于对象来实现继承的两种方案,这两种方案对于最后一种方案的出现有很大的帮助,请大家仔细看看理解

---

## 04-原型式继承

> 这个方案是由*道格拉斯·克罗克福德（Douglas Crockford）*所提出来的,是对我们前端届贡献特别大的一个人物
>
> 这个方案是专门针对**对象**的

我们先看下他当时是怎么实现的

```js
// o是对象
function createObject(o){
    function fn(){};
    //将对象赋值给fn的原型
    fn.prototype=o;
    //将实例化的fn赋值给新对象,这样新对象的隐式原型就会指向我们传递进来的obj
    var newObj=new fn();
    return newObj;
}
```

大家可以浏览下我上面写的代码,这是道格拉斯当时的想法

现在随着js的逐渐变化,我们写这种方案也变得比较简单了,我们来看下面代码

```js
function createObject(o){
    var newObj={};
    Obejct.setPrototypeof(newObj,o);
    return newObj;
}
```

`Object.setPrototypeof()`可以给对象设置一个新的原型,相比之前更加方便了

基于最新的ECMA标准的化,我们还可以这么写

```js
var newObj=Object.create(o);
```

直接创建一个以`o`为原型的对象

🧨接下来是针对这一种方案做的一个完善版

---

## 05-寄生式继承

```js
var personObj = {
  running: function() {
    console.log("running")
  }
}
function createStudent(name) {
  var stu = Object.create(personObj)
  stu.name = name
  stu.studying = function() {
    console.log("studying~")
  }
  return stu
}
var stuObj = createStudent("why")
var stuObj1 = createStudent("kobe")
var stuObj2 = createStudent("james")
```

这种方案是基于第四种方案进行改编的

寄生式继承的思路是结合原型类继承和工厂模式的一种方式；

即创建一个封装继承过程的函数, 该函数在内部以某种方式来增强对象，最后再将这个对象返回；

✨好,现在结合上述五种方案,我们可以开始介绍最后一种方案啦,只有了解了上述五种方案后,再来看这种方案,会有一种恍然大悟的感觉🧑

----

## 06-寄生组合式继承

> 这种方案就是JS社区这么多年积累出来的最佳方案,我们来看下

```js
//因为继承是一个可能很常用的方法,所以我们把继承的方法提炼出来了,作为一个工具函数
//这样我们只需要传递父类和子类,函数就能自动帮助我们实现继承
function inherit(faObj, chiObj) {
    //因为父类和子类的原型都是对象,所以可以用这个方法
    //创建一个以父类原型对象为原型的对象,并且将它赋值给子类原型
    //这帮助我们解决了第二种方案的父类执行了两次的问题,不需要实例化父类对象
    chiObj.prototype = Object.create(faObj.prototype);
    //这是为了解决前面方案都没有解决的constructor的方法
    Object.defineProperty(chiObj.prototype, "constructor", {
        value: chiObj,
        enumerable: false,
        writable: false,
        configurable: false,
    })
}

function Person(name, age, height) {
    this.name = name;
    this.age = age;
    this.height = height;
}
//下面是我们讲的第二种方案 借用构造函数实现继承
function Student(name, age, height, sno) {
    Person.call(this, name, age, height);
    this.sno = sno;
}
function Teacher(name, age, height, pro) {
    Person.call(this, name, age, height);
    this.pro = pro;
}

//在这里使用我们自己定义的继承函数
inherit(Person, Student);
inherit(Person, Teacher);
//注意:上下的顺序不能错,我在第二种方案的时候有讲过
Person.prototype.playing = function () {
    console.log(this.name + " is playing");
}
Student.prototype.studying = function () {
    console.log(this.name + " is studying");
}
Teacher.prototype.teaching = function () {
    console.log(this.name + " is teaching");
}
var s1 = new Student("czx", 18, 1.88, 180047101);
var t1 = new Teacher("Mr.cao", 21, 1.88, "computer");

//可以打印出所有的属性 并且打印的是对应的类,而不是父类了
console.log(s1);  // Student{}
console.log(t1); // Teacher{}
s1.studying();
t1.teaching();
s1.playing();
t1.playing();
```

我在代码中写的很详细了,大家一定要好好看看下,理解理解,如果觉得有啥疑惑,可以把之前的几种方案连起来好好看看

如果还有什么疑惑,欢迎大家在评论区留言😁😁😁