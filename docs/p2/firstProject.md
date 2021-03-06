# 2. run the first project

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.2.1.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.lin</groupId>
	<artifactId>missyou</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>missyou</name>
	<description>Demo project for Spring Boot</description>

```

- version `2.2.1`

---

## how to change port

- `application.properties`

```java
server.port = 8081
```

- run springboot project

- 其实用 spirngboot 框架开发应用是非常快的，比很多框架都快，比python php 还要快

- 现在开始配置`api`， 用来写springboot 路由`route`

![](img/2020-05-08-00-02-33.png)

- 之所以创建两个版本api, 因为客户端也有可能老用户不更新版本还在用之前的版本

![](img/2020-05-08-00-04-25.png)

- 我们写了这样一个class

```java
package com.lin.missyou.api.v1;

public class BannerController {
    //MVC SpringMVC
    //Controller Model View

    public String test(){
        return "Hello World!";
    }
}
```

- 无论写多少个，springboot 都不会管你，但是如果要让前端访问这个method, 那就必须接受springboot 管理



---

## ResponseBody

- 尽管class name 是 controller, 但是只是普通类，想要让springboot 识别就必须

- run 

![](img/2020-05-08-00-23-22.png)

- 由于我们之前已经配置到 `8081` 端口

- 我们需要引入一个 `HttpServletResponse` 
- 同时给 BannerController 上面加上 @Contoller, 不打上标识就变成了普通的类，就没有意义。

```java
@Controller
public class BannerController {
    //MVC SpringMVC
    //Controller Model View

    @GetMapping("/test")
    public void test(HttpServletResponse response){
        try {
            response.getWriter().write("Hello World!");
        } catch (IOException e) {
            e.printStackTrace();
        }
//        return "Hello World!";
    }
}
```

![](img/2020-05-08-00-29-26.png)


## `ResponseBody` 简化 `ServletResponse`

- `ResponseBody` 还可以写中文格式, 解决编码问题

```java
@Controller
public class BannerController {
    //MVC SpringMVC
    //Controller Model View

    @GetMapping("/test")
    @ResponseBody
    public String test(){
//            response.getWriter().write("Hello World!");

    //response header text/plain
    //application/json
    //POSTMAN
    //Junit test
        return "Hello World!";
    }
}

```

- 同时，responsebody 还可以解决中文编码问题

![](img/2020-05-08-00-35-52.png)

---


## 热启动


- `pom.xml` 里替换成 `<version>2.2.2.RELEASE</version>`


```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
```

- 添加以上这段到 pom.xml


![](img/2021-01-04-13-25-56.png)

- 同时build automatically

---

## RESTful API

- `@RestController` 包含了 `Controller` and `ResponseBody`



