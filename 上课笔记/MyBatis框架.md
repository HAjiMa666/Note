# MyBatis框架

# 第一章 框架的概述

## 三层架构

mvc:web开发种,使用mvc架构模式

m:数据

v:试图

c:控制器

* 控制器:接受请求,调用Service对象,显示请求的处理结果,使用servlet作为控制器
* 视图:现在使用jsp,html,css,js显示请求的处理结果,把数据显示出来
* 数据:来自数据库mysql,来自文件,来自网络

mvc作用:

* 实现解耦合
* 让mvc各赋其值
* 使得系统扩展更好,更容易维护

三层架构:

1. 界面层(视图层):接受用户的请求,调用Service,显示请求的处理结果,包含了jsp,html,servlet等对象,对应的包是Controller
2. 业务逻辑层:处理业务逻辑,使用算法处理数据,把数据返回给界面层,对应的是service包,和包中的很多XXXService类
3. 持久层(数据库访问层):访问数据库,或者读取文件,访问网络,获取数据,对应的包是dao,dao包种很多的,例如StudentDao....

## 2.三层架构请求的处理流程

> 用户发起请求->界面层->业务逻辑层->持久层->数据库(mySql)



## 为什么要使用三层

![image-20210529080748490](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210529080748490.png)

## 三层架构模式和框架

每一层对应的一个架构

1. 界面层---SpringMVC框架
2. 业务层---Spring框架
3. 持久层---MyBatis框架

## 框架解决的问题

1. 能实现技术的整合
2. 提高开发的效率,降低难度

## JDBC访问数据库的优缺点

优点:

* 直观,好理解

缺点:

* 创建很多对象
* 注册驱动
* 执行SQL语句
* 把result转为STudent,List集合
* 关闭资源
* sql语句和业务逻辑代码混在一块

## MyBatis框架

> 是一个持久化框架,原名ibatis,2013改名为MyBatis,可以操作数据库,对数据库执行增删查改

它能做什么

* 注册驱动
* 创建JDBC种用的Connection,Statement,ResultSet
* 执行SQl语句,得到ResultSet
* 处理,将记录转化为Java对象,同时还能把java对象放入List集合种
* 关闭资源
* 实现SQl语句和Java代码的解耦合

官网:

[mybatis – MyBatis 3 | 简介](https://mybatis.org/mybatis-3/zh/index.html)

