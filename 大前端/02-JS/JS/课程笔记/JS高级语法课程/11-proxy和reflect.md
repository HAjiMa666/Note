# 监听对象的操作

## 使用defineProperty

* 设置get和set函数,对属性进行一个拦截
* 但是对于更加复杂的操作无能为力,所以推出了Proxy

## 使用Proxy

> 帮助我们创建一个代理,有13种捕获器
>
> 对对象的所有操作,都通过代理对象来完成,代理对象可以监听我们想要对元对象进行哪些操作

## 捕获器种类

1. has:监听`in`操作符
2. deleteProperty:监听`delete`操作符

![image-20211015204656174](https://gitee.com/IU_czx/images/raw/master/img/%E6%8D%95%E8%8E%B7%E5%99%A8%E7%A7%8D%E7%B1%BB.png)

