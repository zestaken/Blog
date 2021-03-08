---
title: SpringMVC
date: 2021-03-04 09:35:32
tags:
---

# SpringMVC简介

[官方文档](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#spring-web)
* SpringMVC是一个web框架，围绕`DispatcherServlet`设计；
* DispacherServelt的作用是将请求分发到不同的处理器。
  * DispatcherServlet是一个实际的Servlet，它继承自HttpServlet类。
* SpringMVC和许多其他的MVC框架一样，以请求为驱动，围绕一个中心servlet分派请求及提供其他功能。
* 传统MVC架构：
  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307210022.png)

# SpringMVC执行原理

* SpringMVC核心架构：
  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307210107.png)

# 快速入门

1. 建立一个web支持的项目；
2. 配置maven的资源过滤问题：
```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```
3. 导入相关依赖，主要是`spring-webmvc`
```xml
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.3</version>
    </dependency>
```
4. 配置web.xml
   * web.xml的版本要4.0及以上；
   * 在项目结构中，将maven导入的依赖，全部导入到artifacts的依赖中去。
   * 注册DispatchServlet,管理SpringMVC配置文件，设置启动级别为1，映射路径为`/`
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">

        <!-- 注册servlet -->
        <servlet>
            <servlet-name>SpringMVC</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>、
            <!-- 通过初始化参数指定SpringMVC配置文件的位置，进行关联 -->
            <init-param>
                <param-name>contextConfigLocation</param-name>
                <param-value>classpath:springmvc-servlet.xml</param-value>
            </init-param>
            <!-- 启动顺序，数字越小，启动越早 -->
            <load-on-startup>1</load-on-startup>
        </servlet>

        <!-- 所有请求都会被springmvc拦截 -->
        <servlet-mapping>
            <servlet-name>SpringMVC</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
    </web-app>
  ```
5. 配置Springmvc-servlet.xml(web.xml关联的springmvc配置文件，放在resouce目录下)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
            https://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">


    <context:annotation-config/>
    <!--    自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
    <context:component-scan base-package="com.zestaken.controller"/>
    <!--    让springmvc不处理静态资源，如.css .js .html .mp3 .mp4-->
        <mvc:default-servlet-handler/>

    <!--    支持mvc注解驱动-->
        <mvc:annotation-driven/>

    <!--    配置视图解析器-->
        <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
            id="internalResourceViewResolver">
    <!--        前缀-->
            <property name="prefix" value="/WEB-INF/jsp/"/>
    <!--        后缀-->
            <property name="suffix" value=".jsp"/>
        </bean>
</beans>
```
   * 在视图解析器中，将所有的视图都放在**/WEB-INF/**目录下，这样可以保证视图安全，因为这个目录下的文件，客户端不能直接访问。
6. 创建controller：
```java
package com.zestaken.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/HelloController")
public class HelloController {
    
    //真实访问地址就是：项目名/HelloController/hello1
    @RequestMapping("/hello1")
    public String sayHello(Model model) {
        //向模型中添加属性msg与值，可以在jsp页面中取出并渲染
        model.addAttribute("msg", "hello, springmvc");
        //返回值代表视图：WEB-INF/jsp/hello.jsp
        return "hello";
    }
}
```
   * `@Controller`是为了让Spring IOC容器自动扫描到；被这个注解的类中的所有方法，如果返回值是String，并且有具体的页面可以操作，那么就会被视图解析器解析。#
   * `@ResquestMapping`是为了映射请求路径，这里因为类与方法上都有映射，所以访问时应该是`HelloController/hello`(类上的映射可以不写)
   * 方法中声明的Model类型的参数是为了把Action中的数据带到视图层中；
   * 方法返回的结果是视图的名称hello，加上==配置文件中的前后缀==变成WEB-INF/jsp/hello.jsp
7. 创建视图层：
   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
    <h1>${msg}</h1>
    </body>
    </html>
   ```
8. 启动tomcat，访问/HelloController/hello1。
   ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210307221352.png)

# Restful风格

* Restful风格：一种软件架构风格、设计风格，而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。
* REST即Representational State Transfer的缩写，可译为"表现层状态转化”。REST最大的几个特点为：资源、统一接口、URI和无状态。
* 资源：互联网所有的事物都可以被抽象为资源 。
* 资源操作：使用POST、DELETE、PUT、GET，使用不同方法对资源进行操作。 
分别对应 添加、 删除、修改、查询。 
* 传统方式操作资源：通过不同的参数来实现不同的效果，方法单一，都是GET或者POST。
```
http://127.0.0.1/item/queryUser.action?id=1   查询,GET 
http://127.0.0.1/item/saveUser.action             新增,POST 
http://127.0.0.1/item/updateUser.action          更新,POST 
http://127.0.0.1/item/deleteUser.action?id=1  删除,GET或POST
```
* 使用RESTful操作资源 :
  * 通过不同的请求方法来实现不同的效果。请求的地址一样，但是因为请求的方式不同，实现的功能不同。
    * 可以通过 GET、 POST、 PUT、 PATCH、 DELETE 等方式对服务端的资源进行操作。其中，GET 用于查询资源，POST 用于创建资源，PUT 用于更新服务端的资源的全部信息，PATCH 用于更新服务端的资源的部分信息，DELETE 用于删除服务端的资源。
  * 同时隐藏了参数的传递，直接将参数写入到地址中，隐藏了参数名。
```
【GET】 /users # 查询用户信息列表

【GET】 /users/1001 # 查看某个用户信息（其中1001就是要用到方法中的参数）

【POST】 /users # 新建用户信息

【PUT】 /users/1001 # 更新用户信息(全部字段)

【PATCH】 /users/1001 # 更新用户信息(部分字段)

【DELETE】 /users/1001 # 删除用户信息
```
* 传统方法实现示例：
```java
package com.zestaken.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {

    @RequestMapping("/hello1")
    public String sayHello(int a, int b,Model model) {
        int res = a + b;
        model.addAttribute("msg", "输出结果为："+res);
        return "hello";
    }
}
```
  * 请求这个方法的路径：`http://localhost:8080/SpringMVC_war_exploded/hello1?a=1&b=2`
* Restful风格实现示例：
```java
package com.zestaken.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class HelloController {

//    @RequestMapping(value = "/hello1/{a}/{b}",method = RequestMethod.GET)
    @GetMapping("/hello/{a}/{b}")
    public String GETHello(@PathVariable int a, @PathVariable int b, Model model) {
        int res = a - b;
        model.addAttribute("msg", "GET输出结果为："+res);
        return "hello";
    }

    @PostMapping("/hello/{b}/{a}")
    public String POSTHello(@PathVariable int a, @PathVariable int b, Model model) {
        int res = a - b;
        model.addAttribute("msg", "POST输出结果为："+res);
        return "hello";
    }
}
}
```
  * 将参数的传递放到路径中去：
    * 方法的参数必须加上`@PathVariable`注解
    * 方法的路径中，必须对应方法的参数(名称相同，`{a}`对应参数`int a`)，并且用花括号括起来。
  * 限制不同的请求方法，只能使用不同的方法
    * 一种方法是给`@RequestMapping`注解加上method参数
    * 一种方法是使用对应请求方法特有的map注解,如，GEI方法对应的`@GETMapping`注解。
  * 请求GETHello的请求路径：`http://localhost:8080/SpringMVC_war_exploded/hello/1/2`
    * 路径中的参数必须与参数的类型对应。
    * 请求生效必须采用GET方法。


