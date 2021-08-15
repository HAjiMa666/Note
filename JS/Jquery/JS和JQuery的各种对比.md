# JS和Jquery获取元素的各种对比

|                              JS                              |                            JQuery                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|            `通过ID获取`:document.getElementById()            |     $(""),这个就能获取所有的元素了,语法就和JS的原生一样      |
|       `通过标签名获取`:document.getElementsByTagName()       |               `元素选择器`,语法同左的css选择器               |
|      `通过类名来选择`:document.getElementsByClassName()      | `属性选择器`,可以通过Xpath属性来选取,$("[href]") 选取所有带有 href 属性的元素。 |
| 通过`CSS选择器`来选择:document.querySelectorAll(),获取所有的,也可以不加All,只获取一个 |    $("[href='#']") 选取所有带有 href 值等于 "#" 的元素。     |
|                                                              | `CSS选择器:`$("p").css("background-color","red");将P标签的背景颜色改成了红色 |

* JQuery中的css选择器是可以 以对象的形式传递参数进去的

  ````js
  $().css({
      width: 400,
      height: 400,
      backgrounColor:"color"
  })
  ````

  

------

# 获取内容和属性的操作

获取内容的操作

|                    JS                    |                   JQuery                    |
| :--------------------------------------: | :-----------------------------------------: |
| document.write():他会直接覆盖文档,修改后 |        text():返回所选元素的文本内容        |
|     Element.innerHTML:能识别HTML标签     | html():设置返回所选元素的内容(包括HTML标记) |
|    Element.innerText:只能识别文本内容    |       val():设置或返回`表单字段的值`        |
|                                          |          remove():删除自己和子元素          |
|                                          |        empty():删除选中元素的子元素         |

* JS的对文本内容操作是要加等号的

  * ````js
    document.getElementById(id).innerHTML = new text
    ````

    

* JQuery在获取文本内容的值的时候,是要加括号的,==牢记==

* JQuery在remove内可以接受一个参数,用于进行过滤,只删除含有这个属性的元素

* JQuery在给文本内容赋值的时候直接在()添加内容即可

获取改变属性的操作

|                            JS                             |                      JQuery                      |
| :-------------------------------------------------------: | :----------------------------------------------: |
|           Element.attribute=new value:进行改变            |    attr():可以获取标签的固有属性,和自定义属性    |
| document.getElementById("myImage").src = "landscape.jpg"; | data("设置数据名","数据"):这个是存在元素内存当中 |
|                 setAttribute("属性","值")                 |   prop():也可以获取固有属性,不能获取自定义属性   |
|                   getAttribute("属性")                    |        以上三种都可以在后面接上要改变的值        |
|                removeAttribute():移除属性                 |                                                  |
|    element.dataset.index:H5新增的获取自定义属性的方法     |                                                  |

* JS在获取自定义属性的值,时data-不要加进去

---

 # 样式的操作

|             JS             |      JQuery       |
| :------------------------: | :---------------: |
| element.style:行内样式操作 |     $().css()     |
| element.className:类名操作 |  $().addClass()   |
|                            | $().removeClass() |

* 这里要注意一个点,JS的用类名修改样式会直接覆盖原先的类名,如果向要保留之前的类名,在添加类名之时,添加上自己原来的类名即可,而JQuery不会覆,而是追加类名

# 节点操作的不同

|              JS              |     Jquery     |
| :--------------------------: | :------------: |
|   parentNode:获取父亲节点    | $().children() |
|     children:获取子节点      |  $().parent()  |
|    createElement:创建节点    | $().siblings() |
|     appendChild:追加元素     |    $().find    |
| insertBefofe(指定元素,child) |    $().eq()    |
|      removeChild(child)      |                |
|                              |                |

* 注意JS获取父亲节点的时候,后面不要加括号,还有获取父亲节点的时候,目标一定要明确,它只能返回单个数的父亲节点
* 注意Jquery这个是要加括号的,切记

