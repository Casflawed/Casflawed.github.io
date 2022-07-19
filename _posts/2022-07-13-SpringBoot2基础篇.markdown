---
title: SpringBoot2基础篇
date: 2022-07-12 +/-TTTT
categories: [框架, SpringBoot]
tags: []     # TAG names should always be lowercase
---

# 前言
本笔记依照黑马视频链接：<br>
[黑马SpringBoot](https://www.bilibili.com/video/BV15b4y1a7yG?spm_id_from=333.999.0.0&vd_source=ac4c81d3d3ecffb8a040265405d786b8)

我的IDEA版本：IntelliJ IDEA 2020.1(Ultimate Editon)

# SpringBoot概述
SpringBoot是由Pivotal团队提供的全新框架，其设计目的是用来简化Spring应用的初始搭建以及开发过程

# 新建SpringBoot工程
1.创建新模块，选择Spring Initializr，并配置模块相关基础信息

![img](https://img-blog.csdnimg.cn/0839ab0b92fc4deea70e706e84c9a27d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

2.选择当前模块需要使用的技术集

![img](https://img-blog.csdnimg.cn/5108acf698f8423aa6d0ecc73f133a4e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

3.开发控制器类

```java
//Rest 模式
@RestController
@RequestMapping("/books")
public class BookController {
   
    @GetMapping
    public String getById() {
   
        System.out.println("springboot is running...");
        return "springboot is running...";
    }
}
```

4.运行自动生成的Application类

![img](https://img-blog.csdnimg.cn/e0d7e6b7371845e8a91aa6aebaccc94c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

5.打开浏览器访问url地址为：http://localhost:8080/books

![img](https://img-blog.csdnimg.cn/163c4ae2c0c0411a92cad10009683141.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

## 工程文件介绍
最简SpringBoot程序所包含的基础文件 (pom.xml文件 和 Application类 ) 

1.pom.xml文件 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.6</version>
    </parent>
    <groupId>com.example</groupId>
    <artifactId>springboot-01-quickstart</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

2.Application类

```java
@SpringBootApplication
public class Springboot0101QuickstartApplication {
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot0101QuickstartApplication.class, args);
    }
}
```

Spring程序与SpringBoot程序对比<br>
![img](https://img-blog.csdnimg.cn/414b7f3210694d5a8686a62ae4f9feff.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

**注意: 基于idea开发SpringBoot程序需要确保联网且能够加载到程序框架结构**

## IDEA的SpringBoot工程中隐藏不常用的文件
如以.mvn、.gitignore、HELP.md、mvnw、mvnw.cmd、.iml为后缀的文件，我们再开发的时候通常不会修改其中的内容，这个时候觉得这些文件碍眼可以选择再IDEA中隐藏它们 
![不常修改文件](/blog/202207151533521.png "不常修改文件")

处理方法：<br>
![处理方法](/blog/202207151622151.png  "处理方法")




![img](https://img-blog.csdnimg.cn/7cc7cea23a274189855c039ea6c8613a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

- parent

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.6</version>
    </parent>
    <groupId>com.example</groupId>
    <artifactId>springboot-01-quickstart</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

按住Ctrl点击pom.xml中的spring-boot-starter-parent，跳转到了spring-boot-starter-parent的pom.xml，xml配置如下（只摘抄了部分重点配置）：

```java
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.5.6</version>
  </parent>
```

按住Ctrl点击pom.xml中的spring-boot-starter-dependencies，跳转到了spring-boot-starter-dependencies的pom.xml，xml配置如下（只摘抄了部分重点配置）：

```java
<properties>
  	<activemq.version>5.15.3</activemq.version>
  	<antlr2.version>2.7.7</antlr2.version>
  	<appengine-sdk.version>1.9.63</appengine-sdk.version>
  	<artemis.version>2.4.0</artemis.version>
  	<aspectj.version>1.8.13</aspectj.version>
  	<assertj.version>3.9.1</assertj.version>
  	<atomikos.version>4.0.6</atomikos.version>
  	<bitronix.version>2.1.4</bitronix.version>
  	<build-helper-maven-plugin.version>3.0.0</build-helper-maven-plugin.version>
  	<byte-buddy.version>1.7.11</byte-buddy.version>
  	... ... ...
</properties>
<dependencyManagement>
  	<dependencies>
      	<dependency>
        	<groupId>org.springframework.boot</groupId>
        	<artifactId>spring-boot</artifactId>
        	<version>2.0.1.RELEASE</version>
      	</dependency>
      	<dependency>
        	<groupId>org.springframework.boot</groupId>
        	<artifactId>spring-boot-test</artifactId>
        	<version>2.0.1.RELEASE</version>
      	</dependency>
      	... ... ...
	</dependencies>
</dependencyManagement>
<build>
  	<pluginManagement>
    	<plugins>
      		<plugin>
        		<groupId>org.jetbrains.kotlin</groupId>
        		<artifactId>kotlin-maven-plugin</artifactId>
        		<version>${kotlin.version}</version>
      		</plugin>
      		<plugin>
        		<groupId>org.jooq</groupId>
        		<artifactId>jooq-codegen-maven</artifactId>
        		<version>${jooq.version}</version>
      		</plugin>
      		<plugin>
        		<groupId>org.springframework.boot</groupId>
        		<artifactId>spring-boot-maven-plugin</artifactId>
        		<version>2.0.1.RELEASE</version>
      		</plugin>
          	... ... ...
    	</plugins>
  	</pluginManagement>
</build>
```

从上面的spring-boot-starter-dependencies的pom.xml中我们可以发现，一部分坐标的版本、依赖管理、插件管理已经定义好，所以我们的SpringBoot工程继承spring-boot-starter-parent后已经具备版本锁定等配置了。所以起步依赖的作用就是进行依赖的传递。

小结:

1. 开发SpringBoot程序要继承spring-boot-starter-parent 
2. spring-boot-starter-parent中定义了若干个依赖管理 
3. 继承parent模块可以避免多个依赖使用相同技术时出现依赖版本冲突 
4. 继承parent的形式也可以采用引入依赖的形式实现效果


- spring-boot-starter-web.pom 按住Ctrl点击pom.xml中的spring-boot-starter-web，跳转到了spring-boot-starter-web的pom.xml，xml配置如下（只摘抄了部分重点配置）：

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd" xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  	<modelVersion>4.0.0</modelVersion>
  	<parent>
    	<groupId>org.springframework.boot</groupId>
    	<artifactId>spring-boot-starters</artifactId>
    	<version>2.0.1.RELEASE</version>
  	</parent>
  	<groupId>org.springframework.boot</groupId>
  	<artifactId>spring-boot-starter-web</artifactId>
  	<version>2.0.1.RELEASE</version>
  	<name>Spring Boot Web Starter</name>
  
  	<dependencies>
    	<dependency>
      		<groupId>org.springframework.boot</groupId>
      		<artifactId>spring-boot-starter</artifactId>
      		<version>2.0.1.RELEASE</version>
      		<scope>compile</scope>
    	</dependency>
    	<dependency>
      		<groupId>org.springframework.boot</groupId>
      		<artifactId>spring-boot-starter-json</artifactId>
      		<version>2.0.1.RELEASE</version>
      		<scope>compile</scope>
    	</dependency>
    	<dependency>
      		<groupId>org.springframework.boot</groupId>
      		<artifactId>spring-boot-starter-tomcat</artifactId>
      		<version>2.0.1.RELEASE</version>
      		<scope>compile</scope>
    	</dependency>
    	<dependency>
      		<groupId>org.hibernate.validator</groupId>
      		<artifactId>hibernate-validator</artifactId>
      		<version>6.0.9.Final</version>
      		<scope>compile</scope>
    	</dependency>
    	<dependency>
      		<groupId>org.springframework</groupId>
      		<artifactId>spring-web</artifactId>
      		<version>5.0.5.RELEASE</version>
      		<scope>compile</scope>
    	</dependency>
    	<dependency>
      		<groupId>org.springframework</groupId>
      		<artifactId>spring-webmvc</artifactId>
      		<version>5.0.5.RELEASE</version>
      		<scope>compile</scope>
    	</dependency>
  	</dependencies>
</project>
```


从上面的spring-boot-starter-web的pom.xml中我们可以发现，spring-boot-starter-web就是将web开发要使用的spring-web、spring-webmvc等坐标进行了“打包”，这样我们的工程只要引入spring-boot-starter-web起步依赖的坐标就可以进行web开发了，同样体现了依赖传递的作用。 ![img](https://img-blog.csdnimg.cn/fa715bd348524022b66380523392144f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

- starter SpringBoot中常见项目名称，定义了当前项目使用的所有依赖坐标，以达到减少依赖配置的目的 
- parent 所有SpringBoot项目要继承的项目，定义了若干个坐标版本号（依赖管理，而非依赖），以达到减少依赖冲突的目的 spring-boot-starter-parent各版本间存在着诸多坐标版本不同 
- 实际开发 使用任意坐标时，仅书写GAV(groupId, artifactId, version)中的G和A，V由SpringBoot提供，除非SpringBoot未提供对应版本V 如发生坐标错误，再指定Version（要小心版本冲突）

小结:

1. 开发SpringBoot程序需要导入坐标时通常导入对应的starter 
2. 每个不同的starter根据功能不同，通常包含多个依赖坐标 
3. 使用starter可以实现快速配置的效果，达到简化配置的目的


- 启动方式

```java
@SpringBootApplication
public class Springboot0101QuickstartApplication {
   

    public static void main(String[] args) {
   
        ConfigurableApplicationContext ctx = SpringApplication.run(Springboot0101QuickstartApplication.class, args);
        //获取bean对象
        BookController bean = ctx.getBean(BookController.class);
        System.out.println("bean======>" + bean);
    }
}
```

- SpringBoot的引导类是Boot工程的执行入口，运行main方法就可以启动项目 
- SpringBoot工程运行后初始化Spring容器，扫描引导类所在包加载bean

小结:

1. SpringBoot工程提供引导类用来启动程序 
2. SpringBoot工程启动后创建并初始化Spring容器



- 辅助功能 内嵌tomcat ![img](https://img-blog.csdnimg.cn/98a74e208b8242dfa4cce4a9dddf466f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 
- 使用maven依赖管理变更起步依赖项

```java
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <!--web 起步依赖环境中，排除 Tomcat 起步依赖 -->
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-tomcat</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <!-- 添加 Jetty 起步依赖，版本由 SpringBoot 的 starter 控制 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jetty</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

- Jetty比Tomcat更轻量级，可扩展性更强（相较于Tomcat），谷歌应用引擎（GAE）已经全面切换为Jetty 
- 内置服务器 tomcat(默认) apache出品，粉丝多，应用面广，负载了若干较重的组件 jetty 更轻量级，负载性能远不及tomcat undertow undertow，负载性能勉强跑赢tomcat

小结:

1. 内嵌Tomcat服务器是SpringBoot辅助功能之一 
2. 内嵌Tomcat工作原理是将Tomcat服务器作为对象运行，并将该对象交给Spring容器管理 
3. 变更内嵌服务器思想是去除现有服务器，添加全新的服务器

## 总结:

1. 入门案例（4种方式） 
2. SpringBoot概述 parent starter 引导类 辅助功能（内嵌tomcat）


1.  什么是 rest ： 
 <ul> 
  1.  REST（Representational State Transfer）表现形式状态转换  
  1.  传统风格资源描述形式 http://localhost/user/getById?id=1 (得到id为1的用户) http://localhost/user/saveUser (保存用户)  
  1.  REST风格描述形式 http://localhost/user/1 (得到id为1的用户) http://localhost/user (保存用户)  
 </ul>  
5.  优点: 
 <ul> 
  5. 隐藏资源的访问行为， 无法通过地址得知对资源是何种操作 
  5. 书写简化 
 </ul>  
8.  按照REST风格访问资源时使用行为动作区分对资源进行了何种操作 GET 用来获取资源，POST 用来新建资源，PUT 用来更新资源，DELETE 用来删除资源 
 <ul> 
  8. http://localhost/users 查询全部用户信息 GET (查询) 
  8. http://localhost/users/1 查询指定用户信息 GET (查询) 
  8. http://localhost/users 添加用户信息 POST (新增/保存) 
  8. http://localhost/users 修改用户信息 PUT (修改/更新) 
  8. http://localhost/users/1 删除用户信息 DELETE (删除) 
 </ul> 注意: 上述行为是约定方式，约定不是规范，可以打破，所以称REST风格，而不是REST规范 描述模块的名称通常使用复数，也就是加s的格式描述，表示此类资源,而非单个资源，例如: users、 books、 accounts…  
14.  根据REST风格对资源进行访问称为RESTful  
15.  小结： 
 <ol> 
  15. REST 
  15. 动作4个 
  15. RESTful 
 </ol> 


步骤:

①:设定http请求动作(动词)

使用 @RequestMapping 注解的 method 属性声明请求的方式

使用 @RequestBody 注解 获取请求体内容。直接使用得到是 key=value&amp;key=value…结构的数据。get 请求方式不适用。

使用@ResponseBody 注解实现将 controller 方法返回对象转换为 json 响应给客户端。

@RequestMapping(value="/users",method=RequestMethod.POST)


![img](https://img-blog.csdnimg.cn/img_convert/8fc4afea23a513d605b885db910e2ac8.png)

②:设定请求参数(路径变量)

使用@PathVariable 用于绑定 url 中的占位符。例如：请求 url 中 /delete/{id}，这个{id}就是 url 占位符。


![img](https://img-blog.csdnimg.cn/img_convert/d35b1e484bae94e8f5b5c5804610afbe.png)

- @RequestMapping


![img](https://img-blog.csdnimg.cn/img_convert/1b6cff3e21c9f8f39d03609ca5549dc5.png)

- @PathVariable


![img](https://img-blog.csdnimg.cn/img_convert/70f82ea4f1c61a34eb68fda48cc9ada3.png)

- @RequestBody @RequestParam @PathVariable


![img](https://img-blog.csdnimg.cn/img_convert/9b9324456b495d978751d23ce868c101.png)


- 使用 @RestController 注解开发 RESTful 风格


![img](https://img-blog.csdnimg.cn/img_convert/e7b67442721c662525b77651f8c60f11.png)

- 使用 @GetMapping @PostMapping @PutMapping @DeleteMapping 简化 @RequestMapping 注解开发


![img](https://img-blog.csdnimg.cn/img_convert/5c4f5989f8975d8c058a2038752b528b.png)







- 原则 保留工程基础结构 抹掉原始工程痕迹 ![img](https://img-blog.csdnimg.cn/c6454eaca62a4b849a40c9a57b82f06a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/b0eba06b936d4243b47b6faaf3842e95.png) ![img](https://img-blog.csdnimg.cn/img_convert/5f36f2235926f2a2a7aa521a850a7109.png) 在IDEA 中点击模块管理添加模块 ![img](https://img-blog.csdnimg.cn/img_convert/e77f0a788b783f52d3e5af7551d79964.png) ![img](https://img-blog.csdnimg.cn/img_convert/e4df792ceb5e646c193f40c545cd58cd.png)

小结:

1. 在工作空间中复制对应工程，并修改工程名称 
2. 删除与Idea相关配置文件，仅保留src目录与pom.xml文件 
3. 修改pom.xml文件中的artifactId与新工程/模块名相同 
4. 删除name标签（可选） 
5. 保留备份工程供后期使用



- 修改服务器端口 ![img](https://img-blog.csdnimg.cn/e6418b08801140318e071b8775b4898c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 
- SpringBoot默认配置文件application.properties，通过键值对配置对应属性 
- 修改配置 修改服务器端口# 服务器端口配制
server.port=80 小结:

1. SpringBoot默认配置文件application.properties


1. 修改配置 修改服务器端口 server.port=80 关闭运行日志图标（banner） spring.main.banner-mode=off 设置日志相关 logging.level.root=debug

```java
# 服务器端口配置
server.port=80

# 修改banner
# spring.main.banner-mode=off
# spring.banner.image.location=logo.png

# 日志
logging.level.root=info
```

1. SpringBoot内置属性查询 https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties 官方文档中参考文档第一项：Application Propertie

小结:

1. SpringBoot中导入对应starter后，提供对应配置属性 
2. 书写SpringBoot配置采用关键字+提示形式书写



- 配置文件格式 ![img](https://img-blog.csdnimg.cn/36a410c00f9e42c89f24bdf75b0f48d5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 
- SpringBoot提供了多种属性配置方式

1. application.properties

```java
server.port=80
```

1. application.yml

```java
server:
  port: 81
```

1. application.yaml

```java
server:
  port: 82
```


![img](https://img-blog.csdnimg.cn/76cb70b654bc412f8f46c7dd19a8d1e0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结:

1. SpringBoot提供了3种配置文件的格式 properties（传统格式/默认格式） **yml（主流格式）** yaml


- SpringBoot配置文件加载顺序 application.properties &gt; application.yml &gt; application.yaml 
- 常用配置文件种类 application.yml

小结:

1. 配置文件间的加载优先级 properties（最高） yml yaml（最低） 
2. 不同配置文件中相同配置按照加载优先级相互覆盖 (**高优先级配置内容会覆盖低优先级配置内容**)，不同配置文件中不同配置全部保留




![img](https://img-blog.csdnimg.cn/cdea13a6b8514c51a842920f8516b73f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/505e5dd390a940aaac58ea8552c53d08.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 小结:

1. 指定SpringBoot配置文件 Setting → Project Structure → Facets 选中对应项目/工程 Customize Spring Boot 选择配置文件


## yaml

- YAML（YAML Ain’t Markup Language），一种数据序列化格式

1.  优点： 
 <ul> 
  1. 容易阅读 
  1. 容易与脚本语言交互 
  1. 以数据为核心，重数据轻格式 
 </ul>  
5.  YAML文件扩展名 
 <ul> 
  5. .yml（**主流**） 
  5. .yaml 
 </ul> 

## yaml语法规则

### 基本语法

- key: value -&gt; **value** 前面一定要有**空格** 
- 大小写**敏感** 
- 属性层级关系使用多行描述，每行结尾使用冒号结束 
- 使用**缩进**表示层级关系，同层级**左侧对齐**，只允许使用**空格**（不允许使用Tab键） 
- 属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔） 
- # 表示注释
- 核心规则：**数据前面要加空格与冒号隔开**

```java
server:
  servlet:
    context-path: /hello
  port: 82
```

### 数据类型


- 字面值表示方式 ![img](https://img-blog.csdnimg.cn/8adfbf4c27ca407d8567716e62f8e83c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
# 字面值表示方式

boolean: TRUE       #TRUE,true,True,FALSE,false ， False 均可
float: 3.14         #6.8523015e+5 # 支持科学计数法
int: 123            #0b1010_0111_0100_1010_1110 # 支持二进制、八进制、十六进制
# null: ~             # 使用 ~ 表示 null
string: HelloWorld  # 字符串可以直接书写
string2: "Hello World"  # 可以使用双引号包裹特殊字符
date: 2018-02-17        # 日期必须使用 yyyy-MM-dd 格式
datetime: 2018-02-17T15:02:31+08:00   # 时间和日期之间使用 T 连接，最后使用 + 代表时区
```


- 数组表示方式：在属性名书写位置的下方使用减号作为数据开始符号，每行书写一个数据，减号与数据间空格分隔 ![img](https://img-blog.csdnimg.cn/516176cc575049a4b41d3353100f26b1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
subject:
  - Java
  - 前端
  - 大数据

enterprise:
  name: zhangsan
  age: 16

subject2:
  - Java
  - 前端
  - 大数据
likes: [王者荣耀,刺激战场] # 数组书写缩略格式


users: # 对象数组格式
  - name: Tom
    age: 4

  - name: Jerry
    age: 5
users2: # 对象数组格式二
  -
    name: Tom
    age: 4
  -
    name: Jerry
    age: 5

# 对象数组缩略格式
users3: [ {
    name:Tom , age:4 } , {
    name:Jerry , age:5 } ]
```

小结:

```java
1. yaml语法规则
	大小写敏感
	属性层级关系使用多行描述，每行结尾使用冒号结束
	使用缩进表示层级关系，同层级左侧对齐，只允许使用空格（不允许使用Tab键）
	属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔）
	# 表示注释
2. 注意属性名冒号后面与数据之间有一个空格
3. 字面值、对象数据格式、数组数据格式（略）
```



- 使用@Value读取单个数据，属性名引用方式：${一级属性名.二级属性名……} ![img](https://img-blog.csdnimg.cn/18fece154b904361b4504388b8eddf86.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
@Value("${country}")
    private String country1;

    @Value("${user.age}")
    private String age1;

    @Value("${likes[1]}")
    private String likes1;

    @Value("${users[1].name}")
    private String name1;


    @GetMapping
    public String getById() {
   
        System.out.println("springboot is running2...");
        System.out.println("country1=>" + country1);
        System.out.println("age1=>" + age1);
        System.out.println("likes1=>" + likes1);
        System.out.println("name1=>" + name1);
        return "springboot is running2...";
    }
```

小结:

1. 使用@Value配合SpEL读取单个数据 
2. 如果数据存在多层级，依次书写层级名称即可


-  在配置文件中可以使用属性名引用方式引用属性  
-  属性值中如果出现转移字符，需要使用双引号包裹 

小结:

1. 在配置文件中可以使用${属性名}方式引用属性值 
2. 如果属性中出现特殊字符，可以使用双引号包裹起来作为字符解析




- 封装全部数据到Environment对象 
- 注意 要导这个 包 
- **import org.springframework.core.env.Environment;** ![img](https://img-blog.csdnimg.cn/ed4baa57eda34773b40c3a97422a81e9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/1700017907384046addf32a0e2415f3a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结:

1. 使用Environment对象封装全部配置信息 
2. 使用@Autowired自动装配数据到Environment对象中




- 自定义对象封装指定数据 ![img](https://img-blog.csdnimg.cn/2ca987772d7f43f394abf299eacccf3d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 
- 自定义对象封装指定数据的作用 ![img](https://img-blog.csdnimg.cn/c3dc819fbfc64fbabeacf0e6536ff9d5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
# 创建类，用于封装下面的数据
# 由spring帮我们去加载数据到对象中，一定要告诉spring加载这组信息
# 使用时候从spring中直接获取信息使用

datasource:
  driver: com.mysql.jdbc.Driver
  url: jdbc:mysql://localhost/springboot_db
  username: root
  password: root666123
```

```java
//1.定义数据模型封装yaml文件中对应的数据
//2.定义为spring管控的bean
@Component
//3.指定加载的数据
@ConfigurationProperties(prefix = "datasource")
public class MyDataSource {
   

    private String driver;
    private String url;
    private String username;
    private String password;
	
	//省略get/set/tostring 方法
}
```

使用自动装配封装指定数据

```java
@Autowired
 private MyDataSource myDataSource;
```

输出查看

```java
System.out.println(myDataSource);
```

小结:

1. 使用@ConfigurationProperties注解绑定配置信息到封装类中 
2. 封装类需要定义为Spring管理的bean，否则无法进行属性注入


- 添加Junit的起步依赖 Spring Initializr 创建时自带

```java
<!--测试的起步依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

- SpringBoot整合JUnit

```java
@SpringBootTest
class Springboot07JunitApplicationTests {
   
	@Autowired
	private BookService bookService;
	@Test
	public void testSave(){
   
		bookService.save();
	}
}
```

- @SpringBootTest 名称：@SpringBootTest 类型：测试类注解 位置：测试类定义上方 作用：设置JUnit加载的SpringBoot启动类 范例：

```java
@SpringBootTest
class Springboot05JUnitApplicationTests {
   }
```

小结:

1. 导入测试对应的starter 
2. 测试类使用@SpringBootTest修饰 
3. 使用自动装配的形式添加要测试的对象



![img](https://img-blog.csdnimg.cn/a5ff949c6b094e57b7510b1352b53926.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
@SpringBootTest(classes = Springboot04JunitApplication.class)
//@ContextConfiguration(classes = Springboot04JunitApplication.class)
class Springboot04JunitApplicationTests {
   
    //1.注入你要测试的对象
    @Autowired
    private BookDao bookDao;

    @Test
    void contextLoads() {
   
        //2.执行要测试的对象对应的方法
        bookDao.save();
        System.out.println("two...");
    }

}
```

注意:

- 如果测试类在SpringBoot启动类的包或子包中，可以省略启动类的设置，也就是省略classes的设定

小结:

1. 测试类如果存在于引导类所在包或子包中无需指定引导类 
2. 测试类如果不存在于引导类所在的包或子包中需要通过 classes 属性指定引导类




①：创建新模块，选择Spring初始化，并配置模块相关基础信息 ![img](https://img-blog.csdnimg.cn/a0b3488f2acf47ba84e4ea2aed8ec631.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ②：选择当前模块需要使用的技术集（MyBatis、MySQL） ![img](https://img-blog.csdnimg.cn/a22c35c2d7b04746aca34fd386b10c64.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ③：设置数据源参数

```java
#DB Configuration:
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springboot_db
    username: root
    password: 123456
```

④：创建user表 在 springboot_db 数据库中创建 user 表

```java
-- ----------------------------
-- Table structure for `user`
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) DEFAULT NULL,
  `password` varchar(50) DEFAULT NULL,
  `name` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of user
-- ----------------------------
INSERT INTO `user` VALUES ('1', 'zhangsan', '123', '张三');
INSERT INTO `user` VALUES ('2', 'lisi', '123', '李四');
```

⑤：创建实体Bean

```java
public class User {
   
    // 主键
    private Long id;
    // 用户名
    private String username;
    // 密码
    private String password;
    // 姓名
    private String name;
  
    //此处省略getter,setter,toString方法 .. ..
    
}
```

⑥: 定义数据层接口与映射配置

```java
@Mapper
public interface UserDao {
   

    @Select("select * from user")
    public List<User> getAll();
}
```

⑦：测试类中注入dao接口，测试功能

```java
@SpringBootTest
class Springboot05MybatisApplicationTests {
   

    @Autowired
    private UserDao userDao;

    @Test
    void contextLoads() {
   
        List<User> userList = userDao.getAll();
        System.out.println(userList);
    }

}
```

⑧：运行如下

```java
[User{
   id=1, username='zhangsan', password='123', name='张三'}, User{
   id=2, username='lisi', password='123', name='李四'}]
```

总结:

1. 勾选MyBatis技术，也就是导入MyBatis对应的starter 
2. 数据库连接相关信息转换成配置 
3. 数据库SQL映射需要添加@Mapper被容器识别到


SpringBoot版本低于2.4.3(不含)，Mysql驱动版本大于8.0时，需要在url连接串中配置时区

```java
jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
```

或在MySQL数据库端配置时区解决此问题

1.MySQL 8.X驱动强制要求设置时区

- 修改url，添加serverTimezone设定 
- 修改MySQL数据库配置（略）

2.驱动类过时，提醒更换为com.mysql.cj.jdbc.Driver



![img](https://img-blog.csdnimg.cn/c93496840bd44dcb9b754368fc65b8c7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ①：手动添加SpringBoot整合MyBatis-Plus的坐标，可以通过mvnrepository获取

```java
<dependency>
       <groupId>com.baomidou</groupId>
       <artifactId>mybatis-plus-boot-starter</artifactId>
       <version>3.4.3</version>
   </dependency>
```

注意事项: 由于SpringBoot中未收录MyBatis-Plus的坐标版本，需要指定对应的Version

②：定义数据层接口与映射配置，继承BaseMapper

```java
@Mapper
public interface UserDao extends BaseMapper<User> {
   

}
```

③：其他同SpringBoot整合MyBatis （略）

④：测试类中注入dao接口，测试功能

```java
@SpringBootTest
class Springboot06MybatisPlusApplicationTests {
   

    @Autowired
    private UserDao userDao;

    @Test
    void contextLoads() {
   
        List<User> users = userDao.selectList(null);
        System.out.println(users);
    }

}
```

⑤: 运行如下:

```java
[User{
   id=1, username='zhangsan', password='123', name='张三'}, User{
   id=2, username='lisi', password='123', name='李四'}]
```

**注意**: 如果你的数据库表有前缀要在 application.yml 添加如下配制

```java
#设置Mp相关的配置
mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
```

小结: 1.手工添加MyBatis-Plus对应的starter 2.数据层接口使用BaseMapper简化开发 3.需要使用的第三方技术无法通过勾选确定时，需要手工添加坐标



![img](https://img-blog.csdnimg.cn/01f38eb4c4164996a36a68975b2c36da.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ①: 导入Druid对应的starter

```java
<dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>druid-spring-boot-starter</artifactId>
       <version>1.2.6</version>
   </dependency>
```

②: 指定数据源类型 (这种方式只需导入一个 Druid 的坐标)

```java
#DB Configuration:
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
    username: root
    password: 123456
    type: com.alibaba.druid.pool.DruidDataSource
```

**或者 变更Druid的配置方式(推荐) 这种方式需要导入 Druid对应的starter**

```java
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
      username: root
      password: 123456
```

小结:

1.整合Druid需要导入Druid对应的starter 2.根据Druid提供的配置方式进行配置 3.整合第三方技术通用方式

- 导入对应的starter 
- 根据提供的配置格式，配置非默认值对应的配置项


## 案例效果演示:


![img](https://img-blog.csdnimg.cn/0c7fddc8737f4d0db4c494e7162ba132.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

## 案例实现方案分析与流程解析

```java
1. 案例实现方案分析
	实体类开发————使用Lombok快速制作实体类
	Dao开发————整合MyBatisPlus，制作数据层测试类
	Service开发————基于MyBatisPlus进行增量开发，制作业务层测试类
	Controller开发————基于Restful开发，使用PostMan测试接口功能
	Controller开发————前后端开发协议制作
	页面开发————基于VUE+ElementUI制作，前后端联调，页面数据处理，页面消息处理
		列表、新增、修改、删除、分页、查询
	项目异常处理
	按条件查询————页面功能调整、Controller修正功能、Service修正功能
2. SSMP案例制作流程解析
	先开发基础CRUD功能，做一层测一层
	调通页面，确认异步提交成功后，制作所有功能
	添加分页功能与查询功能
```




![img](https://img-blog.csdnimg.cn/3a77fb8804f54341bf7bc08d95aac49f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/c15a95bf6dcd4f5b97157dc3106e3009.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_10,color_FFFFFF,t_70,g_se,x_16)

pom.xml

```java
<dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>

       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <scope>runtime</scope>
       </dependency>

       <dependency>
           <groupId>com.baomidou</groupId>
           <artifactId>mybatis-plus-boot-starter</artifactId>
           <version>3.4.3</version>
       </dependency>

       <dependency>
           <groupId>com.alibaba</groupId>
           <artifactId>druid-spring-boot-starter</artifactId>
           <version>1.2.6</version>
       </dependency>

       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>

   </dependencies>
```

## tbl_book.sql

```java
DROP TABLE IF EXISTS `tbl_book`;
CREATE TABLE `tbl_book` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `type` varchar(20) DEFAULT NULL,
  `name` varchar(50) DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of tbl_book
-- ----------------------------
INSERT INTO `tbl_book` VALUES ('1', '计算机理论', 'Spring实战第5版', 'Spring入门经典教程,深入理解Spring原理技术内幕');
INSERT INTO `tbl_book` VALUES ('2', '计算机理论', 'Spring 5核心原理与30个类手写实战', '十年沉淀之作，写Spring精华思想');
INSERT INTO `tbl_book` VALUES ('3', '计算机理论', 'Spring 5设计模式', '深入Spring源码剖析Spring源码中蕴含的10大设计模式');
INSERT INTO `tbl_book` VALUES ('4', '计算机理论', 'Spring MVC+ MyBatis开发从入门到项目实战', '全方位解析面向Web应用的轻量级框架,带你成为Spring MVC开发高手');
INSERT INTO `tbl_book` VALUES ('5', '计算机理论', '轻量级Java Web企业应用实战', '源码级剖析Spring框架,适合已掌握Java基础的读者');
INSERT INTO `tbl_book` VALUES ('6', '计算机理论', 'Java核心技术卷|基础知识(原书第11版)', 'Core Java第11版，Jolt大奖获奖作品，针对Java SE9、10、 11全面更新');
INSERT INTO `tbl_book` VALUES ('7', '计算机理论', '深入理解Java虚拟机', '5个维度全面剖析JVM,面试知识点全覆盖');
INSERT INTO `tbl_book` VALUES ('8', '计算机理论', 'Java编程思想(第4版)', 'Java学习必读经典殿堂级著作!赢得了全球程序员的广泛赞誉');
INSERT INTO `tbl_book` VALUES ('9', '计算机理论', '零基础学Java (全彩版)', '零基础自学编程的入门]图书，由浅入深，详解Java语言的编程思想和核心技术');
INSERT INTO `tbl_book` VALUES ('10', '市场营销', '直播就该这么做:主播高效沟通实战指南', '李子柒、李佳琦、薇娅成长为网红的秘密都在书中');
INSERT INTO `tbl_book` VALUES ('11', '市场营销', '直播销讲实战一本通', '和秋叶一起学系列网络营销书籍');
INSERT INTO `tbl_book` VALUES ('12', '市场营销', '直播带货:淘宝、天猫直播从新手到高手', '一本教你如何玩转直播的书， 10堂课轻松实现带货月入3W+');
```

小结:

1. 勾选SpringMVC与MySQL坐标 
2. 修改配置文件为yml格式 
3. 设置端口为80方便访问server:
  port: 80 


- Lombok，一个Java类库，提供了一组注解，简化POJO实体类开发

```java
<!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
```

- lombok版本由SpringBoot提供，无需指定版本 
- 常用注解：@Data

```java
@Data
public class Book {
   
    private Integer id;
    private String type;
    private String name;
    private String description;
}
```

- 为当前实体类在编译期设置对应的get/set方法，toString方法，hashCode方法，equals方法等

小结:

```java
1. 实体类制作
2. 使用lombok简化开发
	导入lombok无需指定版本，由SpringBoot提供版本
	@Data注解
```


- 导入MyBatisPlus与Druid对应的starter

```java
<dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.3</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.2.6</version>
        </dependency>
```

- 配置数据源与MyBatisPlus对应的基础配置（id生成策略使用数据库自增策略）

```java
# druid 数据源配制
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
      username: root
      password: 123456

# mybatis-plus
mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
      id-type: auto # 主键策略
```

- 继承BaseMapper并指定泛型

```java
@Mapper
public interface BookDao extends BaseMapper<Book> {
   

    /**
     * 查询一个
     * 这是 Mybatis 开发
     * @param id
     * @return
     */
    @Select("select * from tbl_book where id = #{id}")
    Book getById(Integer id);
}
```

- 制作测试类测试结果

```java
@SpringBootTest
public class BookDaoTestCase {
   

    @Autowired
    private BookDao bookDao;

    @Test
    void testGetById() {
   
        System.out.println(bookDao.getById(1));
        System.out.println(bookDao.selectById(1));
    }

    @Test
    void testSave() {
   
        Book book = new Book();
        book.setType("测试数据123");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookDao.insert(book);
    }

    @Test
    void testUpdate() {
   
        Book book = new Book();
        book.setId(13);
        book.setType("测试数据asfd");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookDao.updateById(book);
    }

    @Test
    void testDelete() {
   
        bookDao.deleteById(13);
    }

    @Test
    void testGetAll() {
   
        System.out.println(bookDao.selectList(null));
    }

    @Test
    void testGetPage() {
   
    }

    @Test
    void testGetBy() {
   
    }
}
```

小结:

1. 手工导入starter坐标（2个） 
2. 配置数据源与MyBatisPlus对应的配置 
3. 开发Dao接口（继承BaseMapper） 
4. 制作测试类测试Dao功能是否有效


- 为方便调试可以开启MyBatisPlus的日志

```java
# mybatis-plus
mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
      id-type: auto # 主键策略
  configuration:
    # 开启MyBatisPlus的日志
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

小结:


1. 使用配置方式开启日志，设置日志输出方式为标准输出 ![img](https://img-blog.csdnimg.cn/a6d40f4884f945d0a0c28577885cf3d1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)


- 分页操作需要设定分页对象IPage

```java
@Test
    void testGetPage() {
   
        IPage page = new Page(1, 5);
        bookDao.selectPage(page, null);
    }
```

-  IPage对象中封装了分页操作中的所有数据 数据 当前页码值 每页数据总量 最大页码值 数据总量  
-  分页操作是在MyBatisPlus的常规操作基础上增强得到，内部是动态的拼写SQL语句，因此需要增强对应的功能， 使用MyBatisPlus拦截器实现 

```java
@Configuration
public class MybatisPlusConfig {
   

    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
   
        //1. 定义 Mp 拦截器
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        //2. 添加具体的拦截器 分页拦截器
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        return interceptor;
    }
}
```

- 测试

```java
@Test
    void testGetPage() {
   
        IPage page = new Page(1, 5);
        bookDao.selectPage(page, null);
        System.out.println(page.getCurrent());
        System.out.println(page.getSize());
        System.out.println(page.getPages());
        System.out.println(page.getTotal());
        System.out.println(page.getRecords());
    }
```


![img](https://img-blog.csdnimg.cn/ecdb62572ac5446bba2e89be2e2f389f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 小结:

1. 使用IPage封装分页数据 
2. 分页操作依赖MyBatisPlus分页拦截器实现功能 
3. 借助MyBatisPlus日志查阅执行SQL语句


- 使用QueryWrapper对象封装查询条件，推荐使用LambdaQueryWrapper对象，所有查询操作封装成方法调用

```java
@Test
    void testGetBy2() {
   
        LambdaQueryWrapper<Book> lambdaQueryWrapper = new LambdaQueryWrapper<>();
        lambdaQueryWrapper.like(Book::getName, "Spring");
        bookDao.selectList(lambdaQueryWrapper);
    }
```

```java
@Test
    void testGetBy() {
   
        QueryWrapper<Book> queryWrapper = new QueryWrapper<>();
        queryWrapper.like("name", "Spring");
        bookDao.selectList(queryWrapper);
    }
```

- 支持动态拼写查询条件

```java
@Test
    void testGetBy2() {
   
        String name = "1";
        LambdaQueryWrapper<Book> lambdaQueryWrapper = new LambdaQueryWrapper<>();
        //if (name != null) lambdaQueryWrapper.like(Book::getName,name);
        lambdaQueryWrapper.like(Strings.isNotEmpty(name), Book::getName, name);
        bookDao.selectList(lambdaQueryWrapper);
    }
```


![img](https://img-blog.csdnimg.cn/ab95ccf9ac8f4c4baae6c94847a93544.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结:

1. 使用QueryWrapper对象封装查询条件 
2. 推荐使用LambdaQueryWrapper对象 
3. 所有查询操作封装成方法调用 
4. 查询条件支持动态条件拼装


-  Service层接口定义与数据层接口定义具有较大区别，不要混用 selectByUserNameAndPassword(String username,String password); 数据层接口 login(String username,String password); Service层接口  
-  接口定义 

```java
public interface BookService {
   

    Boolean save(Book book);

    Boolean update(Book book);

    Boolean delete(Integer id);

    Book getById(Integer id);

    List<Book> getAll();

    IPage<Book> getPage(int currentPage,int pageSize);
}
```

- 实现类定义

```java
@Service
public class BookServiceImpl implements BookService {
   

    @Autowired
    private BookDao bookDao;

    @Override
    public Boolean save(Book book) {
   
        return bookDao.insert(book) > 0;
    }

    @Override
    public Boolean update(Book book) {
   
        return bookDao.updateById(book) > 0;
    }

    @Override
    public Boolean delete(Integer id) {
   
        return bookDao.deleteById(id) > 0;
    }

    @Override
    public Book getById(Integer id) {
   
        return bookDao.selectById(id);
    }

    @Override
    public List<Book> getAll() {
   
        return bookDao.selectList(null);
    }

    @Override
    public IPage<Book> getPage(int currentPage, int pageSize) {
   
        IPage page = new Page(currentPage, pageSize);
        bookDao.selectPage(page, null);
        return page;
    }
}
```

- 测试类定义

```java
@SpringBootTest
public class BookServiceTestCase {
   

    @Autowired
    private BookService bookService;

    @Test
    void testGetById() {
   
        System.out.println(bookService.getById(4));
    }

    @Test
    void testSave() {
   
        Book book = new Book();
        book.setType("测试数据123");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookService.save(book);
    }

    @Test
    void testUpdate() {
   
        Book book = new Book();
        book.setId(14);
        book.setType("测试数据asfd");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookService.update(book);
    }

    @Test
    void testDelete() {
   
        bookService.delete(14);
    }

    @Test
    void testGetAll() {
   
        System.out.println(bookService.getAll());
    }

    @Test
    void testGetPage() {
   
        IPage<Book> page = bookService.getPage(2, 5);
        System.out.println(page.getCurrent());
        System.out.println(page.getSize());
        System.out.println(page.getPages());
        System.out.println(page.getTotal());
        System.out.println(page.getRecords());
    }
}
```

小结:

1. Service接口名称定义成业务名称，并与Dao接口名称进行区分 
2. 制作测试类测试Service功能是否有效



- 快速开发方案 使用MyBatisPlus提供有业务层通用接口（ISerivce）与业务层通用实现类（ServiceImpl&lt;M,T&gt;） 在通用类基础上做功能重载或功能追加 注意重载时不要覆盖原始操作，避免原始提供的功能丢失 ![img](https://img-blog.csdnimg.cn/3f7f7ce8ae2c4c8ebe42503b61e183fb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 
- 接口定义

```java
public interface IBookService extends IService<Book> {
   
}
```

- 接口追加功能

```java
public interface IBookService extends IService<Book> {
   

    // 追加的操作与原始操作通过名称区分，功能类似
    Boolean delete(Integer id);

    Boolean insert(Book book);

    Boolean modify(Book book);

    Book get(Integer id);
}
```


![img](https://img-blog.csdnimg.cn/6bc84748f4ca42fd829a7ec6a6023dd9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

- 实现类定义

```java
@Service
public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
   
}
```

- 实现类追加功能

```java
@Service
public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
   

    @Autowired
    private BookDao bookDao;

    public Boolean insert(Book book) {
   
        return bookDao.insert(book) > 0;
    }

    public Boolean modify(Book book) {
   
        return bookDao.updateById(book) > 0;
    }

    public Boolean delete(Integer id) {
   
        return bookDao.deleteById(id) > 0;
    }

    public Book get(Integer id) {
   
        return bookDao.selectById(id);
    }
}
```

- 测试类定义

```java
@SpringBootTest
public class BookServiceTest {
   

    @Autowired
    private IBookService bookService;

    @Test
    void testGetById() {
   
        System.out.println(bookService.getById(4));
    }

    @Test
    void testSave() {
   
        Book book = new Book();
        book.setType("测试数据123");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookService.save(book);
    }

    @Test
    void testUpdate() {
   
        Book book = new Book();
        book.setId(14);
        book.setType("===========");
        book.setName("测试数据123");
        book.setDescription("测试数据123");
        bookService.updateById(book);
    }

    @Test
    void testDelete() {
   
        bookService.removeById(14);
    }

    @Test
    void testGetAll() {
   
        System.out.println(bookService.list());
    }

    @Test
    void testGetPage() {
   
        IPage<Book> page = new Page<>(2, 5);
        bookService.page(page);
        System.out.println(page.getCurrent());
        System.out.println(page.getSize());
        System.out.println(page.getPages());
        System.out.println(page.getTotal());
        System.out.println(page.getRecords());
    }
}
```

小结：

1. 使用通用接口（ISerivce）快速开发Service 
2. 使用通用实现类（ServiceImpl&lt;M,T&gt;）快速开发ServiceImpl 
3. 可以在通用接口基础上做功能重载或功能追加 
4. 注意重载时不要覆盖原始操作，避免原始提供的功能丢失


- 基于Restful进行表现层接口开发 
- 使用Postman测试表现层接口功能

表现层开发

```java
@RestController
@RequestMapping("/books")
public class BookController {
   

    @Autowired
    private IBookService bookService;

    @GetMapping
    public List<Book> getAll() {
   
        return bookService.list();
    }

    @PostMapping
    public Boolean save(@RequestBody Book book) {
   
        return bookService.save(book);
    }

    @PutMapping
    public Boolean update(@RequestBody Book book) {
   
        return bookService.modify(book);
    }

    @DeleteMapping("{id}")
    public Boolean delete(@PathVariable Integer id) {
   
        return bookService.delete(id);
    }

    @GetMapping("{id}")
    public Book getById(@PathVariable Integer id) {
   
        return bookService.getById(id);
    }

    @GetMapping("{currentPage}/{pageSize}")
    public IPage<Book> getPage(@PathVariable Integer currentPage, @PathVariable int pageSize) {
   
        return bookService.getPage(currentPage, pageSize);
    }

}
```

添加 分页的业务层方法

IBookService

```java
IPage<Book> getPage(int currentPage,int pageSize);
```

BookServiceImpl

```java
@Override
    public IPage<Book> getPage(int currentPage, int pageSize) {
   

        IPage page = new Page(currentPage, pageSize);
        bookDao.selectPage(page, null);

        return page;
    }
```




功能测试 ![img](https://img-blog.csdnimg.cn/36443892e8d244f1b9d8be0bb82fd0a3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/7effd9c5d6a84ab985ec19967e5a8b85.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ![img](https://img-blog.csdnimg.cn/65cc31e45a2145a1a1cebdbd3dce8c6d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)


![img](https://img-blog.csdnimg.cn/ec50a6dde4aa4466a62c7235a32beb4f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 小结:

1. 基于Restful制作表现层接口 新增：POST 删除：DELETE 修改：PUT 查询：GET 
<li>接收参数 实体数据：@RequestBody 路径变量：@PathVariable</li>


-  之前的格式  
-  增加一个 data 属性，把数据全部封装到 data 里 当数据为 null 可能出现的问题 
 <ul> 
  - 查询id不存在的数据，返回 null 
  - 查询过程中抛出异常，catch 中返回 null 
 </ul>  
-  增加 一个状态属性  
-  设计表现层返回结果的模型类，用于后端与前端进行数据格式统一，也称为前后端数据协议 

```java
@Data
public class R {
   
    private Boolean flag;
    private Object data;

    public R() {
   
    }

    /**
     * 不返回数据的构造方法
     *
     * @param flag
     */
    public R(Boolean flag) {
   
        this.flag = flag;
    }

    /**
     * 返回数据的构造方法
     *
     * @param flag
     * @param data
     */
    public R(Boolean flag, Object data) {
   
        this.flag = flag;
        this.data = data;
    }
}
```

- 表现层接口统一返回值类型结果

```java
@RestController
@RequestMapping("/books")
public class BookController {
   

    @Autowired
    private IBookService bookService;

    @GetMapping
    public R getAll() {
   
        return new R(true, bookService.list());
    }

    @PostMapping
    public R save(@RequestBody Book book) {
   
        return new R(bookService.save(book));

    }

    @PutMapping
    public R update(@RequestBody Book book) {
   
        return new R(bookService.modify(book));
    }

    @DeleteMapping("{id}")
    public R delete(@PathVariable Integer id) {
   
        return new R(bookService.delete(id));
    }

    @GetMapping("{id}")
    public R getById(@PathVariable Integer id) {
   
        return new R(true, bookService.getById(id));
    }

    @GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable Integer currentPage, @PathVariable int pageSize) {
   
        return new R(true, bookService.getPage(currentPage, pageSize));
    }

}
```


![img](https://img-blog.csdnimg.cn/83f9d3b203a34ad0b9dc1c1012d0817d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结：

1. 设计统一的返回值结果类型便于前端开发读取数据 
2. 返回值结果类型可以根据需求自行设定，没有固定格式 
3. 返回值结果模型类用于后端与前端进行数据格式统一，也称为前 后端数据协议


## 使用VUE的方法时提示报错：

Method definition shorthands are not supported by current JavaScript version

表示：该方法定义的缺陷是不支持当前的JavaScript版本，虽然可以程序可以正常运行，但是这个方法会出现红色的波浪线，很不爽

解决： <strong>打开 File -&gt; Settings -&gt; Languages &amp; Frameworks -&gt; Javascript 把JavaScript版本为ECMAScript 6就可以了</strong>

- 前后端分离结构设计中页面归属前端服务器 
- 单体工程中页面放置在resources目录下的static目录中（建议执行clean） 
- 前端发送异步请求，调用后端接口

```java
//钩子函数，VUE对象初始化完成后自动执行
        created() {
   
            //调用查询全部数据的操作
            this.getAll();
        },
```

```java
//列表
            getAll() {
   
                //发送异步请求
                axios.get("/books").then((res)=>{
   
                    console.log(res.data);
                })
            },
```


![img](https://img-blog.csdnimg.cn/096ebaebba9d433f9d532cdc89566437.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 小结：

1. 单体项目中页面放置在resources/static目录下 
2. created钩子函数用于初始化页面时发起调用 
3. 页面使用axios发送异步请求获取数据后确认前后端是否联通


- 列表页

```java
//列表
    getAll() {
   
        //发送异步请求
        axios.get("/books").then((res) => {
   
            //console.log(res.data);
            this.dataList = res.data.data;
        })
    },
```


![img](https://img-blog.csdnimg.cn/e5efe8ab609f494baf68f6337f7a0ff3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结：

1. 将查询数据返回到页面，利用前端数据双向绑定进行数据展示


- 弹出添加窗口

```java
// 弹出添加窗口
handleCreate() {
   
	this.dialogFormVisible = true;
},
```

- 清除数据

```java
//重置表单
   resetForm() {
   
       this.formData = {
   };
   },
```

- 在弹出添加窗口时 清除数据

```java
//弹出添加窗口
  handleCreate() {
   
      this.dialogFormVisible = true;
      this.resetForm();
  },
```

- 发送添加请求

```java
//添加
   handleAdd() {
   
       axios.post("/books", this.formData).then((res) => {
   
           //判断当前操作是否成功
           if (res.data.flag) {
   
               //1.关闭弹层
               this.dialogFormVisible = false;
               this.$message.success("添加成功");
           } else {
   
               this.$message.error("添加失败");
           }
       }).finally(() => {
   
           //2.重新加载数据
           this.getAll();
       })
   },
```

- 取消添加

```java
//取消
  cancel() {
   
      //1.关闭弹层
      this.dialogFormVisible = false;
      //2.提示用户
      this.$message.info("当前操作取消");
  },
```

小结:

1. 请求方式使用POST调用后台对应操作 
2. 添加操作结束后动态刷新页面加载数据 
3. 根据操作结果不同，显示对应的提示信息 
4. 弹出添加Div时清除表单数据


- 删除

```java
// 删除
  handleDelete(row) {
   
      axios.delete("/books/" + row.id).then((res) => {
   
          if (res.data.flag) {
   
              this.$message.success("删除成功");
          } else {
   
              this.$message.error("删除失败");
          }
      }).finally(() => {
   
          this.getAll();
      });
  }
```

- 加入确认删除对话框

```java
// 删除
   handleDelete(row) {
   
       //1. 弹出提示框
       this.$confirm("些操作永久删除当前信息,是否继续?", "提示", {
   type: "info"}).then(() => {
   
           //2. 做删除业务
           axios.delete("/books/" + row.id).then((res) => {
   
               //判断当前操作是否成功
               if (res.data.flag) {
   
                   this.$message.success("删除成功");
               } else {
   
                   this.$message.error("删除失败");
               }
           }).finally(() => {
   
               //2.重新加载数据
               this.getAll();
           })
       }).catch(() => {
   
           //3. 取消删除
           this.$message.info("取消操作");
       });

   },
```

小结:

1. 请求方式使用Delete调用后台对应操作 
2. 删除操作需要传递当前行数据对应的id值到后台 
3. 删除操作结束后动态刷新页面加载数据 
4. 根据操作结果不同，显示对应的提示信息 
5. 删除操作前弹出提示框避免误操作


- 弹出修改窗口

```java
//弹出编辑窗口
  handleUpdate(row) {
   
      axios.get("/books/" + row.id).then((res) => {
   
          if (res.data.flag && res.data.data != null) {
   
              // 展示弹层，加载数据
              this.dialogFormVisible4Edit = true;
              this.formData = res.data.data;
          } else {
   
              this.$message.error("数据同步失败，自动刷新");
          }
      }).finally(() => {
   
          //重新加载数据
          this.getAll();
      });
  },
```

- 删除消息维护

```java
// 删除
   handleDelete(row) {
   
       //1. 弹出提示框
       this.$confirm("些操作永久删除当前信息,是否继续?", "提示", {
   type: "info"}).then(() => {
   
           //2. 做删除业务
           axios.delete("/books/" + row.id).then((res) => {
   
               //判断当前操作是否成功
               if (res.data.flag) {
   
                   this.$message.success("删除成功");
               } else {
   
                   this.$message.error("数据同步失败，自动刷新");
               }
           }).finally(() => {
   
               //2.重新加载数据
               this.getAll();
           });
       }).catch(() => {
   
           //3. 取消删除
           this.$message.info("取消操作");
       });

   },
```

小结:

1. 加载要修改数据通过传递当前行数据对应的id值到后台查询数据 
2. 利用前端数据双向绑定将查询到的数据进行回显


- 修改

```java
//修改
  handleEdit() {
   
      axios.put("/books", this.formData).then((res) => {
   
          //判断当前操作是否成功
          if (res.data.flag) {
   
              //1.关闭弹层
              this.dialogFormVisible4Edit = false;
              this.$message.success("修改成功");
          } else {
   
              this.$message.error("修改失败");
          }
      }).finally(() => {
   
          //2.重新加载数据
          this.getAll();
      });
  },
```

- 取消添加和修改

```java
//取消
  cancel() {
   
      //1.关闭弹层
      this.dialogFormVisible = false;
      this.dialogFormVisible4Edit = false;
      //2.提示用户
      this.$message.info("当前操作取消");
  },
```

小结:

1. 请求方式使用PUT调用后台对应操作 
2. 修改操作结束后动态刷新页面加载数据（同新增） 
3. 根据操作结果不同，显示对应的提示信息（同新增）


- 业务操作成功或失败返回数据格式

```java
{
   
    "flag": true,
    "data": null
}

{
   
    "flag": false,
    "data": null
}
```

- 后台代码BUG导致数据格式不统一性

```java
{
   
    "timestamp": "2021-11-07T12:44:29.343+00:00",
    "status": 500,
    "error": "Internal Server Error",
    "path": "/books"
}
```

- 对异常进行统一处理，出现异常后，返回指定信息

```java
@RestControllerAdvice
public class ProjectExceptionAdvice {
   

    //拦截所有的异常信息
    @ExceptionHandler(Exception.class)
    public R doException(Exception ex) {
   
        // 记录日志
        // 发送消息给运维
        // 发送邮件给开发人员 ,ex 对象发送给开发人员
        ex.printStackTrace();
        return new R(false, null, "系统错误，请稍后再试！");
    }
}
```

- 修改表现层返回结果的模型类，封装出现异常后对应的信息 flag：false Data: null 消息(msg): 要显示信息

```java
@Data
public class R{
   
	private Boolean flag;
	private Object data;
	private String msg;
	public R(Boolean flag,Object data,String msg){
   
		this.flag = flag;
		this.data = data;
		this.msg = msg;
	}
}
```

- 页面消息处理，没有传递消息加载默认消息，传递消息后加载指定消息

```java
//添加
  handleAdd() {
   
      axios.post("/books", this.formData).then((res) => {
   
          //判断当前操作是否成功
          if (res.data.flag) {
   
              //1.关闭弹层
              this.dialogFormVisible = false;
              this.$message.success("添加成功");
          } else {
   
              this.$message.error(res.data.msg);
          }
      }).finally(() => {
   
          //2.重新加载数据
          this.getAll();
      })
  },
```

- 可以在表现层Controller中进行消息统一处理

```java
@PostMapping
    public R save(@RequestBody Book book) throws IOException {
   
		//if (book.getName().equals("123")) throw new IOException();
        boolean flag = bookService.save(book);
        return new R(flag, flag ? "添加成功^_^" : "添加失败-_-!");
    }
```

- 页面消息处理

```java
//添加
  handleAdd() {
   
      axios.post("/books", this.formData).then((res) => {
   
          //判断当前操作是否成功
          if (res.data.flag) {
   
              //1.关闭弹层
              this.dialogFormVisible = false;
              this.$message.success(res.data.msg);
          } else {
   
              this.$message.error(res.data.msg);
          }
      }).finally(() => {
   
          //2.重新加载数据
          this.getAll();
      })
  },
```

小结:

1. 使用注解@RestControllerAdvice定义SpringMVC异常处理器用来处理异常的 
2. 异常处理器必须被扫描加载，否则无法生效 
3. 表现层返回结果的模型类中添加消息属性用来传递消息到页面


- 页面使用 el 分页组件添加分页功能

```java
<!--分页组件-->
  <div class="pagination-container">

      <el-pagination
              class="pagiantion"

              @current-change="handleCurrentChange"

              :current-page="pagination.currentPage"

              :page-size="pagination.pageSize"

              layout="total, prev, pager, next, jumper"

              :total="pagination.total">

      </el-pagination>

  </div>
```

- 定义分页组件需要使用的数据并将数据绑定到分页组件

```java
data: {
   
    pagination: {
    // 分页相关模型数据
        currentPage: 1, // 当前页码
        pageSize: 10,	// 每页显示的记录数
        total: 0,		// 总记录数
    }
},
```

- 替换查询全部功能为分页功能

```java
getAll() {
   
    axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize).then((res) => {
   });
},
```

- 分页查询 使用路径参数传递分页数据或封装对象传递数据

```java
@GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable Integer currentPage, @PathVariable int pageSize) {
   
        return new R(true, bookService.getPage(currentPage, pageSize));
    }
```

- 加载分页数据

```java
//分页查询
     getAll() {
   
         //发送异步请求
         axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize).then((res) => {
   
             //console.log(res.data);
             this.pagination.currentPage = res.data.data.current;
             this.pagination.pageSize = res.data.data.size;
             this.pagination.total = res.data.data.total;

             this.dataList = res.data.data.records;
         })
     },
```

- 分页页码值切换

```java
//切换页码
   handleCurrentChange(currentPage) {
   
       //修改页码值为当前选中的页码值
       this.pagination.currentPage = currentPage;
       //执行查询
       this.getAll();
   },
```

小结:

1. 使用el分页组件 
2. 定义分页组件绑定的数据模型 
3. 异步调用获取分页数据 
4. 分页数据页面回显


- 对查询结果进行校验，如果当前页码值大于最大页码值，使用最大页码值作为当前页码值重新查询

```java
@GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable Integer currentPage, @PathVariable int pageSize) {
   
        IPage<Book> page = bookService.getPage(currentPage, pageSize);
        // 如果当前页码值大于了总页码值，那么重新执行查询操作，使用最大页码值作为当前页码值
        if (currentPage > page.getPages()) {
   
            page = bookService.getPage((int) page.getPages(), pageSize);
        }
        return new R(true, page);
    }
```

小结:

1. 基于业务需求维护删除功能


- 查询条件数据封装 单独封装 与分页操作混合封装

```java
pagination: {
   //分页相关模型数据
       currentPage: 1,//当前页码
       pageSize: 10,//每页显示的记录数
       total: 0,//总记录数
       type: "",
       name: "",
       description: ""
   }
```

- 页面数据模型绑定

```java
<div class="filter-container">
    <el-input placeholder="图书类别" v-model="pagination.type" class="filter-item" />
    <el-input placeholder="图书名称" v-model="pagination.name" class="filter-item" />
    <el-input placeholder="图书描述" v-model="pagination.description" class="filter-item" />
    <el-button @click="getAll()" class="dalfBut">查询</el-button>
    <el-button type="primary" class="butT" @click="handleCreate()">新建</el-button>
</div>
```

- 组织数据成为get请求发送的数据

```java
//分页查询
   getAll() {
   
       console.log(this.pagination.type);

       //  /books/1/10?type=???&name=???&decription=?? ;
       //1. 获取查询条件 , 拼接查询条件
       param = "?name=" + this.pagination.name;
       param += "&type=" + this.pagination.type;
       param += "&description=" + this.pagination.description;
       //console.log("-----------------" + param);

       //发送异步请求
       axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize + param).then((res) => {
   
           //console.log(res.data);
           this.pagination.currentPage = res.data.data.current;
           this.pagination.pageSize = res.data.data.size;
           this.pagination.total = res.data.data.total;

           this.dataList = res.data.data.records;
       })
   },
```

- 条件参数组织可以通过条件判定书写的更简洁 
- Controller接收参数

```java
@GetMapping("{currentPage}/{pageSize}")
public R getAll(@PathVariable int currentPage,@PathVariable int pageSize,Book book) {
   
	System.out.println("参数=====>"+book);
	IPage<Book> pageBook = bookService.getPage(currentPage,pageSize);
	return new R(null != pageBook ,pageBook);
}
```

- 业务层接口功能开发

```java
/**
   * 分页的条件查询
   *
   * @param currentPage
   * @param pageSize
   * @param book
   * @return
   */
  IPage<Book> getPage(Integer currentPage, int pageSize, Book book);
```

- 业务层接口实现类功能开发

```java
@Override
    public IPage<Book> getPage(Integer currentPage, int pageSize, Book book) {
   

        LambdaQueryWrapper<Book> lambdaQueryWrapper = new LambdaQueryWrapper<>();

        lambdaQueryWrapper.like(Strings.isNotEmpty(book.getType()), Book::getType, book.getType());
        lambdaQueryWrapper.like(Strings.isNotEmpty(book.getName()), Book::getName, book.getName());
        lambdaQueryWrapper.like(Strings.isNotEmpty(book.getDescription()), Book::getDescription, book.getDescription());

        IPage page = new Page(currentPage, pageSize);
        bookDao.selectPage(page, lambdaQueryWrapper);

        return page;
    }
```

- Controller调用业务层分页条件查询接口

```java
@GetMapping("{currentPage}/{pageSize}")
    public R getPage(@PathVariable Integer currentPage, @PathVariable int pageSize, Book book) {
   

        // System.out.println("book=>" + book);

        IPage<Book> page = bookService.getPage(currentPage, pageSize, book);
        // 如果当前页码值大于了总页码值，那么重新执行查询操作，使用最大页码值作为当前页码值
        if (currentPage > page.getPages()) {
   
            page = bookService.getPage((int) page.getPages(), pageSize, book);
        }
        return new R(true, page);
    }
```

- 页面回显数据

```java
//分页查询
   getAll() {
   
       console.log(this.pagination.type);

       //  /books/1/10?type=???&name=???&decription=?? ;
       //1. 获取查询条件 , 拼接查询条件
       param = "?name=" + this.pagination.name;
       param += "&type=" + this.pagination.type;
       param += "&description=" + this.pagination.description;
       //console.log("-----------------" + param);

       //发送异步请求
       axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize + param).then((res) => {
   
           //console.log(res.data);
           this.pagination.currentPage = res.data.data.current;
           this.pagination.pageSize = res.data.data.size;
           this.pagination.total = res.data.data.total;

           this.dataList = res.data.data.records;
       })
   },
```

小结:

1. 定义查询条件数据模型（当前封装到分页数据模型中） 
2. 异步调用分页功能并通过请求参数传递数据到后台


## 基于SpringBoot的SSMP整合案例

1. pom.xml 配置起步依赖 
<li>application.yml 设置数据源、端口、框架技术相关配置等</li> 
<li>dao 继承BaseMapper、设置@Mapper</li> 
4. dao测试类 
<li>service 调用数据层接口或MyBatis-Plus提供的接口快速开发</li> 
6. service测试类 
<li>controller 基于Restful开发，使用Postman测试跑通功能</li> 
<li>页面 放置在resources目录下的static目录中</li>

总结:

1. 整合JUint 
2. 整合MyBatis 
3. 整合MyBatis-Plus 
4. 整合Druid 
5. 基于SpringBoot的SSMP整合案例

## 后续学习

- 基础篇 
 <ul> 
  - 能够创建SpringBoot工程 
  - 基于SpringBoot实现ssm/ssmp整合 
 </ul>  
- 实用篇 
 <ul> 
  - 运维实用篇  [Spring Boot 2 运维实用篇学习笔记](https://blog.csdn.net/qq_42324086/article/details/121386859) 
   <ul> 
    - 能够掌握SpringBoot程序多环境开发 
    - 能够基于Linux系统发布SpringBoot工程 
    - 能够解决线上灵活配置SpringBoot工程的需求 
   </ul>  
  - 开发实用篇 
   <ul> 
    - 能够基于SpringBoot整合任意第三方技术 
   </ul>  
 </ul>  
- 原理篇


内容介绍

- 打包与运行 
- 配置高级 
- 多环境开发 
- 日志

课程目标：

- 能够掌握SpringBoot程序多环境开发 
- 能够基于Linux系统发布SpringBoot工程 
- 能够解决线上灵活配置SpringBoot工程的需求


## 程序为什么要打包


将程序部署在独立的服务器上 ![img](https://img-blog.csdnimg.cn/img_convert/ab8d2df714d42356c71b0f13f92d20e9.png)

## SpringBoot项目快速启动（Windows版）

### 步骤

①：对SpringBoot项目打包（执行Maven构建指令package） 执行 package 打包命令之前 先执行 **mvn clean** 删除 target 目录及内容

```java
mvn package
```




![img](https://img-blog.csdnimg.cn/img_convert/f806bb3c8544f33ec010bab7d25b02bb.png) 打包完成 生成对应的 jar 文件 ![img](https://img-blog.csdnimg.cn/img_convert/aadc7af46bb5f273b03bbf1f05856e1b.png) **可能出现的问题: IDEA下 执行 Maven 命令控制台中文乱码** Ctr+Alt+S 打开设置，在Build，Execution ，Deployment找到Build Tools下Maven项下的Runner ，在VM Options 添加 -Dfile.encoding=GB2312 ，点击OK。 ![img](https://img-blog.csdnimg.cn/img_convert/b5b5318fb3ab2881dd3390c7427ced55.png)

②：运行项目（执行启动指令） java -jar &lt;打包文件名&gt;

```java
java –jar springboot.jar
```

注意事项： jar支持命令行启动需要依赖maven插件支持，请确认打包时是否具有SpringBoot对应的maven插件

```java
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```




![img](https://img-blog.csdnimg.cn/img_convert/40ad8c77bd7bd529b61c5bc01242ffd4.png) 地址栏输入 cmd 回车 ![img](https://img-blog.csdnimg.cn/img_convert/0016c8a2a1d291e54fd50ce3a87b77ad.png) 执行 java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar ![img](https://img-blog.csdnimg.cn/img_convert/a4ca10991375676ce6c0290662852adf.png) ③：浏览器访问:  [http://localhost/pages/books.html](http://localhost/pages/books.html)

### 打包优化：跳过 test 生命周期



![img](https://img-blog.csdnimg.cn/img_convert/01533f23027c4bb8579eee0e726ba369.png) ![img](https://img-blog.csdnimg.cn/img_convert/fd7a1ee45ea66c2aa98208a0899a39f6.png)

## 小结:

1. SpringBoot工程可以基于java环境下独立运行jar文件启动服务 
2. SpringBoot工程执行mvn命令package进行打包 
3. 执行jar命令：java –jar 工程名.jar



如果没有配制spring boot 打包插件可能遇到下面的问题: ![img](https://img-blog.csdnimg.cn/img_convert/70d95f157126511ccc2ffc6e19f899d4.png)

- 使用SpringBoot提供的maven插件可以将工程打包成可执行jar包

```java
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

## 可执行jar包目录结构


![img](https://img-blog.csdnimg.cn/img_convert/35f27fe78e4ca242139ac84ce1391af7.png)

## jar包描述文件（MANIFEST.MF）

- 普通工程

```java
Manifest-Version: 1.0
Implementation-Title: springboot_08_ssmp
Implementation-Version: 0.0.1-SNAPSHOT
Build-Jdk-Spec: 1.8
Created-By: Maven Jar Plugin 3.2.0
```

- 基于spring-boot-maven-plugin打包的工程

```java
Manifest-Version: 1.0
Spring-Boot-Classpath-Index: BOOT-INF/classpath.idx
Implementation-Title: springboot_08_ssmp
Implementation-Version: 0.0.1-SNAPSHOT
Spring-Boot-Layers-Index: BOOT-INF/layers.idx
Start-Class: com.example.SSMPApplication 启动类
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/lib/
Build-Jdk-Spec: 1.8
Spring-Boot-Version: 2.5.6
Created-By: Maven Jar Plugin 3.2.0
Main-Class: org.springframework.boot.loader.JarLauncher  jar启动器
```

## 命令行启动常见问题及解决方案

- Windonws端口被占用

```java
# 查询端口
netstat -ano
# 查询指定端口
netstat -ano |findstr "端口号"
# 根据进程PID查询进程名称
tasklist |findstr "进程PID号"
# 根据PID杀死任务
taskkill /F /PID "进程PID号"
# 根据进程名称杀死任务
taskkill -f -t -im "进程名称"
```

```java
D:\code\Java\IdeaProjects\springboot-study\springboot_08_ssmp\target>netstat -ano

活动连接

  协议  	 本地地址          		  外部地址       		 状态            PID
  TCP    0.0.0.0:80             0.0.0.0:0              LISTENING       30988
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       1792
  TCP    0.0.0.0:443            0.0.0.0:0              LISTENING       9400
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:902            0.0.0.0:0              LISTENING       6188
  TCP    0.0.0.0:912            0.0.0.0:0              LISTENING       6188
 
D:\code\Java\IdeaProjects\springboot-study\springboot_08_ssmp\target>netstat -ano |findstr "80"
  TCP    0.0.0.0:80             0.0.0.0:0              LISTENING       30988
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING       4864
  TCP    0.0.0.0:8680           0.0.0.0:0              LISTENING       7976
  TCP    192.168.1.102:9808     119.96.138.240:443     ESTABLISHED     20604
  TCP    [::]:80                [::]:0                 LISTENING       30988
  TCP    [::]:7680              [::]:0                 LISTENING       4864
  UDP    127.0.0.1:65312        *:*                                    5680
  UDP    [fe80::2952:170d:f2f2:1464%16]:1900  *:*                                    2872
  UDP    [fe80::2952:170d:f2f2:1464%16]:60720  *:*                                    2872
  UDP    [fe80::4c2b:9d2f:a625:8b1c%6]:1900  *:*                                    2872
  UDP    [fe80::4c2b:9d2f:a625:8b1c%6]:60719  *:*                                    2872
  UDP    [fe80::e1e0:a2c9:200:2f34%19]:1900  *:*                                    2872
  UDP    [fe80::e1e0:a2c9:200:2f34%19]:60721  *:*                                    2872
  
  
D:\code\Java\IdeaProjects\springboot-study\springboot_08_ssmp\target>tasklist |findstr "30988"
java.exe                     30988 Console                    3    273,388 K


D:\code\Java\IdeaProjects\springboot-study\springboot_08_ssmp\target>tasklist

映像名称                       PID 会话名              会话#       内存使用
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0      1,500 K
Registry                       172 Services                   0     94,584 K
smss.exe                       648 Services                   0      1,084 K
csrss.exe                     1080 Services                   0      5,888 K
wininit.exe                   1320 Services                   0      6,868 K
services.exe                  1436 Services                   0      9,264 K
lsass.exe                     1488 Services                   0     11,932 K
svchost.exe                   1612 Services                   0     17,804 K
fontdrvhost.exe               1648 Services                   0        488 K
WUDFHost.exe                  1688 Services                   0      2,660 K
svchost.exe                   1792 Services                   0     13,428 K
WUDFHost.exe                  1840 Services                   0      2,628 K
svchost.exe                   1868 Services                   0      3,460 K


D:\code\Java\IdeaProjects\springboot-study\springboot_08_ssmp\target>taskkill /F /PID "30988"
成功: 已终止 PID 为 30988 的进程。
```

## 小结:

1. spring-boot-maven-plugin插件作用 
2. Windonws端口被占用



![img](https://img-blog.csdnimg.cn/img_convert/80846308dc04e36693e023795d8a06b1.png)

- 基于Linux（CenterOS7） 
- 安装JDK，且版本不低于打包时使用的JDK版本 
 <ul> 
  - 可以使用 yum 安装 
 </ul>  
- 安装 MySQL 
 <ul> 
  - 可以参考:  [https://blog.csdn.net/qq_42324086/article/details/120579197](https://blog.csdn.net/qq_42324086/article/details/120579197) 
 </ul>  
- 安装包保存在/usr/local/自定义目录中或$HOME下 
- 其他操作参照Windows版进行

## 启动成功无法访问

### 添加 80 端口

- 添加 端口

```java
firewall-cmd --zone=public --permanent --add-port=80/tcp
```

- 重启

```java
systemctl restart firewalld
```

## 后台启动命令

```java
nohup java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar > server.log 2>&1 &
```

## 停止服务

- ps -ef | grep “java -jar” 
- kill -9 PID 
- cat server.log (查看日志)

```java
[root@cjbCentos01 app]# ps -ef | grep "java -jar"
UID         PID   PPID  C STIME TTY          TIME CMD
root       6848   6021  7 14:45 pts/2    00:00:19 java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar
root       6919   6021  0 14:49 pts/2    00:00:00 grep --color=auto java -jar
[root@cjbCentos01 app]# kill -9 6848
[root@cjbCentos01 app]# ps -ef | grep "java -jar"
root       7016   6021  0 14:52 pts/2    00:00:00 grep --color=auto java -jar
[1]+  已杀死               nohup java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar > server.log 2>&1
[root@cjbCentos01 app]#
```

## 小结:

1. 上传安装包 
2. 执行jar命令：java –jar 工程名.jar

## 总结:

1. Boot程序打包依赖SpringBoot对应的Maven插件即可打包出可执行的jar包 
2. 运行jar包使用jar命令进行 
3. Windows与Linux下执行Boot打包程序流程相同，仅需确保运行环境有效即可



![img](https://img-blog.csdnimg.cn/img_convert/00250c08fd078a09e38cfc777f2a6e30.png)

- 带属性数启动SpringBoot

```java
java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar --server.port=8080
```

- 携带多个属性启动SpringBoot，属性间使用空格分隔

## 属性加载优先顺序

1. 参看  [https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config)


![img](https://img-blog.csdnimg.cn/img_convert/c0465f0f841336a9f3e6c8a43558c41d.png) 小结:

1. 使用jar命令启动SpringBoot工程时可以使用临时属性替换配置文件中的属性 
2. 临时属性添加方式：java –jar 工程名.jar --属性名=值 
3. 多个临时属性之间使用空格分隔 
4. 临时属性必须是当前boot工程支持的属性，否则设置无效



![img](https://img-blog.csdnimg.cn/img_convert/cbd760661547dc8a32c78fe5275ebd46.png)

- 带属性启动SpringBoot程序，为程序添加运行属性



![img](https://img-blog.csdnimg.cn/img_convert/7f0f706308f900b8e8c84c5da49b0eef.png) ![img](https://img-blog.csdnimg.cn/img_convert/33c79353fd3f41ede3e0d852a3c32035.png) 在启动类中 main 可以通过 System.out.println(Arrays.toString(args)); 查看配制的属性

- 通过编程形式带参数启动SpringBoot程序，为程序添加运行参数

```java
public static void main(String[] args) {
   
	String[] arg = new String[1];
	arg[0] = "--server.port=8080";
	SpringApplication.run(SSMPApplication.class, arg);
}
```

- 不携带参数启动SpringBoot程序

```java
public static void main(String[] args) {
   
    //可以在启动boot程序时断开读取外部临时配置对应的入口，也就是去掉读取外部参数的形参
	SpringApplication.run(SSMPApplication.class);
}
```

小结:

1. 启动SpringBoot程序时，可以选择是否使用命令行属性为SpringBoot程序传递启动属性



![img](https://img-blog.csdnimg.cn/img_convert/28fb89c70d79a60d4255054072cba77f.png)

## 配置文件分类

1. SpringBoot中4级配置文件 
 <ol> 
  1. 1级：file ：config/application.yml **【最高】** 
  1. 2级：file ：application.yml 
  1. 3级：classpath：config/application.yml 
  1. 4级：classpath：application.yml **【最低】** 
 </ol>  
6. 作用： 
 <ol> 
  6. 1级与2级留做系统打包后设置通用属性，1级常用于运维经理进行线上整体项目部署方案调控 
  6. 3级与4级用于系统开发阶段设置通用属性，3级常用于项目经理进行整体项目属性调控 
 </ol> 

思 考: 如果yml与properties在不同层级中共存会是什么效果？ 例：类路径application.properties属性是否覆盖文件系统config目录中application.yml属性 properties文件的优先级大于yml文件 (properties文件会覆盖yml文件的配制) ​

小结:

1. 配置文件分为4种 项目类路径配置文件：服务于开发人员本机开发与测试 项目类路径config目录中配置文件：服务于项目经理整体调控 工程路径配置文件：服务于运维人员配置涉密线上环境 工程路径config目录中配置文件：服务于运维经理整体调控 
2. 多层级配置文件间的属性采用叠加并覆盖的形式作用于程序



![img](https://img-blog.csdnimg.cn/img_convert/17f4bdc7002679ed1800a32887b32f7c.png)

- 通过启动参数加载配置文件（无需书写配置文件扩展名) --spring.config.name=ebank


![img](https://img-blog.csdnimg.cn/img_convert/17dba20aaac666832c0bb3de5665d294.png) properties与yml文件格式均支持 ​

- 通过启动参数加载指定文件路径下的配置文件 --spring.config.location=classpath:/ebank.yml


![img](https://img-blog.csdnimg.cn/img_convert/b35d55e4ec222afad45ff3357a5999fe.png) properties与yml文件格式均支持

- 通过启动参数加载指定文件路径下的配置文件时可以加载多个配置,后面的会覆盖前面的

```java
--spring.config.location=classpath:/ebank.yml,classpath:/ebank-server.yml
```


![img](https://img-blog.csdnimg.cn/img_convert/00fa952d9b0e3e73345fa84d6d6ab079.png) 注意事项: 多配置文件常用于将配置进行分类，进行独立管理，或将可选配置单独制作便于上线更新维护 ​

**自定义配置文件——重要说明**

- 单服务器项目：使用自定义配置文件需求较低 
- 多服务器项目：使用自定义配置文件需求较高，将所有配置放置在一个目录中，统一管理 
- 基于SpringCloud技术，所有的服务器将不再设置配置文件，而是通过配置中心进行设定，动态加载配置信息

小结:

1. 配置文件可以修改名称，通过启动参数设定 
2. 配置文件可以修改路径，通过启动参数设定 
3. 微服务开发中配置文件通过配置中心进行设置

总结:

1. SpringBoot在开发和运行环境均支持使用临时参数修改工程配置 
2. SpringBoot支持4级配置文件，应用于开发与线上环境进行配置的灵活设置 
3. SpringBoot支持使用自定义配置文件的形式修改配置文件存储位置 
4. 基于微服务开发时配置文件将使用配置中心进行管理





多环境 ![img](https://img-blog.csdnimg.cn/img_convert/8fd600d1f34d1c80cb86671b4e99a638.png) 多环境开发（YAML版） ![img](https://img-blog.csdnimg.cn/img_convert/cf40efa2028ab24ad72481558a56b7ac.png) ![img](https://img-blog.csdnimg.cn/img_convert/644c8d460616b3fda1b7c8bdb9c5a1e7.png)

```java
#应用环境
#公共配制
spring:
  profiles:
    active: dev


#设置环境
#开发环境
---
spring:
  config:
    activate:
      on-profile: dev
server:
  port: 81

#生产环境
---
spring:
  profiles: pro
server:
  port: 80

#测试环境
---
spring:
  profiles: test
server:
  port: 82
```

小结:

1. 多环境开发需要设置若干种常用环境，例如开发、生产、测试环境 
2. yaml格式中设置多环境使用—区分环境设置边界 
3. 每种环境的区别在于加载的配置属性不同 
4. 启用某种环境时需要指定启动时使用该环境



![img](https://img-blog.csdnimg.cn/img_convert/1aa65d7c3cc15d3cae4394a50fa158ea.png)

## 多环境开发（YAML版）多配置文件格式

1. 主启动配置文件application.yml

```java
#应用环境
#公共配制
spring:
  profiles:
    active: test
```

1. 环境分类配置文件application-**pro**.yml

```java
server:
  port: 81
```

1. 环境分类配置文件application-**dev**.yml

```java
server:
  port: 82
```

1. 环境分类配置文件application-**test**.yml

```java
server:
  port: 83
```

## 多环境开发配置文件书写技巧（一）

- 主配置文件中设置公共配置（全局） 
- 环境分类配置文件中常用于设置冲突属性（局部）

小结:

1. 可以使用独立配置文件定义环境属性 
2. 独立配置文件便于线上系统维护更新并保障系统安全性


- 主启动配置文件application.properties

```java
spring.profiles.active=dev
```

- 环境分类配置文件application-**pro**.properties

```java
server.port=9081
```

- 环境分类配置文件application-**dev**.properties

```java
server.port=9082
```

- 环境分类配置文件application-**test**.properties

```java
server.port=9083
```

小结:

1. properties文件多环境配置仅支持多文件格式


## 多环境开发独立配置文件书写技巧（二）

- 根据功能对配置文件中的信息进行拆分，并制作成独立的配置文件，命名规则如下 
 <ul> 
  - application-devDB.yml 
  - application-devRedis.yml 
  - application-devMVC.yml 
 </ul>  
- 使用include属性在激活指定环境的情况下，同时对多个环境进行加载使其生效，多个环境间使用逗号分隔

```java
spring:
  profiles:
    active: dev
    include: devDB,devMVC
```

注意事项: **当主环境dev与其他环境有相同属性时，主环境属性生效；其他环境中有相同属性时，最后加载的环境属性生效**

```java
The following profiles are active: devDB,devMVC,dev
```

****

- 从Spring2.4版开始使用group属性替代include属性，降低了配置书写量 
- 使用**group**属性定义多种主环境与子环境的包含关系

```java
spring:
  profiles:
    active: dev
    group:
      "dev": devDB,devMVC
      "pro": proDB,proMVC
      "test": testDB,testRedis,testMVC
```

注意事项: **使用group属性，会覆盖 主环境dev (active) 的内容，最后加载的环境属性生效**

```java
The following profiles are active: dev,devDB,devMVC
```

小结：

1. 多环境开发使用group属性设置配置文件分组，便于线上维护管理



![img](https://img-blog.csdnimg.cn/img_convert/35dfd3ba820eeda9b5108fa134c0b9b7.png) Maven与SpringBoot多环境兼容 ①：Maven中设置多环境属性

```java
<!--Maven中设置多环境属性-->
    <profiles>
        <profile>
            <id>dev_env</id>
            <properties>
                <profile.active>dev</profile.active>
            </properties>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
        </profile>
        <profile>
            <id>pro_env</id>
            <properties>
                <profile.active>pro</profile.active>
            </properties>

        </profile>
        <profile>
            <id>test_env</id>
            <properties>
                <profile.active>test</profile.active>
            </properties>
        </profile>
    </profiles>
```

②：SpringBoot中引用Maven属性

```java
spring:
  profiles:
    active: @profile.active@
    group:
      "dev": devDB,devMVC
      "pro": proDB,proMVC
```




![img](https://img-blog.csdnimg.cn/img_convert/16c8a5b48611896ab3f94a6915322893.png) ③：执行Maven打包指令，并在生成的boot打包文件.jar文件中查看对应信息 问题：**修改pom.xml 文件后，启动没有生效 手动 compile 即可** ![img](https://img-blog.csdnimg.cn/img_convert/5b35e9530a6c9b84d1a590b08392716a.png) 或者 设置 IDEA进行自动编译 ![img](https://img-blog.csdnimg.cn/img_convert/c3b20b8b674f4c4339c22daded35bbd1.png) 小结：

1. 当Maven与SpringBoot同时对多环境进行控制时，以Mavn为主，SpringBoot使用@…@占位符读取Maven对应的配置属性值 
2. 基于SpringBoot读取Maven配置属性的前提下，如果在Idea下测试工程时pom.xml每次更新需要手动compile方可生效

总结：

1. 多环境开发（YAML版） 
2. 多环境开发（Properties版） 
3. Maven与SpringBoot多环境冲突现象解决方案


日志（log）作用

1. 编程期调试代码 
2. 运营期记录信息 
 <ul> 
  2. 记录日常运营重要信息（峰值流量、平均响应时长……） 
  2. 记录应用报错信息（错误堆栈） 
  2. 记录运维过程数据（扩容、宕机、报警……） 
 </ul> 

代码中使用日志工具记录日志

- 先引入 Lombok 工具类

```java
<!--lombok-->
  <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
  </dependency>
```

①：添加日志记录操作

```java
@RestController
@RequestMapping("/books")
public class BookController {
   
    private static final Logger log = LoggerFactory.getLogger(BookController.class);

    @GetMapping
    public String getById() {
   
        System.out.println("springboot is running...");
        log.debug("debug ...");
        log.info("info ...");
        log.warn("warn ...");
        log.error("error ...");
        return "springboot is running...";
    }
}
```

- 日志级别

TRACE：运行堆栈信息，使用率低 DEBUG：程序员调试代码使用 INFO：记录运维过程数据 WARN：记录运维过程报警数据 ERROR：记录错误堆栈信息 FATAL：灾难信息，合并计入ERROR ​

②：设置日志输出级别

```java
# 开启 debug 模式，输出调试信息，常用于检查系统运行状况
debug: true
# 设置日志级别， root 表示根节点，即整体应用日志级别
logging:
  level:
    root: debug
```

③：设置日志组，控制指定包对应的日志输出级别，也可以直接控制指定包对应的日志输出级别

```java
logging:
  # 设置分组
  group:
    # 自定义组名，设置当前组中所包含的包
    ebank: com.example.controller,com.example.service,com.example.dao
    iservice: com.alibaba
  level:
    root: info
    # 设置某个包的日志级别
#    com.example.controller: debug
    # 为对应组设置日志级别
    ebank: warn
```

小结：

1. 日志用于记录开发调试与运维过程消息 
2. 日志的级别共6种，通常使用4种即可，分别是DEBUG，INFO,WARN,ERROR 
3. 可以通过日志组或代码包的形式进行日志显示级别的控制



![img](https://img-blog.csdnimg.cn/img_convert/ef19395db7ae199acec096600b0ecbff.png)

- 使用lombok提供的注解@Slf4j简化开发，减少日志对象的声明操作

```java
@Slf4j
//Rest模式
@RestController
@RequestMapping("/books")
public class BookController {
   

    @GetMapping
    public String getById(){
   
        System.out.println("springboot is running...2");

        log.debug("debug...");
        log.info("info...");
        log.warn("warn...");
        log.error("error...");

        return "springboot is running...2";
    }

}
```

小结：

1. 基于lombok提供的@Slf4j注解为类快速添加日志对象



![img](https://img-blog.csdnimg.cn/img_convert/31052c620b4cfd40b68c4318289bd353.png)

- PID：进程ID，用于表明当前操作所处的进程，当多服务同时记录日志时，该值可用于协助程序员调试程序 
- 所属类/接口名：当前显示信息为SpringBoot重写后的信息，名称过长时，简化包名书写为首字母，甚至直接删除 
- 设置日志输出格式

```java
logging:
  pattern:
    console: "%d - %m%n"
```


%d：日期 %m：消息 %n：换行 ![img](https://img-blog.csdnimg.cn/img_convert/6dcf8a6c3596115d805a6806fccc9da3.png)

```java
logging:
  pattern:
#    console: "%d - %m%n"
    console: "%d %clr(%5p) --- [%16t] %clr(%-40.40c){cyan} : %m %n"
```

小结：

1. 日志输出格式设置规则


- 设置日志文件

```java
logging:
  file:
    name: server.log
```

- 日志文件详细配置

```java
logging:
  file:
    name: server.log
  logback:
    rollingpolicy:
      max-file-size: 4KB
      file-name-pattern: server.%d{
   yyyy-MM-dd}.%i.log
```


![img](https://img-blog.csdnimg.cn/img_convert/b7edc1d3ce55bc54bacdc747530fcb0d.png)

小结：

1. 日志记录到文件 
2. 日志文件格式设置

总结：

1. 日志基础使用规则 
2. 编辑日志输出格式 
3. 日志文件设置

