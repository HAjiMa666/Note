# HTML

## 01-跨标签页通信有哪几种方式

下面介绍的都是基于同源之间 进行通信的

  1. BroadCast Channel

     缺点:

     * 他的兼容性稍微差点

     优点:

     * 与localStorage方案生命周期短(不持久化),相对干净点

  2. LocalStorage

     * API简单直观，兼容性好，除了跨域场景下需要配合其他方案，无其他缺点

  3. window.open:获取句柄

  4. Shared Worker

     * 相较于其他方案没有优势，此外，API复杂而且调试不方便。

  5. Cookie

     * 相较于其他方案没有存在优势的地方，只能同域使用，而且污染cookie以后还额外增加AJAX的请求头内容。

  6. 基于服务器端推送:WebSocket

  7. Service-Worker

## 02-块级元素和行内元素

> 具体的可以去看我在语雀记录的文章
>
> 这里就简单介绍一些重点

1. 行内元素无法设置margin和padding的上下值,只能设置左右的值
2. p标签内不能嵌套块级元素

## 03-前端路由

前端路由有两种形式,一种是history,一种是hash模式

1. hash

   1. 触发情况:通过window中的hashchange进行监听

   2. 浏览器的前进或者后退,他是会触发window.location.hash的变化,从而触发onhashchange的

   3. 改变浏览器url地址后面的hash值,这时候不会向服务器发送请求,但是hash值发生改变,也会触发

   4. 在浏览器中输入带有hash值的url地址,首先会先将hash前面网址的地址向服务器请求,这时候会再设置散列值,也就是hash,进而触发事件

   5. 向a链接中的锚点链接,例如<a href="#home"/>这种的,这种会触发window.location.hash,进而触发事件

2. history

   1. 概述:

      1. window.history会指向History对象,他表示的是当前窗口的浏览历史.发生改变时,只会刷新更改url地址,不会刷新页面

      2. 由于安全原因,浏览器不允许脚本读取这些地址

   2. 触发情况

      1. 通过监听popState来触发,触发的情况只有,下面三个API,他们改变了才会发生变化

      2. 可以使用History中的三个API,History.back(),History.go(),History.forward()进行一个触发

      3. back和forward只能移动一次,分别是向后,向前
      4. go的话.会接受数字,数字代表着移动方向

   3. History.pushState

      > history.pushState(object,title,url);
      > 第一个是你要传入的对象值
      > 第二个参数,浏览器大部分不支持,所以传个空字符串即可
      > 第三个参数是新的网址,要在同域下,设置了跨域网址,则会报错
      > 如果你想要取值的话,需要调用history.state,里面存放的是你放入的对象

   4. replaceState,用法和pushState差不多
   5. 注意事项
      1. 页面刚加载的时候,不会触发popState
      2. 如果后端没有准备好的话,强制刷新会导致错误

## 04-async和defer的区别

1. async : 在脚本上加上async后,这个脚本会变成异步执行,但是执行顺序不能得到保证
2. defer: 在脚本上加上defer后,这个脚本就会延迟执行,但是执行顺序能得到保证

相同点:

1. 加载文件时不阻塞页面渲染
2. 对于inline的script无效,当script标签中间有代码时,两个属性都不会起作用
3. 使用这两个属性的脚本中不能调用document.write方法
4. 有脚本的onload的事件回调

不同点

1. 在HTML4.0中定义了defer,html5.0中定义了async
2. 每一个async属性的脚本都在它下载结束之后立即执行,同时会在window的load事件之前执行,所以可能出现顺序被打乱的情况
3. defer的话再页面解析完毕之后,按照原本的顺序执行
4. 当一个script标签内同时包含defer与async属性时,只会触发async,不会触发defer,除非浏览器不支持async