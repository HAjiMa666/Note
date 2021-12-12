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