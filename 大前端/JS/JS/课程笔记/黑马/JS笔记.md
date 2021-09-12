#  学习心得

* 在新浪下拉菜单案例中,我使用了盒子模型:border-box

  我也发现了问题:

  如果给父盒子和子盒子都设置了高度和宽度,盒子模型不能父子盒子一起使用,会造成子盒子往父盒子底下沉,会影响布局,只要给子盒子设置就行,这样就能嵌套在父盒子内,不发生那种现象

* **opacity:.5**,可以使图片半透明效果

* 如果遇到需要移动的值,在样式表中不要加其他固定的数值,会导致两个值互相之间冲突,造成效果错误



#                                              JS笔记

 学习目标:

1. 能够说出什么是编程语言

2. 能够区分编程语言和标记语言的不同

3. 能够说出常见的数据存储及单位换算关系

4. ==能够说出内存的主要作用以及特点==

   

###### 数据存储单位(加深印象 再记一遍)

1. 位(bit): 1bit可以保存一个0或者1(最小的存储单位)
2. 字节(Byte): 1B=8b
3. 千字节(KB) 1KB=1024B
4. 兆字节(MB): 1MB=1024KB
5. 吉字节(GB) : 1GB=1024MB
6. 太字节(TB): 1TB=1024GB

###### 程序运行

1. 打开某个程序,先从硬盘中把程序的代码加载到内存中

2. CPU执行内存中的代码

   注意:要内存,是因为CPU和硬盘速度不匹配,会导致性能浪费,所以用一个内存条,内存条用电,硬盘是机械

####                                                                     初识JavaScript

==布兰登.艾奇==发明了这门语言

JavaScript是一种在运行在客户端的脚本语言

==脚本语言:不需要编译的语言,通过js解释器来逐行进行编译==

**浏览器分为渲染引擎和JS引擎**



<center>
    <h4>
    JS的组成
    </h4>
</center>



* JavaScript语法(ECMAScript)

* 页面文档对象模型(DOM)

* 浏览器对象模型(BOM)

  

  > JS有三种书写位置,分别为行内,内嵌和外部

# JS的基础语法

  * alert是一个弹出窗口
* prompt是一个输入窗口
  * console.log是一个在后台给程序员看的
  * var 用来声明变量的



![JS命名规范](https://gitee.com/IU_czx/images/raw/master/img/JS%E5%91%BD%E5%90%8D%E8%A7%84%E8%8C%83.png)

==JavaScript是一种弱类型语言==

js是根据右边的值类型来确定变量类型,他是动态语言,数据类型是可以发生变化的

## js数据类型

1. 简单数据类型:数字型Number

   ==程序数字前面加0是八进制==

   ==数字前面+0x就是16进制==

###### 数字型范围

   JavaScript中数值的最大值和最小值:

   ```js
   alert(Number.MAX_VALUE);
   alert(Number.MIN_VALUE);
   ```

   ==infinity:无穷大==

   ==- infinity:无穷小==

   ==NaN: not a number==

isNaN()这个方法来判断非数字,是数字返回false

###### 字符串类型

* 在JS中推荐字符串使用==单引号==
* js可以用嵌套的,遵从外单内双,或者外双内单
* ==\n==进行换行         ==注意:\n要在字符串里面写,位置要弄对==

* 转义字符都是用\开头的
* \\\斜杠 
* \\'单引号 
* \\ "双引号 
* \t== tab缩进 
* \b空格 
* 字符串长度:str.length 
* 字符串拼接:使用+号,就是拼接的意思,只要是字符串和任意数据类型相加,所得数据一定是字符串类型

###### 剩下的一些类型

* 布尔类型中,true代表是1,false代表是0,相加的时候是这样取值的
* Undefined:数字和Undefined相加的,会出现NaN值
* Null:空值

  ###### 获取数据类型

* typeof:这个可以获取数据类型
* prompt:取过来的值是String类型的

###### 数据类型转化

*  转换为字符串类型:
* * toString方法
  * String(变量)
  * ==利用加号实现==这一种也称为隐式转换
* ==转换为数字型== 
* * paresInt:将String类型转换为整数类型
  * parseFloat:转换为浮点型数值型
  * Number() 强制转换函数
  * 隐式转换(- * /):利用算术运算隐式转换为数值型
* 转换为布尔型:Boolean函数

> 代表空值,否定值都会被转化为false.如0,NaN,null,undefined, 其余都会被转为true

###### 第一个扩展面

* 解释型语言:边解释边运行
* 编译型语言:把所有代码全部写完,才能进行编译
* 标识符:人员为变量,函数,参数所取的名字
* 关键字:js本身已经使用的字,不能当作关键字
* 保留字:预留的关键字,未来可能会用到的,所以比能当作标识符.

##  JS运算符

### 算数运算符

* +

* -

* *

* /

* %:除余

* 浮点数直接参与运算,会对运算精度产生影响

* 我们不能直接判断浮点数是否相等

* 余数为零说明能被整除

#### 表达式和返回值

* 表达式:是由数字,运算符,变量组成的式子
* 返回值:2=1+1,右边的表达式计算完返回给左边

####   递增和递减运算符

* ++和--实现的就是递增和递减
* 后置自增:先返回原值,,后自加一
* 前置自增:就先加一,在返回值

### 比较运算符

* 大于,小于,等于==,不等于!=

  > 在==中,会进行类型转换

* ===全等,所有东西都要一样(值和数据类型)

* !==:不完全一样

### 逻辑运算符

* &&:与
* ||:逻辑或
* !:逻辑非,取反符

> 一种特殊情况,逻辑中断,如果我们不在使用布尔值进行运算,使用多个值进行计算,会出现短路运算
>
> 短路运算原理:当有多个值时,左边的表达式可以确定结果时,就不在计算右边的表达式的值
>
> 语法:表达式1&&表达式2,如果第一个表达式为真,则返会表达式2,如果第一个值为假,则返回表达式1.

* 逻辑或||的短路运算

  > 表达式一为真,则返回表达式一,为假,则返回表达式二

### 赋值运算符

* num+=2同等于num=num+2;其他符号同理

### 运算符优先级(序号代表他的优先级,序号越小,优先级越高)

1. 小括号的运算级式最高的
2. 一元运算符(++,--,!)
3. 算数运算符(+,-,*,/)
4. 关系运算符(大于号,小于号啥的)
5. 相等运算符
6. 逻辑运算符
7. 赋值运算符
8. 逗号运算符

## JS的流程控制



#### 顺序结构

* 按顺序执行的

#### 分支结构

* if(表达式为真),则执行大括号的值
* * if else if语句,多个判断,第一个条件需要判断,第二个条件不用判断第一个条件了,这样写代码更简单
* switch语句

* * switch() {

    case value1:

    break;

    .......

    default：

    执行最后的语句

    }

    > switch括号里的值是全等，所有类型都要一样.
    >
    > switch每条语句都要加上break,要不然,会全部执行

#### 循环结构

##### for循环

> 重复执行某种操作

* 大括号里面是循环体
* for(初始化变量; 条件表达式; 操作表达式)

##### while循环

> 语法:
>
> while(语法执行条件){
>
> 条件为真,则执行循环体
>
> 里面应该也要有操作表达式,完成计数器的更新,防止==防止死循环==
>
> }

##### do While循环

> 语法:
>
> do{
>
> }while(循环体)
>
> 和while不同的是:会先执行一次循环体,如果表达式为真,则继续执行循环体,否则退出循环

#####  continue关键字

> 直接跳出循环
>
> 只要遇见continue,就退出本次循环,直接到i++

##### break关键字

> 用于立即跳出循环,不执行后续循环



#### 三元表达式(简化版的if-else)

* 表达式 ? 表达式1 : 表达式2
* 表达式为真,则返回表达式1,否则返回表达式2

## JS命名规范

> 函数,变量的命名一定要有意义
>
> 变量一般名词,函数一般动词
>
> 操作符左右两侧都要有一个空格
>
> 单行注释前面一般有一个空格
>
> 还有就是循环要对齐

## 数组

### 概念

> 数组是一组数据的集合,其中每个数据都是元素,在数组中可以存放任意类型的数据

### 创建方式

1. var arry=new Array();//利用new方式

2. var arr= [];//利用数组字面量创建数组

> 注意里面的数据用逗号隔开

### 获取数组的元素

* 数组的索引(下标):是从==0==开始的
* 通过数组的下标来获取到数组的元素
* 想要输出多个元素,在括号里面用逗号隔开即可

### 数组中新增元素

1. 修改length长度
2. 通过修改数组元素,修改索引号
3. 不要直接给==数组名(例arr,而不是arr[0])==赋值,否则里面的数组元素都没有了
4. 如果让一个数组的元素赋值给新数组,新数组的数组长度不确定,可以这么使用

> newarr[newarr.length]=arr[i];
>
> 这样子可以自适应的添加数组长度,比较方便
>
> 如果要让数组倒序输出,让i为arr.length-1,在赋值给新数组,即可,就能实现倒序输出的作用

### 冒泡排序

> 一次比较两个元素,每次比一套循环,按顺序两两相比
>
> 算法找规律

## 函数

### 函数的一些性质

> 封装了一段可以重复执行代码块

* 声明函数
* 执行函数
* 函数名一般是动词
* 在声明函数中的小括号中是形参,在调用函数中的小括号是实参
* 如果实参的个数小于形参的个数,另外的几个就会定义为Undefined
* 函数可以带参数,也可以不带参数
* 函数的返回值

> function(){
>
> return 需要返回的结果
>
> }

- return有终止函数的作用
- 如果函数有return则返会return后面的值,否则返回undefined

### arguments的使用方法

* arguments里面存储了所有传递过来的实参
* 他本质上是一个伪数组,但它具有数组的length属性
* 它是按照索引的方式进行存储
* 他没有真正数组的一些方法 pop() push()等
* 只有函数才有arguments对象,每个函数都内置好的

### 函数表达式(匿名函数)

> var 变量名=function(){}
>
> var fun=function(){
>
> 直接在里面写
>
> }
>
> 这个fun是变量名,不是函数名
>
> 变量里面存的是值,函数里面存的是函数
>
> 函数表达式也可以进行正常的值传递

### 函数的作用域

#### 概念

> 代码名字在某个范围内起作用和效果,目的是为了提高程序的可靠性,主要是减少命名冲突

#### 全局作用域

* 整个script标签,或者一个单独的js文件

#### 局部作用域

* 只在函数内部起效果和作用

#### 注意

* 如果在函数内部没有直接声明的变量也属于全局变量
* 全局变量只有浏览器关闭时才会销毁,比较消耗资源
* 局部变量则不会,比较节省资源
* 所以最好是多使用局部变量,节省内存空间

### 作用域链

* 内部函数访问外部函数的变量,采取的是链式查找的方式来决定取哪个值,这种结构我们称为作用域链(就近原则)

## JS预解析

* 我们js引擎运行js分为两步

1. 预解析(会把js里面所有的var,还有function提升到当前作用域的最前面)
2. 代码执行(按照代码书写的顺序从上往下执行)

* 预解析分为变量预解析(变量提升)和函数预解析(函数提升)
* (1) 变量提升:就是把所有的变量声明提升到当前的作用域最前面 不提升赋值操作
* (2)函数提升 就是把所有的函数声明提升到当前作用域的最前面 不调用函数
* var　ａ＝ｂ＝ｃ＝９相当于var a=9; b=9;c=9;
* 集体声明: var a=9,b=9,c=9

> ==eg:==
>
> ```js
> f1();
> console.log(c);
> console.log(b);
> console.log(a);
> function f1(){
>     var a=b=c=9;//这个相当于相当于var a=9; b=9;c=9;也就是说b和c没有声明,即b和c为全局变量
>     console.log(a);
>     console.log(b);
>     console.log(c);
> }
> //所以最后的结果是9 9 9 9 9 报错
> ```

## JS对象

### 概念

* 对象由==属性==和==方法==组成的
* 属性:事物的特征
* 方法:事物的行为

### 创建对象的三种方法

1. ==利用字面量创建对象==

> ```js
>  var obj={
> 
>    userName: '张三凤',
> 
>    age: 18;
> 
>    sex: '男'
> 
>    sayHi:function(){
>        console.log('hi');
>    }
> }
> ```
>
> * 里面的属性或者方法我们采取键值对的形式   键 属性名: 值  属性值
> * 多个属性或者方法中间用逗号隔开
> * 方法冒号后面的是一个匿名函数
> * 调用对象的属性 我们采取 ==对象名.属性名==
> * 调用对象的另外一种方法:对象名['属性名']
> * 调用对象的方法sayHi   对象名.方法名 obj.sayHi()

2. ==利用new object创建对象(是使用等号赋值)==

   ```js
   var obj=new Object();
   obj.name='张三丰;
   ```


3. ==利用构造函数创建对象==

> 因为我们一次创建一个对象,里面有很多的属性和方法是大量相同的 我们只能复制
>
> 因此我们可以利用函数的方法,重复这些相同的代码,我们就把这个函数成为构造函数
>
> 因为这个函数不一样,里面封装的不是函数,而是封装的对象
>
> 构造函数:就是把我们对象里面一些相同的属性和方法抽象出来封装的函数里面

构造函数的语法格式

```js
function 构造函数名(){
    this.属性=值;
    this.方法=function(){}
}
```

==构造函数的首字母要大写==

==调用构造函数一定要用new==

==构造函数泛指的某一类==

### new关键字执行过程

1. new 构造函数可以在内存中创建了一个空的对象
2. this就会指向刚才创建的空对象
3. 执行构造函数里面的代码,给这个空对象添加属性和方法
4. 返回这个对象

### 对象的遍历

格式

~~~
for(var k in obj){
   console.log(k);//k 变量输出得到的是属性名
   console.log(obj[k]);//他输出的是属性值
}
~~~

for in 里面的变量我们喜欢用的是key或者k.

## 内置 对象

* js中的对象分为三种:自定义对象,内置对像,浏览器对象
* 前面两种对象是js基础内容,属于ECMAScript,第三个浏览器属于我们js独有的,我们JS API讲解

#### MDN(查文档)

* 里面一些内置对象直接去MDN官网查看,解释的非常详细

### 常用的数学函数

```
Math.PI
Math.floor()//向下取整
Math.ceil()//向上取整
Math.round()//四舍五入函数,它往大了取,无论整数还是负数
Math.random()//随机函数
```

### 常用的日期函数（Date）

- 查文档去
- 时间戳(获取到1970.1.1到现在的时间)

### 倒计时案例

核心算法:

1. 输入的时间减去现在的时间就是剩余的时间,即倒计时,但是不能拿着时分秒相减,比如05减去25,结果会是负数的
2. 用时间戳来做,用户输入时间总的秒数减去现在时间的总毫秒数,得到的就是剩余时间的毫秒数
3. 把剩余的时间总的毫秒数转换为天,时,分,秒

### 常用的数组函数(array)

* 查文档  

* 检测是否为函数的两种方式

  ```
  变量名 instanceof Array
  Array.isArray(变量名)
  ```

* ==push()==//在我们数组的末尾 添加一个或者多个数组元素

* 参数直接写数组元素就可以,返回的结果时是新数组的长度

* ==unshift()==:是在头部添加元素

* ==pop()==:是用来删除数组的最后一个元素,返回的是删除的元素

* ==shift()==:是用来删除数组的第一个元素,同样是返回删除的第一个元素

* ==reverse()==:反转数组

* ==sort==:排序

  ```
  array.sort(function(a,b){
   return a-b;//升序
   return b-a//降序
  })
  ```

* ==indexof(元素名称)==:返回该数组元素的索引号,前面加上last,是从后开始查找

* 数组转换为字符串:

  * arr.toString()
  * arr.join('自己想用的分隔符')

### 字符串对象

* 基本包装类型:就是把简单数据类型包装成为复杂数据类型(String,Number,Boolean)

~~~js
过程:
var str='czx';
var temp=new String('czx');
str=temp;
销毁临时变量temp
~~~

* 字符串不可变

  > 里面的值不会变的,他是在内存空间中开辟一个新的内存空间,你重新赋值,只是让指针指向了一个新的地址.

* charAt:返回索引的字符

* str[index]和charAt一样

* charCodeAt(index):返回相应索引号的字符ASCII码值

* substr():用来截取字符串,第一个参数是索引号,第二个参数是取几个字符

* replace:替换字符串

*  split:分割字符

## 简单类型和复杂类型

* 简单数据类型null 返回的是一个对象(特殊情况)

* 简单数据类型(值类型):在存储变量中的是值本身,null特殊

  总共有5种,string,number,Boolean,undefined,null

* 引用类型:复杂数据类型,在存储时变量中存储的仅仅是地址(引用),因此叫做引用数据类型,通过new关键字创建的对象(系统对象,自定义队象)

* ==简单类型传参数,只是复制了一份值给参数,在栈中开辟了一个新的空间给参数,并不会影响简单类型的值==

* ==复杂类型传参,其实是把他在栈的地址复制了一份给参数,那么参数和复杂类型所指向的都是一个地址,那么如果我们在函数内部对于这个地址进行了修改,那么原来复杂类型所指向的数据也会发生改变==

## 堆和栈

1. 栈:由操作系统自动分配释放存放函数的参数值,局部变量的值等,简单数据类型存放在栈中
2. 堆:存储复杂类型对象,一般由程序员分配释放,若程序员不释放,由垃圾回收机制回收

# WebApIs

## API

### 概念

> API是程序员提供的一种工具,以便更轻松实现想要功能

## WebAPIs

### 概念

针对浏览器提供交互效果

## DOM

> W3C推荐的处理可扩展标记语言(HTML或者XML)的标准编程接口

### DOM树

* 文档:一个页面就是一个文档,DOM中使用Document表示
* 元素:页面中的所有标签都是元素,DOM中使用element表示
* 节点:网页中的所有内容都是节点(标签,属性,文本,注释等),DOM中使用node表示
* ==DOM==把以上内容都看作是对象

### 获取元素

#### 根据ID获取

* 使用getElementByID获取

> ==注意==:因为页面是从上往下加载,所以得先有标签,所以我们==script==写到标签下面.参数==ID==是大小写敏感的字符串
>
> ```js
> console.dir()打印我们返回的元素对象,更加的查看里面的对象的属性和方法
> ```

#### 根据标签名获取

* getElementByTagName

* 通过标签名获取的元素,返回的是一个伪数组形式

* 如果页面中没有这个元素,那么返回的是一个空元素的伪数组

* 但是有时候你要获取比较精确的标签,可以通过给那个标签的父元素加上id,先通过ID来获取元素,在用那个ID作为元素,使用标签名获取,较为准确

* ```
  var ol=doucment.getElementByID('OL');
  var 精确元素=ol.getElementByTagName('li');
  ```

#### HTML5新增的方法

* 通过类名获取

```
doucment.getElementByClassName
```

* querySelector:返回指定选择器的第一个元素对象
* 里面的选择器要加符号,什么样的选择器,就加什么,id前面加#,类加==.==
* querySelectorAll:获取所有这种元素

#### 获取特殊元素

* 获取body元素

  ```
  document.body  返回body元素对象
  ```

* 获取html元素

  ```
  document.documentElement //返回html元素对象
  ```

### 事件基础

事件由三部分组成

* 事件源
* 事件类型
* 事件处理程序

```html
  <button id='btn'>曹志贤</button>
        <script>
            //(1)事件源 事件被触发的对象 谁 按钮
            var btn = document.getElementById('btn');
            //(2)事件类型 如何触发 什么事件 比如鼠标点击(onClick) 还是鼠标经过 还是键盘按下
            //(3)事件处理程序 通过一个函数赋值的方式完成
            btn.onclick = function () {
                alert('曹志贤,你要好好学习');
            }
        </script>
```

* 执行事件的步骤
  1. 获取事件源
  2. 绑定事件类型,注册事件
  3. 添加事件处理程序

### ==操作元素==

#### 改变元素内容

```
element.innerText
从起始位置到终止位置的内容,但它去除html标签,同时空格和换行也会去掉,不识别HTML标签,所以会直接显示
element.innerHtml
同上,包括HTML标签,同时保留空格和换行,这个是识别HTML标签
```

#### 常用元素的操作

eg

```html
  <button id='btn'>曹志贤_好好学习</button>
    <button id="btn_2">曹志贤_不好好学习</button>
    <img src="" alt="给你个奖励">
    <script>
        var btn = document.getElementById('btn');
        var btn_2 = document.getElementById('btn_2');
        var img = document.querySelector('img');
        btn.onclick = function () {
            img.alt = '不好好学习,给你一棒槌';
        }
    </script>
```

#### 案例(根据时间的不同来给出不同的问候语)

```html
<body>
    <div id='greet'>你好</div>
    <img src="" alt="你好">
    <script>
        var time = new Date();
        var getTime = function () {
            var y = time.getFullYear();
            var m = time.getMonth();
            var d = time.getDay();
            var h = time.getHours();
            var m = time.getMinutes();
            var s = time.getSeconds();
            return '你好,现在是' + y + '年' + m + '月' + d + '号' + h + '时' + m + '分' + s + '秒';
        }
        var greet = document.getElementById('greet');
        var img = document.querySelector('img');
        greet.innerHTML = getTime();
        var option = time.getHours();
        if (option >= 6 && option <= 8) {
            img.alt = '早上好';
        } else if (option <= 12) {
            img.alt = '上午好';
        } else if (option < 14) {
            img.alt = '中午好'
        } else if (option < 17) {
            img.alt = '下午好';
        } else {
            img.alt = '晚上好';
        }
    </script>
```



#### 表单元素的属性操作

```
input.value='通过value来修改表单元素的值'
//如果想某个表单元素被禁用,不能再点击 disabled 可以使用这个属性来使得按钮禁用
btn.disable=true
或者
this.disable=true
//this指向的是事件函数的调用者 btn
```

#### 案例(京东显示密码)

```html
<style>
    .box {
        position: relative;
        width: 200px;
        border-bottom: 1px solid #ccc;
        margin: 100px auto;
    }

    .box input {
        width: 170px;
        height: 20px;
        border: 0;
        outline: none;
    }

    .box img {
        position: absolute;
        width: 20px;
        top: 3px;
        right: 5px;
    }
</style>

<body>
    <div class="box">
        <label for="">
            <img src="image/close.jpg" id="eye">
        </label>
        <form action="">
            <input type="password" id="password">
        </form>
    </div>

    <script>
        var eye = document.getElementById('eye');
        var pwd = document.getElementById('password');
        var flag = 0;//使用flag进行重复点击
        eye.onclick = function () {
            if (flag == 0) {
                pwd.type = 'text';
                eye.src = 'image/open.jpeg'
                flag = 1;
            } else {
                pwd.type = 'password';
                eye.src = 'image/close.jpg';
                flag = 0;
            }
        }
    </script>
```

#### 用js修改样式

```js
element.style 行内样式操作
element.className 类名样式操作
```

````js
<style>
    .box {
        background-color: pink;
    }
</style>

<body>
    <div class="box" id="box_2">nihao</div>
    <script>
        var box = document.getElementById('box_2');
        box.onclick = function () {
            this.style.backgroundColor = 'red'
        }
    </script>
````

element.className的用法

````js
<style>
    .box {
        background-color: pink;
    }

    .box_2 {
        background-color: red;
    }
</style>

<body>
    <div class="box" >nihao</div>
    <div class="box_2">nihao</div>
    <script>
        var box = document.querySelector('.box');
        box.onclick = function () {
            this.className = 'box_2';
        }
    </script>
````

#### 淘宝二维码隐藏

只要加上一句 box.style.diplay=none

就能直接让它不显示

#### 精灵图显示案例

```js
<style>
    * {
        list-style: none;
    }

    .box {
        width: 250px;
        height: 220px;
        margin: 100px auto;
        background-color: #ccc;
    }

    .box li {
        float: left;
        width: 24px;
        height: 24px;
        margin: 15px;
        background-color: white;
        background: url(image/精灵图.png) no-repeat;
    }
</style>

<body>
    <div class="box">
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
    <script>
        var lis = document.querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            index = i * 44;
            lis[i].style.backgroundPosition = '0 -' + index + 'px';
        }
    </script>
```

#### 案例(隐藏显示文字)

````js
<style>
    input {
        color: #ccc;
    }
</style>

<body>
    <input type="text" value="请输入搜索内容">

    <script>
        var text = document.querySelector('input');
        text.onfocus = function () {
            if (this.value == '请输入搜索内容') {
                this.value = '';
            }
            this.style.color = 'black';
        }

        text.onblur = function () {
            if (this.value == '') {
                this.value = '请输入搜索内容';
                this.style.color = '#ccc';
            }
        }
    </script>
````

#### 使用className修改样式

* 这个className相当于封装样式,你想要同时修改多个类,可以用这个样式进行统一修改

* 如果你想保留原来的类名,那就使用多类名选择器

  ```
  element.className='原先的类名 你封装的类名';
  ```

#### 案例(关闭广告和新浪下拉菜单)

  ```js
<style>
    * {
        list-style: none;
    }

    .ad {
        width: 100px;
        height: 100px;
        margin: 100px auto;
        background-color: purple;
    }

    .big_box {
        width: 100px;
        height: 100px;
        margin: 100px auto;
        background-color: pink;
    }
</style>

<body>
    <div class="ad">这是一个广告</div>
    <div class="big_box">
        <div class="littleBox">
            <a href="#">球球你 快出来</a>
        </div>
        <div class="littleBox2" style="display: none;">
            <ul>
                <li><a href="">22</a></li>
                <li><a href="">11</a></li>
            </ul>
        </div>
    </div>
    <script>
        var close = document.querySelector('.ad');
        close.onclick = function () {
            this.style.display = 'none';
        }
        var text = document.querySelector('.big_box');
        var hide = document.querySelector('.littleBox2');
        text.onmouseover = function () {
            this.style.backgroundColor = 'orange';
            hide.style.display = 'block';
        }
        text.onmouseout = function () {
            hide.style.display = 'none';
        }
    </script>
  ```

#### 排他思想

> 首先排除其他人,然后才设置自己的样式,这种排除他人思想的我们称为排他思想

```js
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>

    <script>
        var bt = document.getElementsByTagName('button');
        for (var i = 0; i < bt.length; i++) {
            bt[i].onclick = function () {
                // 先将其他人干掉,每次循环,把所有颜色先设置为空
                for (var i = 0; i < bt.length; i++) {
                    bt[i].style.backgroundColor = '';
                }
                // 最后只留下自己,进行颜色变换
                this.style.backgroundColor = 'red';
            }
        }
    </script>
```

* 用var 声明的局域变量不能进入function函数中,得需要块状局部变量let才行

#### 表格经过换色案例

```
<style>
    table {
        border-spacing: 0px;
    }

    td {
        border: 1px solid black;
    }
</style>

<body>
    <table>
        <thead>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
        </tbody>
    </table>
    <script>
        var tb = document.getElementsByTagName('tr');
        for (var i = 0; i < tb.length; i++) {
            tb[i].onmouseover = function () {
                this.style.backgroundColor = 'orange';
            }
            tb[i].onmouseout = function () {
                this.style.backgroundColor = '';
            }
        }

    </script>
</body>
```

* 如果js函数名调用对的话,颜色应该是和你的标签一样的颜色

#### 全选反选案例

```js
<style>
    * {
        padding: 0;
        margin: 0;
    }

    .w {
        width: 300px;
        margin: 100px auto;
    }

    table {
        border-collapse: collapse;
        border-spacing: 0;
        border: 1px solid #c0c0c0;
        width: 300px;
    }

    th,
    td {
        border: 1px solid #d0d0d0;
        color: #404060;
        padding: 10px;
    }

    th {
        background-color: #09c;
        font: bold 16px "微软雅黑";
        color: #fff;
    }

    td {
        font: 14px "微软雅黑";
    }

    tbody tr:hover {
        cursor: pointer;
        background-color: #fafafa;
    }
</style>

<body>
    <div class="w">
        <table>
            <thead>
                <tr>
                    <th>
                        <input type="checkbox" id="j_cbAll">
                    </th>
                    <th>商品</th>
                    <th>价钱</th>
                </tr>
            </thead>
            <tbody id="j_tb">
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPad Pro</td>
                    <td>5000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPad Air</td>
                    <td>2000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>Apple Watch</td>
                    <td>2000</td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        var j_cbAll = document.getElementById('j_cbAll');
        var j_tb = document.getElementById('j_tb').getElementsByTagName('input');
        /*当点击全选按钮时,给单选按钮一个循环来给他们注册点击事件,再把全选按钮的checked属性赋值给单选按钮,这样就能实现
         全选时,所有单选按钮都选上*/
        j_cbAll.onclick = function () {
            for (var i = 0; i < j_tb.length; i++) {
                j_tb[i].checked = this.checked;
            }
        }

        /*同理 当点击单选按钮时,在函数中给一个计数器,如果计数器的值等于单选按钮的所有数量,那么就可以使的全选按钮选上
        否则就取消掉*/
        for (var i = 0; i < j_tb.length; i++) {
            var count = 0;
            j_tb[i].onclick = function () {
                if (this.checked)
                    count++;
                else
                    count--;
                if (count == j_tb.length)
                    j_cbAll.checked = true;
                else
                    j_cbAll.checked = false;
            }
        }
    </script>
</body>
```

#### 自定义属性操作

* element.属性  获取属性值

  他是获取内置属性值

* element.getAttribute('属性');

  主要获得自定义属性(标准),程序员自定的属性

* 赋值是

  element.属性='值'

  element.className

  但是用setAttribute是class而不是className

  element.setAttribute('属性','值');

* 移除属性

  element.removeAttribute();

#### tab栏切换案例

````js
<style>
    * {
        padding: 0px;
        margin: 0px;
    }

    .clearfix:after {
        content: "";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden
    }

    .tab {
        width: 800px;
        margin: 100px auto;
    }

    .tab-list {
        text-align: center;
    }

    .tab-list li {
        float: left;
        list-style: none;
        width: 20%;
        height: 45px;
        padding: 0px 30px;
        line-height: 45px;
        box-sizing: border-box;
        background-color: pink;
    }
</style>

<body>
    <div class="tab">
        <div class="tab-list clearfix">
            <ul>
                <li>动漫</li>
                <li>影视</li>
                <li>游戏</li>
                <li>饮食</li>
                <li>看书</li>
            </ul>
            <div class="tab-text">
                <div style="display: none;">1</div>
                <div style="display: none;">2</div>
                <div style="display: none;">3</div>
                <div style="display: none;">4</div>
                <div style="display: none;">5</div>
            </div>

        </div>

        <script>
            var tablist = document.getElementsByClassName('tab-list');
            var lis = tablist[0].getElementsByTagName('li');
            var tabtext = document.getElementsByClassName('tab-text');
            var text = tabtext[0].getElementsByTagName('div');
            //给我们的li加上编号,让我们知道点击的时候,是点击了哪个
            for (var i = 0; i < lis.length; i++) {
                lis[i].setAttribute('index', i);
            }
            //下面两个排他思想,不再赘述
            for (let i = 0; i < lis.length; i++) {
                lis[i].onclick = function () {
                    for (var j = 0; j < lis.length; j++) {
                        lis[j].style.backgroundColor = '';
                    }
                    this.style.backgroundColor = 'red';

                    //这里就是让index获取当前我们点击的是哪个
                    var index = lis[i].getAttribute('index');
                    for (var j = 0; j < text.length; j++) {
                        text[j].style.display = 'none';
                    }
                    //下面就用index来确定该显示哪一个
                    //因为不是这个函数的调用者,所以不用this
                    text[index].style.display = 'block';
                }
            }


        </script>
````

* DOM获取元素时,Element+s的话,返回的就是一个数组,写法就想我上面一样
* 获取元素返回的伪数组,里面存储的是标签名.

#### 自定义属性

* 自定义属性目的:是为了保存并使用数据,有些数据可以保存到页面而不用保存到数据库内

* 自定义属性:前面一定有**data-**开头作为属性名并且赋值

* H5新增的 获取自定义属性的方法

  * element.dataset.index 或者 element.dataset['index'],ie11才开始支持
  
* 如果有多个短横线,获取它的值的时候用驼峰命名法
### 节点操作

> 引言:为什么要写学节点操作
>
> 1. 利用DOM提供的方法获取元素
>    * document.getElementByID().......
>    * 他们的逻辑性不是很强,用起来比较繁琐
> 2. 利用节点层级关系获取元素
>    * 利用父子兄节点关系获取元素
>    * 逻辑性强,但是兼容性稍差
> 3. 后面两种方法都会使用,但是节点操作会更简单

#### 节点层级

1. 父子兄层级关系

   ```
   node.parentNode
   ```

2. 子节点

   ```
   parentNode.childNode
   包含所有文本节点,包含元素节点,文本节点
   不太推荐使用
   ```

   ```
   推荐使用
   children,能获取所有子节点中的所有元素节点
   ```

   * firstChild和lastChild,能获取第一个和最后一个节点,但是文本节点也会获取到,所以不推荐使用
   * firstElementChild能获取到第一个元素节点,但是兼容性有问题
   * 所以实际开发中,我们就用children来获取,通过数组索引的方式来写

#### 新浪下拉菜单案例

```js
<style>
    .clearfix:after {
        content: "";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden
    }

    * {
        margin: 0px;
        padding: 0px;
        list-style: none;
    }

    .nav {
        width: 400px;
        margin: 100px auto;
    }

    .nav li {
        position: relative;
        top: 0px;
        float: left;
    }

    .nav li ul li,
    .nav li {
        text-align: center;
        width: 100px;
        height: 41px;
    }

    .nav li a {
        display: block;
        box-sizing: border-box;
        padding: 10px 0px;
    }

    .nav li a:hover {
        background-color: #ccc;
    }

    .nav li ul {
        display: none;
        position: absolute;
        top: 45px;
    }

    .nav li ul li {
        background-color: #e4e4e4;
        border: 1px solid #ccc;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
</style>

<body>
    <ul class="nav ">
        <li>
            <a href="">游戏</a>
            <ul>
                <li>Baldr Sky</li>
                <li>恋爱奇谭~不存在的夏天</li>
                <li>徒花异谭</li>
            </ul>
        </li>
        <li>
            <a href="">动漫</a>
            <ul>
                <li>命运石之门</li>
                <li>ViVy</li>
                <li>MaGalBox</li>
            </ul>
        </li>
        <li>
            <a href="">美食</a>
            <ul>
                <li>鱼香肉丝</li>
                <li>红烧猪蹄</li>
                <li>可乐鸡翅</li>
            </ul>
        </li>
        <li>
            <a href="">书籍</a>
            <ul>
                <li>小妇人</li>
                <li>三体</li>
                <li>我亲爱的甜橙树</li>
            </ul>
        </li>
    </ul>

    <script>
        var nav = document.querySelector('.nav');
        var lis = nav.children;
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function () {
                this.children[1].style.display = 'block';
            }
            lis[i].onmouseout = function () {
                this.children[1].style.display = 'none';
            }
        }
    </script>
</body>
```

* 这种开发用的是ul里面嵌套a和ul的写法,较为方便
* 使用children,选择起来较为方便

#### 兄弟节点

* nextSibling
* previousSibling
* nextElementSibling
* previousElementSibling
* 后面两个都是有兼容问题的

#### 创建节点

> createElement　

#### 添加节点

> appendChild  追加元素
>
> insertBefore(指定元素,child) 

#### 删除节点

> removeChild(child);

* 如果使用删除节点全部完毕,可以接个小小的判断,使用disable这个属性为true,使得这个按钮禁用

#### 删除案例

```js
    <script>
        var text = document.querySelector('.text');
        var button = document.querySelector('.button');
        var ul = document.querySelector('ul');
        button.onclick = function () {
            var li = document.createElement('li');
            // 在取li的值的时候,直接在value后面加上一个删除的链接
            li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";
            ul.insertBefore(li, ul.children[0]);
            var a = document.querySelectorAll('a');
            for (var i = 0; i < a.length; i++) {
                a[i].onclick = function () {
                    ul.removeChild(this.parentNode);
                }
            }
        }
    </script>
```

> 解释:为什么不在把获取链接a的那一段函数放到外面?
>
> 因为我把它放在外面后,js会进行解析,那么在我还没有点击发布留言按钮时,他所获取到的a的数量就是0,并不会随着我们逐渐添加,而发生改变,所以需要把它放在里面来进行给链接点击事件.

#### 复制节点

> cloneNode()

```
ul.children[0].cloneNode();`
```

* 如果括号参数为空或者false,则是浅拷贝,即只复制克隆节点本身,不克隆里面的的子节点.
* 如果括号参数为true,则是深度拷贝,会复制节点本身以及里面的所有子节点

#### 动态生成表格案例

```js
<style>
    table {
        width: 400px;
        margin: 100px auto;
        text-align: center;
        border-spacing: 0px;
        border-collapse: collapse;
    }

    table,
    th,
    td {
        border: 1px solid #ccc;
    }
</style>

<body>
    <table>
        <thead>
            <tr>
                <th>姓名</th>
                <th>学科</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <script>
        var datas = [
            {
                name: '曹志贤',
                subject: 'javaScript',
                score: '100'
            },
            {
                name: '朱冬宇',
                subject: 'javaScript',
                score: '90'
            },
            {
                name: '郑仕文',
                subject: 'javaScript',
                score: '90'
            }, {
                name: '陈志朋',
                subject: 'javaScript',
                score: '90'
            }
        ]
        var tbody = document.querySelector('tbody');
        for (var i = 0; i < datas.length; i++) {
            // 添加行
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            // 添加单元格
            for (k in datas[i]) {
                var td = document.createElement('td');
                // 往单元格中添加数据
                td.innerHTML = datas[i][k];
                tr.appendChild(td);
            }
            // 创建删除单元格
            var dtr = document.createElement('td');
            dtr.innerHTML = '<a href="javascript:;" class="deletion">删除</a>';
            tr.appendChild(dtr);
        }
        // 不把这个删除放在循环里面,可以节省内存空间
        // 省的每循环一次就要创建一次删除事件
        var deletion = document.querySelectorAll('.deletion');
        for (var i = 0; i < deletion.length; i++) {
            deletion[i].onclick = function () {
                tbody.removeChild(this.parentNode.parentNode);
            }
        }
    </script>
</body>
```

####　三种动态创建元素的区别

1. doucument.write

   > 他有一个显著的特点,如果页面文档流加载完毕,再调用write语句的话,就会导致页面重绘,之前的页面消失,会创建出一个新的页面,
   >
   > 文档流加载完毕:就是html所有的语句都执行完毕

2. element.innerHTML

3. document.createElement()

* innerHTML和createElement效率对比

  createElement创建多个元素效率稍微低一点,但是结构更加清晰

  innerHTML创建多个元素效率更高,不需要采取拼接字符串,采取数组形式拼接,结构稍复杂.

  > 使用数组的形式
  >
  > ```
  > 先arr.push();
  > 再element.innerHTML=arr.join('');
  > join是先将数组转换为字符串,再把字符串赋值给innerHTML
  > ```

### DOM重点核心

* 主要是针对元素的操作,创建,增删查改,属性操作,事件操作

创建:三种创建方式

增加:两种增加方式,appendChild,insertBefore

删除:removeChild

查询:方法比较多,推荐使用H5新增的方法,利用节点操作获取元素

改:主要修改元素的属性

事件操作:给事件添加一些功能

### 事件的高级技巧

#### 注册事件

> 给元素添加事件,称为注册事件或者绑定事件
>
> 注册事件有两种方式,传统方式和方法监听注册方式

**传统注册方式**

1. 利用on开头的事件
2. 注册事件的唯一性
3. 同一个元素同一个事件只能设置一个处理函数,最后注册的处理函数将会覆盖前面注册的处理函数

**方法监听注册事件**

1. W3C标准推荐方式
2. addEventListener()它是一个方法
3. IE9之前并不支持
4. 同一个元素同一个事件可以注册多个监听器
5. 按注册顺序依次执行

该方法接受三个参数

* type:事件类型字符串,比如click,mouseover,注意这里不用带on
* listener:事件处理函数,事件发生时,会调用该监听函数
* useCapture:可选参数,是一个布尔值,默认false.

#### 删除事件

传统的:

eventTarget.onclick=null

方法监听注册方式:

eventTarget.removeEventListener(参数和注册一样)

#### DOM的事件流

> 事件流描述的是从页面中接收事件的顺序.
>
> 事件发生时会在节点之间按照特定的顺序传播,这个传播过程即DOM事件流
>
> eg:我们给一个div注册了点击事件
>
> DOM事件流分为三个阶段
>
> 1. 捕获阶段
> 2. 当前目标阶段
> 3. 冒泡阶段

````js
<style>
    .father {
        width: 200px;
        height: 200px;
        margin: 100px auto;
        background-color: black;
    }

    .son {
        position: relative;
        top: 25%;
        left: 25%;
        width: 100px;
        height: 100px;
        background-color: white;
    }
</style>

<body>
    <div class="father">
        <div class="son">son</div>
    </div>

    <script>
        var father = document.querySelector('.father');
        var son = document.querySelector('.son');
        // 事件捕获阶段,如果useCapture为true则会捕获阶段,顺序为
        // Document->father->son,Document是HTML的根节点
        // 冒泡阶段,则和现在反着来
        father.addEventListener('click', function () {
            alert('捕获 我是父亲 我先弹出');
        }, true);
        son.addEventListener('click', function () {
            alert('捕获 我是儿子 我后弹出');
        }, true);
        document.addEventListener('click', function () {
            alert('捕获 我是Document 我最先弹出');
        }, true);
    </script>
</body>
````

* JS代码中只能执行捕获或冒泡的其中一个阶段
* onclick和attachEvent只能得到冒泡阶段
* useCapture中true表示执行捕获阶段,反之则是冒泡阶段
* 实际开发中,使用的更多是冒泡阶段
* 有些事件是没有冒泡的,比如onblur,onfocus,onmouseenter,onmouseleave

#### 事件对象

> 在function()的小括号里面加上event,这个Event就是事件对象
>
> 官方:event对象代表事件的状态,比如键盘按键的状态,鼠标的位置,鼠标按钮的状态
>
> 简单一点说:事件发生后, 和事件相关的一系列信息数据的集合都放在这个对象里面,这个对象就是事件对象event,他有很多属性和方法
>
> event是个形参,可以直接拿来使用

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210501090949337.png)

#### 阻止事件冒泡

* 标准写法

  > e.stopPropagation

* 兼容性写法

  > window.event.cancelBubble=true
  >
  > e.cancelBubble=true

#### 事件委托(代理委派)

==事件委托的原理==

**不是每个子节点单独设置事件监听器,而是事件监听器设置在其父节点上,然后利用冒泡原理影响设置每个子节点**

案例:给ul注册点击事件,然后利用事件对象的target来找到当前点击的li,因为点击li,事件会冒泡到ul上,ul有注册事件,就会触发事件监听器

事件委托的作用,我们只操纵了一次DOM,提高了程序的性能

#### 常用的鼠标事件

1. 禁止鼠标右键菜单

   contextmenu主要控制何时显示上下文菜单,主要用于程序员用于取消默认的上下文菜单

   ```
   docunment.addEventListener('contextmenu',function(e){
   e.preventDefault();
   })
   ```

2. 禁止选中文字
   selectstart

#### 鼠标事件对象

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210501093609222.png)

#### 案例(跟随鼠标的图片)

```js
<style>
    img {
        position: absolute;
    }
</style>

<body>
    <img src="image/open.jpeg" alt="">
    <script>
        var image = document.querySelector('img');
        document.addEventListener('mousemove', function (e) {
            var x = e.pageX;
            var y = e.pageY;
            console.log(x);
            console.log(y);
            image.style.left = x + 'px';
            image.style.top = y + 'px';
        })
    </script>
```

记得给图片位置加上px单位

#### 常用键盘事件

事件除了使用鼠标触发,还可以使用键盘触发

**image-20210501100249655**

* 使用addEventListener不需要加on
* 三个事件的执行顺序为:keydown->keypress->keyup

#### 键盘事件对象

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210501101207740.png)

#### 案例(京东放大和搜索)

```js
<style>
    * {
        margin: 0px;
        padding: 0px;
    }

    .clearfix:after {
        content: "";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden
    }

    .search {
        position: relative;
        top: 0px;
        width: 300px;
        margin: 100px auto;
    }

    .amplify {
        display: none;
        position: absolute;
        bottom: 25px;
        width: 250px;
        height: 30px;
        /* 让透明三角显示的关键是在于下面的盒子阴影 */
        /* 有了盒子阴影，三角能显示出来，并且非常美观 */
        /* 具体的运行代码查看 */
        box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
        border: 1px solid #ccc;
    }

    /* 利用为元素生成小三角 */
    .amplify::before {
        content: '';
        width: 0;
        height: 0;
        position: absolute;
        top: 30px;
        left: 20px;
        border: 8px solid #000;
        border-style: solid;
        /* 只给上边框颜色,其余的颜色都为透明色 */
        border-color: #fff transparent transparent;

    }

    .text,
    .button {
        float: left;
        width: 250px;
        height: 15px;
        border: 0px;
        outline: none;
    }

    .text {
        background-color: #ccc;
    }

    .button {
        font-size: 10px;
        float: left;
        width: 50px;
        height: 15px;
        background-color: #e4e4e4;
    }
</style>

<body>

    <div class="search clearfix">
        <div class="amplify">123</div>
        <input type="text" class="text">
        <button class="button">搜索</button>
    </div>

    <script>
        var ay = document.querySelector('.amplify');
        var search = document.querySelector(".search");
        var text = document.querySelector('.text');
        var button = document.querySelector('.button');
        document.addEventListener('keyup', function (e) {
            if (e.keyCode === 83) {
                // 使用js里面的获取焦点的方法
                text.focus();
            }
        })
        text.addEventListener('keyup', function (e) {
            if (text.value != '') {
                ay.innerHTML = text.value;
                ay.style.display = 'block';
            } else {
                ay.style.display = 'none';
            }
        });

        text.addEventListener('blur', function () {
            ay.style.display = 'none';
        })
        text.addEventListener('focus', function () {
            if (this.value == '')
                ay.style.display = 'none';
            else
                ay.style.display = 'block';
        })
    </script>
</body>
```

* 具体情况请运行查看

## BOM(浏览器对象模型)

### 介绍

> 他提供了独立于内容而与浏览器窗口进行交互的对象,其核心对象是Window
>
> BOM是一系列相关的对象构成,并且每个对象都提供了很多方法和属性
>
> BOM缺乏标准,JS语法的标准化是ECMA,DOM的标准化W3C,BOM最初是Netscape浏览器标准的一部分

### 构成

1. window对象是浏览器的顶级对象,它具有双重角色

   > 1. 他是JS访问浏览器窗口的一个接口
   > 2. 他是一个全局对象,定义在全局作用域中的变量,函数都会变成window对象的属性和方法,在调用的时候可以省略window,前面学习的对话框都属于window对象方法,如alert,prompt
   > 3. 在声明变量中,不要用name,是window一个属性

### 常用window事件

1. 窗口加载事件

   > window.onload(传统)//只能用一次
   >
   > window.addEventListener("load",function(){});//可以无限用
   >
   > 有了这个之后,可以放到任何位置

   > DOMContentLoaded事件触发时,仅当DOM加载完成后,不包括样式表,图片,flash等
   >
   > 如果页面图片比较多,使用这个属性会更好,用户体验会更好

2. 调整窗口大小事件

   > resize
   >
   > 只要窗口大小发生像素变化,就会触发这个事件
   >
   > 我们经常利用这个事件完成响应式布局.
   >
   > window.innerWidth当前屏幕的宽度
#### 定时器

   > 1. setTimeout()
   > 2. setInterval()

##### setTimeout()定时器

   > window.setTimeout(调用函数,[延迟的毫秒数]);
   >
   > 用于设置一个定时器,该定时器在定时器到期后执行调用函数
   >
   > 1. 这个函数可以直接写函数,或者写函数名或者采取字符串'函数名()'三种形式,第三种不推荐
   >
   > 2. 延迟的毫秒数省略默认是0,如果写,必须是毫秒
   >
   > 3. 因为定时器可能有很多,所以我们经常给定时器赋值一个表示符
   > 4. 这个函数我们也称为==回调函数==

##### 停止定时器

> window.clearTimeout(timeoutID)
>
> 这个方法取消了先前通过调用setTimeout()建立的定时器

##### setInterVal定时器

> 他和setTimeout不同的是,每隔这个延时时间,就去调用这个回调函数,会调用很多次,重复调用这个函数  
>
> 写了几个案例,在vscode里看

#### this

1. 一般情况下this的最终指向的是那个调用它的对象
2. 全局作用域或者普通函数中this指向全局对象window(注意 定时器里面的this指向window)
3. 方法调用谁,this指向谁
4. 构造函数中this指向函数的实例
5. 看看箭头函数的指向

#### JS执行队列

* JS是单线程

##### 同步和异步

###### 同步任务

> 同步任务都在主线程上执行,形成一个执行栈

###### 异步任务

> JS的异步是通过回调函数实现的
>
> 一般而言,异步任务有以下三种类型
>
> 1. 普通事件,如click,resize等
> 2. 资源加载,如load,error
> 3. 定时器,包括setInterval,setTimeout等

##### 执行机制

1. 先完成执行栈中的同步任务
2. 异步任务(回调函数)放入任务队列中
3. 一旦执行栈中的同步任务结束,系统就会按次序读取任务队列中的异步任务,于是被读取的异步任务结束等待状态,进入执行栈,开始执行

> 异步进程处理
>
> 只有回调函数使用过后,才会进入到异步任务队列中

* 由于主线程不断地重复获得任务,执行任务,再获取任务,在执行,所以这种机制被称为**事件循环**

#### location对象

> window对象给我们提供了一个location属性用于获取或设置窗体的url,并且可以用于解析url.因为这个属性返回的是一个对象,所以我们将这个属性也称为location对象

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210502081304208.png)

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210502081128055.png)

==重点记住:href和search==

* location对象的方法
  * assign:和href一样,可以跳转页面
  * replace:替换当前页面,因为不记录历史,不能后退页面
  * reload:重新加载页面,相当于刷新按钮或者f5,如果参数为true,强制刷新crtl+f5

#### navigator对象

> 它包含有关浏览器的信息,他有很多属性,我们最常用的是userAgent,该属性可以返回由客户机发送服务器的user-agent头部的值

#### history对象

* forward:前进
* back:后退
* go:参数为1前进一个页面,-1后退一个页面

## PC端网页特效

### 元素偏移offset系列

> 可以使用相关属性可以动态的得到该元素的位置,大小等
>
> * 获得元素距离带有==定位父元素==的位置
> * 获得元素自身的大小
> * ==注意==:返回的数值都不带单位

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210502092435846.png)

* parentNode也是返回父亲,但是他是返回最近一级的父亲,不管有没有定位 

![image-20210502093248087](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210502093248087.png)

#### 案例

* 动态获取盒子鼠标坐标
* 拖动的模态框
* 京东的放大镜

### 元素可视区client系列

> client翻译过来就是客户端,我们使用client系列的相关属性来获取元素可视区的相关信息,通过client系列的相关属性可以动态的得到该元素的边框大小,元素大小等.

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210503094142482.png)

### 淘宝flexible.js源码分析

* 立即执行函数(function(){})()

  主要作用:创建一个独立的作用域

  写法:**(function(){})()**或者**(function(){}())**

  也可以传递参数进来,多个立即函数要用分号隔开

  里面所有变量都是局部变量,不会有命名冲突问题

*  dpr物理像素比

* pageshow:重新加载页面,与load不一样的是,缓冲取过来的页面load无法重新加载,而pageshow可以加载,e.persisted返回的是true,就是说如果这个页面是从缓存取过来的页面,需要重新计算一下rem的大小

### Scroll系列

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210504053907944.png)

* 元素被卷去的头部是element.scrollTop
* 页面被卷去的头部则是window.pageYoffset

![](https://gitee.com/IU_czx/images/raw/master/img/image-20210504055316343.png)

### mouseenter鼠标事件

* 当鼠标移动到元素上就会触发mouseenter事件
* 类似于mouseover,他们之间显著的区别是,mouseover经过自身盒子会触发,经过子盒子也会触发,而mouseenter只会经过自身盒子触发
* 他不会冒泡
* mouseleave:鼠标离开

### 动画实现

> 原理:通过定时器setInterval()不断移动盒子
>
> 步骤:
>
> 1. 获得当前盒子的位置
> 2. 让盒子在当前位置加上一个移动距离
> 3. 利用定时器不断重复这个操作
> 4. 加一个结束定时器的条件
> 5. 注意此元素需要添加定位,才能使用left

* 简单的函数封装

  ![](https://gitee.com/IU_czx/images/raw/master/img/image-20210504081208751.png)

  这个就是封装函数,只需要传递参数,就能够使用了

#### 给不同元素指定不同定时器

* 在函数封装中,我们传递一个对象进去,我们只需要给这个对象添加一个定时器的属性即可

  ```
  obj.timer=function(){}
  ```

  这样可以避免反复开辟timer内存空间,提高运行速度

#### 缓动效果原理

> 思路:让盒子每次移动的距离变小
>
> 核心算法: (目标值-现在的位置)/10,作为每次移动的距离.
>
> 正数向大的取整,负数向小的取整

#### 动画的回调函数

* 在封装的动画函数内,添加一个callback回调函数类型,通过传递属性进去,这样子可以在动画结束后,执行函数

#### 调用动画函数案例

* 看我vscode,里面做了详解

#### 节流阀

> 防止轮播图按钮连续点击造成播放过快
>
> 节流阀的目的:当上一个函数动画内容执行完毕,再去执行下一个函数动画,让事件无法连续触发
>
> 核心思路:利用回调函数,添加一个变量来控制,锁住函数和解锁函数

> 开始设置一个变量var flag=true;
>
> if(flag){flag=false; do something}关闭水龙头
>
> 利用回调函数 动画执行完毕,flag=true,打开水龙头