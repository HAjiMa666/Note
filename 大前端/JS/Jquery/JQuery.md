# JQuery入门

* 先从官网下载jquery的js包

* JQuery的入口函数

  ```js
         // //这是第一种加载方式
          $(document).ready(function () {
              $('div').hide();
          })
          // 这是第二种加载方式
          $(function () {
              $('div').hide();
          })
  ```

  相当于原生js的DOMContentLoaded,不是load事件

* $相当于js中的window对象

* $(' ')和document获取的对象是不一样的`$`获取的是JQuery对象,documnet获取的是DOM对象

* JQuery对象转化成DOM对象,只需要$()[]或`$`(索引号).get(索引号),就能进行转换 

# JQuery选择器

![image-20210519123006147](https://gitee.com/IU_czx/images/raw/master/img/image-20210519123006147.png)

* ```js
  $("div").css("background","pink");
  ```

> 在上面这句代码中,首先选中了代码中的所有div的盒子,然后统一给他们附了样式,这边不需要我们和原来js一样需要用循环给选取到的元素赋值相应的样式,JQuery统一帮我们做了,这是==隐式迭代==

![image-20210519124245646](https://gitee.com/IU_czx/images/raw/master/img/image-20210519124245646.png)

![image-20210519124921856](https://gitee.com/IU_czx/images/raw/master/img/image-20210519124921856.png)

* 重点记住:parent() children() find() siblings() eq()

# JQuery的排他思想

第一个案例:Button的排他思想

```js
    <script>
        // 1.第一步隐式迭代,给所有的button都加上了点击事件
        $(function () {
            $("button").click(function () {
                // 2.当前的元素变化背景颜色
                $(this).css("background", "red");
                // 3.其余的兄弟去掉背景颜色
                $(this).siblings("button").css("background", "");
            })
        })
    </script>
```

第二个案例:淘宝服饰精品

```js
    <script>
        $(function () {
            // 鼠标经过左侧的li
            $("ul li").mouseover(function () {
                // 2.得到li的索引号
                var index = $(this).index();
                console.log(index);
                $(".image img").eq(index).show();
                $(".image img").eq(index).siblings().hide();
            });

        })
    </script>
```

# JQuery链式编程

```js
        $(this).css("background", "red");
        $(this).siblings("button").css("background", "");
		等价于
		$(this).css("background", "red").sibilings("button").css("background","");
```

# JQuery样式操作

```js
//第一种操作
$().css("你需要修改的样式属性","修改的值");
//第二种操作,可以以传递对象方法去修改CSS样式
$().css({
    width: 400,
    height: 400,
    backgrounColor:"color"
})
```

```js
    <script>
        $(function () {
            // 第二种修改样式的方法
            // $("div").css({
            //     width: "200px",
            //     height: "300px",
            //     backgroundColor: "red"
            // })

            // 通过添加类的方法来修饰样式,这种也较为常用
            $("div").addClass("current");
            // 删除类
            // $("div").removeClass("current");
            // 切换类
            $("div").click(function () {
                $("div").toggleClass("rotate");
            })
        })
    </script>
```

==注意==:

* 原生JS中className会覆盖元素原先里面的类名.
* jQuery里面类操作只是对指定类进行操作,不影响原先的类名,只是在之前的类名后面在追加了一个类名

# JQuery效果

![image-20210519195614993](https://gitee.com/IU_czx/images/raw/master/img/image-20210519195614993.png)

<h3>查JQuery手册<h3>

---

```js
     // 事件切换hover 如果只写一个函数,那么默认,鼠标经过或者离开都会执行那个函数
        $(function () {
            $(".box").hover(function () {
                $(this).children("ul").slideToggle();
            })
        })

```

<p style="font-size: 25px; color:red">
   停止JQuery动画排队效果 
</p> 

* 在动画前面加上stop(),不能在动画后面加上stop()

图片高亮显示案例:

```js
    <script>
        $(function () {
            var index = $(".box div").index();
            $(".box img").hover(function () {
                $(this).siblings().stop().fadeTo(400, .5);
            }, function () {
                $(this).siblings().stop().fadeTo(400, 1);
            })
        })
    </script>
```

<p style="font-size:25px;color:pink">JQuery动画效果</p>

> 语法
>
> animate(params.[speed],[easing],[fn])

* ==params==想要改变的样式属性,**以对象的形式传递**
* 案例:王者荣耀手风琴效果

==注意==动画效果是针对元素进行操作的,不能对整个文档进行操作

# JQuery属性操作

**获取属性**

```js
//第一种方法
element.prop("属性名")获取元素固有的属性值
后面可以跟你想要变化的值

//第二种方法 元素的自定义苏醒 通过attr()
console.log($("div").attr("index"));
console.log($("div").attr("data-index"));

//第三种方法 数据缓冲data() 这个里面的数据是存放在元素的内存里面
$("span").data("uname","andy");//设置数据
$("span").data("uname"); //获取数据
$("span").data("uname"); //这个也可以获取data开头的自定义数据,返回的是数字型的
```

案例:全选全不选

```js
    <script>
        $(function () {
            // 思路:就是把全选按钮的状态赋给剩余的小按钮即可
            // 事件用change,该事件仅适用于文本域（text field），以及 textarea 和 select 元素。
            // 当用于 select 元素时，change 事件会在选择某个选项时发生。当用于 text field 或 text area 时
            // 该事件会在元素失去焦点时发生。
            $(".total").change(function () {
                $(".total").siblings().prop("checked", $(this).prop("checked"));
            })
        
        	 $(".lbtn").change(function () {
                // 当所有的小按钮选中,全选按钮也要选中
                if ($(".lbtn:checked").length == $(".lbtn").length) {
                    console.log($(".lbtn:checked").length);
                    $(".total").prop("checked", true);
                } else {
                    $(".total").prop("checked", false);
                }
            })
        })
    </script>
```

# JQuery内容文本值

1. 普通元素内容html()

   > html():获取元素的内容
   >
   > html("内容"):设置元素的内容

2. 普通元素文本内容text() 相当于原生的innerHTML

3. 如果有许多层级的HTML元素,那么可以用parents这个属性,括号里面可以指定类名,指定要获取的那个类名

4. 最后结果如果想保留几位小数,用Tofixed(想保留的几位小数).

# JQuery元素操作

## 遍历元素

第一种遍历

```js
语法:
$("div").each(function(index,domEle){xxx;})
```

* 里面的回调函数有两个参数:index是每个元素的索引号,demEle是每个DOM元素对象,不是jQuery对象

* 所以要使用jquery方法,需要用$()进行对象转化

第二种遍历

> $.each(function(i,ele){})
>
> * 他可以遍历任何对象

## 创建元素

添加元素

* 内部添加
  * $("").append("")
  * $("").prepend("")
* 外部添加
  * element.after("内容")  :把内容放入目标元素后面
  * element.before("内容")  :把内容放入目标元素前面

删除元素

* remove:删除自身元素
* empty:删除元素内的子节点
* html(""):同empty

# JQuery尺寸测量

![image-20210521053214705](https://gitee.com/IU_czx/images/raw/master/img/image-20210521053214705.png)

![image-20210521053637331](https://gitee.com/IU_czx/images/raw/master/img/image-20210521053637331.png)

# JQuery事件

![image-20210521072909048](https://gitee.com/IU_czx/images/raw/master/img/image-20210521072909048.png)

> 用on()注册绑定事件的优势:
>
> 1. 它可以同时注册多个事件
>
>    ```js
>    $("div").on(function(){
>        click:function(){},
>        mouserenter:function(){},
>            ...
>    })
>    ```
>
>    ```js
>    //也可以为一个元素同时附上同一个事件
>    $("div").on("mouseenter mouseover",function(){})
>    ```
>
> 2. 可以使用on来进行事件委派
>
>    ```js
>    $("div").on("click","li",function(){
>        alert(11);
>    })
>    //括号中的第二个参数是选中元素的子元素,函数的作用是给li的,因为冒泡,事件全部会冒泡到div这个盒子上
>    ```
>
> 3. **可以动态创建的元素进行绑定事件**

> 用off()可以解绑on绑定的所有事件

> 用one()绑定事件 只会注册一次事件

> 自动触发事件:
>
> 1. trigger()
> 2. click()
> 3. triggerHandler():不会触发事件的默认行为

# JQuery事件对象

* 参照js的事件对象

# JQuery对象拷贝

> ```js
> $.extend(目标对象,被拷贝的对象)
> ```

![image-20210521085504481](https://gitee.com/IU_czx/images/raw/master/img/image-20210521085504481.png)

# JQuery多库共存

![image-20210521085819370](https://gitee.com/IU_czx/images/raw/master/img/image-20210521085819370.png)

# JQuery插件

![image-20210521092015418](https://gitee.com/IU_czx/images/raw/master/img/image-20210521092015418.png)

<h3>图片懒加载

当我们划到当前区域,才显示当前图片,必须在最后面引入懒加载插件

<h3>全屏滚动插件

# TODOList 案例

* 数据要先存储到本地存储里面,页面读取数据的时候,刷新页面数据也不会丢失
* 利用事件对象.keyCode判断用户按下回车键(13)
* 声明一个数组
* 先读取原来的存储的数据,放到这个数组内

```js
    // 数据存储
    var todo = [{
        title: "11111",
        done: false
    }, {
        title: "1122e",
        done: true
    }];
    // 本地存储只能存储字符串的数据格式
    // 把我们的数组对象转换为字符串格式 JSON.stringify()
    localStorage.setItem("todo", JSON.stringify(todo));
    var todo = localStorage.getItem("todo");
    // 获取本地存储的数据 我们需要把里面的字符串数据转换为对象格式 JSON.parse();
```

```js
    // 保存本地存储数据
    function saveData(data) {
        localStorage.setItem("todolist", JSON.stringify(data));
    }

    // 读取本地存储的数据
    function getData() {
        var data = localStorage.getItem("todolist");
        if (data != null) {
            // 本地存储里面的数据是字符串格式,需要进行类型转换
            return JSON.parse(data);
        } else {
            return [];
        }
    }
//后面要用存什么数据 直接调用即可
```

```js
    // 删除操作
    $("ul").on("click", "a", function () {
        // 拿到索引号
        index = $(this).attr("id");
        // 获取存取数据的数组
        var data = getData();
        // 用splice删除数组中的一个元素
        data.splice(index, 1);
        // 将data存入本地存储
        saveData(data);
        // 重新渲染数据到页面上
        load();
    })
```

```js
    // 完成和未完成的事件切换
    $(".task,.completed").on("click", ".checkBtn", function () {
        var data = getData();
        var index = $(this).siblings("a").attr("id");
        data[index].done = $(this).prop("checked");
        saveData(data);
        load();
    })
```

```js
   // 渲染页面数据
    function load() {
        var data = getData();
        console.log(data);
        // 遍历之前要清空所有的元素
        $("ul").empty();
        $.each(data, function (i, n) {
            var li = $("<li></li>");
            // 根据done的属性来判断任务应该插到正在进行中,还是已完成
            if (data[i].done) {
                // 已经完成的在input上加上一个checked属性
                li.html("<p>" + n.title + "</p>" + "<input type='checkbox' class='checkBtn'  checked='checked'>" + "<a href='javascript:;' id=" + i + ">删除</a>");
                $(".completed ul").prepend(li);
            } else {
                li.html("<p>" + n.title + "</p>" + "<input type='checkbox' class='checkBtn'>" + "<a href='javascript:;' id=" + i + ">删除</a>");
                $(".task ul").prepend(li);
            }
        });
    }
```

