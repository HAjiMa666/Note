# Spring

## Spring初认识

###  1.1简介

> 简化了企业级开发的流程
>
> 2002 首次推出Spring框架的雏形,Interfae21
>
> 2004 3.24 首次推出Spring1.0版本
>
> Rod Johson
>
> Spring理念:使现有的技术更加容易使用,整合了现有的技术框架
>
> SSH: Struct+Spring+Hibernate!
>
> SSM:SpringMvc+Spring+Mybatis

### 1.2优点

* 它是一个开源的免费的框架(容器)
* 它是一个轻量级的,非入侵式的框架
* 控制反转(IOC),面向切面编程(AOP)
* 支持事物的处理,对框架整合的支持

> spring就是一个轻量级的控制反转（ＩＯＣ）和面向切面编程（ＡＯＰ）的框架

### 1.3组成

![image.png](https://i.loli.net/2021/05/10/kXLWVmrPN4egDGA.png)

### 1.4拓展

* spring Boot

  * 一个快速开发的脚手架
  * 基于SpringBoot可以快速的开发单个微服务
  * 约定大于配置
* Spring Cloud

  * SpringCloud是基于SpringBoot实现
* 学习SpringBoot的前提是完全掌握Spring及SpringMvc

## IOC理论推导

* UserDao接口
* UserDaoImpl实现类
* UserService业务接口
* UserServiceImpl业务实现类

> 在以前写代码的时候,用户的需求可能会影响原来的代码.程序员需要根据用户的需求去修改源代码,如果程序代码量十分大,修改一次的代价相当昂贵

> 我们使用一个Set接口实现,已经发生革命性的变化

```java
private UserDao userDao;

//利用set进行动态实现值的注入
public void setUserDao(userDao userDao){
    this.userDao=userDao;
}

```

* 之前,程序是主动创建对象! 控制权在程序员手上
* 使用了set注入后.程序不在具有主动性,而是变成了被动接受对象

* 这种思想,从本质上解决了问题,我们程序员不用再去管理对象的创建.系统的耦合性大大降低,可以更加专注在业务上的实现,这是IOC的原型

### IOC本质

> 控制反转IOC(Inversion of Control),是一种设计思想,DI(依赖注入)是实现IOC的一种方法,也有人认为DI只是IOC的另一种说法,没有IOC的程序中,我们使用面向对象编程,对象的创建与对象间的以来关系完全硬编码在程序中,对象的创建由程序自己控制,控制反转后将对象的创建转移给第三方,简单来讲,获得依赖对象的方式反转了



> 采用XML配置Bean,Bean的定义信息是和现实分离的,而采用注解的方式可以把两者何为一体,Bean的定义信息直接以注解的形式定义在现实类中,从而达到零配置的目的

> 控制反转是一种通过描述(XML或注解)并通过第三方去生产或获取特定对象的方式.在Spring中实现控制反转的是IOC容器,其实现方法是依赖注入(Dependency Injection, DI)

* 我们不用在程序中发生变动,只需要在xml配置文件中进行修改,所谓的IOC,一句话搞定:对象由Spring来**创建,管理,装配**

* 问题

  Hello的对象是由谁创建的?

  ​	答:Hello的对象是由Spring创建的

  hello的属性是谁设置的?

  ​	答:是由Spring容器设置的

### IOC创建对象的方式

1. 使用无参构造创建对象,默认!

2. 假设要用有参构造,有以下三种方式

   * 参数类型(不推荐使用,如果有两个字符串,就行不通了)

   ```java
   <bean id="exampleBean" class="examples.ExampleBean">
       <constructor-arg type="int" value="7500000"/>
       <constructor-arg type="java.lang.String" value="42"/>
   </bean>
   ```

   * 通过index属性

   ```java
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg index="0" value="7500000"/>
         <constructor-arg index="1" value="42"/>
     </bean>
   ```

   * 构造函数参数名

   ```Java
     <bean id="exampleBean" class="examples.ExampleBean">
         <constructor-arg name="years" value="7500000"/>
         <constructor-arg name="ultimateAnswer" value="42"/>
     </bean>
   ```

3. 在配置文件加载的时候,容器中管理的对象就已经初始化了

## Spring配置说明

### 别名

```
//如果添加了别名,我们也可以使用别名来获取到这个对象
<alias name="user" alias="userNew"/>
```

### Bean的配置

```
//id:bean的唯一标识符,也就是相当于我们学的对象名
//class:bean对象所对应的全限定名:包名+类型
//name:也是别名,而且name可以同时取多个别名,中间用逗号或者空格隔开
   <bean id="user" class="com.czx.pojo.User " name="class1 class2">
        <property name="name" value="曹志贤"/>
    </bean>
```



```xml
//id就是你要获取里面的值的时候,所要用到的
//property中的name属性,是你需要注入值的变量名,要和函数内一样
<bean id="address" class="com.czx.pojo.Address">
            <property name="address" value="景德镇"/>
 </bean>
```



### import

* 一般用于团队开发使用,它可以将多个配置文件,导入合并为一个

* ```
    <import resource="beans.xml"/>
  ```

* 标准的名字是applicationContext

## DI依赖注入

### 构造器注入

> 前面有参构造的时候用到了,那个就是构造器注入

### Set方式注入[重点]

* 依赖注入:set注入

  * 依赖:bean对象的创建依赖于容器
  * 注入:bean对象中的所有属性

* 对于各种类型的值是如何注入的

  ```xml
          <bean id="address" class="com.czx.pojo.Address">
              <property name="address" value="景德镇"/>
              <property name="uname" value="曹志贤"/>
          </bean>
  
          <bean id="student" class="com.czx.pojo.Student">
              <!--第一种,普通值注入,value-->
              <property name="name" value="曹志贤"/>
              <!--第二种, Bean注入,ref-->
              <property name="address" ref="address"/>
              <!--数组注入,ref-->
              <property name="books">
                  <array>
                      <value>书1</value>
                      <value>书2</value>
                      <value>书3</value>
                      <value>书4</value>
                  </array>
              </property>
  
              <!--list-->
              <property name="hoobies">
                  <list>
                      <value>兴趣1</value>
                      <value>兴趣2</value>
                      <value>兴趣3</value>
                  </list>
              </property>
  
              <!--Map-->
              <property name="card">
                  <map>
                      <entry key="身份证" value="12345"/>
                      <entry key="学习证" value="12345"/>
                  </map>
              </property>
  
              <!--Set-->
              <property name="games">
                  <set>
                      <value>Baldr Sky</value>
                      <value>Hollow Knight</value>
                  </set>
              </property>
  
              <!--null-->
              <property name="wife" value=""/>
              <!--properties-->
              <property name="info">
                  <props>
                      <prop key="学号">180047101</prop>
                      <prop key="性别">男</prop>
                  </props>
              </property>
          </bean>
  ```

  

### 拓展方式注入

* C命名空间
* P命名空间
* 使用要引入P和c的xml的约束

```xml
		xmlns:p="http://www.springframework.org/schema/p"
         xmlns:c="http://www.springframework.org/schema/c"
```



```xml
        <bean id="user" class="com.czx.pojo.User" p:name="曹志贤" p:age="18"/>
		//c命名空间需要有参构造
        <bean id="user2" class="com.czx.pojo.User" c:name="曹志贤" c:age="18"/>
```

## Bean的作用域(Scopes)

![image-20210511161010152](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210511161010152.png)



1. 单例模式(Spring的默认机制)
2. 原型模式:每次从容器中get的时候,都会产生一个新对象
3. 其余的只能在web中开发

## Bean的自动装配

* 自动装配是Spring满足bean依赖的一种方式
* Spring会在上下文中自动寻找,并自动给bean装配属性

> 在Spring中有三种装配的方式
>
> * 在Xml中显示的配置
> * 在java中显示配置
> * 隐式的自动装配bean[重要]

### byName自动装配

```xml
    <bean id="cat" class="com.czx.pojo.Cat"/>
    <bean id="dogs" class="com.czx.pojo.Dog"/>
    <!--用byName的方法来进行自动装配,他会寻找你对象set方法的后面的值(名字)对应的beanid-->
    <bean id="people" class="com.czx.pojo.People" autowire="byName">
        <property name="name" value="czx"/>
    </bean>
```

### byType自动装配

* 他是根据你的对象属性类型相同的bean

### 总结

* byName需要保证bean的id唯一
* byType的时候需要保证bean的class唯一

### 使用注解实现自动装配

* 从Spring2.5就支持注解了

* 要使用注解须知

  * 引入约束
  * 配置注解的支持

  ````
      <context:annotation-config/>
  ````

* @AutoWired

  1. 可以直接在属性上使用
  2. 是根据类型来进行匹配的
  3. 可以不用写setter方法了,前提是这个自动装配属性在IOC(Spring)容器中存在
  4. @Nullable 字段标记了这个注解,说明这个字段可以为null
  5. Autowired中的required属性为false,说明这个对象可以为NULL,否则不允许为空

* 如果@AutoWired自动装配的环境比较复杂,自动装配无法通过一个注解[@AutoWired],可以使用@Qualifier(value="xxxx")去配置@AutoWired的使用,指定一个唯一的bean的对象注入
* @Resource和@AutoWired的区别
  * @AutoWired先通过byType进行类型匹配,如果有多个类型,就会对byName进行匹配
  * @Resource和@AutoWired相反

## 注解系列

1. @AutoWired

   > 先通过byType匹配,在通过byName匹配

2. @Resource

   > 先通过byName匹配,再通过byType匹配

3. @Component

   > 组件,放在类上的,说明该类被Spring管理了,就是bean

4. @Service

   > service层的所加注解,功能和Component一样

5. @Controller

   > 放在控制层上的注解,功能同上

6. @Repository

   > 放在DAO层上的注解,功能同上

7. @Value

   > 用来给对象注入属性值的
   
8. @Scope

   > 用来设定你想放入什么样的作用域的



## 使用注解开发

###  1.注解前的准备

```xml
    <context:component-scan base-package="放入你所需要注入的包"/>
    <context:annotation-config/>
```

### 2.属性如何注入

```java
@Component
public class User {
    @Value("cao zhi xian")
    public String name;
}
```

### 3.衍生的注解

* @Component有几个衍生注解,我们在Web开发中,会按照mvc三层架构分层
  * DAO	[@Repository]
  * Service  [@Service] 
  * Controller  [@Controller]
  * 以上的四个功能都是一样的,都是代表将类注册到Spring容器中,装配bean

### 4.作用域

```xml
@Scope("你想要放进去的作用域")
```

### 5.总结

* XML与注解
  * xml更加万能，适用于任何场所！维护简单方便
  * 注解不是自己类使用不了，维护相对复杂
* xml与注解最佳实践
  * xml用来管理bean
  * 注解只负责完成属性的注入
  * 我们只要注意：必须让注解生效，就必须扫描到下面的包，需要开启注解的支持

## 使用Java的方式配置Spring

> 我们现在要完全不使用Spring的XML配置,全权交给java去做
>
> JavaConfig是Spring的一个子项目,在Spring4之后,他成为一个核心功能



实体类

```java
package com.czx.pojo;

import org.springframework.beans.factory.annotation.Value;



public class User {
    @Value("cao zhi xian")
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}

```

配置文件

```java
//@Configuration也是相当于把它交给Spring容器托管,因为在Configuration内也是加入了@Component,注册进Spring容器中了
@Configuration
public class CZXconfig {
    @Bean
    public User user(){
        return new User();
    }
}
```

测试类

```java
public class Mytest {
    public static void main(String[] args) {
//     如果完全使用了配置类方式去做,我们只能通过AnnotationConfig 上下文来获取容器,通过配置类的class对象加载!
        ApplicationContext context = new AnnotationConfigApplicationContext(CZXconfig.class);
        User user = (User) context.getBean("user");
        System.out.println(user.getName());
    }
}
```

## 代理模式

> 为什么要学代理模式?
>
> 因为这个是SpringAop的底层!	[SpringAop 和SpringMVC]

代理模式的分类

* 静态代理
* 动态代理

### 静态代理

角色分析:

* 抽象角色:一般会使用接口或者抽象类来解决
* 真实角色:被代理的角色
* 代理角色:代理真实角色,代理真实角色之后,一般会做些附属操作
* 客户:访问代理角色的人

代理模式的好处:

* 可以使真实角色的操作更加纯粹,不用去关注一些公共的业务
* 公共交给代理的角色,实现了业务的分工
* 在不改变源代码的时候,使用代理类可以增强原来的效果,实现更多的业务

缺点:

* 一个真实角色会产生一个代理角色;代码量会翻倍,开发效率差点

![image-20210513153956579](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210513153956579.png)

### 动态代理

* 动态代理和静态代理角色一样
* 动态代理的代理类是动态生成的,不是直接写好的
* 动态代理分为两大类:基于接口的动态代理,基于;类的动态代理
  * 基于接口--JDK动态代理
  * 基于类:cglib
  * java字节码实现:javasist

需要了解两个类:proxy:代理,invocationHandler:调用处理程序

动态代理的好处:

* 可以使真实角色的操作更加纯粹,不用去关注一些公共的业务
* 公共的业务也之交给代理角色,实现了业务的分工
* 公共业务发生扩展的话,方便集中管理
* 一个动态代理类代理的是一个接口,一般也就是对应的一类业务
* 一个动态代理类可以代理多个类,只要实现了同一个接口

## AOP

> AOP(Aspect OrientedProgramming)意为:面向切面编程,通过预编译方式和运行期静态代理实现程序功能的统一维护的一种技术.AOP是OOP的延续,是软件开发中的一个热点,也是Spring框架中的一个重要内容,是函数式编程的一种衍生范型.利用AOP可以对业务逻辑的各个部分进行隔离,从而使得业务逻辑各部分之间的耦合度降低,提高程序的可重用性,同时提高了开发的效率

![image-20210513193319041](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210513193319041.png)

![image-20210513193545416](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210513193545416.png)

### 使用Spring实现AOP

![image-20210513194502350](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210513194502350.png)

### 使用XML配置

#### 方式一:使用原生Spring API接口

配置类

```xml
    <bean id="afterLog" class="com.czx.Log.afterLog"/>
    <bean id="log" class="com.czx.Log.log"/>
    <bean id="user" class="com.czx.service.User"/>

    <!--方式一:使用原生Spring API接口-->
    <aop:config>
        <!--切入点: expression:表达式,execution(要执行的位置!(*(修饰词) *(返回值) *(类名) *(方法名) *(参数)-->
        <aop:pointcut id="pointcut" expression="execution(* com.czx.service.User.*(..))"/>
        <!--执行环绕增强-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>

    </aop:config>
```

> pointcut是用来指定要想插入哪个类
>
> advice-ref是你想插入的函数,pointcut-ref是指定要插入的方法

测试类

```java
public class Mytest {
    public static void main(String[] args) {
        ApplicationContext context=new ClassPathXmlApplicationContext("ApplicationContext.xml");
        UserService userservice= context.getBean("user",UserService.class);
        userservice.add();
    }
}
```

#### 方法二:使用自定义切片

```xml
    <!--方式二:使用自定义类-->
    <bean id="diy" class="com.czx.diy.displayPointCut"/>
    <aop:config>
        <!--自定义切面, ref要引用的类-->
        <aop:aspect ref="diy">
            <!--切入点-->
            <aop:pointcut id="point" expression="execution(* com.czx.service.User.*(..))"/>
            <!--通知-->
            <aop:before method="before" pointcut-ref="point"/>
            <aop:after method="after" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>
```

### 注解配置

```xml
    <!--第三种:使用注解方式-->
    <bean id="annotationPointcut" class="com.czx.diy.AnnotationpointCut"/>
    <!--开启注解支持-->
    <aop:aspectj-autoproxy/>
<aop:aspectj-autoproxy proxy-target-class="true"/>
    <!--后面加上了这个变量.使用cglib-->
```

测试类

```java
@Aspect
public class AnnotationpointCut {

    @Before("execution(* com.czx.service.User.*(..))")
    public void before(){
        System.out.println("============方法执行前==========");
    }
    @After("execution(* com.czx.service.User.*(..))")
    public void after(){
        System.out.println("===========方法执行后===========");
    }
    
        @Around("execution(* com.czx.service.User.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable{
        System.out.println("环绕前");
        Signature signature=jp.getSignature();//获得签名
        System.out.println("signatrue"+signature);
        System.out.println("环绕后");
        Object proceed=jp.proceed();//通过这个来判定插入方法的前后
    }
```

# SpringBoot

![image-20210515133623684](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210515133623684.png)

## 微服务架构

​	all in one的架构方式,我们把所有的功能单元放在一个应用里面,然后我们把整个应用部署到服务器上,如果负载能力不行,我们将整个应用进行水平复制.进行扩展,然后在负载均衡

​	所谓微服务架构,打破之前all in one的架构方式,把每个功能元素独立出来,把独立出来的功能元素的动态组合,需要的功能元素才去拿来组合,所以微服务架构是对功能元素进行复制,而没有对整个应用进行复制

​	这样做的好处是:

* 节省了调度资源

* 每个功能元素的服务都是一个可替换的,可独立升级的软件代码

* 阅读这篇文章

  [微服务（Microservices）——Martin Flower - 船长&CAP - 博客园 (cnblogs.com)](https://www.cnblogs.com/liuning8023/p/4493156.html)

## SpringBoot自动装配原理初探

自动装配:

pom.xml:

* spring-boot-dependencies:核心依赖在父工程中
* 我们在写或者引入一些Springboot依赖的时候,不需要指定

启动器

* ```xml
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
  ```

* 启动器:说白了就是springboot的启动场景;

* 比如spring-boot-start-web,帮助我们自动导入web环境下所有的依赖

* springboot将所有的功能场景,都变成一个个的启动器

* 我们需要使用什么功能,只需要找到对应的启动器就可以了:starter

主程序

```java
// @SpringBootApplication:标注这是一个SpringBoot程序
@SpringBootApplication
@RestController
public class SpringbootApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootApplication.class, args);
    }
    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {

        return String.format("Hello %s!", name);
    }

}
```

* 注解

  * ```
    @SpringBootConfiguration	:springboot的配置
    	@Configuration	:spring的配置类
    	@Component	:说明也是一个Spring的组件
    @EnableAutoConfiguration	:自动装配
    	@AutoConfigurationPackage	:自动装配包
    	@Import(AutoConfigurationPackages.Registrar.class)	:自动配置包注册
    	@Import(AutoConfigurationImportSelector.class)		:自动配置导入选择
    //获取所有配置
    	List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
    ```

获取核心的配置

```java
	protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
		List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
				getBeanClassLoader());
		Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
				+ "are using a custom packaging, make sure that file is correct.");
		return configurations;
	}
```

META-INF/spring.factories:自动配置的核心文件

![image-20210515160813426](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210515160813426.png)

结论: springboot所有自动配置都是在启动的时候扫描并加载: spring.factories所有的自动配置类都在这里面,但是不一定会生效,要判断条件是否成立,只要导入了对应的start,就有对应的启动器,有了启动器,我们自动装配就会生效,然后就会配置成功

1. 它在启动的时候,从类路径下/META-INF/spring.factories获取指定的值
2. 将这些自动配置的类导入容器,自动配置就会生效,帮我进行自动配置
3. 以前需要配置的东西,现在springboot帮助我们做了
4. 整合javaEE,解决方案和自动配置的东西都i在spring-boot-autoconfigure-2.2.0.RELEASE.jar
5. 他会导入所有需要导入的组件,以类名的方式返回,这些组件就会被添加到容器
6. 容器中也会存在非常多的xxxAutoConfigure的文件(@Bean),就是这些类给容器中导入了这个场景需要的所有组件,并自动配置,@Configure,javaConfig
7. 有了自动配置,省的我们手动配置



面试可能会问

* 关于SpringBoot 谈谈你的理解:
  * 自动装配
  * run()

## SpringBoot 配置

### yaml语法

* 对空格的要求相当严格

* ```java
  需要在你需要的类上加上这个注解,这样属性的值才能引入进来
  @ConfigurationProperties(prefix = "cat")
  ```

* ```Java
      @Autowired
      private People person;
  // 在启动类 你需要在声明的时候进行一个主动注入,这样值才算真正的注入成功.
  ```

* ```yaml
  // 给你需要的对象设置属性
  person:
    name: "czx"
    cat:
      name: "喵呜"
      breed: "短尾猫"
    age: 21
    happy: true
    birth: "2000/5/15"
    maps: {k1: czx,k2: zsw,k3: zdy,k4: czp}
    lists:
      - qwe3
      - czx1
      - zsw2
      - czp3
      - zdy4
  ```

* JSR303校验(自己去了解)

* 可以在多个位置设置yaml文件

  > 1. `optional:classpath:/`
  > 2. `optional:classpath:/config/`
  > 3. `optional:file:./`
  > 4. `optional:file:./config/`
  > 5. `optional:file:./config/*/`
  > 6. `optional:classpath:custom-config/`
  > 7. `optional:file:./custom-config/`

* 可以设置多个配置环境

  > 如果是以.prpperties配置
  >
  > 名字命名以application-xxx.properties
  >
  > 激活在主配置文件中以
  >
  > spring.profiles.active=xxx
  >
  > 去激活

* > 在YAML文件中
  >
  > 只需要---就能实现多配置

# SpringBootWeb开发

## 模板引擎Thymeleaf

* 只要需要使用thymeleaf,只需要导入对应的依赖就可以了,我们将html放在我们的template目录下

在thymeleaf中导入css文件

![image-20210517165242746](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20210517165242746.png)

# 



