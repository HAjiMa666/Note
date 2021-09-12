# 定位

==定位=定位模式+边偏移==

## static(静态定位)

* 了解就行

* grammar:

  ````html
  选择器{position:static;}
  ````

## relative(相对定位)

- 相对定位是元素在移动位置的时候,是相对于它原来的位置来说的

- ```css
  选择器{ position:relative; }
  ```

* 特点:
  * 他是相对于自己原来的位置来移动的(==移动位置参照点是自己原来的位置==)
  * 原来在标准流的位置继续占有,后面的盒子仍然以标准流的方式对待它(==不脱标,继续保留原来的位置==)

## absolute(绝对定位)

> 绝对定位是元素在移动位置时,相对于它的祖先元素来说的
>
> 语法同上

* 如果没有祖先元素,或者祖先元素没有的定位,则以浏览器为标准
* 子元素在父元素内,父元素没有定位的情况

```html
<style>
    .father {
        width: 100px;
        height: 100px;
        background-color: pink;
    }

    .son {
        position: absolute;
        top: 100px;
        width: 20px;
        height: 20px;
        background-color: plum;
    }
</style>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
```

- 如果祖先元素有定位(相对,绝对,固定),则以==最近一级的有定位祖先元素==为参考点移动位置
- 绝对定位是不占有原先的位置(脱标)
- 浮动是影响后面的位置,不影响前面的位置

## fixed(固定定位)==重要==

特点:

* 他是根据可视区域位置为参照点显示定位的
* 固定位置也是不占据原来的位置的

### 固定定位小技巧

小算法:

* 让固定定位的盒子left:50%,走到浏览器可视区,也可以看作是版心一半的位置
* 让固定定位的盒子margin-left:版心宽度的一半距离,多走版心宽度的一般位置

## 边偏移

* 总共有四种属性可以调整
  * top:80px
  * bottom:80px
  * left:80px
  * right:80px

## 子绝父相由来

1. 子级绝对定位,不会占有位置,可以放到父盒子里面的任何一个地方,不会影响其他的兄弟盒子
2. 父盒子需要加定位限制子盒子在父盒子内显示
3. 父盒子布局时,需要占有位置,因此父亲只能是相对定位

## 粘性定位(兼容性比较差)

* 可以被认为是相对定位和固定定位的混合.sticky

* ````
  选择器{position: sticky; top:10px}
  ````

* 特点:

  * 以浏览器的可视窗口为参照点移动元素(固定定位特点)
  * 粘性定位占有原来的位置(相对定位的特点)
  * 必须添加top,bottom,right,left四种属性之一才会生效
  * 跟页面滚动搭配使用,兼容性较差,IE不支持

## 定位叠放次序(z-index)

```
选择器{z-index:1;}
```

* 数值可以是正整数,负整数,默认是auto,数值越大,盒子越靠上

## 定位的拓展

### 绝对定位的居中对齐

* 绝对定位不能通过margin:auto来进行居中
* 方法的话还是和固定定位的方法一样,详情往上看

### 定位的特殊性

* 行内元素添加绝对定位或者固定定位,可以直接设置高度和宽度
* 块级元素添加绝对定位或者固定定位,如果不给宽度或者高度,默认大小是内容的大小

###  绝对定位(固定定位)会完全压住盒子

* 浮动元素不同,只会压住它下面标准流的盒子,但是不会压住下面标准流里面的文字或者图片

  但是绝对定位(固定定位)会压住下面标准流所有的内容

* 浮动最初设计的目的是用来进行实现文字环绕效果的

### 案例(淘宝焦点图)

* 如果相同样式过多,采取并集选择器,将相同样式提取出来

```
<style>
    * {
        margin: 0px;
        padding: 0px;
        list-style: none;
    }

    .tb_promo {
        position: relative;
        top: 0px;
        width: 520px;
        height: 280px;
        margin: 100px auto;
    }

    .prev {
        position: absolute;
        left: 0px;
        top: 120px;
        width: 35px;
        height: 20px;
        text-decoration: none;
        background-color: #ccc;
        border-top-right-radius: 15px;
        border-bottom-right-radius: 15px;
    }


    .next {
        position: absolute;
        right: 0px;
        top: 120px;
        height: 20px;
        width: 35px;
        text-decoration: none;
        background-color: #ccc;
        border-top-left-radius: 15px;
        border-bottom-left-radius: 15px;
    }

    a:hover {
        background-color: black;
    }

    ul {
        position: absolute;
        left: 50%;
        margin-left: -15px;
        bottom: 15px;
        width: 70px;
        height: 13px;
        background: rgba(0, 0, 0, .3);
        border-radius: 7px;
    }

    ul li {
        float: left;
        width: 8px;
        height: 8px;
        background-color: #fff;
        margin: 2px 4px;
        border-radius: 50%;
    }
</style>

<body>
    <div class="tb_promo">
        <img src="taobao_1.jpg" alt="">
        <a href="" class="prev">prev</a>
        <a href="" class="next">next</a>
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
</body>
```

### 元素的隐藏和显示

1. display
   * display:none 隐藏元素
   * display:block 除了转换为块级元素,同时还有显示元素的意思
   * display隐藏元素后,不在占有原来的位置
   * 后面应用及其广泛,搭配JS可以做很多的网页特效
2. visibility
   * visibility: visible:元素可视
   * visibility:hidden: 元素隐藏
   * 隐藏后,他会继续占有位置

3. overFlow 溢出
   * overflow: visible/hidden/scroll/auto
   * 用auto我觉得更好看点
   * 如果我们故意超出一点,不要用overflow来隐藏,他就会切掉多余的部分

# CSS高阶技巧

## 精灵图的使用方法

* 主要是针对小的背景图来使用的

* 在网页中的布局是X轴往右越大,Y轴越往下越大
* 所以说,在网页中往上往左都是负值.

```
<style>
    .a1,
    .a2,
    .a3 {
        float: left;
        width: 110px;
        height: 125px;

    }

    .a1 {
        background: url(images/abcd.jpg) no-repeat -236px 0px;
    }

    .a2 {
        background: url(images/abcd.jpg) no-repeat -478px -546px;
    }

    .a3 {
        background: url(images/abcd.jpg) no-repeat -253px -556px;
    }
</style>

<body>
    <div class="a1"></div>
    <div class="a2"></div>
    <div class="a3"></div>
    <div class="a4"></div>
</body>
```

* 因为对齐都是靠盒子的左上角对齐的,所以说是以图标左上角坐标为基准的.

## 字体图标

* 主要用于显示网页中通用,常用的一些小图标
* 精灵图的缺点:
  * 图片文件本身还是挺大的
  * 图片本身放大和缩小会失真
  * 一旦图片制作完成后,想更换非常复杂
* 这时候就出现了字体图标iconfont
* 它可以为前端工程师提供一种方便高效的图标使用方法,==展示的是图标,本质属于字体==
*  iconfont优点
  * 轻量级
  * 灵活性
  * 兼容性高
* 总结:
  * 如果遇到样式比较简单的小图标,就用字体图标
  * 如果结构和样式复杂一点的小图片,就用精灵图

## 字体图标下载

* 已经收藏

## 字体图标的引入

* 字体文件格式要放在与html文件同级目录下
* 如果无法显示,记得先下载fonts文件夹下的.tff文件

## 字体图标的追加

* 把压缩包中的select.json文件从新上传,然后选中自己想要的新图标,从新下载压缩包,并替换原来的文件即可

## CSS三角样式

````
 .box {
        /* line-height和font-size是适用于低版本的浏览器的 */
        width: 0;
        height: 0;
        line-height: 0;
        font-size: 0px;
        border-top: 10px solid pink;
        border-right: 10px solid red;
        border-bottom: 10px solid blue;
        border-left: 10px solid green;
    }
````

* 只要设置一个边框方向,而不设置高度和宽度,就能形成三角形

## 鼠标样式

* ````
  {cursor:pointer;}
  ````

* 属性:

  * default
  * pointer
  * move
  * text
  * not-allowed

## 轮廓线

* outline:none:就能取消轮廓线

## 防止文本域拖拽

* resize:none

* 文本域textarea属性中,不要有空格,显示出来不好看

## verticla-align

* 只针对行内元素和行内块元素有效

* 图片,表单和文字对齐
* 图片和表单都属于行内块元素.默认的是基线对齐
* 基线就是英文四道杠中的第三道杠
* top就是第一条
* middlel就是第二条,也就是文字的中心
* bottom就是针对最后一条线

### 解决图片底部默认空白缝隙问题

* bug:图片底侧会有一个空白缝隙,原因是行内块元素和文字的基线对齐
* 解决方法:
  * 给图片添加vertical-align: middle|top|bottom等
  * 把图片转化为块级元素

## 溢出文字显示省略号问题

* 单行文本做法

  ```html
  .box {
          width: 100px;
          height: 100px;
          background-color: green;
          margin: 100px auto;
          /* 这个意思是如果文字显示不下去, 会进行自动换行 */
          /* white-space: normal; */
          /*1. 这个意思就是强制让你在一行内显示 */
          white-space: nowrap;
          /*2. 溢出的部分隐藏起来 */
          overflow: hidden;
          /*3. 文字溢出的时候用省略号显示 */
          text-overflow: ellipsis;
      }
  ```

* 多行文本溢出显示

  > 多行文本溢出显示省略号,有较大兼容性问题,适合于webKit浏览器或移动端(大部分是webkit内核)

```
overflow:hidden;
text-overflow:ellipsis;
//弹性伸缩盒子模型显示
display:-webkit-box;
//限制在一个快元素显示的文本的行数
-webkit-line-clamp:2;
//设置或检索伸缩盒子对象的子元素的排列方式
-webkit-box-orient:vertical
```

* 让后台去做会比较好,它能控制显示多少个字,更方便

## 布局技巧

### margin负值运用

```
<style>
    .box_1,
    .box_2,
    .box_3 {
        position: relative;
        //首先先让盒子浮动起来,让后面的盒子都能跟的上,这样就会有边框压在一起
        float: left;
        height: 100px;
        width: 100px;
        border: 1px solid black;
        background-color: white;
        //然后通过margin,让它往左挪一点,如下面所示
        margin-left: -1px;
    }
//要想显示鼠标一经过,就能把完整的边框显示出来,如果你的盒子都加了定位,那么我们需要z-index来提高鼠标经过该盒子的层级即可
//如果没有定位,那么加一个相对定位即可
    div:hover {
        z-index: 1;
        border-color: coral;
    }
```

### 行内块的巧妙运用

* 行内块可以设置宽度和高度,还自带间距,非常方便做那种切换页面的小数字,非常方便

### CSS三角强化

# HTML5新特性(部分)剩下的查文档

## 新增的语法标签

```
1.<header>:头部标签
2.<nav>:导航标签
3.<article>:内容标签
4.<section>:定义文档某个区域
5.<aside>:侧边栏标签
6.<footer>:尾部标签
```

## 新增的video和音频标签

## 新增的input表单

## 新增的表单属性

# CSS新增特性

## 属性选择器

![image-20210422071022023](https://gitee.com/IU_czx/images/raw/master/img/image-20210422071022023.png)

==注意==:类选择器,属性选择器,伪类选择器的权重都为10

##　伪类选择器

<img src="https://gitee.com/IU_czx/images/raw/master/img/image-20210422071657280.png" alt="image-20210422071657280" style="zoom: 80%;" />

* nth-child(n)选择某个父元素的一个或特定的子元素
* n可以是数字,关键字和公式
* n如果是数字,就是选择第n个子元素,里面数字从1开始
* n可以是关键字:even欧式,odd奇数
* n可以是公式,n从0开始nth-of-type和child的区别
  * nth-child执行的时候会先看第一个孩子,如果第一个孩子和前门面指定元素不一样,他就不会把后面的选出来
  * nth-of-type对父元素里面指定子元素进行排序选择,先去匹配E,然后在根据E找第n个孩子

##　伪元素选择器

* before 和after创建一个元素,但是属于行内元素
* 新创建的这个元素在文档树中是找不到的,所以称为伪元素
* 语法:element::before{}
* before和after必须有content属性
* before在父元素内容面前创建元素,after在父元素内容的后面插入元素
* 伪元素选择器和标签选择器一样,权重为1
* 所以呢div::before,前面标签选择器的权重是1,后面伪类元素选择器的权重也为1,所以他们的权重就为2

### 使用场景

1. 用它来做一点文字图标的效果

2. 伪元素清除浮动

   第一种方法更为推荐

   ````
   .clearfix:before,.clearfix:after{
      content:"";
      display:table;
   }
   .clearfix:after{
    clear:both
   }
   ````

   ```
   .clearfix:after{
     content:"";
     display:block;
     height:0;
     clear: both;
     visibility:hidden
   }
   ```

## 盒子模型

> CSS3可以通过box-sizing来指定盒模型,有两个值,即可指定为**content-box**,**border-box**,这样我们计算盒子大小的方式就发生了改变.

可以分成两种情况:

1. content-box,盒子大小为宽度+内边距+边框
2. border-box,盒子大小就是宽度

   在第二种情况下,padding和border就不会撑大盒子了,前提是padding和border不会超过width

## CSS3其他特性(了解)

* 图片变模糊
* 计算盒子宽度width:calc
* filter:blur(模糊处理),括号里面数值越大,越模糊
* width: calc(100%-80px),这个100%保持与父盒子的宽度一样,然后加减,可以控制这个子盒子的宽度,让它动态保持宽度

##　过渡动画（==重要==）

* transition:要过过渡的属性 花费的时间 运动曲线  何时开始
  * 属性:想要变化的css属性,宽度高度 背景颜色 内外边距都可以.如果像要属性变化过渡,写一个all就可以
  * 花费时间:单位是 秒(必须写单位)
  * 运动曲线:默认是ease(可以省略)
  * 何时开始:单位是 秒,可以设置延迟触发事件 默认是0秒
  * 谁做过渡给谁加
  * 配合hover使用才行

# PC端品优购项目制作

## 模块化开发

* 将相同的样式放在一个CSS文件中
* 在很多页面的头部,尾部,导航栏部分大部分都是相同的样式,这时候可以将他们的样式统一放在一个文件中,节省开发,注重可重复使用

## 网站favicon图标

* 把品优购的图片切成png文件
* 然后在第三方网站进行格式转换成ico文件

## 网站TDK三大标签SEO优化

### title网站标题

###　网站说明

### keywords关键字

## logoSEO优化

* logo里面首先放一个h1标签,目的是为了提权,告诉搜索引擎,这个地方很重要
* 再在h1标签内放一个链接,可以返回首页,把logo的背景图片给链接即可
* 为了搜索引擎收入我们,我们的链接要放文字(网站名称),但是不要显示出来
  * text-indent移到盒子外面(text-indent:-9999px),然后overflow:hidden
  * 直接给font-size:0
* 最后给链接一个title属性,这样鼠标放到logo上就可以看到提示文字了

## 注意

* 一般a里面放块级元素的话,也要把a设置为块级元素,最为安全
* li本身就带有1px的边框,不过是不显示的,如果这个时候,你给li设置了hover属性,让鼠标经过时,边框变颜色,那么他就会抖一下,在li中设置一下,将边框变成透明色

# CSS3 2D转换

## 2D转换之移动translate

``` 
trnsform:translate(x,y);或者分开写 后面一定要加单位px
		translateX(n);
		translateY(n);
```

* 重点
  1. 定义2d转换中的移动,沿着X和Y轴移动元素
  2. 它最大的优点,不会影响到其他元素的位置
  3. translate中的百分比单位是相当于自身元素的  translate:(50%,50%);
  4. 它对行内标签没有影响

## 旋转Rotate

```
transform:rotate(度数) //单位是deg
```

* 2D转换我们可以设置转换中心点transform-origin

  ```html
  transform-orign:x y; 
  ```

  > 1. 这个是空格隔开的
  > 2. x y默认转换的中心点是元素的中心点(50% 50%)
  > 3. 还可以给 X Y设置像素或者方位名词(top bottom left right center)
  > 4. 左下角就是left bottom

## 缩放scale

```
transform:scale(x,y);
```

* 注意是用逗号隔开,后面不带单位
* 里面参数都为1,宽高都放大一倍,相当于没有放大
* 只写一个参数,说明宽高都是一样的
* 0.5就是缩小
* 最大的优势:可以设置转换中心点缩放,默认以中心点缩放,而且不影响盒子

## 2D转换总结

* 可以同时使用多个转换,其格式为:

  ```
  transform:translate() rotate() scale()
  ```

* 其顺序会影响转换的效果,先旋转会改变坐标轴的方向

* 同时有位移和其他属性的时候,记得要将位移放到最前面

# CSS动画

> 动画是CSS3具有颠覆性的特征之一,可通过设置多个节点来精确控制一个或一组动画,常用来实现比较复杂的动画效果
>
> 相比较过渡,动画可以实现更多变化,更多控制,连续自动播放等效果

## 5.1动画基本使用

1. 先定义动画
2. 在调用动画

```css
    @keyframes move {
        0% {}

        25% {
            transform: translate(1000px, 0);
        }

        50% {
            transform: translate(1000px, 500px);
        }

        75% {
            transform: translate(0px, 500px);
        }

        /* 100% {
            transform: translate(0, 0);
        } */
    }

    div {
        width: 100px;
        height: 100px;
        animation: move 10s;//调用动画
        background-color: pink;
    }
```

## 动画的属性

![image-20210514061031112](https://gitee.com/IU_czx/images/raw/master/img/image-20210514061031112.png)

### 速度曲线调节

![image-20210514083825915](https://gitee.com/IU_czx/images/raw/master/img/image-20210514083825915.png)

steps就是把动画分成几步完成

# CSS-3D转换

## 三维坐标系

三维坐标系就是指立体空间,立体空间是由3个轴共同组成的.

* x轴:水平向右 x向右是正值,左边是负值
* y轴:垂直向下 y下面是正值,上面是负值

* z轴:垂直屏幕 往外面是正值,往里面是负值

## 透视

![image-20210514090213573](https://gitee.com/IU_czx/images/raw/master/img/image-20210514090213573.png)

* 透视写在被观察元素的父盒子上面的
* d:就是视距,视距就是一个距离人的眼睛到屏幕的距离
* z轴:物体距离屏幕的距离,z轴越大(正值)吗,我们所看到的物体也就越大

## 3D旋转

## 3D呈现 transform-style

![image-20210514095504432](https://gitee.com/IU_czx/images/raw/master/img/image-20210514095504432.png)

## 浏览器私有前缀

![image-20210514211351154](https://gitee.com/IU_czx/images/raw/master/img/image-20210514211351154.png)

