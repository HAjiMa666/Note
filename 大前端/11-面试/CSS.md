# 01-圣杯布局和双飞翼布局

> 圣杯布局
>
> 头部和尾部固定,中间两列固定宽度,中间自适应的三列布局,如下所示
>
> 最重要的一点是要让中间的内容先显示出来,所以要将content的盒子放在最前面
>
> 我使用了两种方法
>
> 1. 浮动
> 2. flex
>
> 在写这个的时候,我想用sass来写这个,顺便练习一下,我遇到了一个问题
>
> 在浮动的情况下,怎么让中间的盒子自适应高度呢,我找到了CSS3中的`calc()`这个函数,这个可以对各种值进行一个转换,所以我觉得是个绝佳的解决办法
>
> ```css
> height: calc(100vh - 2*#{$height})
> ```
>
> 从上面可以看出,因为圣杯布局头部和尾部的高度是一样的,所以中间的高度就当前的视窗高度减去两个高度,就能实现高度的自适应,可以自己填满当前容器的高度

<img src="https://gitee.com/IU_czx/images/raw/master/img/%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%80.png" alt="image-20210831220139382" style="zoom:25%;" />

> 双飞翼布局和圣杯布局的不同之处:主要是为了解决中间div被遮挡的问题
>
> 圣杯布局采用的方案是
>
> 1. 中间的盒子先使用padding-left和padding-right让两边空出来放我们的两列内容
> 2. 左右两边的小盒子就是通过margin和定位来放到正确的位置
>
> 双飞翼布局是采用
>
> 1. 中间的盒子让他占满,在中间的盒子再放上一个子盒子,使用margin将两边的盒子内容空出来
>
> 2. 再让两边的盒子进行margin,移动回来
>

# 02-盒子模型

> CSS盒模型本质上是一个盒子,封装周围的HTML元素,它包括  外边距(margin),内边距(padding),边框(border),实际内容(content)四个属性

<h3>W3C盒子模型(标准盒模型)和IE盒子模型(怪异盒模型)

标准盒模型

* 我们设置的内容  宽高   就是我们盒子的宽度和高度

怪异盒模型

* 我们设置的宽度和高度等于怪异盒模型的  内容的宽高+padding+margin+border

要想要解决两者的冲突问题

>  最好就是不要对元素本身设置 内边距或者外边距
>
> 将这两个属性设置到该元素的父元素或者子元素上

<h3>CSS3指定盒子模型</h3>

1. content-box(标准盒)

   宽度和高度分别应用到元素的内容框.在宽度和高度之外绘制元素的内边距和边框

2. border-box(怪异盒)

   我们所设置的宽度和高度 包括了内容,边框,外边距,内边距

3. inhreit:从父元素继承box-sizing属性的值

# 水平居中和垂直居中的方案

先看HTML的骨架

后面的代码都是基于这个来写的

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<link rel="stylesheet" href="./style.css">

<body>
    <div class="box vertical align"></div>
</body>
</html>
```



## 水平居中

1. 通过 margin 水平居中

   ```css
   /* 1. 通过margin 水平居中 */
   .box {
       width: 200px;
       height: 200px;
       background-color: orange;
   }
   .align {
       margin: 0 auto;
   }
   ```

2. 通过 position 和 transform 水平居中

   ```css
   /* 2.通过 position 和 transform 水平居中 */
   .box {
       width: 200px;
       height: 200px;
       background-color: orange;
   }
   .align {
       position: relative;
       left: 50%;
       transform: translateX(-50%);
   }
   ```

3. 通过flex水平居中

   ```css
   body {
       display: flex;
       justify-content: center;
   }
   ```

4. 通过 text-align:center 水平居中

   注意:使用text-align的时候,子元素要设置为行内块元素,是利用了行内元素的特性

   ```css
   body {
       text-align: center;
   }
   .box {
       display: inline-block;
       width: 200px;
       height: 200px;
       background-color: orange;
   }
   ```

## 垂直居中

1. flex布局垂直居中

   可以在父类上加 align-item:center实现垂直居中

   ```css
   body {
       height: 100vh;
       display: flex;
       align-items: center;
   }
   ```

   也可以在子类元素上加 align-self:center 实现垂直居中

   ````css
   .box {
       align-self: center;
       width: 200px;
       height: 200px;
       background-color: orange;
   }
   ````

2. 通过position和transform 来垂直居中

   ```css
   /* 第二种方案 position和transform */
   .vertical{
       position: relative;
       top: 50%;
       transform: translateY(-50%);
   }
   ```

## 绝对居中

1. flex布局实现绝对居中

   ```css
   body {
       height: 100vh;
       display: flex;
       align-items: center;
       justify-content: center;
   }
   ```

2. 通过 position和transform 实现绝对居中

   ```css
   
   /* 第二种方案 position和transform */
   .box {
       position: relative;
       top: 50%;
       left: 50%;
       transform: translate(-50%, -50%);
   }
   ```

   
