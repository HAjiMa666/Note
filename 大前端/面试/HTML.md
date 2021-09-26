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

## 05-iframe有什么缺点

1. `iframe`会阻塞主页面的`onload`事件

2. 搜索引擎的检索程序无法解读这种页面,不利于`seo`

3. `iframe`和主页面共享连接池,而浏览器对于相同域的连接有限制,所以会影响页面的并行加载

4. 使用`iframe`之前要考虑两个缺点,如果需要使用`iframe`,最好是通过`javaScript`

5. 动态给`iframe`添加src属性,可以绕开以上两个问题

![image-20210913113031219](https://gitee.com/IU_czx/images/raw/master/img/%E8%BF%9E%E6%8E%A5%E6%B1%A0%E8%A7%A3%E9%87%8A.png)

## 06-Src和href的区别

* `src`是用于替换当前元素,`href`用于在当前文档和引用资源之间确认联系

* `src`是`source`的缩写,指向外部资源的位置,指向的内容将会嵌入到文档中当前标签所在的位置;在请求`src`资源时会将其指向的资源下载并应用到文档中,如`js`脚本,`img`图片,`iframe`等元素

  ```js
  <script src="js.js"></script>
  ```

  > 当浏览器解析到该元素时,会暂停其他资源的下载和处理,直到将该资源加载,编译,执行完毕,图片和框架等元素也是如此,类似于将所指向资源嵌入到当前标签内,这也是为什么js脚本放在底部和不是头部

* `href`是`Hypertext Reference`的缩写,指向网络资源所在位置,建立和当前元素(锚点)或者当前文档(链接)之间的链接,如果我们在文档中添加

  ```js
  <link href=”common.css” rel=”stylesheet”/>
  ```

  > 浏览器会识别该文档为css文件,就会并行下载资源并且不会停止对当前文档的处理
  >
  > 这也是为什么会建议使用link的方式来加载css,而不是使用`@import`的方式 

## 07-H5的新特性

1. 画布(canvas)API

2. 地理(Geolocation)API

3. 音频和视频(audio和video)API

4. `lcoalStorage`和`sessionStorage`

5. `webworker`和`websocket`

6. 新的一套标签

   `header` `nav` `footer` `aside` `article` `section`

7. `web worker`是运行在浏览器后台的js程序，他不影响主程序的运行，是另开的一个js线程，可以用这个线程执行复杂的数据操作，然后把操作结果通过postMessage传递给主线程，这样在进行复杂且耗时的操作时就不会阻塞主线程了。

8. `HTML5 History`两个新增的API：`history.pushState` 和 `history.replaceState`，两个 API 都会操作浏览器的历史记录，而不会引起页面的刷新。

> `Hash`就是`url` 中看到 `#` ,我们需要一个根据监听哈希变化触发的事件( `hashchange`) 事件。我们用 `window.location`处理哈希的改变时不会重新渲染页面，而是当作新页面加到历史记录中，这样我们跳转页面就可以在 hashchange 事件中注册 ajax 从而改变页面内容。 可以为hash的改变添加监听事件：

```js
window.addEventListener("hashchange", funcRef, false)
```

- `WebSocket` 使用`ws`或`wss`协议，`Websocket`是一个持久化的协议，相对于HTTP这种非持久的协议来说。WebSocket API最伟大之处在于服务器和客户端可以在给定的时间范围内的任意时刻，相互推送信息。`WebSocket`并不限于以Ajax(或XHR)方式通信，因为Ajax技术需要客户端发起请求，而WebSocket服务器和客户端可以彼此相互推送信息；XHR受到域的限制，而`WebSocket`允许跨域通信

```js
// 创建一个Socket实例
var socket = new WebSocket('ws://localhost:8080');
// 打开Socket
socket.onopen = function(event) {
  // 发送一个初始化消息
  socket.send('I am the client and I\'m listening!');
  // 监听消息
  socket.onmessage = function(event) {
    console.log('Client received a message',event);
  };
  // 监听Socket的关闭
  socket.onclose = function(event) {
    console.log('Client notified socket has closed',event);
  };
  // 关闭Socket....
  //socket.close()
};
```

