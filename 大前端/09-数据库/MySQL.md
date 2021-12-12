# 初识MySQL

## 数据库分类

* 关系数据库:
  * MySQL,Oracle,SQLServer,DB2,SQLite
  * 通过表和表之间,行和行之间的关系进行数据的存储,如学员信息表...
* 非关系型数据库:
  * Redis,MongDB
  * 非关系型数据库,对象存储,通过对象的自身的属性来决定
* ==DBMS(数据库管理系统)==
  * 数据库的管理软件,科学有效的管理我们的数据.维护和获取数据
  * MySQL,数据库管理系统

## MySQL安装

1. 首先可以在镜像网站下载一下MySQL的安装包,我自己是在

   [欢迎访问网易开源镜像站](http://mirrors.163.com/)这里找到安装的

2. 解压放到你喜欢的文件,配置一下环境变量

![image-20210515092906913](https://gitee.com/IU_czx/images/raw/master/img/image-20210515092906913.png)

3. 在你的mysql文件夹中,新建一个配置文件(my.ini)

   ```ini
   #注意使用自己的根目录
   [mysqld]
   basedir=D:\MySQL-5.7.31\mysql
   datadir=D:\MySQL-5.7.31\mysql\data\
   port=3306
   #skip-grant-tables
   #第一次进入先把上面那行注释掉
   
   ```

4. 以管理员的身份打开命令提示符,进入bin目录下后运行以下命令

   ```mysql
   D:\MySQL-5.7.31\mysql\bin>mysqld -install     //安装命令
   D:\MySQL-5.7.31\mysql\bin>mysqld --initialize-insecure --user=mysql  //初始数据库
   D:\MySQL-5.7.31\mysql\bin>net start mysql   //开始mysql的服务
   D:\MySQL-5.7.31\mysql\bin>mysql -u root -p //进入mysql
   mysql> update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost'; //第一次进入没有密码,这个是用来设置密码和用户的
   mysql> flush privileges; //刷新权限
   
   //后面就是测试一下 你的mysql密码有没有设置成功,能通过你的密码进入mysql说明安装成功了
   ```

## Navicate安装

[Windows下 Navicat Premium 15安装教程（图文，含注册） - ZChen1996 - 博客园](https://www.cnblogs.com/zhangzhicheng1996/p/13326251.html)

## 命令行连接数据库

![image-20210515103220522](https://gitee.com/IU_czx/images/raw/master/img/image-20210515103220522.png)

# 操作数据库

> 操作数据库->操作数据库中的表->操作数据库中表的数据

==mysql关键字不区分大小写==

## 基本操作

> []:方框内的表示可选内容

1. 创建数据库

   ```sql
   CREATE DATABASE [IF NOT EXISTS] school
   ```

2. 删除数据库

   ```sql
   DROP DATABASE  [IF  EXISTS] school;
   ```

3. 指定表

   ```sql
   -- 如果你的表名或者字段名是一个特殊字符,就需要带`这个符号是`tab键上面的`
   USE `school`
   ```

4. 查看数据库

   ```sqlite
   show DATABASES --查看数据库
   ```


## 数据类型

> 数值

* tinyint 十分小的数据 1个字节
* smallint 较小的数据  2个字节
* mediumint 中等大小的数据 3个字节
* int 标准的数据 4个字节 常用
* bight 较大的数据 8个字节
* float 浮点数 4个字节
* double 浮点数 8个字节
* decimal 字符串形式的浮点数 金融计算一般使用decimal



> 字符串

* char 字符串固定的大小 0-255
* varchar 可变字符串 0-65535 常用的变量 String
* tinytext 微型文本 2^8-1
* text 文本串 2^16-1 保存大文本

> 时间日期

* Java.util.Data
* date YYYY-MM-DD,日期格式
* datetime YYYY-MM-DD HH: mm: ss 最常用的时间格式
* timestramp  时间戳,1970.1.1到现在的毫秒数 较为常用
* year 年份表示

> null

* 没有值,未知
* ==注意 不要使用NULL计算==

## 数据库的字段类型(重点)

Unsigned:

* 无符号的整数
* 声明了该列不能声明为负数

zerofill:

* 0填充
* 不足的位数,使用0来填充,int(3),5----005

自增:

* 通常理解为自增,自动在上一条记录的基础上+1
* 通常用来设计唯一的主键~index,必须是整数类型
* 可以自定义设计主键自增的起始值和步长

非空 NULL not NULL

* 假设设置为 not null,不给它赋值,就会报错
* null 默认null

拓展

> 每一个表,都必须存在以下五个字段!未来做项目用,表示每一个记录存在有意义
>
> id 主键
>
> `version`乐观锁
>
> is_delete伪删除
>
> gmt_create 创建时间
>
> gmt_update 修改时间

```sql
CREATE TABLE IF NOT EXISTS `student` (
	`id` INT(4) NOT NULL DEFAULT '180047101' COMMENT '学号',
	`name` VARCHAR(10) NOT NULL DEFAULT '曹志贤' COMMENT '姓名',
	`sex` VARCHAR(2) NOT NULL  DEFAULT '男' COMMENT'性别'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

![image-20210516092050941](https://gitee.com/IU_czx/images/raw/master/img/image-20210516092050941.png)

## 数据库常用命令

```sql
SHOW CREATE xxx
相当于一个逆向操作,可以查看是如何建立的,比如如何创建数据库,数据表的
例:
SHOW CREATE DATABASE school  --显示数据库
SHOW CREATE TABLE student --显示学生表是如何创建的
DESC student --显示学生表的结构
```

### 关于数据库引擎

INNODB 默认使用

MYISAM 早些年使用的

## 修改删除表

```sql
-- 修改表
 ALTER TABLE student RENAME AS students
-- 增加表的字段
 ALTER TABLE students ADD `Myage` INT(11);
-- 修改表的字段 (重命名,修改约束)
 ALTER TABLE students MODIFY `Myage` VARCHAR(11) --修改约束
 ALTER TABLE students CHANGE `Myage` `age` INT(2) --可以用来字段重命名
-- 删除表的字段
ALTER TABLE students DROP age
```

创建和删除最好加上判断,以免报错



注意点:

* ``字段名,使用这个包裹
* 注释 -- /**/
* sql关键字大小写不敏感,建议小写
* 所有符号用英文符号

# MYSQL数据管理

### 外键(了解即可)

设置外键有以下条件:

* 要设置外键的字段不能为主键
* 该键所参考的字段为主键
* 两个字段必须具有相同的数据类型和约束

```sql
ALTER TABLE　表　ADD CONSTRAINT 约束名 FOREIGN　KEY（作为外键的列）REFERENCES  哪个表(哪个字段)
```

以上操作是物理外键,数据库级别的外键,不建议使用(避免数据库过多造成困扰)



最佳实践:

* 数据库是单纯的表,只用来记数据
* 要想使用多张表的数据,要使用外键(程序去实现)

### DML语言(全部记住)

> 数据库意义:数据存储,数据管理

DML语言

* insert

  ```sql
  -- 插入语句
  -- INSERT INTO 表名([字段名1,字段2,字段3...])VALUES('值1','值2','值3'....)
  INSERT INTO `students`(`name`)VALUES('曹志贤');
  ```

* update

  ```sql
  -- 更新语句
  -- UPDATE 表名 SET 需要改的列名='你要改成的数据',[后面可以加多个你要改的,用逗号隔开] WHERE 需要改的列名=指定改的哪个具体列名存的数据
  UPDATE students SET `id`='1234' WHERE id=180047101; 
  ```

  | 操作符           | 含义     | 范围 | 结果 |
  | ---------------- | -------- | ---- | ---- |
  | =                |          |      |      |
  | <>或!= 不等于    |          |      |      |
  | >                |          |      |      |
  | <                |          |      |      |
  | <=               |          |      |      |
  | >=               |          |      |      |
  | Between...and... | 闭合区间 |      |      |
  | AND              |          |      |      |
  | OR               |          |      |      |

* ![image-20210516104728504](https://gitee.com/IU_czx/images/raw/master/img/image-20210516104728504.png)

* Delete命令

  ```sql
  -- delete 删除数据库
   DELETE FROM `student`
  
  -- 推荐用这个清空表
  TRUNCATE 成绩表
  ```

  

delete 和 TRUNCATE的区别

相同点:

- 都能删除数据,都不会删除表的结构

不同:

* TRUNCATE 重新设置 自增列 计数器会归零
* 不会影响事务

了解即可:`delete`删除现象,重启数据库,现象

* innodb 自增列会从1开始(存在内存当中的,断电即失)
* MYISAM 继续从上一个自增量开始(存在文件当中的,不会丢失)

#  DQL查询数据(超级重点)

### 最基本的查询,一定要掌握

```sql
-- 查询全部的学生
SELECT * FROM `subject`;

-- 查询指定字段
SELECT `subjectname` from subject;

-- 别名 给你查询出来的数据添加上另外一个名字
-- 别名你可以加上as也可以不加
SELECT `subjectname` 学科 FROM subject;

-- 函数 Concat(a,b) 字符串连接
SELECT CONCAT('学科: ',subjectname) newName FROM subject

-- 去重处理
SELECT DISTINCT studentno FROM result;
```

 一些小操作

```sql
SELECT VERSION();
SELECT 100*3-1 AS 计算结果; -- 用来计算(表达式)
SELECT @@auto_increment_increment; -- 查询自增的步长 (变量)

-- 学院考试成绩+ 1分查看
SELECT `studentno`,`studentresult`+1 提分后 from result
```

### Where条件子句,可以用以下逻辑运算符

![image-20210516153025816](https://gitee.com/IU_czx/images/raw/master/img/image-20210516153025816.png)



### ==模糊查询==

![image-20210516154153778](https://gitee.com/IU_czx/images/raw/master/img/image-20210516154153778.png)

```sql
SELECT * from subject;

SELECT * from subject WHERE subjectname LIKE '高等%';

SELECT * from subject WHERE subjectname LIKE '%语言%';

SELECT * from subject WHERE classhour BETWEEN 110 AND 120;

SELECT * from subject WHERE classhour IN (110,120);
```

### 联表查询

* INNER JOIN ＯN

  语法:

  ```sql
  SELECT column_name(s)
  FROM table1
  INNER JOIN table2
  ON table1.column_name=table2.column_name;
  
  SELECT column_name(s)
  FROM table1
  JOIN table2
  ON table1.column_name=table2.column_name;
  
  -- JOIN 和 INNER JOIN是等价的
  ```

  ```sql
  -- INNER JOIN表示两张表之间的交集,至少得有一个匹配值才会返回
  SELECT student.studentname,st.subjectname from student
  INNER JOIN subject st
  ON  student.studentno=st.gradeid;
  ```

* LEFT JOIN ＯN

  语法:

  ```sql
  SELECT column_name(s)
  FROM table1
  LEFT JOIN table2
  ON table1.column_name=table2.column_name;
  
  SELECT column_name(s)
  FROM table1
  LEFT OUTER JOIN table2
  ON table1.column_name=table2.column_name;
  ```

  ```sql
  -- LEFT JOIN表示以左边表的值为中心,右边即使没有与左边的表相匹配到,他也会返回
  SELECT student.studentname,st.subjectname from student
  LEFT JOIN subject st
  ON  student.sex=st.gradeid;
  
  ```

* RIGHT JOIN

  语法:

  ```sql
  SELECT column_name(s)
  FROM table1
  RIGHT JOIN table2
  ON table1.column_name=table2.column_name;
  
  SELECT column_name(s)
  FROM table1
  RIGHT OUTER JOIN table2
  ON table1.column_name=table2.column_name;
  ```

  ```sql
  -- RIGHT JOIN表示以右边的值为中心,左边即使没有与右边的表的值相匹配,他也会返回值
  SELECT student.studentname,st.subjectname from student
  RIGHT JOIN subject st
  ON  student.gradeid=st.gradeid;
  ```

在使用JOIN中,on和where的区别

![image-20210516193706655](https://gitee.com/IU_czx/images/raw/master/img/image-20210516193706655.png)

![image-20210516193730342](https://gitee.com/IU_czx/images/raw/master/img/image-20210516193730342.png)

![image-20210516193745939](https://gitee.com/IU_czx/images/raw/master/img/image-20210516193745939.png)

> 自连接(了解即可)
>
> 大概就时一张表内同时有父级和子级,用表中的其他属性去匹配,筛选父级和对应的子级

![image-20210518213748233](https://gitee.com/IU_czx/images/raw/master/img/image-20210518213748233.png)

### 分页和排序

* 排序:order by desc降序	order by asc升序

* 分页公式

  ```sql
  limit (n-1) * pageSize  -- n-1是表示从哪开始读取数据  
  ```

  