# this在全局作用域下绑定什么

1. 在浏览器环境下,this绑定window
2. 在node环境下,this绑定一个{}

# this的指向

> this是在即将执行的时候,动态绑定到执行上下文的
>
> 根据不同的绑定规则,this的绑定是不同的

## this的绑定规则

1. 默认绑定

   即this在浏览器中全局作用域环境下默认绑定`window`

   在node环境下,绑定的是`{}`

2. 隐式绑定

   即哪个调用普通函数的,就会隐式绑定到哪个上面

3. 显式绑定

   使用call,apply,bind进行绑定

   | call               | apply              | bind                  |
   | ------------------ | ------------------ | --------------------- |
   | 传递参数是剩余参数 | 传递参数是数组     | 不传递参数            |
   | 绑定了就会立马执行 | 绑定了就会立马执行 | 只负责绑定,不负责执行 |
   | 每次使用都需要绑定 | 每次都需要绑定     | 只需要绑定一次        |

4. new绑定

   通过面向对象的思想,new出来的,会直接绑定到new的那个对象上
   
   ```js
   function Person(name, age) {
       this.name = name;
       this.age = age;
   }
   
   /**
    * 通过new出来的,会产生一个Person{}对象
    * this就是执行Person对象
    * 所以在this.name=name
    * 就是把name放在this中指向的那个对象内
    */
   
   const student = new Person("czx", 18);
   
   console.log(student);
   ```
   
   

## 一些函数的this分析

1. `setTimeout`

   他在内部其实是一个独立函数调用,所以在定时器中使用普通函数的话,他的this指向是window

2. `DOM元素`

   在使用监听事件的时候,this的指向的是调用它的DOM元素

3. `forEach`

   在使用`forEach`的时候,里面传入的是`普通函数`的话,不做其他的操作,默认的this是window

4. 类似于`forEach`的高阶函数

   this在不做任何操作的时候,默认都是独立调用

   高阶函数是可以传入第二个参数,就是this的绑定,我们可以选择绑定那个

   不确定的话,可以看下`IDE`工具内的提示

   不过吗,我在实际用的时候,基本都是用箭头函数,所以用不用看自己

## 规则优先级

1. 显示绑定高于隐式绑定
2. new的绑定高于bind
3. 在显示绑定的时候,bind的优先级最高

显示绑定遇见null和undefined

如果显示绑定null和undefined的话,那么会直接做一个忽略,还是原来的调用

## 特殊绑定(间接函数引用)

```js
var obj1 = {
    myname: "czx",
    foo: function () {
        console.log(this);
    }
}

var obj2 = {
    nyname: "bar",
};
// var bar = 0;
// 类似于这种的是间接函数调用
// 这种调用的是独立函数调用,指向window
(bar = obj1.foo)();
(obj2.bar = obj1.foo)();
```

## 箭头函数的this绑定

> 箭头函数中没有this,他会继承上下文

```js
var obj = {
    myname: "czx",
    foo: () => {
        console.log(this);
    }
}

//即使是obj调用的foo函数,依然输出的是window
//这是因为 箭头函数不管是谁调用他的,他是根据上下文的作用域去寻找的
//这道题内 foo的作用域是 GO 也就是window
obj.foo(); //window


var obj2 = {
    myname: "czx",
    foo: function () {
        (() => {
            console.log(this);
        })()
    }
}


//我们可以分析一下
//执行foo的时候呢,我是在普通函数中嵌套了一个箭头函数
//那么 箭头函数在执行的时候,就会去寻找它的作用域
// 此时他的作用域就是 foo外层的普通函数
//普通函数是obj2进行调用的,那么普通函数的this绑定了obj2
//所以箭头函数的this也就是普通函数的this
obj2.foo(); //obj2
```

## 面试题分析

1. 面试题一

   ```js
   var name = "window";
   
   var person = {
       name: "person",
       sayName: function () {
           console.log(this.name);
       }
   };
   
   function sayName() {
       var sss = person.sayName;
       sss();  //window
       person.sayName(); //person
       (person.sayName)(); //person
       (b = person.sayName)(); //window
   }
   
   sayName();
   ```

   我们现在来分析一下

   1. 首先 我们看 `sayName()`执行,它是独立函数调用,所以`this`指向`window`

   2. 再看`sss()`,它也是独立函数调用,输出结果为 全局的`name`,也就是window
   3. 看`person.sayName()`,这个是person进行了隐式调用,那么this绑定到了person,所以输出结果为person
   4. 看`(person.sayName)()`,这个其实等价于`person.sayName()`,所以输出结果为person
   5. 看最后一个`(b=person.sayName)()`,这个就是间接函数引用,实际上是独立函数,所以指向window,输出window

2. 面试题二
   
   ```js
   var name = 'window'
   var person1 = {
       name: 'person1',
       foo1: function () {
           console.log(this.name)
       },
       foo2: () => console.log(this.name),
       foo3: function () {
           return function () {
               console.log(this.name)
           }
       },
       foo4: function () {
           return () => {
               console.log(this.name)
           }
       }
   }
   
   var person2 = { name: 'person2' }
   
   person1.foo1(); //person1
   person1.foo1.call(person2);//person2
   
   person1.foo2(); //window
   person1.foo2.call(person2); //window
   
   person1.foo3()(); //window
   person1.foo3.call(person2)();//window
   person1.foo3().call(person2); //person2
   
   person1.foo4()(); //person1
   person1.foo4.call(person2)();//person2
   person1.foo4().call(person2);//person1
   ```
   
   分析
   
   1. `person1.foo1()`执行这个的时候,隐式绑定,`this`指向`person1`,所以name输出为person1
   2. `person1.foo1.call(person2)`执行这个时候,使用`call`显示绑定了`person2`,所以输出name为person2
   3. `person1.foo2()`因为foo2是箭头函数,他会去寻找作用域,作用域为GO,所以指向window
   4. `person1.foo2.call(person2)`因为是箭头函数,绑定对它来讲是没有用的,所以指向的还是window
   5. `person1.foo3()()`这个我们仔细看`person1.foo3()`这个时候已经执行完了,返回的是一个函数,后面再加了个`()`,此时执行的是新函数了,这相当于是独立函数调用,那么指向的就是window
   6. `person1.foo3.call(person2)()`,这个和上面是一样的,前面只是将foo3的this换绑了,并不影响执行完毕后,返回的函数,实际上还是一个独立函数调用,指向的是`window`
   7. `person1.foo3().call(person2)`,这个和上面稍微有点区别,这个是将执行完毕的返回函数进行了一个显示绑定,那么最后的绑定结果就是person2,this指向的是person2
   8. `person1.foo4()()`首先我们看foo4()是一个普通函数,`person1.foo4()`他的this是指向的person1,而他们执行完毕后的返回的是一个箭头函数,此时再执行,箭头函数就会去寻找作用域,离他最近的作用域是foo4,而foo4指向的是person1,那么箭头函数的this也就是person1
   9. `person1.foo4.call(person2)()`这个解释和上面一样,只不过`person1.foo4`这个显示绑定到了person2上面,所以箭头函数的this指向的是person2
   10. `person1.foo4().call(person2)`这个是在箭头函数上显示绑定,这个是无效的,所以还是person1
   
3. 面试题三

   ```js
   var name = 'window'
   
   function Person(name) {
       this.name = name
       this.foo1 = function () {
           console.log(this.name)
       },
           this.foo2 = () => console.log(this.name),
           this.foo3 = function () {
               return function () {
                   console.log(this.name)
               }
           },
           this.foo4 = function () {
               return () => {
                   console.log(this.name)
               }
           }
   }
   
   var person1 = new Person('person1')
   var person2 = new Person('person2')
   
   person1.foo1()//person1
   person1.foo1.call(person2) //person2
   
   person1.foo2() //person1
   person1.foo2.call(person2) //person1
   
   person1.foo3()()//window
   person1.foo3.call(person2)()//window
   person1.foo3().call(person2)//person2
   
   person1.foo4()() //person1
   person1.foo4.call(person2)()//person2
   person1.foo4().call(person2) //person1
   ```

   分析

   1. `person1.foo1()`隐式绑定person1,所以输出为person1
   2. `person1.foo1.call(person2)`显示给foo1绑定person2,所以输出为person2
   3. `person1.foo2()`箭头函数寻找作用域,找到了Person,因为是person1这个实例对象去调用foo2的,所以箭头函数的this指向person1
   4. `person1.foo2.call(person2)`因为这个是给箭头函数绑定,无效,所以还是person1
   5. `person1.foo3()()`返回函数,再执行,是独立函数调用,this指向window
   6. `person1.foo3.call(person2)()`返回函数,再指向,是独立函数调用,this指向window
   7. `person1.foo3().call(person2)`给返回的函数显示绑定.所以再执行的时候是this是指向person2
   8. `person1.foo4()()`返回的是箭头函数,执行的时候寻找作用域,是person1,所以this指向的是person1
   9. `person1.foo4.call(person2)()`执行的时候,给foo4进行了换绑,所以箭头函数寻找的时候找到了person2,所以this指向person2
   10. `person1.foo4().call(person2) `因为是给箭头函数绑定,所以无效,还是指向person1

4. 面试题四

   ```js
   var name = 'window'
   function Person(name) {
       this.name = name
       this.obj = {
           name: 'obj',
           foo1: function () {
               return function () {
                   console.log(this.name)
               }
           },
           foo2: function () {
               return () => {
                   console.log(this.name)
               }
           }
       }
   }
   var person1 = new Person('person1')
   var person2 = new Person('person2')
   
   person1.obj.foo1()() //window
   person1.obj.foo1.call(person2)() //window
   person1.obj.foo1().call(person2) //person2
   
   person1.obj.foo2()()  //obj
   person1.obj.foo2.call(person2)() // person2
   person1.obj.foo2().call(person2)//obj
   ```

   分析

   1. `person1.obj.foo1()()` 返回函数 独立函数调用 this指向window
   2. `person1.obj.foo1.call(person2)()`返回函数 独立函数调用 this指向window
   3. `person1.obj.foo1().call(person2) `返回函数显示绑定`person2`,指向person2
   4. `person1.obj.foo2()()` 首先`person1.obj.foo2()`执行,我们来看下,是谁在调用foo2,是obj在调用,那么foo2的this指向的是obj,所以返回的箭头函数寻找作用域,找打的是foo2,foo2的this指向的是obj,所以箭头函数this的指向的是obj
   5. `person1.obj.foo2.call(person2)()`给foo2显示换绑到person2,所以箭头函数找到的作用域是person2,所以this指向的是person2
   6. `person1.obj.foo2().call(person2)`给this绑定是无效的,所以还是obj