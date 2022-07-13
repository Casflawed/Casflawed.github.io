---
title: SpringBoot2
date: 2022-07-12 +/-TTTT
categories: [框架, SpringBoot]
tags: []     # TAG names should always be lowercase
---

学习要求

- 熟悉Spring基础 
- 熟悉Maven使用

环境要求

- Java8及以上 
- Maven 3.5及以上：https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-system-requirements

学习资料

-  Spring Boot官网：https://spring.io/projects/spring-boot  
-  Spring Boot 官方文档：https://docs.spring.io/spring-boot/docs/current/reference/html/  
-  Spring Boot 中文文档：http://felord.cn/_doc/_springboot/2.1.5.RELEASE/_book/  
-  视频地址：https://www.bilibili.com/video/BV15b4y1a7yG?p=24&share_source=copy_web  
-  源码地址：GitHub Gitee 


- 基础篇

```java
Java基础语法
Spring与SpringMVC
	知道Spring是用来管理bean，能够基于Restful实现页面请求交互功能
Mybatis与Mybatis-Plus
	基于Mybatis和MybatisPlus能够开发出包含基础CRUD功能的标准Dao模块
数据库MySQL
	能够读懂基础CRUD功能的SQL语句
服务器
	知道服务器与web工程的关系，熟悉web服务器的基础配置
maven
	知道maven的依赖关系，知道什么是依赖范围，依赖传递，排除依赖，可选依赖，继承
web技术（含vue，ElementUI)
	知道vue如何发送ajax请求，如何获取响应数据，如何进行数据模型双向绑定
```


- SpringBoot是由Pivotal团队提供的全新框架，其设计目的是用来简化Spring应用的初始搭建以及开发过程



①：创建新模块，选择Spring Initializr，并配置模块相关基础信息 ![img](https://img-blog.csdnimg.cn/0839ab0b92fc4deea70e706e84c9a27d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ②：选择当前模块需要使用的技术集 ![img](https://img-blog.csdnimg.cn/5108acf698f8423aa6d0ecc73f133a4e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

③：开发控制器类

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


④：运行自动生成的Application类 ![img](https://img-blog.csdnimg.cn/e0d7e6b7371845e8a91aa6aebaccc94c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) ⑤：打开浏览器访问url地址为：http://localhost:8080/books


![img](https://img-blog.csdnimg.cn/163c4ae2c0c0411a92cad10009683141.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

- 最简SpringBoot程序所包含的基础文件 (pom.xml文件 和 Application类 ) 
 <ul> 
  - pom.xml文件 
 </ul> 

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

- Application类

```java
@SpringBootApplication
public class Springboot0101QuickstartApplication {
   

    public static void main(String[] args) {
   
        SpringApplication.run(Springboot0101QuickstartApplication.class, args);
    }

}
```


- Spring程序与SpringBoot程序对比 ![img](https://img-blog.csdnimg.cn/414b7f3210694d5a8686a62ae4f9feff.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 注意: 基于idea开发SpringBoot程序需要确保联网且能够加载到程序框架结构

小结:

1. 开发SpringBoot程序可以根据向导进行联网快速制作 
2. SpringBoot程序需要基于JDK8进行制作 
3. SpringBoot程序中需要使用何种功能通过勾选选择技术 
4. 运行SpringBoot程序通过运行Application程序入口进行



- 基于SpringBoot官网创建项目，地址：https://start.spring.io/ ![img](https://img-blog.csdnimg.cn/e74fee358083447a80a38fde8ade98e2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

小结:

1. 打开SpringBoot官网，选择Quickstart Your Project 
2. 创建工程，并保存项目 
3. 解压项目，通过IDE导入项目



- 基于阿里云创建项目，地址：https://start.aliyun.com ![img](https://img-blog.csdnimg.cn/6bcd048d7f014158b0aab0617ca36c63.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

注意事项:

-  阿里云提供的坐标版本较低，如果需要使用高版本，进入工程后手工切换SpringBoot版本  
-  阿里云提供的工程模板与Spring官网提供的工程模板略有不同  

小结:

1. 选择start来源为自定义URL 
2. 输入阿里云start地址 
3. 创建项目



- 手工创建项目（手工导入坐标） ![img](https://img-blog.csdnimg.cn/1724035ac0724e3ca3177fd10e77f77a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.6</version>
    </parent>

    <groupId>com.example</groupId>
    <artifactId>springboot_01_04_quickstart</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
</project>
```

- 手工创建项目（手工制作引导类）

```java
@SpringBootApplication
public class Application {
   

    public static void main(String[] args) {
   
        SpringApplication.run(Application.class, args);
    }

}
```

小结:

1. 创建普通Maven工程 
2. 继承spring-boot-starter-parent 
3. 添加依赖spring-boot-starter-web 
4. 制作引导类Application

总结:

1. 创建SpringBoot工程的四种方式 基于Idea创建SpringBoot工程 基于官网创建SpringBoot工程 基于阿里云创建SpringBoot工程 **手工创建Maven工程修改为SpringBoot工程**



- .mvn;.gitignore;HELP.md;mvnw;mvnw.cmd;*.iml; ![img](https://img-blog.csdnimg.cn/e2014530ac5b432ba546e44ec00c1ca4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16)



2018版的做法: ![img](https://img-blog.csdnimg.cn/52caab4e4aae44aa98a3fc8815c93083.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 较新版本的做法 : ![img](https://img-blog.csdnimg.cn/fd8efbad436e406c900ad501d3af496e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pqX5oGL6Iqx6aaZ,size_20,color_FFFFFF,t_70,g_se,x_16) 小结:

1. Idea中隐藏指定文件或指定类型文件 Setting → File Types → Ignored Files and Folders 输入要隐藏的文件名，支持*号通配符 回车确认添加



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


-  热部署  
-  配置高级  
-  测试  
-  数据层解决方案  
-  整合第三方技术  
-  监控 


1. 启动热部署

**步骤①**：导入开发者工具对应的坐标

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

**步骤②**：构建项目，可以使用快捷键激活此功能


![img](https://img-blog.csdnimg.cn/img_convert/5a19c508ea3be524040f1ec90d3961d7.png)

对应的快捷键一定要记得 **Ctrl** + **F9**

1. 关于热部署

- 重启（Restart）：自定义开发代码，包含类、页面、配置文件等，加载位置restart类加载器 
- 重载（ReLoad）：jar包，加载位置base类加载器

1.  小结 1.开启开发者工具后启用热部署 2.使用构建项目操作启动热部署（Ctrl+F9） 3.热部署仅仅加载当前开发者自定义开发的资源，不加载jar资源 


**步骤①**：设置自动构建项目

​ 打开【File】，选择【settings…】,在面板左侧的菜单中找到【Compile】选项，然后勾选【Build project automatically】，意思是自动构建项目


![img](https://img-blog.csdnimg.cn/img_convert/40a4d59bf7fd741322a72e07d6244145.png)

​ 自动构建项目选项勾选后

**步骤②**：允许在程序运行时进行自动构建

​ 使用快捷键【Ctrl】+【Alt】+【Shit】+【/】打开维护面板，选择第1项【Registry…】


![img](https://img-blog.csdnimg.cn/img_convert/e8b82af3c60b6587af3f1232bd29b3e9.png)


​ 在选项中搜索compile，然后勾选对应项即可 ![img](https://img-blog.csdnimg.cn/da7957c9b38c4f3fa8a948d2ba43f7fa.png)

​ 这样程序在运行的时候就可以进行自动构建了，实现了热部署的效果。

- 激活方式：Idea失去焦点5秒后启动热部署

小结:

​ 1. 设置自动构建用于自动热部署


配置中默认不参与热部署的目录信息如下

- /META-INF/maven 
- /META-INF/resources 
- /resources 
- /static 
- /public 
- /templates

自定义不参与重启排除项

```java
spring:
  devtools:
    restart:
      # 设置不参与热部署的文件或文件夹
      exclude: static/**,public/**,config/application.yml
```

小结:

1. 自定义重启排除项


属性加载优先顺序

1.  参看https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config  

禁用热部署

-  配制文件中 spring:
  devtools:
    restart:
      enabled: false 

​ 如果当心配置文件层级过多导致相符覆盖最终引起配置失效，可以提高配置的层级，在更高层级中配置关闭热部署。例如在启动容器前通过系统属性设置关闭热部署功能。

```java
@SpringBootApplication
public class HotDeployApplication {
   

    public static void main(String[] args) {
   
        //禁用热部署
        System.setProperty("spring.devtools.restart.enabled", "false");
        SpringApplication.run(HotDeployApplication.class);
    }

}
```

小结:

1. 禁用热部署功能

## 总结

1.  手动启动热部署  
2.  自动启动热部署  
3.  热部署范围配置  
4.  关闭热部署 


在基础篇学习了@ConfigurationProperties注解，此注解的作用是用来为bean绑定属性的。开发者可以在yml配置文件中以对象的格式添加若干属性

```java
servers:
  ip-address: 192.168.0.1 
  port: 2345
  timeout: -1
```

​ 然后再开发一个用来封装数据的实体类，注意要提供属性对应的setter方法

```java
@Component
@Data
public class ServerConfig {
   
    private String ipAddress;
    private int port;
    private long timeout;
}
```

​ 使用@ConfigurationProperties注解就可以将配置中的属性值关联到开发的模型类上

```java
@Component
@Data
@ConfigurationProperties(prefix = "servers")
public class ServerConfig {
   
    private String ipAddress;
    private int port;
    private long timeout;
}
```

在启动类里测试

```java
@SpringBootApplication
public class Springboot13ConfigurationApplication {
   

    public static void main(String[] args) {
   
        //获取容器对象
        ConfigurableApplicationContext run = SpringApplication.run(Springboot13ConfigurationApplication.class, args);
        ServerConfig bean = run.getBean(ServerConfig.class);
        System.out.println(bean);

    }
}
```

- 使用@ConfigurationProperties为第三方bean绑定属性

**步骤①**：使用@Bean注解定义第三方bean

```java
@Bean
public DruidDataSource datasource(){
   
    DruidDataSource ds = new DruidDataSource();
    return ds;
}
```

**步骤②**：在yml中定义要绑定的属性，注意datasource此时全小写

```java
datasource:
  driverClassName: com.mysql.jdbc.Driver
```

**步骤③**：使用@ConfigurationProperties注解为第三方bean进行属性绑定，注意前缀是全小写的datasource

```java
@Bean
@ConfigurationProperties(prefix = "datasource")
public DruidDataSource datasource(){
   
    DruidDataSource ds = new DruidDataSource();
    return ds;
}
```

测试:

```java
@SpringBootApplication
public class Springboot13ConfigurationApplication {
   

    @Bean
    @ConfigurationProperties(prefix = "datasource")
    public DruidDataSource datasource() {
   
        DruidDataSource ds = new DruidDataSource();
        return ds;
    }

    public static void main(String[] args) {
   
        //获取容器对象
        ConfigurableApplicationContext run = SpringApplication.run(Springboot13ConfigurationApplication.class, args);
        ServerConfig bean = run.getBean(ServerConfig.class);
        System.out.println(bean);

        DruidDataSource druidDataSource = run.getBean(DruidDataSource.class);
        System.out.println(druidDataSource.getDriverClassName());

    }
}
```

-  @EnableConfigurationProperties 作用: 标注使用@ConfigurationProperties注解绑定属性的bean是哪些 步骤①：在配置类上开启@EnableConfigurationProperties注解，并标注要使用@ConfigurationProperties注解绑定属性的类 <pre><code class="prism language-java"><span class="token annotation punctuation">@SpringBootApplication</span>
<span class="token annotation punctuation">@EnableConfigurationProperties</span><span class="token punctuation">(</span><span class="token class-name">ServerConfig</span><span class="token punctuation">.</span><span class="token keyword">class</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Springboot13ConfigurationApplication</span> <span class="token punctuation">{
     
    <!-- --></span>
<span class="token punctuation">}</span>
</code></pre> 步骤②：在对应的类上直接使用@ConfigurationProperties进行属性绑定 <pre><code class="prism language-java"><span class="token annotation punctuation">@Data</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"servers"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ServerConfig</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> ipAddress<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> port<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">long</span> timeout<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> 当使用@EnableConfigurationProperties注解时，spring会默认将其标注的类定义为bean，因此无需再次声明@Component注解了 注意: @EnableConfigurationProperties与@Component不能同时使用  
-  解除使用@ConfigurationProperties注释警告  出现这个提示后只需要添加一个坐标此提醒就消失了 <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
</dependency> 小结: 
 <ol> 
  - 使用@ConfigurationProperties可以为使用@Bean声明的第三方bean绑定属性 
  - 当使用@EnableConfigurationProperties声明进行属性绑定的bean后，无需使用@Component注解再次进行bean声明 
 </ol> 


即配置文件中的命名格式与变量名的命名格式可以进行格式上的最大化兼容

-  @ConfigurationProperties绑定属性支持属性名宽松绑定  servers:
#  ipAddress: 192.168.0.1       # 驼峰模式
#  ip_address: 192.168.0.2      # 下划线模式
  ip-address: 192.168.0.3      # 烤肉串模式
# IP_ADDRESS: 192.168.0.4      # 常量模式 注意: 宽松绑定不支持注解@Value引用单个属性的方式  <pre><code class="prism language-java">    <span class="token annotation punctuation">@Bean</span>
    <span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"data-source"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">DruidDataSource</span> <span class="token function">datasource</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">DruidDataSource</span> ds <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">DruidDataSource</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> ds<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
</code></pre> @Value和@ConfigurationProperties比较 
 <table> 
  <thead> 
   <tr> 
    <th>项目</th> 
    <th><strong>@ConfigurationProperties</strong></th> 
    <th><strong>@Value</strong></th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td>功能</td> 
    <td>批量注入配置文件中的属性</td> 
    <td>分别指定</td> 
   </tr> 
   <tr> 
    <td>松散绑定（松散语法）</td> 
    <td>支持</td> 
    <td>不支持</td> 
   </tr> 
   <tr> 
    <td>SpEL</td> 
    <td>不支持</td> 
    <td>支持</td> 
   </tr> 
   <tr> 
    <td>JSR-303数据校验</td> 
    <td>支持</td> 
    <td>不支持</td> 
   </tr> 
   <tr> 
    <td>复杂类型封装</td> 
    <td>支持</td> 
    <td>不支持</td> 
   </tr> 
  </tbody> 
 </table>无论配置文件是 yml 还是 properties 他们都能获取到值。 如果说，我们只是在某个业务逻辑中需要获取一下配置文件中的某项值，使用 @Value。 如果说，我们专门编写了一个 JavaBean 来和配置文件进行映射，我们就直接使用@ConfigurationProperties。 小结: 
 <ol> 
  -  @ConfigurationProperties绑定属性支持属性名宽松绑定  
  -  @Value注解不支持松散绑定  
  -  绑定前缀命名命名规则  
  -  绑定前缀名推荐采用烤肉串命名规则，即使用中划线做分隔符  
 </ol> 


-  SpringBoot支持JDK8提供的时间与空间计量单位 <pre><code class="prism language-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@Data</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"servers"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ServerConfig</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> ipAddress<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> port<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">long</span> timeout<span class="token punctuation">;</span>

    <span class="token comment">//时间计量单位</span>
    <span class="token annotation punctuation">@DurationUnit</span><span class="token punctuation">(</span><span class="token class-name">ChronoUnit</span><span class="token punctuation">.</span>MINUTES<span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">Duration</span> serverTimeOut<span class="token punctuation">;</span>

    <span class="token comment">//空间计量单位</span>
    <span class="token annotation punctuation">@DataSizeUnit</span><span class="token punctuation">(</span><span class="token class-name">DataUnit</span><span class="token punctuation">.</span>MEGABYTES<span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">DataSize</span> dataSize<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> 

><strong>Duration</strong>：表示时间间隔，可以通过@DurationUnit注解描述时间单位，例如上例中描述的单位分钟（ChronoUnit.MINUTES）

Druation常用单位如下：


![img](https://img-blog.csdnimg.cn/39741c24aee54e28acc27fc4cdd96a56.png)

DataSize常用单位如下：


![img](https://img-blog.csdnimg.cn/bc15f6effa6744c4a25b544ae556a0db.png)

小结:

1. 常用的计量单位的使用


开启数据校验有助于系统安全性，J2EE规范中JSR303规范定义了一组有关数据校验相关的API

-  开启Bean数据校验 步骤①：开启校验框架 <!--1.导入JSR303规范-->
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
</dependency>
<!--使用hibernate框架提供的校验器做实现-->
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency> 步骤②：在需要开启校验功能的类上使用注解@Validated开启校验功能 <pre><code class="prism language-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@Data</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"servers"</span><span class="token punctuation">)</span>
<span class="token comment">//开启对当前bean的属性注入校验</span>
<span class="token annotation punctuation">@Validated</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ServerConfig</span> <span class="token punctuation">{
     
    <!-- --></span>
<span class="token punctuation">}</span>
</code></pre> 步骤③：对具体的字段设置校验规则 <pre><code class="prism language-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@Data</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"servers"</span><span class="token punctuation">)</span>
<span class="token comment">//开启对当前bean的属性注入校验</span>
<span class="token annotation punctuation">@Validated</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">ServerConfig</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token comment">//设置具体的规则</span>
    <span class="token annotation punctuation">@Max</span><span class="token punctuation">(</span>value <span class="token operator">=</span> <span class="token number">8888</span><span class="token punctuation">,</span>message <span class="token operator">=</span> <span class="token string">"最大值不能超过8888"</span><span class="token punctuation">)</span>
    <span class="token annotation punctuation">@Min</span><span class="token punctuation">(</span>value <span class="token operator">=</span> <span class="token number">202</span><span class="token punctuation">,</span>message <span class="token operator">=</span> <span class="token string">"最小值不能低于202"</span><span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> port<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>  只加Hibernate校验框架坐标也可以实现 

小结:

1. 启用Bean属性校验

-  导入JSR303与Hibernate校验框架坐标  
-  使用@Validated注解启用校验功能  
-  使用具体校验规则规范数据校验格式 


yaml语法规则

-  字面值表达方式 # 字面值表示方式

boolean: TRUE       #TRUE,true,True,FALSE,false ， False 均可
float: 3.14         #6.8523015e+5 # 支持科学计数法
int: 123            #0b1010_0111_0100_1010_1110 # 支持二进制、八进制、十六进制
# null: ~             # 使用 ~ 表示 null
string: HelloWorld  # 字符串可以直接书写
string2: "Hello World"  # 可以使用双引号包裹特殊字符
date: 2018-02-17        # 日期必须使用 yyyy-MM-dd 格式
datetime: 2018-02-17T15:02:31+08:00   # 时间和日期之间使用 T 连接，最后使用 + 代表时区 二进制前缀 0b 八进制前缀 0 十六进制前缀 0X 
 <table> 
  <thead> 
   <tr> 
    <th>进制基数(radix)</th> 
    <th>前缀</th> 
    <th>示例</th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td>二进制 binary</td> 
    <td>0b 0B</td> 
    <td>0b11 = 2+1=3</td> 
   </tr> 
   <tr> 
    <td>八进制 octal</td> 
    <td>0o 0O 0</td> 
    <td>0o11 = 8+1=9</td> 
   </tr> 
   <tr> 
    <td>十进制 decimal</td> 
    <td>无前缀</td> 
    <td>11 = 11</td> 
   </tr> 
   <tr> 
    <td>十六进制 hex</td> 
    <td>0x 0X</td> 
    <td>0x11</td> 
   </tr> 
  </tbody> 
 </table>注意在配制文件中 字符串的书写 加上引号包裹，养成习惯，遇到0开头的数据多注意。 

小结：

1. 注意yaml文件中对于数字的定义支持进制书写格式，如需使用字符串请使用引号明确标注

总结：

1.  @ConfigurationProperties  
2.  宽松绑定/松散绑定  
3.  常用计量单位绑定  
4.  数据校验 


加载测试专用属性

- 在启动测试环境时可以通过properties参数设置测试环境专用的属性

```java
//properties属性可以为当前测试用例添加临时的属性配置
@SpringBootTest(properties = {
   "test.prop=testValue1"})
class PropertiesAndArgsTest {
   

    @Value("${test.prop}")
    private String msg;

    @Test
    void contextLoads() {
   
        System.out.println(msg);
    }

}
```

优势：比多环境开发中的测试环境影响范围更小，仅对当前测试类有效

-  在启动测试环境时可以通过args参数设置测试环境专用的传入参数 <pre><code class="prism language-java"><span class="token comment">//args属性可以为当前测试用例添加临时的命令行参数</span>
<span class="token annotation punctuation">@SpringBootTest</span><span class="token punctuation">(</span>args<span class="token operator">=</span><span class="token punctuation">{
     
    <!-- --></span><span class="token string">"--test.prop=testValue2"</span><span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">PropertiesAndArgsTest</span> <span class="token punctuation">{
     
    <!-- --></span>
    
    <span class="token annotation punctuation">@Value</span><span class="token punctuation">(</span><span class="token string">"${test.prop}"</span><span class="token punctuation">)</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> msg<span class="token punctuation">;</span>
    
    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testProperties</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>msg<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>  当 args参数 与 properties参数 设置共存时, args属性配置优先于properties属性配置加载。 

小结:

1. 加载测试临时属性应用于小范围测试环境


**步骤①**：在测试包test中创建专用的测试环境配置类

```java
@Configuration
public class MsgConfig {
   
    @Bean
    public String msg(){
   
        return "bean msg";
    }
}
```

​ 上述配置仅用于演示当前实验效果，实际开发可不能这么注入String类型的数据

**步骤②**：在启动测试环境时，导入测试环境专用的配置类，使用@Import注解即可实现

```java
@SpringBootTest
@Import({
   MsgConfig.class})
public class ConfigurationTest {
   

    @Autowired
    private String msg;

    @Test
    void testConfiguration(){
   
        System.out.println(msg);
    }
}
```

小结:

1. 加载测试范围配置应用于小范围测试环境


- 模拟端口

每一个springboot的测试类上方都会标准@SpringBootTest注解，而注解带有一个属性，叫做webEnvironment。通过该属性就可以设置在测试用例中启动web环境，具体如下：

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class WebTest {
   

    @Test
    void testRandomPort() {
   

    }
}
```

​ 测试类中启动web环境时，可以指定启动的Web环境对应的端口，springboot提供了4种设置值，分别如下：


![img](https://img-blog.csdnimg.cn/5cb1ef56af424e67a5efb4e9870a2223.png)

- MOCK：根据当前设置确认是否启动web环境，例如使用了Servlet的API就启动web环境，属于适配性的配置 
- DEFINED_PORT：使用自定义的端口作为web服务器端口 
- RANDOM_PORT：使用随机端口作为web服务器端口 
- NONE：不启动web环境


-  新建 BookController <pre><code class="prism language-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BookController</span> <span class="token punctuation">{
     
    <!-- --></span>

    <span class="token annotation punctuation">@GetMapping</span>
    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getById</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"getById is running ....."</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> <span class="token string">"springboot"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>  
-  虚拟请求测试 <pre><code class="prism language-java"><span class="token comment">//1.使用 webEnvironment 属性开启web环境</span>
<span class="token annotation punctuation">@SpringBootTest</span><span class="token punctuation">(</span>webEnvironment <span class="token operator">=</span> <span class="token class-name">SpringBootTest<span class="token punctuation">.</span>WebEnvironment</span><span class="token punctuation">.</span>RANDOM_PORT<span class="token punctuation">)</span>
<span class="token comment">//2.开启虚拟mvc调用</span>
<span class="token annotation punctuation">@AutoConfigureMockMvc</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">WebTest</span> <span class="token punctuation">{
     
    <!-- --></span>

    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testRandomPort</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>

    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@Test</span>
    <span class="token comment">//注入虚拟mvc调用对象</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">testWeb</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Autowired</span> <span class="token class-name">MockMvc</span> mvc<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token comment">//3.创建虚拟请求,当前访问/books</span>
        <span class="token class-name">MockHttpServletRequestBuilder</span> builder <span class="token operator">=</span> <span class="token class-name">MockMvcRequestBuilders</span><span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">//执行请求</span>
        <span class="token class-name">ResultActions</span> actions <span class="token operator">=</span> mvc<span class="token punctuation">.</span><span class="token function">perform</span><span class="token punctuation">(</span>builder<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 


-  虚拟请求状态匹配 <pre><code class="prism language-java"><span class="token annotation punctuation">@Test</span>
<span class="token comment">//注入虚拟mvc调用对象</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">testStatus</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Autowired</span> <span class="token class-name">MockMvc</span> mvc<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token comment">//创建虚拟请求,当前访问/books</span>
    <span class="token class-name">MockHttpServletRequestBuilder</span> builder <span class="token operator">=</span> <span class="token class-name">MockMvcRequestBuilders</span><span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//执行请求</span>
    <span class="token class-name">ResultActions</span> actions <span class="token operator">=</span> mvc<span class="token punctuation">.</span><span class="token function">perform</span><span class="token punctuation">(</span>builder<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//设定预期值 与真实值进行比较，成功测试通过，失败测试失败</span>
    <span class="token comment">//定义本次调用的预期值</span>
    <span class="token class-name">StatusResultMatchers</span> status <span class="token operator">=</span> <span class="token class-name">MockMvcResultMatchers</span><span class="token punctuation">.</span><span class="token function">status</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//预计本次调用时成功的：状态200</span>
    <span class="token class-name">ResultMatcher</span> ok <span class="token operator">=</span> status<span class="token punctuation">.</span><span class="token function">isOk</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//添加预计值到本次调用过程中进行匹配</span>
    actions<span class="token punctuation">.</span><span class="token function">andExpect</span><span class="token punctuation">(</span>ok<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token punctuation">}</span>
</code></pre> 匹配失败的信息提示如: java.lang.AssertionError: Status expected:<200> but was:<404>
Expected :200
Actual   :404
 <Click to see difference> 


-  响应体匹配（非json数据格式） <pre><code class="prism language-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">void</span> <span class="token function">testBody</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Autowired</span> <span class="token class-name">MockMvc</span> mvc<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token class-name">MockHttpServletRequestBuilder</span> builder <span class="token operator">=</span> <span class="token class-name">MockMvcRequestBuilders</span><span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">ResultActions</span> action <span class="token operator">=</span> mvc<span class="token punctuation">.</span><span class="token function">perform</span><span class="token punctuation">(</span>builder<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//设定预期值 与真实值进行比较，成功测试通过，失败测试失败</span>
    <span class="token comment">//定义本次调用的预期值</span>
    <span class="token class-name">ContentResultMatchers</span> content <span class="token operator">=</span> <span class="token class-name">MockMvcResultMatchers</span><span class="token punctuation">.</span><span class="token function">content</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">ResultMatcher</span> result <span class="token operator">=</span> content<span class="token punctuation">.</span><span class="token function">string</span><span class="token punctuation">(</span><span class="token string">"springboot2"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//添加预计值到本次调用过程中进行匹配</span>
    action<span class="token punctuation">.</span><span class="token function">andExpect</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> 匹配失败的信息提示如: MockHttpServletResponse:
           Status = 200
    Error message = null
          Headers = [Content-Type:"text/plain;charset=UTF-8", Content-Length:"10"]
     Content type = text/plain;charset=UTF-8
             Body = springboot
    Forwarded URL = null
   Redirected URL = null
          Cookies = []

java.lang.AssertionError: Response content expected:<springboot2> but was:<springboot>
Expected :springboot2
Actual   :springboot
 <Click to see difference> 


-  响应体匹配（json数据格式，开发中的主流使用方式） 创建 book 实体类 <pre><code class="prism language-java"><span class="token annotation punctuation">@Data</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Book</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token keyword">private</span> <span class="token class-name">Integer</span> id<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> type<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> name<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> description<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> 修改 BookController <pre><code class="prism language-java"><span class="token annotation punctuation">@RestController</span>
<span class="token annotation punctuation">@RequestMapping</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BookController</span> <span class="token punctuation">{
     
    <!-- --></span>

    <span class="token annotation punctuation">@GetMapping</span>
    <span class="token keyword">public</span> <span class="token class-name">String</span> <span class="token function">getById</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"getById is running ....."</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> <span class="token string">"springboot"</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token annotation punctuation">@GetMapping</span><span class="token punctuation">(</span><span class="token string">"{id}"</span><span class="token punctuation">)</span>
    <span class="token keyword">public</span> <span class="token class-name">Book</span> <span class="token function">getById1</span><span class="token punctuation">(</span><span class="token annotation punctuation">@PathVariable</span> <span class="token keyword">int</span> id<span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span><span class="token string">"getById is running ....."</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">Book</span> book <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Book</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setId</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setName</span><span class="token punctuation">(</span><span class="token string">"springboot"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setType</span><span class="token punctuation">(</span><span class="token string">"springboot"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setDescription</span><span class="token punctuation">(</span><span class="token string">"springboot"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span> book<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

<span class="token punctuation">}</span>
</code></pre> 测试方法 <pre><code class="prism language-java">    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testJson</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Autowired</span> <span class="token class-name">MockMvc</span> mvc<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">MockHttpServletRequestBuilder</span> builder <span class="token operator">=</span> <span class="token class-name">MockMvcRequestBuilders</span><span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">"/books/1"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">ResultActions</span> action <span class="token operator">=</span> mvc<span class="token punctuation">.</span><span class="token function">perform</span><span class="token punctuation">(</span>builder<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">//设定预期值 与真实值进行比较，成功测试通过，失败测试失败</span>
        <span class="token comment">//定义本次调用的预期值</span>
        <span class="token class-name">ContentResultMatchers</span> content <span class="token operator">=</span> <span class="token class-name">MockMvcResultMatchers</span><span class="token punctuation">.</span><span class="token function">content</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">ResultMatcher</span> result <span class="token operator">=</span> content<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token string">"{\"id\":1,\"name\":\"springboot2\",\"type\":\"springboot\"}"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token comment">//添加预计值到本次调用过程中进行匹配</span>
        action<span class="token punctuation">.</span><span class="token function">andExpect</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
</code></pre> 匹配失败的信息提示如:  


-  虚拟请求响应头匹配 <pre><code class="prism language-java"><span class="token annotation punctuation">@Test</span>
<span class="token keyword">void</span> <span class="token function">testContentType</span><span class="token punctuation">(</span><span class="token annotation punctuation">@Autowired</span> <span class="token class-name">MockMvc</span> mvc<span class="token punctuation">)</span> <span class="token keyword">throws</span> <span class="token class-name">Exception</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token class-name">MockHttpServletRequestBuilder</span> builder <span class="token operator">=</span> <span class="token class-name">MockMvcRequestBuilders</span><span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">"/books"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">ResultActions</span> action <span class="token operator">=</span> mvc<span class="token punctuation">.</span><span class="token function">perform</span><span class="token punctuation">(</span>builder<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//设定预期值 与真实值进行比较，成功测试通过，失败测试失败</span>
    <span class="token comment">//定义本次调用的预期值</span>
    <span class="token class-name">HeaderResultMatchers</span> header <span class="token operator">=</span> <span class="token class-name">MockMvcResultMatchers</span><span class="token punctuation">.</span><span class="token function">header</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token class-name">ResultMatcher</span> contentType <span class="token operator">=</span> header<span class="token punctuation">.</span><span class="token function">string</span><span class="token punctuation">(</span><span class="token string">"Content-Type"</span><span class="token punctuation">,</span> <span class="token string">"application/json"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment">//添加预计值到本次调用过程中进行匹配</span>
    action<span class="token punctuation">.</span><span class="token function">andExpect</span><span class="token punctuation">(</span>contentType<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> 匹配失败的信息提示如:  

​ 基本上齐了，头信息，正文信息，状态信息都有了，就可以组合出一个完美的响应结果比对结果了。以下范例就是三种信息同时进行匹配校验，也是一个完整的信息匹配过程。

```java
@Test
    void testGetById(@Autowired MockMvc mvc) throws Exception {
   
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books/1");
        ResultActions action = mvc.perform(builder);

        StatusResultMatchers status = MockMvcResultMatchers.status();
        ResultMatcher ok = status.isOk();
        action.andExpect(ok);

        HeaderResultMatchers header = MockMvcResultMatchers.header();
        ResultMatcher contentType = header.string("Content-Type", "application/json");
        action.andExpect(contentType);

        ContentResultMatchers content = MockMvcResultMatchers.content();
        ResultMatcher result = content.json("{\"id\":1,\"name\":\"springboot\",\"type\":\"springboot\"}");
        action.andExpect(result);
    }
```

小结:

1. web环境模拟测试

-  设置测试端口  
-  模拟测试启动  
-  模拟测试匹配（各组成部分信息均可匹配） 


-  为测试用例添加事务，SpringBoot会对测试用例对应的事务提交操作进行回滚 <pre><code class="prism language-java"><span class="token annotation punctuation">@SpringBootTest</span>
<span class="token annotation punctuation">@Transactional</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">DaoTest</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">private</span> <span class="token class-name">BookService</span> bookService<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testSave</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">Book</span> book <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Book</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setName</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setType</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setDescription</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        bookService<span class="token punctuation">.</span><span class="token function">save</span><span class="token punctuation">(</span>book<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>  
-  如果想在测试用例中提交事务，可以通过@Rollback注解设置回滚状态为false即可正常提交事务 <pre><code class="prism language-java"><span class="token annotation punctuation">@SpringBootTest</span>
<span class="token annotation punctuation">@Transactional</span>
<span class="token annotation punctuation">@Rollback</span><span class="token punctuation">(</span><span class="token boolean">false</span><span class="token punctuation">)</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">DaoTest</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">private</span> <span class="token class-name">BookService</span> bookService<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testSave</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">Book</span> book <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">Book</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setName</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setType</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        book<span class="token punctuation">.</span><span class="token function">setDescription</span><span class="token punctuation">(</span><span class="token string">"springboot3"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

        bookService<span class="token punctuation">.</span><span class="token function">save</span><span class="token punctuation">(</span>book<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 

小结:

1. 在springboot的测试类中通过添加注解@Transactional来阻止测试用例提交事务 
2. 通过注解@Rollback控制springboot测试类执行结果是否提交事务，需要配合注解@Transactional使用


-  测试用例数据通常采用随机值进行测试，使用SpringBoot提供的随机数为其赋值 ①yml中设置随机值 <pre><code class="prism language-yaml"><span class="token key atrule">testcase</span><span class="token punctuation">:</span>
  <span class="token key atrule">book</span><span class="token punctuation">:</span>
    <span class="token key atrule">id</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.int<span class="token punctuation">}</span>
    <span class="token key atrule">id2</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.int(10)<span class="token punctuation">}</span>
    <span class="token key atrule">type</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.int<span class="token tag">!5</span><span class="token punctuation">,</span>10<span class="token tag">!</span><span class="token punctuation">}</span>
    <span class="token key atrule">name</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.value<span class="token punctuation">}</span>
    <span class="token key atrule">uuid</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.uuid<span class="token punctuation">}</span>
    <span class="token key atrule">publishTime</span><span class="token punctuation">:</span> $<span class="token punctuation">{
     
    <!-- --></span>random.long<span class="token punctuation">}</span>
</code></pre> ②创建 BookCase 类封装数据 <pre><code class="prism language-java"><span class="token comment">//1.定义数据模型封装yaml文件中对应的数据</span>
<span class="token comment">//2.定义为spring管控的bean</span>
<span class="token annotation punctuation">@Component</span>
<span class="token comment">//3.指定加载的数据</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"testcase.book"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Data</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BookCase</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> id<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> id2<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> type<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> name<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> uuid<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">long</span> publishTime<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre> ③测试 <pre><code class="prism language-java"><span class="token annotation punctuation">@SpringBootTest</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BookCaseRandom</span> <span class="token punctuation">{
     
    <!-- --></span>

    <span class="token annotation punctuation">@Autowired</span>
    <span class="token keyword">private</span> <span class="token class-name">BookCase</span> bookCase<span class="token punctuation">;</span>

    <span class="token annotation punctuation">@Test</span>
    <span class="token keyword">void</span> <span class="token function">testProperties</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>bookCase<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 对于随机值的产生，还有一些小的限定规则，比如产生的数值性数据可以设置范围等，具体如下： 


![img](https://img-blog.csdnimg.cn/97dfd0e66eda49db90a548a01503b101.png)

- ${random.int}表示随机整数 
- ${random.int(10)}表示10以内的随机数 
- ${random.int(10,20)}表示10到20的随机数 
- 其中()可以是任意字符，例如[]，!!均可

小结:

1. 使用随机数据替换测试用例中书写固定的数据

## 总结:

1.  加载测试专用属性  
2.  加载测试专用配置  
3.  Web环境模拟测试  
4.  数据层测试回滚  
5.  测试用例数据设定 


1.现有数据层解决方案技术选型 Mysql+Druid+MyBatisPlus

- 数据源：DruidDataSource 
- 持久化技术：MyBatis-Plus / MyBatis 
- 数据库：MySQL

​ 目前我们使用的数据源技术是Druid，运行时可以在日志中看到对应的数据源初始化信息，具体如下：

```java
INFO 28600 --- [           main] c.a.d.s.b.a.DruidDataSourceAutoConfigure : Init DruidDataSource
INFO 28600 --- [           main] com.alibaba.druid.pool.DruidDataSource   : {dataSource-1} inited
```

​ 如果不配制数据源默认是 HikariDataSource

2.数据源配置格式

-  格式一 （通用配制未声明数据源技术）默认是 hikari 数据源 spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
    username: root
    password: 123456  
-  格式二 (配制指定的数据源需要导入对应的 starter) # druid 数据源配制
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
      username: root
      password: 123456 # hikari 数据源配制 url地址要单独配置
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
    hikari:
      driver-class-name: com.mysql.cj.jdbc.Driver
      username: root
      password: root 

3.数据源配置

​ springboot提供了3款内嵌数据源技术，分别如下：

- HikariCP：默认内置数据源对象 
- Tomcat提供DataSource：HikariCP不可用的情况下，且在web环境中，将使用tomcat服务器配置的数据源对象 
- Commons DBCP：Hikari不可用，tomcat数据源也不可用，将使用dbcp数据源

4.通用配置无法设置具体的数据源配置信息，仅提供基本的连接相关配置，如需配置，在下一级配置中设置具体设定

```java
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springboot_db?serverTimezone=UTC
    username: root
    password: 123456
    hikari:
      maximum-pool-size: 50
```

**小结**

1. SpringBoot内置3款数据源可供选择

-  HikariCP（默认）  
-  Tomcat提供DataSource  
-  Commons DBCP 


- 内置持久化解决方案——JdbcTemplate

**步骤①**：导入jdbc对应的坐标，记得是starter

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

**步骤②**：自动装配JdbcTemplate对象

```java
@SpringBootTest
class Springboot15SqlApplicationTests {
   
    @Test
    void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate){
   
    }
}
```

**步骤③**：使用JdbcTemplate实现查询操作（非实体类封装数据的查询操作）

```java
@Test
void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate){
   
    String sql = "select * from tbl_book";
    List<Map<String, Object>> maps = jdbcTemplate.queryForList(sql);
    System.out.println(maps);
}
```

**步骤④**：使用JdbcTemplate实现查询操作（实体类封装数据的查询操作）

```java
@Test
void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate){
   

    String sql = "select * from tbl_book";
    RowMapper<Book> rm = new RowMapper<Book>() {
   
        @Override
        public Book mapRow(ResultSet rs, int rowNum) throws SQLException {
   
            Book temp = new Book();
            temp.setId(rs.getInt("id"));
            temp.setName(rs.getString("name"));
            temp.setType(rs.getString("type"));
            temp.setDescription(rs.getString("description"));
            return temp;
        }
    };
    List<Book> list = jdbcTemplate.query(sql, rm);
    System.out.println(list);
}
```

**步骤⑤**：使用JdbcTemplate实现增删改操作

```java
@Test
void testJdbcTemplateSave(@Autowired JdbcTemplate jdbcTemplate){
   
    String sql = "insert into tbl_book values(3,'springboot1','springboot2','springboot3')";
    jdbcTemplate.update(sql);
}
```

​ 如果想对JdbcTemplate对象进行相关配置，可以在yml文件中进行设定，具体如下：

```java
spring:
  jdbc:
    template:
      query-timeout: -1   # 查询超时时间
      max-rows: 500       # 最大行数
      fetch-size: -1      # 缓存行数
```

**小结**

1. SpringBoot内置JdbcTemplate持久化解决方案 
2. 使用JdbcTemplate需要导入spring-boot-starter-jdbc的坐标


SpringBoot提供了3种内嵌数据库供开发者选择，提高开发测试效率

- H2 
- HSQL 
- Derby

内嵌数据库（H2）

**步骤①**：导入H2数据库对应的坐标，一共2个

```java
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

**步骤②**：将工程设置为web工程，启动工程时启动H2数据库

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**步骤③**：通过配置开启H2数据库控制台访问程序，也可以使用其他的数据库连接软件操作

```java
spring:
  h2:
    console:
      enabled: true
      path: /h2
```

​ web端访问路径/h2，访问密码123456，如果访问失败，先配置下列数据源，启动程序运行后再次访问/h2路径就可以正常访问了

```java
datasource:
  url: jdbc:h2:~/test
  hikari:
    driver-class-name: org.h2.Driver
    username: sa
    password: 123456
```

## 运行报错

>org.h2.jdbc.JdbcSQLInvalidAuthorizationSpecException: Wrong user name or password [28000-200]

原因: 我们之前创建过该数据库，H2数据库会初始化用户名和密码，配置文件又中重新定义了数据库的用户名和密码，造成了冲突。

解决:

处理方案一：删除原来的数据库 (C:\Users\你的用户名)


![img](https://img-blog.csdnimg.cn/img_convert/3f47c26bf7d964ff8a332984dfc10d37.png)

处理方案二：修改一个不存在的数据库名称


![img](https://img-blog.csdnimg.cn/img_convert/e7d3e93943dbff2eb61742354fa07c59.png)

- 操作数据库（创建表）

```java
create table tbl_book (id int,name varchar,type varchar,description varchar)
```


![img](https://img-blog.csdnimg.cn/img_convert/e1d2eb285ec7152f5c8b97a75740fd64.png)

**步骤④**：使用JdbcTemplate或MyBatisPlus技术操作数据库

记得测试的时候 要web服务器给关了,不然会报如下错误

>Caused by: org.h2.jdbc.JdbcSQLNonTransientConnectionException: Database may be already in use: null. Possible solutions: close all other connection(s); use the server mode [90020-200]

```java
@SpringBootTest
class Springboot15SqlApplicationTests {
   

    @Autowired
    private BookDao bookDao;

    @Test
    void contextLoads() {
   
        Book book = bookDao.selectById(1);
        System.out.println(book);
    }

    /**
     * 非实体类封装数据的查询操作
     *
     * @param jdbcTemplate
     */
    @Test
    void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate) {
   
        String sql = "select * from tbl_book";
        List<Map<String, Object>> maps = jdbcTemplate.queryForList(sql);
        System.out.println(maps);
    }

    /**
     * 实体类封装数据的查询操作
     *
     * @param jdbcTemplate
     */
    @Test
    void testJdbcTemplate1(@Autowired JdbcTemplate jdbcTemplate) {
   
        String sql = "select * from tbl_book";
        RowMapper<Book> rm = new RowMapper<Book>() {
   
            @Override
            public Book mapRow(ResultSet rs, int rowNum) throws SQLException {
   
                Book temp = new Book();
                temp.setId(rs.getInt("id"));
                temp.setName(rs.getString("name"));
                temp.setType(rs.getString("type"));
                temp.setDescription(rs.getString("description"));
                return temp;
            }
        };
        List<Book> list = jdbcTemplate.query(sql, rm);
        System.out.println(list);
    }

    @Test
    void testJdbcTemplateSave(@Autowired JdbcTemplate jdbcTemplate) {
   
        String sql = "insert into tbl_book values(3,'springboot1','springboot2','springboot3')";
        jdbcTemplate.update(sql);
    }
}
```

- SpringBoot可以根据url地址自动识别数据库种类，在保障驱动类存在的情况下，可以省略配置

```java
#h2 数据库配制
spring:
  h2:
    console:
      enabled: true
      path: /h2
  datasource:
    url: jdbc:h2:~/test
    hikari:
#      driver-class-name: org.h2.Driver
      username: sa
      password: sa
```


![img](https://img-blog.csdnimg.cn/img_convert/ff1f089fbf7f5aba9b3dd8c5a9493d2c.png)

**小结**

1. H2内嵌式数据库启动方式，添加坐标，添加配置 
2. H2数据库线上运行时请务必关闭


![img](https://img-blog.csdnimg.cn/img_convert/bba648057445e0d9430ae5de3e1f69ed.png)

总结:

1.  数据源配置（Hikari）  
2.  持久化技术（JdbcTemplate）  
3.  数据库（H2） 


市面上常见的NoSQL解决方案

- Redis 
- Mongo 
- ES 
- Solr

Redis

-  Redis是一款key-value存储结构的内存级NoSQL数据库 
 <ul> 
  -  支持多种数据存储格式  
  -  支持持久化  
  -  支持集群  
 </ul>  
-  Redis下载（ Windows版） 
 <ul> 
  - https://github.com/tporadowski/redis/releases 
 </ul>  
-  Redis安装与启动（ Windows版） 
 <ul> 
  -  Windows解压安装或一键式安装  
  -  服务端启动命令 redis-server.exe redis.windows.conf  
  -  客户端启动命令 redis-cli.exe 如果启动redis服务器失败，可以先启动客户端，然后执行shutdown操作后退出，此时redis服务器就可以正常执行了。  
 </ul> 

## 基本操作

​ 服务器启动后，使用客户端就可以连接服务器，类似于启动完MySQL数据库，然后启动SQL命令行操作数据库。

​ 放置一个字符串数据到redis中，先为数据定义一个名称，比如name,age等，然后使用命令set设置数据到redis服务器中即可

```java
set name itheima
set age 12
```

​ 从redis中取出已经放入的数据，根据名称取，就可以得到对应数据。如果没有对应数据就会得到(nil)

```java
get name
get age
```

​ 以上使用的数据存储是一个名称对应一个值，如果要维护的数据过多，可以使用别的数据存储结构。例如hash，它是一种一个名称下可以存储多个数据的存储模型，并且每个数据也可以有自己的二级存储名称。向hash结构中存储数据格式如下：

```java
hset a a1 aa1		#对外key名称是a，在名称为a的存储模型中，a1这个key中保存了数据aa1
hset a a2 aa2
```

​ 获取hash结构中的数据命令如下

```java
hget a a1			#得到aa1
hget a a2			#得到aa2
```

小结:

1.  Redis安装（Windows版）  
2.  Redis基本操作 


**步骤①**：导入springboot整合redis的starter坐标

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

​ 上述坐标可以在创建模块的时候通过勾选的形式进行选择，归属NoSQL分类中


![img](https://img-blog.csdnimg.cn/09f4a699ac794e249205b1109d9ff4c3.png)

**步骤②**：进行基础配置

```java
spring:
  redis:
    host: localhost
    port: 6379
```

​ 操作redis，最基本的信息就是操作哪一台redis服务器，所以服务器地址属于基础配置信息，不可缺少。但是即便你不配置，目前也是可以用的。因为以上两组信息都有默认配置，刚好就是上述配置值。

**步骤③**：使用springboot整合redis的专用客户端接口操作，此处使用的是RedisTemplate

```java
@SpringBootTest
class Springboot16RedisApplicationTests {
   
    @Autowired
    private RedisTemplate redisTemplate;
    @Test
    void set() {
   
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("age",41);
    }
    @Test
    void get() {
   
        ValueOperations ops = redisTemplate.opsForValue();
        Object age = ops.get("age");
        System.out.println(age);
    }
    @Test
    void hset() {
   
        HashOperations ops = redisTemplate.opsForHash();
        ops.put("info","b","bb");
    }
    @Test
    void hget() {
   
        HashOperations ops = redisTemplate.opsForHash();
        Object val = ops.get("info", "b");
        System.out.println(val);
    }
}
```

​ 在操作redis时，需要先确认操作何种数据，根据数据种类得到操作接口。例如使用opsForValue()获取string类型的数据操作接口，使用opsForHash()获取hash类型的数据操作接口，剩下的就是调用对应api操作了。各种类型的数据操作接口如下：


![img](https://img-blog.csdnimg.cn/5ca6ee344d4e453abed0fd0c3133013e.png)

小结:

1.SpringBoot整合Redis

-  导入redis对应的starter  
-  配置  
-  提供操作Redis接口对象RedisTemplate 
 <ul> 
  - ops*：获取各种数据类型操作接口 
 </ul> 


RedisTemplate以对象作为key和value，内部对数据进行序列化

```java
@SpringBootTest
class Springboot16NosqlApplicationTests {
   
    @Test
    void set(@Autowired RedisTemplate redisTemplate) {
   
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("testKey","testValue");
    }
    @Test
    void get(@Autowired RedisTemplate redisTemplate) {
   
        ValueOperations ops = redisTemplate.opsForValue();
        Object val = ops.get("testKey");
        System.out.println(val);
    }
}
```

StringRedisTemplate以字符串作为key和value，与**Redis客户端操作等效**

```java
@SpringBootTest
class Springboot16NosqlApplicationTests {
   
    @Test
    void set(@Autowired StringRedisTemplate redisTemplate) {
   
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("testKey","testValue");
    }
    @Test
    void get(@Autowired StringRedisTemplate redisTemplate) {
   
        ValueOperations ops = redisTemplate.opsForValue();
        Object val = ops.get("testKey");
        System.out.println(val);
    }
}
```

小结:

1.  RedisTemplate  
2.  StringRedisTemplate（常用） 


```java
springboot整合redis技术提供了多种客户端兼容模式，默认提供的是lettucs客户端技术，也可以根据需要切换成指定客户端技术，例如jedis客户端技术，切换成jedis客户端技术操作步骤如下：
```

**步骤①**：导入jedis坐标

```java
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

​ jedis坐标受springboot管理，无需提供版本号

**步骤②**：配置客户端技术类型，设置为jedis

```java
spring:
  redis:
    host: localhost
    port: 6379
    client-type: jedis
```

**步骤③**：根据需要设置对应的配置

```java
spring:
  redis:
    host: localhost
    port: 6379
    client-type: jedis
    lettuce:
      pool:
        max-active: 16
    jedis:
      pool:
        max-active: 16
```

**lettcus与jedis区别**

- jedis连接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响 
- lettcus基于Netty框架进行与Redis服务器连接，底层设计中采用StatefulRedisConnection。 StatefulRedisConnection自身是线程安全的，可以保障并发访问安全问题，所以一个连接可以被多线程复用。当然lettcus也支持多连接实例一起工作

小结:

1. SpringBoot整合Redis客户端选择

-  lettuce（默认）  
-  jedis 


MongoDB是一个开源、高性能、无模式的文档型数据库。NoSQL数据库产品中的一种，是最像关系型数据库的非关系型数据库

无模式:

​ 没有固定的数据存储结构，第一条数据可能有A、B、C一共3个字段，第二条数据可能有D、E、F也是3个字段，第三条数据可能是A、C、E3个字段，也就是说数据的结构不固定，这就是无模式

MongoDB的使用场景

- 淘宝用户数据 
 <ul> 
  - 存储位置：数据库 
  - 特征：永久性存储，修改频度极低 
 </ul>  
- 游戏装备数据、游戏道具数据 
 <ul> 
  - 存储位置：数据库、Mongodb 
  - 特征：永久性存储与临时存储相结合、修改频度较高 
 </ul>  
- 直播数据、打赏数据、粉丝数据 
 <ul> 
  - 存储位置：数据库、Mongodb 
  - 特征：永久性存储与临时存储相结合，修改频度极高 
 </ul>  
- 物联网数据 
 <ul> 
  - 存储位置：Mongodb 
  - 特征：临时存储，修改频度飞速 
 </ul> 


Windows版Mongo下载

- https://www.mongodb.com/try/download

Windows版Mongo安装

- 解压缩后设置数据目录 
- 通常放置在安装目录中，此处创建data的目录用来存储数据

Windows版Mongo启动(在bin目录下)

- **启动服务器**

```java
mongod --dbpath=..\data\db
```

​ 启动服务器时需要指定数据存储位置，通过参数–dbpath进行设置，可以根据需要自行设置数据存储路径。默认服务端口27017。

- **启动客户端**

```java
mongo --host=127.0.0.1 --port=27017
```


![img](https://img-blog.csdnimg.cn/img_convert/91ea000c2d61d95d4efe12878488b15b.png)

Windows版Mongo安装问题及解决方案


![img](https://img-blog.csdnimg.cn/img_convert/4fbac7db147e58af702863699e8823ec.png)

-  步骤一：下载对应的dll文件（通过互联网搜索即可）  
-  步骤二：拷贝到windows安装路径下的system32目录中  
-  步骤三：执行命令注册对应dll文件 regsvr32 vcruntime140_1.dll 

可视化客户端——Robo 3T

Robot3t是一款绿色软件，无需安装，解压缩即可。解压缩完毕后进入安装目录双击robot3t.exe即可使用。


![img](https://img-blog.csdnimg.cn/07e16d661b354ebb90811b3ba4d596af.png)

​ 打开软件首先要连接MongoDB服务器，选择【File】菜单，选择【Connect…】


![img](https://img-blog.csdnimg.cn/img_convert/12b6fb9e4f540ec76bc786cdb602336b.png)

​ 进入连接管理界面后，选择左上角的【Create】链接，创建新的连接设置


![img](https://img-blog.csdnimg.cn/4e128c4b5a4c441f9cfa325a1a21de00.png)

​ 如果输入设置值即可连接（默认不修改即可连接本机27017端口）


![img](https://img-blog.csdnimg.cn/img_convert/7b4f286e1290460d78d807beb67dee59.png)

​

小结:

1.  Mongodb安装、启动  
2.  可视化客户端Robo 3T安装与连接 


创建数据库：在左侧菜单中使用右键创建，输入数据库名称即可

创建集合：在Collections上使用右键创建，输入集合名称即可，集合等同于数据库中的表的作用

新增文档：（文档是一种类似json格式的数据，初学者可以先把数据理解为就是json数据）

```java
db.集合名称.insert/save/insertOne(文档)
```

```java
db.book.save({name: "张三"})
db.book.save({name: "张三",type: "zs"})
```

删除文档：

```java
db.集合名称.remove(条件)
```

​ 修改文档：

```java
db.集合名称.update(条件，{操作种类:{文档}})
```

例:

```java
// 添加
//db.book.save({name: "张三"})
//db.book.save({name: "张三",type: "zs"})

//修改
db.book.update({type: "zs"},{name: "张三峰"})

//删除
//db.book.deleteOne({type: "zs"})
```

查询文档：

```java
基础查询
查询全部：		   db.集合.find();
查第一条：		   db.集合.findOne()
查询指定数量文档：	db.集合.find().limit(10)					//查10条文档
跳过指定数量文档：	db.集合.find().skip(20)					//跳过20条文档
统计：			  	db.集合.count()
排序：				db.集合.sort({age:1})						//按age升序排序
投影：				db.集合名称.find(条件,{name:1,age:1})		 //仅保留name与age域

条件查询
基本格式：			db.集合.find({条件})
模糊查询：			db.集合.find({域名:/正则表达式/})		  //等同SQL中的like，比like强大，可以执行正则所有规则
条件比较运算：		   db.集合.find({域名:{$gt:值}})				//等同SQL中的数值比较操作，例如：name>18
包含查询：			db.集合.find({域名:{$in:[值1，值2]}})		//等同于SQL中的in
条件连接查询：		   db.集合.find({$and:[{条件1},{条件2}]})	   //等同于SQL中的and、or
```

小结:

1. Mongodb基础CRUD


**步骤①**：导入springboot整合MongoDB的starter坐标

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

​ 上述坐标也可以在创建模块的时候通过勾选的形式进行选择，同样归属NoSQL分类中


![img](https://img-blog.csdnimg.cn/1bb98ef757c74c5c9ac69c00cdaf097a.png)

**步骤②**：进行基础配置

```java
spring:
  data:
    mongodb:
      uri: mongodb://localhost/itheima
```

​ 操作MongoDB需要的配置与操作redis一样，最基本的信息都是操作哪一台服务器，区别就是连接的服务器IP地址和端口不同，书写格式不同而已。

**步骤③**：使用springboot整合MongoDB的专用客户端接口MongoTemplate来进行操作

```java
@SpringBootTest
class Springboot17MongodbApplicationTests {
   
    @Autowired
    private MongoTemplate mongoTemplate;
    @Test
    void contextLoads() {
   
        Book book = new Book();
        book.setId(2);
        book.setName("springboot2");
        book.setType("springboot2");
        book.setDescription("springboot2");
        mongoTemplate.save(book);
    }
    @Test
    void find(){
   
        List<Book> all = mongoTemplate.findAll(Book.class);
        System.out.println(all);
    }
}
```

小结:

1. SpringBoot整合Mongodb

-  导入Mongodb对应的starter  
-  配置mongodb访问uri  
-  提供操作Mongodb接口对象MongoTemplate 


ES（Elasticsearch）是一个分布式全文搜索引擎，重点是全文搜索。

​ 那什么是全文搜索呢？比如用户要买一本书，以Java为关键字进行搜索，不管是书名中还是书的介绍中，甚至是书的作者名字，只要包含java就作为查询结果返回给用户查看，上述过程就使用了全文搜索技术。搜索的条件**不再是仅用于对某一个字段进行比对**，而是在一条数据中使用**搜索条件去比对更多的字段**，只要能匹配上就列入查询结果，这就是全文搜索的目的。而ES技术就是一种可以实现上述效果的技术。

​ 要实现全文搜索的效果，不可能使用数据库中like操作去进行比对，这种效率太低了。ES设计了一种全新的思想，来实现全文搜索。具体操作过程如下：

1.  将被查询的字段的数据全部文本信息进行查分，分成若干个词 
 <ul> 
  1. 例如“中华人民共和国”就会被拆分成三个词，分别是“中华”、“人民”、“共和国”，此过程有专业术语叫做分词。分词的策略不同，分出的效果不一样，不同的分词策略称为分词器。 
 </ul>  
3.  将分词得到的结果存储起来，对应每条数据的id 
 <ul> 
  3.  例如id为1的数据中名称这一项的值是“中华人民共和国”，那么分词结束后，就会出现“中华”对应id为1，“人民”对应id为1，“共和国”对应id为1  
  3.  例如id为2的数据中名称这一项的值是“人民代表大会“，那么分词结束后，就会出现“人民”对应id为2，“代表”对应id为2，“大会”对应id为2  
  3.  此时就会出现如下对应结果，按照上述形式可以对所有文档进行分词。需要注意分词的过程不是仅对一个字段进行，而是对每一个参与查询的字段都执行，最终结果汇总到一个表格中 
   <table> 
    <thead> 
     <tr> 
      <th>分词结果关键字</th> 
      <th>对应id</th> 
     </tr> 
    </thead> 
    <tbody> 
     <tr> 
      <td>中华</td> 
      <td>1</td> 
     </tr> 
     <tr> 
      <td>人民</td> 
      <td>1,2</td> 
     </tr> 
     <tr> 
      <td>共和国</td> 
      <td>1</td> 
     </tr> 
     <tr> 
      <td>代表</td> 
      <td>2</td> 
     </tr> 
     <tr> 
      <td>大会</td> 
      <td>2</td> 
     </tr> 
    </tbody> 
   </table> 
 </ul>  
7.  当进行查询时，如果输入“人民”作为查询条件，可以通过上述表格数据进行比对，得到id值1,2，然后根据id值就可以得到查询的结果数据了。(倒排索引)  

小结:

1.  ES应用场景  
2.  ES相关概念 


windows版安装包下载地址： [https://](https://www.elastic.co/cn/downloads/elasticsearch) [www.elastic.co/cn/downloads/elasticsearch](https://www.elastic.co/cn/downloads/elasticsearch)

​ 下载的安装包是解压缩就能使用的zip文件，解压缩完毕后会得到如下文件


![img](https://img-blog.csdnimg.cn/img_convert/ec64b3dee09294304d4621232cfe82f8.png)

- bin目录：包含所有的可执行命令 
- config目录：包含ES服务器使用的配置文件 
- jdk目录：此目录中包含了一个完整的jdk工具包，版本17，当ES升级时，使用最新版本的jdk确保不会出现版本支持性不足的问题 
- lib目录：包含ES运行的依赖jar文件 
- logs目录：包含ES运行后产生的所有日志文件 
- modules目录：包含ES软件中所有的功能模块，也是一个一个的jar包。和jar目录不同，jar目录是ES运行期间依赖的jar包，modules是ES软件自己的功能jar包 
- plugins目录：包含ES软件安装的插件，默认为空

**启动服务器**

```java
运行 elasticsearch.bat
```

​ 双击elasticsearch.bat文件即可启动ES服务器，默认服务端口9200。通过浏览器访问http://localhost:9200看到如下信息视为ES服务器正常启动

```java
{
  "name" : "CZBK-**********",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "j137DSswTPG8U4Yb-0T1Mg",
  "version" : {
    "number" : "7.16.2",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "2b937c44140b6559905130a8650c64dbd0879cfb",
    "build_date" : "2021-12-18T19:42:46.604893745Z",
    "build_snapshot" : false,
    "lucene_version" : "8.10.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```


ES中保存有我们要查询的数据，只不过格式和数据库存储数据格式不同而已。在ES中我们要先创建倒排索引，这个索引的功能又点类似于数据库的表，然后将数据添加到倒排索引中，添加的数据称为文档。所以要进行ES的操作要先创建索引，再添加文档，这样才能进行后续的查询操作。

​ 要操作ES可以通过Rest风格的请求来进行，也就是说发送一个请求就可以执行一个操作。比如新建索引，删除索引这些操作都可以使用发送请求的形式来进行。

-  创建索引，books是索引名称，下同 PUT请求		http://localhost:9200/books 发送请求后，看到如下信息即索引创建成功 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"acknowledged"</span><span class="token operator">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    <span class="token string">"shards_acknowledged"</span><span class="token operator">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
    <span class="token string">"index"</span><span class="token operator">:</span> <span class="token string">"books"</span>
<span class="token punctuation">}</span>
</code></pre> 重复创建已经存在的索引会出现错误信息，reason属性中描述错误原因 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"error"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"root_cause"</span><span class="token operator">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"resource_already_exists_exception"</span><span class="token punctuation">,</span>
                <span class="token string">"reason"</span><span class="token operator">:</span> <span class="token string">"index [books/VgC_XMVAQmedaiBNSgO2-w] already exists"</span><span class="token punctuation">,</span>
                <span class="token string">"index_uuid"</span><span class="token operator">:</span> <span class="token string">"VgC_XMVAQmedaiBNSgO2-w"</span><span class="token punctuation">,</span>
                <span class="token string">"index"</span><span class="token operator">:</span> <span class="token string">"books"</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"resource_already_exists_exception"</span><span class="token punctuation">,</span>
        <span class="token string">"reason"</span><span class="token operator">:</span> <span class="token string">"index [books/VgC_XMVAQmedaiBNSgO2-w] already exists"</span><span class="token punctuation">,</span>	# books索引已经存在
        <span class="token string">"index_uuid"</span><span class="token operator">:</span> <span class="token string">"VgC_XMVAQmedaiBNSgO2-w"</span><span class="token punctuation">,</span>
        <span class="token string">"index"</span><span class="token operator">:</span> <span class="token string">"book"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"status"</span><span class="token operator">:</span> <span class="token number">400</span>
<span class="token punctuation">}</span>
</code></pre>  
-  查询索引 GET请求		http://localhost:9200/books 查询索引得到索引相关信息，如下 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"book"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"aliases"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span><span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token string">"mappings"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span><span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token string">"settings"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
            <span class="token string">"index"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"routing"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"allocation"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                        <span class="token string">"include"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                            <span class="token string">"_tier_preference"</span><span class="token operator">:</span> <span class="token string">"data_content"</span>
                        <span class="token punctuation">}</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"number_of_shards"</span><span class="token operator">:</span> <span class="token string">"1"</span><span class="token punctuation">,</span>
                <span class="token string">"provided_name"</span><span class="token operator">:</span> <span class="token string">"books"</span><span class="token punctuation">,</span>
                <span class="token string">"creation_date"</span><span class="token operator">:</span> <span class="token string">"1645768584849"</span><span class="token punctuation">,</span>
                <span class="token string">"number_of_replicas"</span><span class="token operator">:</span> <span class="token string">"1"</span><span class="token punctuation">,</span>
                <span class="token string">"uuid"</span><span class="token operator">:</span> <span class="token string">"VgC_XMVAQmedaiBNSgO2-w"</span><span class="token punctuation">,</span>
                <span class="token string">"version"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"created"</span><span class="token operator">:</span> <span class="token string">"7160299"</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 如果查询了不存在的索引，会返回错误信息，例如查询名称为book的索引后信息如下 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"error"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"root_cause"</span><span class="token operator">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"index_not_found_exception"</span><span class="token punctuation">,</span>
                <span class="token string">"reason"</span><span class="token operator">:</span> <span class="token string">"no such index [book]"</span><span class="token punctuation">,</span>
                <span class="token string">"resource.type"</span><span class="token operator">:</span> <span class="token string">"index_or_alias"</span><span class="token punctuation">,</span>
                <span class="token string">"resource.id"</span><span class="token operator">:</span> <span class="token string">"book"</span><span class="token punctuation">,</span>
                <span class="token string">"index_uuid"</span><span class="token operator">:</span> <span class="token string">"_na_"</span><span class="token punctuation">,</span>
                <span class="token string">"index"</span><span class="token operator">:</span> <span class="token string">"book"</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"index_not_found_exception"</span><span class="token punctuation">,</span>
        <span class="token string">"reason"</span><span class="token operator">:</span> <span class="token string">"no such index [book]"</span><span class="token punctuation">,</span>		# 没有book索引
        <span class="token string">"resource.type"</span><span class="token operator">:</span> <span class="token string">"index_or_alias"</span><span class="token punctuation">,</span>
        <span class="token string">"resource.id"</span><span class="token operator">:</span> <span class="token string">"book"</span><span class="token punctuation">,</span>
        <span class="token string">"index_uuid"</span><span class="token operator">:</span> <span class="token string">"_na_"</span><span class="token punctuation">,</span>
        <span class="token string">"index"</span><span class="token operator">:</span> <span class="token string">"book"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"status"</span><span class="token operator">:</span> <span class="token number">404</span>
<span class="token punctuation">}</span>
</code></pre>  
-  删除索引 DELETE请求	http://localhost:9200/books 删除所有后，给出删除结果 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"acknowledged"</span><span class="token operator">:</span> <span class="token boolean">true</span>
<span class="token punctuation">}</span>
</code></pre> 如果重复删除，会给出错误信息，同样在reason属性中描述具体的错误原因 {
    "error": {
        "root_cause": [
            {
                "type": "index_not_found_exception",
                "reason": "no such index [books]",
                "resource.type": "index_or_alias",
                "resource.id": "book",
                "index_uuid": "_na_",
                "index": "book"
            }
        ],
        "type": "index_not_found_exception",
        "reason": "no such index [books]",		# 没有books索引
        "resource.type": "index_or_alias",
        "resource.id": "book",
        "index_uuid": "_na_",
        "index": "book"
    },
    "status": 404
}  
-  创建索引并指定分词器 前面创建的索引是未指定分词器的，可以在创建索引时添加请求参数，设置分词器。目前国内较为流行的分词器是IK分词器，使用前先在下对应的分词器，然后使用。IK分词器下载地址：https://github.com/medcl/elasticsearch-analysis-ik/releases 分词器下载后解压到ES安装目录的plugins目录中即可，安装分词器后需要重新启动ES服务器。使用IK分词器创建索引格式： <pre><code class="prism language-json"><span class="token constant">PUT</span>请求		http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books

请求参数如下（注意是json格式的参数）
<span class="token punctuation">{
     
    <!-- --></span>
  <span class="token string">"mappings"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"properties"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
      <span class="token string">"id"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"keyword"</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token string">"name"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
        <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span><span class="token punctuation">,</span>
        <span class="token string">"copy_to"</span><span class="token operator">:</span> <span class="token string">"all"</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token string">"type"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"keyword"</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token string">"description"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
        <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span><span class="token punctuation">,</span>
        <span class="token string">"copy_to"</span><span class="token operator">:</span> <span class="token string">"all"</span>
      <span class="token punctuation">}</span><span class="token punctuation">,</span>
      <span class="token string">"all"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
        <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 请求参数如下说明: <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"mappings"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>							#定义mappings属性，替换创建索引时对应的mappings属性		
        <span class="token string">"properties"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>						#定义索引中包含的属性设置
            <span class="token string">"id"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>							#设置索引中包含id属性
                <span class="token string">"type"</span><span class="token operator">:</span><span class="token string">"keyword"</span>			#当前属性可以被直接搜索
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token string">"name"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>						#设置索引中包含name属性
                <span class="token string">"type"</span><span class="token operator">:</span><span class="token string">"text"</span><span class="token punctuation">,</span>              #当前属性是文本信息，参与分词  
                <span class="token string">"analyzer"</span><span class="token operator">:</span><span class="token string">"ik_max_word"</span><span class="token punctuation">,</span>   #使用<span class="token constant">IK</span>分词器进行分词             
                <span class="token string">"copy_to"</span><span class="token operator">:</span><span class="token string">"all"</span>				#分词结果拷贝到all属性中
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token string">"type"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"type"</span><span class="token operator">:</span><span class="token string">"keyword"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token string">"description"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"type"</span><span class="token operator">:</span><span class="token string">"text"</span><span class="token punctuation">,</span>	                
                <span class="token string">"analyzer"</span><span class="token operator">:</span><span class="token string">"ik_max_word"</span><span class="token punctuation">,</span>                
                <span class="token string">"copy_to"</span><span class="token operator">:</span><span class="token string">"all"</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token string">"all"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>							#定义属性，用来描述多个字段的分词结果集合，当前属性可以参与查询
                <span class="token string">"type"</span><span class="token operator">:</span><span class="token string">"text"</span><span class="token punctuation">,</span>	                
                <span class="token string">"analyzer"</span><span class="token operator">:</span><span class="token string">"ik_max_word"</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>  创建完毕后返回结果和不使用分词器创建索引的结果是一样的，此时可以通过查看索引信息观察到添加的请求参数mappings已经进入到了索引属性中 <pre><code class="prism language-json"><span class="token punctuation">{
     
    <!-- --></span>
    <span class="token string">"books"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token string">"aliases"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span><span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token string">"mappings"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>						#mappings属性已经被替换
            <span class="token string">"properties"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"all"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
                    <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"description"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
                    <span class="token string">"copy_to"</span><span class="token operator">:</span> <span class="token punctuation">[</span>
                        <span class="token string">"all"</span>
                    <span class="token punctuation">]</span><span class="token punctuation">,</span>
                    <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"id"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"keyword"</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"name"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"text"</span><span class="token punctuation">,</span>
                    <span class="token string">"copy_to"</span><span class="token operator">:</span> <span class="token punctuation">[</span>
                        <span class="token string">"all"</span>
                    <span class="token punctuation">]</span><span class="token punctuation">,</span>
                    <span class="token string">"analyzer"</span><span class="token operator">:</span> <span class="token string">"ik_max_word"</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"type"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"keyword"</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token string">"settings"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
            <span class="token string">"index"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                <span class="token string">"routing"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"allocation"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                        <span class="token string">"include"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                            <span class="token string">"_tier_preference"</span><span class="token operator">:</span> <span class="token string">"data_content"</span>
                        <span class="token punctuation">}</span>
                    <span class="token punctuation">}</span>
                <span class="token punctuation">}</span><span class="token punctuation">,</span>
                <span class="token string">"number_of_shards"</span><span class="token operator">:</span> <span class="token string">"1"</span><span class="token punctuation">,</span>
                <span class="token string">"provided_name"</span><span class="token operator">:</span> <span class="token string">"books"</span><span class="token punctuation">,</span>
                <span class="token string">"creation_date"</span><span class="token operator">:</span> <span class="token string">"1645769809521"</span><span class="token punctuation">,</span>
                <span class="token string">"number_of_replicas"</span><span class="token operator">:</span> <span class="token string">"1"</span><span class="token punctuation">,</span>
                <span class="token string">"uuid"</span><span class="token operator">:</span> <span class="token string">"DohYKvr_SZO4KRGmbZYmTQ"</span><span class="token punctuation">,</span>
                <span class="token string">"version"</span><span class="token operator">:</span> <span class="token punctuation">{
     
    <!-- --></span>
                    <span class="token string">"created"</span><span class="token operator">:</span> <span class="token string">"7160299"</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 

小结:

1.  索引操作  
2.  IK分词器安装  
3.  设置索引创建规则（应用） 


目前我们已经有了索引了，但是索引中还没有数据，所以要先添加数据，ES中称数据为文档，下面进行文档操作。

-  添加文档，有三种方式 <pre><code class="prism language-json"><span class="token constant">POST</span>请求	http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books<span class="token operator">/</span>_doc		#使用系统生成id
<span class="token constant">POST</span>请求	http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books<span class="token operator">/</span>_create<span class="token operator">/</span><span class="token number">1</span>	#使用指定id
<span class="token constant">POST</span>请求	http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books<span class="token operator">/</span>_doc<span class="token operator">/</span><span class="token number">1</span>		#使用指定id，不存在创建，存在更新（版本递增）

文档通过请求参数传递，数据格式json
<span class="token punctuation">{
     
    <!-- --></span>
  <span class="token string">"name"</span><span class="token operator">:</span> <span class="token string">"springboot"</span><span class="token punctuation">,</span>
  <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"springboot"</span><span class="token punctuation">,</span>
  <span class="token string">"description"</span><span class="token operator">:</span> <span class="token string">"springboot"</span>
<span class="token punctuation">}</span>  
</code></pre>  
-  查询文档 GET请求	http://localhost:9200/books/_doc/1		 #查询单个文档 		
GET请求	http://localhost:9200/books/_search		 #查询全部文档  
-  条件查询 GET请求	http://localhost:9200/books/_search?q=name:springboot	# q=查询属性名:查询属性值  
-  删除文档 DELETE请求	http://localhost:9200/books/_doc/1  
-  修改文档（全量更新）注意参数要写全,不然会丢失数据 <pre><code class="prism language-json"><span class="token constant">PUT</span>请求	http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books<span class="token operator">/</span>_doc<span class="token operator">/</span><span class="token number">1</span>

文档通过请求参数传递，数据格式json
<span class="token punctuation">{
     
    <!-- --></span>
  <span class="token string">"name"</span><span class="token operator">:</span> <span class="token string">"springboot"</span><span class="token punctuation">,</span>
  <span class="token string">"type"</span><span class="token operator">:</span> <span class="token string">"springboot"</span><span class="token punctuation">,</span>
  <span class="token string">"description"</span><span class="token operator">:</span> <span class="token string">"springboot"</span>
<span class="token punctuation">}</span> 
</code></pre>  
-  修改文档（部分更新）有就更新,没有就创建 <pre><code class="prism language-json"><span class="token constant">POST</span>请求	http<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token operator">:</span><span class="token number">9200</span><span class="token operator">/</span>books<span class="token operator">/</span>_update<span class="token operator">/</span><span class="token number">1</span>

文档通过请求参数传递，数据格式json
<span class="token punctuation">{
     
    <!-- --></span>			
    <span class="token string">"doc"</span><span class="token operator">:</span><span class="token punctuation">{
     
    <!-- --></span>						#部分更新并不是对原始文档进行更新，而是对原始文档对象中的doc属性中的指定属性更新
        <span class="token string">"name"</span><span class="token operator">:</span><span class="token string">"springboot"</span>		#仅更新提供的属性值，未提供的属性值不参与更新操作
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 

小结:

1.文档操作

- 增删改查


**步骤①**：导入springboot整合ES的starter坐标

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

**步骤②**：进行基础配置

```java
spring:
  elasticsearch:
    rest:
      uris: http://localhost:9200
```

​ 配置ES服务器地址，端口9200

**步骤③**：使用springboot整合ES的专用客户端接口ElasticsearchRestTemplate来进行操作

```java
@SpringBootTest
class Springboot18EsApplicationTests {
   
    @Autowired
    private ElasticsearchRestTemplate template;
}
```

SpringBoot平台并没有跟随ES的更新速度进行同步更新，ES提供了High Level Client操作ES

下面使用高级别客户端方式进行springboot整合ES，操作步骤如下：

**步骤①**：导入springboot整合ES高级别客户端的坐标，此种形式目前没有对应的starter

```java
<dependency>
    <groupId>org.elasticsearch.client</groupId>
    <artifactId>elasticsearch-rest-high-level-client</artifactId>
</dependency>
```

**步骤②**：使用编程的形式设置连接的ES服务器，并获取客户端对象

```java
@SpringBootTest
class Springboot18EsApplicationTests {
   
    private RestHighLevelClient client;
      @Test
      void testCreateClient() throws IOException {
   
          HttpHost host = HttpHost.create("http://localhost:9200");
          RestClientBuilder builder = RestClient.builder(host);
          client = new RestHighLevelClient(builder);
  
          client.close();
      }
}
```

​ 配置ES服务器地址与端口9200，记得客户端使用完毕需要手工关闭。由于当前客户端是手工维护的，因此不能通过自动装配的形式加载对象。

**步骤③**：使用客户端对象操作ES，例如创建索引

```java
@SpringBootTest
class Springboot18EsApplicationTests {
   
    private RestHighLevelClient client;
      @Test
      void testCreateIndex() throws IOException {
   
          HttpHost host = HttpHost.create("http://localhost:9200");
          RestClientBuilder builder = RestClient.builder(host);
          client = new RestHighLevelClient(builder);
          
          CreateIndexRequest request = new CreateIndexRequest("books");
          client.indices().create(request, RequestOptions.DEFAULT); 
          
          client.close();
      }
}
```

​ 高级别客户端操作是通过发送请求的方式完成所有操作的，ES针对各种不同的操作，设定了各式各样的请求对象，上例中创建索引的对象是CreateIndexRequest，其他操作也会有自己专用的Request对象。

​ 当前操作我们发现，无论进行ES何种操作，第一步永远是获取RestHighLevelClient对象，最后一步永远是关闭该对象的连接。在测试中可以使用测试类的特性去帮助开发者一次性的完成上述操作，但是在业务书写时，还需要自行管理。将上述代码格式转换成使用测试类的初始化方法和销毁方法进行客户端对象的维护。

```java
@SpringBootTest
class Springboot18EsApplicationTests {
   
    @BeforeEach		//在测试类中每个操作运行前运行的方法
    void setUp() {
   
        HttpHost host = HttpHost.create("http://localhost:9200");
        RestClientBuilder builder = RestClient.builder(host);
        client = new RestHighLevelClient(builder);
    }

    @AfterEach		//在测试类中每个操作运行后运行的方法
    void tearDown() throws IOException {
   
        client.close();
    }

    private RestHighLevelClient client;

    @Test
    void testCreateIndex() throws IOException {
   
        CreateIndexRequest request = new CreateIndexRequest("books");
        client.indices().create(request, RequestOptions.DEFAULT);
    }
}
```

​ 现在的书写简化了很多，也更合理。下面使用上述模式将所有的ES操作执行一遍，测试结果

小结：

1.  High Leven Client  
2.  客户端初始化  
3.  客户端改进 


**创建索引（IK分词器）**：

```java
@Test
void testCreateIndexByIk() throws IOException {
   
    //客户端操作
    CreateIndexRequest request = new CreateIndexRequest("books");
    //设置请求中的参数
    String json = "{\n" +
        "  \"mappings\": {\n" +
        "    \"properties\": {\n" +
        "      \"id\": {\n" +
        "        \"type\": \"keyword\"\n" +
        "      },\n" +
        "      \"name\": {\n" +
        "        \"type\": \"text\",\n" +
        "        \"analyzer\": \"ik_max_word\",\n" +
        "        \"copy_to\": \"all\"\n" +
        "      },\n" +
        "      \"type\": {\n" +
        "        \"type\": \"keyword\"\n" +
        "      },\n" +
        "      \"description\": {\n" +
        "        \"type\": \"text\",\n" +
        "        \"analyzer\": \"ik_max_word\",\n" +
        "        \"copy_to\": \"all\"\n" +
        "      },\n" +
        "      \"all\": {\n" +
        "        \"type\": \"text\",\n" +
        "        \"analyzer\": \"ik_max_word\"\n" +
        "      }\n" +
        "    }\n" +
        "  }\n" +
        "}";
    request.source(json, XContentType.JSON);
    //获取操作索引的客户端对象，调用创建索引操作
    client.indices().create(request, RequestOptions.DEFAULT);
}
```

​ IK分词器是通过请求参数的形式进行设置的，设置请求参数使用request对象中的source方法进行设置，至于参数是什么，取决于你的操作种类。当请求中需要参数时，均可使用当前形式进行参数设置。

**添加文档**：

```java
@Test
//添加文档
void testCreateDoc() throws IOException {
   
    Book book = bookDao.selectById(1);
    IndexRequest request = new IndexRequest("books").id(book.getId().toString());
    String json = JSON.toJSONString(book);
    request.source(json,XContentType.JSON);
    client.index(request,RequestOptions.DEFAULT);
}
```

​ 添加文档使用的请求对象是IndexRequest，与创建索引使用的请求对象不同。

**批量添加文档**：

```java
@Test
//批量添加文档
void testCreateDocAll() throws IOException {
   
    List<Book> bookList = bookDao.selectList(null);
    BulkRequest bulk = new BulkRequest();
    for (Book book : bookList) {
   
        IndexRequest request = new IndexRequest("books").id(book.getId().toString());
        String json = JSON.toJSONString(book);
        request.source(json,XContentType.JSON);
        bulk.add(request);
    }
    client.bulk(bulk,RequestOptions.DEFAULT);
}
```

​ 批量做时，先创建一个BulkRequest的对象，可以将该对象理解为是一个保存request对象的容器，将所有的请求都初始化好后，添加到BulkRequest对象中，再使用BulkRequest对象的bulk方法，一次性执行完毕。

小结:

1.  创建索引  
2.  添加文档  
3.  批量添加文档 


**按id查询文档**：

```java
@Test
//按id查询
void testGet() throws IOException {
   
    GetRequest request = new GetRequest("books","1");
    GetResponse response = client.get(request, RequestOptions.DEFAULT);
    String json = response.getSourceAsString();
    System.out.println(json);
}
```

​ 根据id查询文档使用的请求对象是GetRequest。

**按条件查询文档**：

```java
@Test
//按条件查询
void testSearch() throws IOException {
   
    SearchRequest request = new SearchRequest("books");

    SearchSourceBuilder builder = new SearchSourceBuilder();
    builder.query(QueryBuilders.termQuery("all","spring"));
    request.source(builder);

    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    SearchHits hits = response.getHits();
    for (SearchHit hit : hits) {
   
        String source = hit.getSourceAsString();
        //System.out.println(source);
        Book book = JSON.parseObject(source, Book.class);
        System.out.println(book);
    }
}
```

​ 按条件查询文档使用的请求对象是SearchRequest，查询时调用SearchRequest对象的termQuery方法，需要给出查询属性名，此处支持使用合并字段，也就是前面定义索引属性时添加的all属性。

## 修改文档

```java
//修改文档
@Test
void testUpdate() throws IOException {
   
    Book book = new Book();
    book.setId(15);
    book.setName("测试数据123张三");
    book.setType("测试数据123");
    book.setDescription("测试数据123");
    bookDao.updateById(book);
    UpdateRequest updateRequest = new UpdateRequest("books", book.getId().toString());
    //设置修改参数
    String json = JSON.toJSONString(book);
    updateRequest.doc(json, XContentType.JSON);
    client.update(updateRequest, RequestOptions.DEFAULT);
}
```

## 删除文档

```java
//删除文档
@Test
void testDelete() throws IOException {
   
    DeleteRequest deleteRequest = new DeleteRequest("books", "18");
    client.delete(deleteRequest, RequestOptions.DEFAULT);
}
```

小结:

1. SpringBoot整合ES文档操作

- 增删改查

总结:

1.  Redis  
2.  Mongodb  
3.  ElasticSearch 


​ 企业级应用主要作用是信息处理，当需要读取数据时，由于受限于数据库的访问效率，导致整体系统性能偏低。


![img](https://img-blog.csdnimg.cn/b825e03cd19a44babca4136bae41e6e3.png)

​ 应用程序直接与数据库打交道，访问效率低

​ 为了改善上述现象，开发者通常会在应用程序与数据库之间建立一种临时的数据存储机制，该区域中的数据在内存中保存，读写速度较快，可以有效解决数据库访问效率低下的问题。这一块临时存储数据的区域就是缓存。


![img](https://img-blog.csdnimg.cn/7493dd7d31e94d568cf51d470ecaf233.png)

```java
使用缓存后，应用程序与缓存打交道，缓存与数据库打交道，数据访问效率提高
```

-  缓存是一种介于数据永久存储介质与数据应用之间的数据临时存储介质  
-  使用缓存可以有效的减少低速数据读取过程的次数（例如磁盘IO），提高系统性能  
-  缓存不仅可以用于提高永久性存储介质的数据读取效率，还可以提供临时的数据存储空间 

自定义缓存

```java
@Autowired
private BookDao bookDao;

private HashMap<Integer,Book> cache = new HashMap<Integer,Book>();

@Override
public Book getById(Integer id) {
   
    //如果当前缓存中没有本次要查询的数据，则进行查询，否则直接从缓存中获取数据返回
    Book book = cache.get(id);
    if(book == null){
   
        book = bookDao.selectById(id);
        cache.put(id,book);
    }
    return book;
}
```

提供临时的数据存储空间

```java
private HashMap<String ,String> cache = new HashMap<String,String>();

@Override
public String get(String tele) {
   
    String code = tele.substring(tele.length() - 6);
    cache.put(tele,code);
    return code;
}

@Override
public boolean check(String tele, String code) {
   
    String queryCode = cache.get(tele);
    return code.equals(queryCode);
}
```

小结:

1.  缓存作用  
2.  自定义缓存 


​ springboot技术提供有内置的缓存解决方案，可以帮助开发者快速开启缓存技术，并使用缓存技术进行数据的快速操作，例如读取缓存数据和写入数据到缓存。

**步骤①**：导入springboot提供的缓存技术对应的starter

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

**步骤②**：启用缓存，在引导类上方标注注解@EnableCaching配置springboot程序中可以使用缓存

```java
@SpringBootApplication
//开启缓存功能
@EnableCaching
public class Springboot19CacheApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot19CacheApplication.class, args);
    }
}
```

**步骤③**：设置操作的数据是否使用缓存

```java
@Service
public class BookServiceImpl implements BookService {
   
    @Autowired
    private BookDao bookDao;

    @Cacheable(value="cacheSpace",key="#id")
    public Book getById(Integer id) {
   
        return bookDao.selectById(id);
    }
}
```

​ 在业务方法上面使用注解@Cacheable声明当前方法的返回值放入缓存中，其中要指定缓存的存储位置，以及缓存中保存当前方法返回值对应的名称。上例中value属性描述缓存的存储位置，可以理解为是一个存储空间名，key属性描述了缓存中保存数据的名称，使用#id读取形参中的id值作为缓存名称。

​ 使用@Cacheable注解后，执行当前操作，如果发现对应名称在缓存中没有数据，就正常读取数据，然后放入缓存；如果对应名称在缓存中有数据，就终止当前业务方法执行，直接返回缓存中的数据。

小结:

1.SpringBoot启用缓存的方式

-  @EnableCaching  
-  @Cacheable 


-  需求 
 <ul> 
  -  输入手机号获取验证码，组织文档以短信形式发送给用户（页面模拟）  
  -  输入手机号和验证码验证结果  
 </ul>  
-  需求分析 
 <ul> 
  - 提供controller，传入手机号，业务层通过手机号计算出独有的6位验证码数据，存入缓存后返回此数据 
  - 提供controller，传入手机号与验证码，业务层通过手机号从缓存中读取验证码与输入验证码进行比对，返回比对结果 
 </ul> 

**注意:** 启用缓存，在引导类上方标注注解@EnableCaching配置springboot程序中可以使用缓存

**步骤①**：定义验证码对应的实体类，封装手机号与验证码两个属性

```java
@Data
public class SMSCode {
   
    private String tele;
    private String code;
}
```

**步骤②**：定义验证码功能的业务层接口与实现类

```java
public interface SMSCodeService {
   
    public String sendCodeToSMS(String tele);
    public boolean checkCode(SMSCode smsCode);
}

@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @Autowired
    private CodeUtils codeUtils;

    @CachePut(value = "smsCode", key = "#tele")
    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        return false;
    }
}
```

获取验证码后，当验证码失效时必须重新获取验证码，因此在获取验证码的功能上不能使用@Cacheable注解，@Cacheable注解是缓存中没有值则放入值，缓存中有值则取值。此处的功能仅仅是生成验证码并放入缓存，并不具有从缓存中取值的功能，因此不能使用@Cacheable注解，应该使用仅具有向缓存中保存数据的功能，使用@CachePut注解即可。

**步骤③**：定义验证码的生成策略与根据手机号读取验证码的功能

```java
@Component
public class CodeUtils {
   
    private String [] patch = {
   "000000","00000","0000","000","00","0",""};

    public String generator(String tele){
   
        int hash = tele.hashCode();
        int encryption = 20206666;
        long result = hash ^ encryption;
        long nowTime = System.currentTimeMillis();
        result = result ^ nowTime;
        long code = result % 1000000;
        code = code < 0 ? -code : code;
        String codeStr = code + "";
        int len = codeStr.length();
        return patch[len] + codeStr;
    }
}
```

**步骤④**：定义验证码功能的web层接口，一个方法用于提供手机号获取验证码，一个方法用于提供手机号和验证码进行校验

```java
@RestController
@RequestMapping("/sms")
public class SMSCodeController {
   

    @Autowired
    private SMSCodeService smsCodeService;

    @GetMapping
    public String getCode(String tele){
   
        String code = smsCodeService.sendCodeToSMS(tele);
        return code;
    }

    @PostMapping
    public boolean checkCode(SMSCode smsCode){
   
        return smsCodeService.checkCode(smsCode);
    }

}
```


获取缓存中的验证码

```java
//定义为spring管控的bean
@Component
public class CodeUtils {
   

    private String[] patch = {
   "000000", "00000", "0000", "000", "00", "0", ""};

    public String generator(String tele) {
   
        int hash = tele.hashCode();
        int encryption = 20206666;
        long result = hash ^ encryption;
        long nowTime = System.currentTimeMillis();
        result = result ^ nowTime;
        long code = result % 1000000;
        code = code < 0 ? -code : code;
        String codeStr = code + "";
        int len = codeStr.length();
        return patch[len] + codeStr;
    }

    /**
     * 获取缓存中的验证码,要以bean 方式注入到spring的容器中
     *
     * @param tele
     * @return
     */
    @Cacheable(value = "smsCode", key = "#tele")
    public String get(String tele) {
   
        return null;
    }

}
```

校验

```java
public boolean checkCode(SMSCode smsCode) {
   
    String code = smsCode.getCode();
    //取出内存中的验证码与传递过来的验证码比对，如果相同，返回true
    String cacheCode = codeUtils.get(smsCode.getTele());
    return code.equals(cacheCode);
}
```


**步骤①**：导入Ehcache的坐标

```java
<dependency>
    <groupId>net.sf.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
```

​ 此处为什么不是导入Ehcache的starter，而是导入技术坐标呢？其实springboot整合缓存技术做的是通用格式，不管你整合哪种缓存技术，只是实现变化了，操作方式一样。这也体现出springboot技术的优点，统一同类技术的整合方式。

**步骤②**：配置缓存技术实现使用Ehcache

```java
spring:
  cache:
    type: ehcache
    #ehcache配置文件路径
    ehcache:
      config: classpath:/ehcache.xml
```

​ 配置缓存的类型type为ehcache，此处需要说明一下，当前springboot可以整合的缓存技术中包含有ehcach，所以可以这样书写。其实这个type不可以随便写的，不是随便写一个名称就可以整合的。

​ 由于ehcache的配置有独立的配置文件格式，因此还需要指定ehcache的配置文件，以便于读取相应配置

**注意: 配制文件的路径要从 classpath: 开始**

新建 resources/ehcache.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">
    <diskStore path="D:\ehcache" />

    <!--默认缓存策略 -->
    <!-- external：是否永久存在，设置为true则不会被清除，此时与timeout冲突，通常设置为false-->
    <!-- diskPersistent：是否启用磁盘持久化-->
    <!-- maxElementsInMemory：最大缓存数量-->
    <!-- overflowToDisk：超过最大缓存数量是否持久化到磁盘-->
    <!-- timeToIdleSeconds：最大不活动间隔，设置过长缓存容易溢出，设置过短无效果，可用于记录时效性数据，例如验证码-->
    <!-- timeToLiveSeconds：最大存活时间-->
    <!-- memoryStoreEvictionPolicy：缓存清除策略-->
    <defaultCache
        eternal="false"
        diskPersistent="false"
        maxElementsInMemory="1000"
        overflowToDisk="false"
        timeToIdleSeconds="60"
        timeToLiveSeconds="60"
        memoryStoreEvictionPolicy="LRU" />

    <cache
        name="smsCode"
        eternal="false"
        diskPersistent="false"
        maxElementsInMemory="1000"
        overflowToDisk="false"
        timeToIdleSeconds="10"
        timeToLiveSeconds="10"
        memoryStoreEvictionPolicy="LRU" />
</ehcache>
```

​ 注意前面的案例中，设置了数据保存的位置是smsCode

```java
@CachePut(value = "smsCode", key = "#tele")
public String sendCodeToSMS(String tele) {
   
    String code = codeUtils.generator(tele);
    return code;
}
```

​ 这个设定需要保障ehcache中有一个缓存空间名称叫做smsCode的配置，前后要统一。在企业开发过程中，通过设置不同名称的cache来设定不同的缓存策略，应用于不同的缓存数据。

​ 到这里springboot整合Ehcache就做完了，可以发现一点，原始代码没有任何修改，仅仅是加了一组配置就可以变更缓存供应商了，这也是springboot提供了统一的缓存操作接口的优势，变更实现并不影响原始代码的书写。

**小结**

1. springboot使用Ehcache作为缓存实现需要导入Ehcache的坐标 
2. 修改设置，配置缓存供应商为ehcache，并提供对应的缓存配置文件



![img](https://img-blog.csdnimg.cn/img_convert/8418a4f9669201805d4a58b0e4f25383.png)

- LFU， Less Frequently Used，就是上面例子中使用的策略，直白一点就是讲一直以来**最少被使用的**。 
- LRU，Least Recently Used，最近最少使用的，缓存的元素有一个时间戳，当缓存容量满了，而又需要腾出地方来缓存新的元素的时候，那么现有缓存元素中**时间戳离当前时间最远的元素将被清出缓存**。


**步骤①**：导入redis的坐标

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

**步骤②**：配置缓存技术实现使用redis

```java
spring:
  redis:
    host: localhost
    port: 6379
  cache:
    type: redis
```

​ 如果需要对redis作为缓存进行配置，注意不是对原始的redis进行配置，而是配置redis作为缓存使用相关的配置，隶属于spring.cache.redis节点下，注意不要写错位置了。

```java
spring:
  redis:
    host: localhost
    port: 6379
  cache:
    type: redis
    redis:
      use-key-prefix: false # 是否使用前缀名（系统定义前缀名）值为 false, key-prefix设置无效
      key-prefix: sms_ # 追加自定义前缀名
      cache-null-values: false # 是否允许存储空值
      time-to-live: 10s # 有效时长
```

Redis 客户端相关操作

```java
127.0.0.1:6379> keys *
1) "smsCode::188666688881"
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> keys *
1) "188666688881"
127.0.0.1:6379> keys *
1) "sms_smsCode::188666688881"
```

**总结**

1. springboot使用redis作为缓存实现需要导入redis的坐标 
2. 修改设置，配置缓存供应商为redis，并提供对应的缓存配置


**安装**

​ windows版安装包下载地址：https://www.runoob.com/memcached/window-install-memcached.html

​ 下载的安装包是解压缩就能使用的zip文件，解压缩完毕后会得到如下文件


![img](https://img-blog.csdnimg.cn/img_convert/1c7b9ae3e4dbcef02d0e50cf08e2f7eb.png)

​ 可执行文件只有一个memcached.exe，使用该文件可以将memcached作为系统服务启动，执行此文件时会出现报错信息，如下：


![img](https://img-blog.csdnimg.cn/2364949642024974804fe843c77a8b94.png)

​ 此处出现问题的原因是注册系统服务时需要使用管理员权限，当前账号权限不足导致安装服务失败，切换管理员账号权限启动命令行


![img](https://img-blog.csdnimg.cn/6653b0457147456d94c0870c7919b403.png)

​ 然后再次执行安装服务的命令即可，如下：

```java
memcached.exe -d install
```

​ 服务安装完毕后可以使用命令启动和停止服务，如下：

```java
memcached.exe -d start		# 启动服务
memcached.exe -d stop		# 停止服务
```

​ 也可以在任务管理器中进行服务状态的切换


![img](https://img-blog.csdnimg.cn/f62d99740ee04f02adf30b614acec8e5.png)

**小结:**

1.  memcached下载与安装  
2.  memcached启动与退出 


-  memcached客户端选择 
 <ul> 
  -  Memcached Client for Java：最早期客户端，稳定可靠，用户群广  
  -  SpyMemcached：效率更高  
  -  Xmemcached：并发处理更好  
 </ul>  
-  SpringBoot未提供对memcached的整合，需要使用硬编码方式实现客户端初始化管理 

**步骤①**：导入xmemcached的坐标

```java
<dependency>
    <groupId>com.googlecode.xmemcached</groupId>
    <artifactId>xmemcached</artifactId>
    <version>2.4.7</version>
</dependency>
```

**步骤②**：配置memcached，制作memcached的配置类

```java
@Configuration
public class XMemcachedConfig {
   
    @Bean
    public MemcachedClient getMemcachedClient() throws IOException {
   
        MemcachedClientBuilder memcachedClientBuilder = new XMemcachedClientBuilder("localhost:11211");
        MemcachedClient memcachedClient = memcachedClientBuilder.build();
        return memcachedClient;
    }
}
```

​ memcached默认对外服务端口11211。

**步骤③**：使用xmemcached客户端操作缓存，注入MemcachedClient对象

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @Autowired
    private CodeUtils codeUtils;
    @Autowired
    private MemcachedClient memcachedClient;

    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        try {
   
            memcachedClient.set(tele,10,code);
        } catch (Exception e) {
   
            e.printStackTrace();
        }
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        String code = null;
        try {
   
            code = memcachedClient.get(smsCode.getTele()).toString();
        } catch (Exception e) {
   
            e.printStackTrace();
        }
        return smsCode.getCode().equals(code);
    }
}
```

​ 设置值到缓存中使用set操作，取值使用get操作，其实更符合我们开发者的习惯。

​ 上述代码中对于服务器的配置使用硬编码写死到了代码中，将此数据提取出来，做成独立的配置属性。

**定义配置属性**

​ 以下过程采用前期学习的属性配置方式进行，当前操作有助于理解原理篇中的很多知识。

-  定义配置类，加载必要的配置属性，读取配置文件中memcached节点信息 <pre><code class="prism language-java"><span class="token annotation punctuation">@Component</span>
<span class="token annotation punctuation">@ConfigurationProperties</span><span class="token punctuation">(</span>prefix <span class="token operator">=</span> <span class="token string">"memcached"</span><span class="token punctuation">)</span>
<span class="token annotation punctuation">@Data</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">XMemcachedProperties</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token keyword">private</span> <span class="token class-name">String</span> servers<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">int</span> poolSize<span class="token punctuation">;</span>
    <span class="token keyword">private</span> <span class="token keyword">long</span> opTimeout<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>  
-  定义memcached节点信息 memcached:
  # memcached服务器地址
  servers: localhost:11211
  # 连接池的数量
  poolSize: 10
  # 设置默认操作超时
  opTimeout: 3000  
-  在memcached配置类中加载信息 

```java
@Configuration
public class XMemcachedConfig {
   
    @Autowired
    private XMemcachedProperties props;
    @Bean
    public MemcachedClient getMemcachedClient() throws IOException {
   
        MemcachedClientBuilder memcachedClientBuilder = new XMemcachedClientBuilder(props.getServers());
        memcachedClientBuilder.setConnectionPoolSize(props.getPoolSize());
        memcachedClientBuilder.setOpTimeout(props.getOpTimeout());
        MemcachedClient memcachedClient = memcachedClientBuilder.build();
        return memcachedClient;
    }
}
```

**小结:**

1.  xmemcached客户端加载方式（bean初始化）  
2.  xmemcached客户端使用方式（set & get） 


- jetCache对SpringCache进行了封装，在原有功能基础上实现了多级缓存、缓存统计、自动刷新、异步调用、数据报表等功能 
- jetCache设定了本地缓存与远程缓存的多级缓存解决方案 
 <ul> 
  - 本地缓存（Local） 
   <ul> 
    - LinkedHashMap 
    - Caffeine 
   </ul>  
  - 远程缓存（Remote） 
   <ul> 
    - Redis 
    - Tair 
   </ul>  
 </ul> 

**步骤①**：导入springboot整合jetcache对应的坐标starter，当前坐标默认使用的远程方案是redis

```java
<dependency>
    <groupId>com.alicp.jetcache</groupId>
    <artifactId>jetcache-starter-redis</artifactId>
    <version>2.6.2</version>
</dependency>
```

**步骤②**：远程方案基本配置

```java
jetcache:
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

​ 其中poolConfig是必配项，否则会报错

**步骤③**：启用缓存，在引导类上方标注注解@EnableCreateCacheAnnotation配置springboot程序中可以使用注解的形式创建缓存

```java
@SpringBootApplication
//jetcache启用缓存的主开关
@EnableCreateCacheAnnotation
public class Springboot20JetCacheApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot20JetCacheApplication.class, args);
    }
}
```

**步骤④**：创建缓存对象Cache，并使用注解@CreateCache标记当前缓存的信息，然后使用Cache对象的API操作缓存，put写缓存，get读缓存。

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @Autowired
    private CodeUtils codeUtils;
    
    @CreateCache(name="jetCache_",expire = 10,timeUnit = TimeUnit.SECONDS)
    private Cache<String ,String> jetCache;

    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        jetCache.put(tele,code);
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        String code = jetCache.get(smsCode.getTele());
        return smsCode.getCode().equals(code);
    }
}
```

​ 通过上述jetcache使用远程方案连接redis可以看出，jetcache操作缓存时的接口操作更符合开发者习惯，使用缓存就先获取缓存对象Cache，放数据进去就是put，取数据出来就是get，更加简单易懂。并且jetcache操作缓存时，可以为某个缓存对象设置过期时间，将同类型的数据放入缓存中，方便有效周期的管理。

​ 上述方案中使用的是配置中定义的default缓存，其实这个default是个名字，可以随便写，也可以随便加。例如再添加一种缓存解决方案，参照如下配置进行：

```java
jetcache:
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
    sms:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

​ 如果想使用名称是sms的缓存，需要再创建缓存时指定参数area，声明使用对应缓存即可

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @Autowired
    private CodeUtils codeUtils;
    
    @CreateCache(area="sms",name="jetCache_",expire = 10,timeUnit = TimeUnit.SECONDS)
    private Cache<String ,String> jetCache;

    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        jetCache.put(tele,code);
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        String code = jetCache.get(smsCode.getTele());
        return smsCode.getCode().equals(code);
    }
}
```

##### 循环依赖

>Description:

设置 spring.main.allow-circular-references 为 true 打破循环

```java
spring:
  main:
    allow-circular-references: true
```


##### 纯本地方案

​ 远程方案中，配置中使用remote表示远程，换成local就是本地，只不过类型不一样而已。

**步骤①**：导入springboot整合jetcache对应的坐标starter

```java
<dependency>
    <groupId>com.alicp.jetcache</groupId>
    <artifactId>jetcache-starter-redis</artifactId>
    <version>2.6.2</version>
</dependency>
```

**步骤②**：本地缓存基本配置

```java
jetcache:
  local:
    default:
      type: linkedhashmap
      keyConvertor: fastjson
```

​ 为了加速数据获取时key的匹配速度，jetcache要求指定key的类型转换器。简单说就是，如果你给了一个Object作为key的话，我先用key的类型转换器给转换成字符串，然后再保存。等到获取数据时，仍然是先使用给定的Object转换成字符串，然后根据字符串匹配。由于jetcache是阿里的技术，这里推荐key的类型转换器使用阿里的fastjson。

**步骤③**：启用缓存

```java
@SpringBootApplication
//jetcache启用缓存的主开关
@EnableCreateCacheAnnotation
public class Springboot20JetCacheApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot20JetCacheApplication.class, args);
    }
}
```

**步骤④**：创建缓存对象Cache时，标注当前使用本地缓存

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @CreateCache(name="jetCache_",expire = 1000,timeUnit = TimeUnit.SECONDS,cacheType = CacheType.LOCAL)
    private Cache<String ,String> jetCache;

    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        jetCache.put(tele,code);
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        String code = jetCache.get(smsCode.getTele());
        return smsCode.getCode().equals(code);
    }
}
```

​ cacheType控制当前缓存使用本地缓存还是远程缓存，配置cacheType=CacheType.LOCAL即使用本地缓存。

##### 本地+远程方案

​ 本地和远程方法都有了，两种方案一起使用如何配置呢？其实就是将两种配置合并到一起就可以了。

```java
jetcache:
  local:
    default:
      type: linkedhashmap
      keyConvertor: fastjson
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
    sms:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

​ 在创建缓存的时候，配置cacheType为BOTH即则本地缓存与远程缓存同时使用。

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @CreateCache(name="jetCache_",expire = 1000,timeUnit = TimeUnit.SECONDS,cacheType = CacheType.BOTH)
    private Cache<String ,String> jetCache;
}
```

​ cacheType如果不进行配置，默认值是REMOTE，即仅使用远程缓存方案。关于jetcache的配置，参考以下信息


小结:

1.  jetcache简介  
2.  jetcache远程缓存使用方式  
3.  jetcache本地缓存使用方式 


​ jetcache提供了方法缓存方案，只不过名称变更了而已。在对应的操作接口上方使用注解@Cached即可

**步骤①**：导入springboot整合jetcache对应的坐标starter

```java
<dependency>
    <groupId>com.alicp.jetcache</groupId>
    <artifactId>jetcache-starter-redis</artifactId>
    <version>2.6.2</version>
</dependency>
```

**步骤②**：配置缓存

```java
jetcache:
  local:
    default:
      type: linkedhashmap
      keyConvertor: fastjson
  remote:
    default:
      type: redis
      host: localhost
      port: 6379
      keyConvertor: fastjson
      valueEncode: java
      valueDecode: java
      poolConfig:
        maxTotal: 50
    sms:
      type: redis
      host: localhost
      port: 6379
      poolConfig:
        maxTotal: 50
```

​ 由于redis缓存中不支持保存对象，因此需要对redis设置当Object类型数据进入到redis中时如何进行类型转换。需要配置keyConvertor表示key的类型转换方式，同时标注value的转换类型方式，值进入redis时是java类型，标注valueEncode为java，值从redis中读取时转换成java，标注valueDecode为java。

​ 注意，为了实现Object类型的值进出redis，需要保障进出redis的Object类型的数据必须实现**序列化接口**。

```java
@Data
public class Book implements Serializable {
   
    private Integer id;
    private String type;
    private String name;
    private String description;
}
```

**步骤③**：启用缓存时开启方法缓存功能，并配置basePackages，说明在哪些包中开启方法缓存

```java
@SpringBootApplication
//jetcache启用缓存的主开关
@EnableCreateCacheAnnotation
//开启方法注解缓存
@EnableMethodCache(basePackages="com.example")
public class Springboot20JetCacheApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot20JetCacheApplication.class, args);
    }
}
```

**步骤④**：使用注解@Cached标注当前方法使用缓存

```java
@Service
public class BookServiceImpl implements BookService {
   
    @Autowired
    private BookDao bookDao;
    
    @Override
    @Cached(name="book_",key="#id",expire = 3600,cacheType = CacheType.REMOTE)
    public Book getById(Integer id) {
   
        return bookDao.selectById(id);
    }
}
```

##### 远程方案的数据同步

​ 由于远程方案中redis保存的数据可以被多个客户端共享，这就存在了数据同步问题。jetcache提供了3个注解解决此问题，分别在更新、删除操作时同步缓存数据，和读取缓存时定时刷新数据

**更新缓存**

```java
@CacheUpdate(name="book_",key="#book.id",value="#book")
public boolean update(Book book) {
   
    return bookDao.updateById(book) > 0;
}
```

**删除缓存**

```java
@CacheInvalidate(name="book_",key = "#id")
public boolean delete(Integer id) {
   
    return bookDao.deleteById(id) > 0;
}
```

**定时刷新缓存**

```java
@Cached(name="book_",key="#id",expire = 3600,cacheType = CacheType.REMOTE)
@CacheRefresh(refresh = 5)
public Book getById(Integer id) {
   
    return bookDao.selectById(id);
}
```

##### 数据报表

​ jetcache还提供有简单的数据报表功能，帮助开发者快速查看缓存命中信息，只需要添加一个配置即可

```java
jetcache:
  statIntervalMinutes: 1
```

​ 设置后，每1分钟在控制台输出缓存数据命中信息

```java
[DefaultExecutor] c.alicp.jetcache.support.StatInfoLogger  : jetcache stat from 2022-02-28 09:32:15,892 to 2022-02-28 09:33:00,003
cache    |    qps|   rate|   get|    hit|   fail|   expire|   avgLoadTime|   maxLoadTime
---------+-------+-------+------+-------+-------+---------+--------------+--------------
book_    |   0.66| 75.86%|    29|     22|      0|        0|          28.0|           188
---------+-------+-------+------+-------+-------+---------+--------------+--------------
```

**总结**

1. jetcache是一个类似于springcache的缓存解决方案，自身不具有缓存功能，它提供有本地缓存与远程缓存多级共同使用的缓存解决方案 
2. jetcache提供的缓存解决方案受限于目前支持的方案，本地缓存支持两种，远程缓存支持两种 
3. 注意数据进入远程缓存时的类型转换问题 
4. jetcache提供方法缓存，并提供了对应的缓存更新与刷新功能 
5. jetcache提供有简单的缓存信息命中报表方便开发者即时监控缓存数据命中情况


jetcache可以在限定范围内构建多级缓存，但是灵活性不足，不能随意搭配缓存，本节介绍一种可以随意搭配缓存解决方案的缓存整合框架，j2cache。下面就来讲解如何使用这种缓存框架，以Ehcache与redis整合为例：

**步骤①**：导入j2cache、redis、ehcache坐标

```java
<dependency>
    <groupId>net.oschina.j2cache</groupId>
    <artifactId>j2cache-core</artifactId>
    <version>2.8.4-release</version>
</dependency>
<dependency>
    <groupId>net.oschina.j2cache</groupId>
    <artifactId>j2cache-spring-boot2-starter</artifactId>
    <version>2.8.0-release</version>
</dependency>
<dependency>
    <groupId>net.sf.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
```

​ j2cache的starter中默认包含了redis坐标，官方推荐使用redis作为二级缓存，因此此处无需导入redis坐标

**步骤②**：配置一级与二级缓存，并配置一二级缓存间数据传递方式，配置书写在名称为j2cache.properties的文件中。如果使用ehcache还需要单独添加ehcache的配置文件

```java
# 1级缓存
j2cache.L1.provider_class = ehcache
ehcache.configXml = ehcache.xml

# 2级缓存
j2cache.L2.provider_class = net.oschina.j2cache.cache.support.redis.SpringRedisProvider
j2cache.L2.config_section = redis
redis.hosts = localhost:6379

# 1级缓存中的数据如何到达二级缓存
j2cache.broadcast = net.oschina.j2cache.cache.support.redis.SpringRedisPubSubPolicy
```

​ 此处配置不能乱配置，需要参照官方给出的配置说明进行。例如1级供应商选择ehcache，供应商名称仅仅是一个ehcache，但是2级供应商选择redis时要写专用的Spring整合Redis的供应商类名SpringRedisProvider，而且这个名称并不是所有的redis包中能提供的，也不是spring包中提供的。因此配置j2cache必须参照官方文档配置，而且还要去找专用的整合包，导入对应坐标才可以使用。

​ 一级与二级缓存最重要的一个配置就是两者之间的数据沟通方式，此类配置也不是随意配置的，并且不同的缓存解决方案提供的数据沟通方式差异化很大，需要查询官方文档进行设置。

**步骤③**：使用缓存

```java
@Service
public class SMSCodeServiceImpl implements SMSCodeService {
   
    @Autowired
    private CodeUtils codeUtils;

    @Autowired
    private CacheChannel cacheChannel;

    public String sendCodeToSMS(String tele) {
   
        String code = codeUtils.generator(tele);
        cacheChannel.set("sms",tele,code);
        return code;
    }

    public boolean checkCode(SMSCode smsCode) {
   
        String code = cacheChannel.get("sms",smsCode.getTele()).asString();
        return smsCode.getCode().equals(code);
    }
}
```

​ j2cache的使用和jetcache比较类似，但是无需开启使用的开关，直接定义缓存对象即可使用，缓存对象名CacheChannel。

​ **总结**

1. j2cache是一个缓存框架，自身不具有缓存功能，它提供多种缓存整合在一起使用的方案 
2. j2cache需要通过复杂的配置设置各级缓存，以及缓存之间数据交换的方式 
3. j2cache操作接口通过CacheChannel实现


j2cache的使用不复杂，配置是j2cache的核心，毕竟是一个整合型的缓存框架。缓存相关的配置过多，可以查阅j2cache-core核心包中的j2cache.properties文件中的说明。如下：

```java
#J2Cache configuration
#########################################
# Cache Broadcast Method
# values:
# jgroups -> use jgroups's multicast
# redis -> use redis publish/subscribe mechanism (using jedis)
# lettuce -> use redis publish/subscribe mechanism (using lettuce, Recommend)
# rabbitmq -> use RabbitMQ publisher/consumer mechanism
# rocketmq -> use RocketMQ publisher/consumer mechanism
# none -> don't notify the other nodes in cluster
# xx.xxxx.xxxx.Xxxxx your own cache broadcast policy classname that implement net.oschina.j2cache.cluster.ClusterPolicy
#########################################
j2cache.broadcast = redis

# jgroups properties
jgroups.channel.name = j2cache
jgroups.configXml = /network.xml

# RabbitMQ properties
rabbitmq.exchange = j2cache
rabbitmq.host = localhost
rabbitmq.port = 5672
rabbitmq.username = guest
rabbitmq.password = guest

# RocketMQ properties
rocketmq.name = j2cache
rocketmq.topic = j2cache
# use ; to split multi hosts
rocketmq.hosts = 127.0.0.1:9876

#########################################
# Level 1&2 provider
# values:
# none -> disable this level cache
# ehcache -> use ehcache2 as level 1 cache
# ehcache3 -> use ehcache3 as level 1 cache
# caffeine -> use caffeine as level 1 cache(only in memory)
# redis -> use redis as level 2 cache (using jedis)
# lettuce -> use redis as level 2 cache (using lettuce)
# readonly-redis -> use redis as level 2 cache ,but never write data to it. if use this provider, you must uncomment `j2cache.L2.config_section` to make the redis configurations available.
# memcached -> use memcached as level 2 cache (xmemcached),
# [classname] -> use custom provider
#########################################

j2cache.L1.provider_class = caffeine
j2cache.L2.provider_class = redis

# When L2 provider isn't `redis`, using `L2.config_section = redis` to read redis configurations
# j2cache.L2.config_section = redis

# Enable/Disable ttl in redis cache data (if disabled, the object in redis will never expire, default:true)
# NOTICE: redis hash mode (redis.storage = hash) do not support this feature)
j2cache.sync_ttl_to_redis = true

# Whether to cache null objects by default (default false)
j2cache.default_cache_null_object = true

#########################################
# Cache Serialization Provider
# values:
# fst -> using fast-serialization (recommend)
# kryo -> using kryo serialization
# json -> using fst's json serialization (testing)
# fastjson -> using fastjson serialization (embed non-static class not support)
# java -> java standard
# fse -> using fse serialization
# [classname implements Serializer]
#########################################

j2cache.serialization = json
#json.map.person = net.oschina.j2cache.demo.Person

#########################################
# Ehcache configuration
#########################################

# ehcache.configXml = /ehcache.xml

# ehcache3.configXml = /ehcache3.xml
# ehcache3.defaultHeapSize = 1000

#########################################
# Caffeine configuration
# caffeine.region.[name] = size, xxxx[s|m|h|d]
#
#########################################
caffeine.properties = /caffeine.properties

#########################################
# Redis connection configuration
#########################################

#########################################
# Redis Cluster Mode
#
# single -> single redis server
# sentinel -> master-slaves servers
# cluster -> cluster servers (数据库配置无效，使用 database = 0）
# sharded -> sharded servers  (密码、数据库必须在 hosts 中指定，且连接池配置无效 ; redis://user:password@127.0.0.1:6379/0）
#
#########################################

redis.mode = single

#redis storage mode (generic|hash)
redis.storage = generic

## redis pub/sub channel name
redis.channel = j2cache
## redis pub/sub server (using redis.hosts when empty)
redis.channel.host =

#cluster name just for sharded
redis.cluster_name = j2cache

## redis cache namespace optional, default[empty]
redis.namespace =

## redis command scan parameter count, default[1000]
#redis.scanCount = 1000

## connection
# Separate multiple redis nodes with commas, such as 192.168.0.10:6379,192.168.0.11:6379,192.168.0.12:6379

redis.hosts = 127.0.0.1:6379
redis.timeout = 2000
redis.password =
redis.database = 0
redis.ssl = false

## redis pool properties
redis.maxTotal = 100
redis.maxIdle = 10
redis.maxWaitMillis = 5000
redis.minEvictableIdleTimeMillis = 60000
redis.minIdle = 1
redis.numTestsPerEvictionRun = 10
redis.lifo = false
redis.softMinEvictableIdleTimeMillis = 10
redis.testOnBorrow = true
redis.testOnReturn = false
redis.testWhileIdle = true
redis.timeBetweenEvictionRunsMillis = 300000
redis.blockWhenExhausted = false
redis.jmxEnabled = false

#########################################
# Lettuce scheme
#
# redis -> single redis server
# rediss -> single redis server with ssl
# redis-sentinel -> redis sentinel
# redis-cluster -> cluster servers
#
#########################################

#########################################
# Lettuce Mode
#
# single -> single redis server
# sentinel -> master-slaves servers
# cluster -> cluster servers (数据库配置无效，使用 database = 0）
# sharded -> sharded servers  (密码、数据库必须在 hosts 中指定，且连接池配置无效 ; redis://user:password@127.0.0.1:6379/0）
#
#########################################

## redis command scan parameter count, default[1000]
#lettuce.scanCount = 1000
lettuce.mode = single
lettuce.namespace =
lettuce.storage = hash
lettuce.channel = j2cache
lettuce.scheme = redis
lettuce.hosts = 127.0.0.1:6379
lettuce.password =
lettuce.database = 0
lettuce.sentinelMasterId =
lettuce.maxTotal = 100
lettuce.maxIdle = 10
lettuce.minIdle = 10
# timeout in milliseconds
lettuce.timeout = 10000
# redis cluster topology refresh interval in milliseconds
lettuce.clusterTopologyRefresh = 3000

#########################################
# memcached server configurations
# refer to https://gitee.com/mirrors/XMemcached
#########################################

memcached.servers = 127.0.0.1:11211
memcached.username =
memcached.password =
memcached.connectionPoolSize = 10
memcached.connectTimeout = 1000
memcached.failureMode = false
memcached.healSessionInterval = 1000
memcached.maxQueuedNoReplyOperations = 100
memcached.opTimeout = 100
memcached.sanitizeKeys = false
```

**例如:**j2cache.properties

```java
# 1级缓存
j2cache.L1.provider_class = ehcache
ehcache.configXml = ehcache.xml

# 设置是否启用二级缓存
j2cache.l2-cache-open = false

# 2级缓存
j2cache.L2.provider_class = net.oschina.j2cache.cache.support.redis.SpringRedisProvider
j2cache.L2.config_section = redis
redis.hosts = localhost:6379

# 1级缓存中的数据如何到达二级缓存
j2cache.broadcast = net.oschina.j2cache.cache.support.redis.SpringRedisPubSubPolicy

redis.mode = single

redis.namespace = j2cache
```

总结:

1. spring-cache

-  simple  
-  ehcache  
-  redis  
-  memcached 

1.  jetcache  
2.  j2cache 


-  定时任务是企业级应用中的常见操作 
 <ul> 
  -  年度报表  
  -  缓存统计报告  
  -  … …  
 </ul>  
-  市面上流行的定时任务技术 
 <ul> 
  - Quartz 
  - Spring Task 
 </ul> 

学习springboot整合Quartz前先普及几个Quartz的概念。

- 工作（Job）：用于定义具体执行的工作 
- 工作明细（JobDetail）：用于描述定时工作相关的信息 
- 触发器（Trigger）：描述了工作明细与调度器的对应关系 
- 调度器（Scheduler）：用于描述触发工作的执行规则，通常使用cron表达式定义规则

​ 简单说就是你定时干什么事情，这就是工作，工作不可能就是一个简单的方法，还要设置一些明细信息。工作啥时候执行，设置一个调度器，可以简单理解成设置一个工作执行的时间。工作和调度都是独立定义的，它们两个怎么配合到一起呢？用触发器。完了，就这么多。下面开始springboot整合Quartz。

**步骤①**：导入springboot整合Quartz的starter

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-quartz</artifactId>
</dependency>
```

**步骤②**：定义任务Bean，按照Quartz的开发规范制作，继承QuartzJobBean

```java
public class MyQuartz extends QuartzJobBean {
   
    @Override
    protected void executeInternal(JobExecutionContext context) throws JobExecutionException {
   
        System.out.println("quartz task run...");
    }
}
```

**步骤③**：创建Quartz配置类，定义工作明细（JobDetail）与触发器的（Trigger）bean

```java
@Configuration
public class QuartzConfig {
   
    @Bean
    public JobDetail printJobDetail(){
   
        //绑定具体的工作
        return JobBuilder.newJob(MyQuartz.class).storeDurably().build();
    }
    @Bean
    public Trigger printJobTrigger(){
   
        ScheduleBuilder schedBuilder = CronScheduleBuilder.cronSchedule("0/5 * * * * ?");
        //绑定对应的工作明细
        return TriggerBuilder.newTrigger().forJob(printJobDetail()).withSchedule(schedBuilder).build();
    }
}
```

​ 工作明细中要设置对应的具体工作，使用newJob()操作传入对应的工作任务类型即可。

​ 触发器需要绑定任务，使用forJob()操作传入绑定的工作明细对象。此处可以为工作明细设置名称然后使用名称绑定，也可以直接调用对应方法绑定。触发器中最核心的规则是执行时间，此处使用调度器定义执行时间，执行时间描述方式使用的是cron表达式。有关cron表达式的规则，各位小伙伴可以去参看相关课程学习，略微复杂，而且格式不能乱设置，不是写个格式就能用的，写不好就会出现冲突问题。

**总结**

1. springboot整合Quartz就是将Quartz对应的核心对象交给spring容器管理，包含两个对象，JobDetail和Trigger对象 
2. JobDetail对象描述的是工作的执行信息，需要绑定一个QuartzJobBean类型的对象 
3. Trigger对象定义了一个触发器，需要为其指定绑定的JobDetail是哪个，同时要设置执行周期调度器


**步骤①**：开启定时任务功能，在引导类上开启定时任务功能的开关，使用注解@EnableScheduling

```java
@SpringBootApplication
//开启定时任务功能
@EnableScheduling
public class Springboot22TaskApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot22TaskApplication.class, args);
    }
}
```

**步骤②**：定义Bean，在对应要定时执行的操作上方，使用注解@Scheduled定义执行的时间，执行时间的描述方式还是cron表达式

```java
@Component
public class MyBean {
   
    @Scheduled(cron = "0/1 * * * * ?")
    public void print(){
   
        System.out.println(Thread.currentThread().getName()+" :spring task run...");
    }
}
```

​ 完事，这就完成了定时任务的配置。总体感觉其实什么东西都没少，只不过没有将所有的信息都抽取成bean，而是直接使用注解绑定定时执行任务的事情而已。

​ 如何想对定时任务进行相关配置，可以通过配置文件进行

```java
spring:
  task:
   	scheduling:
      pool:
       	size: 1							# 任务调度线程池大小 默认 1
      thread-name-prefix: ssm_      	# 调度线程名称前缀 默认 scheduling-      
        shutdown:
          await-termination: false		# 线程池关闭时等待所有任务完成
          await-termination-period: 10s	# 调度线程关闭前最大等待时间，确保最后一定关闭
```

**总结**

1.  spring task需要使用注解@EnableScheduling开启定时任务功能  
2.  为定时执行的的任务设置执行周期，描述方式cron表达式 


springboot整合第三方技术第三部分我们来说说邮件系统，发邮件是java程序的基本操作，springboot整合javamail其实就是简化开发。不熟悉邮件的小伙伴可以先学习完javamail的基础操作，再来看这一部分内容才能感触到springboot整合javamail究竟简化了哪些操作。简化的多码？其实不多，差别不大，只是还个格式而已。

​ 学习邮件发送之前先了解3个概念，这些概念规范了邮件操作过程中的标准。

- SMTP（Simple Mail Transfer Protocol）：简单邮件传输协议，用于**发送**电子邮件的传输协议 
- POP3（Post Office Protocol - Version 3）：用于**接收**电子邮件的标准协议 
- IMAP（Internet Mail Access Protocol）：互联网消息协议，是POP3的替代协议

​ 简单说就是SMPT是发邮件的标准，POP3是收邮件的标准，IMAP是对POP3的升级。我们制作程序中操作邮件，通常是发邮件，所以SMTP是使用的重点，收邮件大部分都是通过邮件客户端完成，所以开发收邮件的代码极少。除非你要读取邮件内容，然后解析，做邮件功能的统一处理。例如HR的邮箱收到求职者的简历，可以读取后统一处理。但是为什么不制作独立的投递简历的系统呢？所以说，好奇怪的需求，因为要想收邮件就要规范发邮件的人的书写格式，这个未免有点强人所难，并且极易收到外部攻击，你不可能使用白名单来收邮件。如果能使用白名单来收邮件然后解析邮件，还不如开发个系统给白名单中的人专用呢，更安全，总之就是鸡肋了。下面就开始学习springboot如何整合javamail发送邮件。

**步骤①**：导入springboot整合javamail的starter

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

**步骤②**：配置邮箱的登录信息

```java
spring:
  mail:
    host: smtp.126.com
    username: test@126.com
    password: test
```

​ java程序仅用于发送邮件，邮件的功能还是邮件供应商提供的，所以这里是用别人的邮件服务，要配置对应信息。

​ host配置的是提供邮件服务的主机协议，当前程序仅用于发送邮件，因此配置的是smtp的协议。

​ password并不是邮箱账号的登录密码，是邮件供应商提供的一个加密后的密码，也是为了保障系统安全性。不然外部人员通过地址访问下载了配置文件，直接获取到了邮件密码就会有极大的安全隐患。有关该密码的获取每个邮件供应商提供的方式都不一样，此处略过。可以到邮件供应商的设置页面找POP3或IMAP这些关键词找到对应的获取位置。下例仅供参考：


![img](https://img-blog.csdnimg.cn/img_convert/6fe8191884beafa2a883ba490c460a60.png)

**步骤③**：使用JavaMailSender接口发送邮件

```java
@Service
public class SendMailServiceImpl implements SendMailService {
   
    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    private String from = "test@qq.com";
    //接收人
    private String to = "test@126.com";
    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "测试邮件正文内容";

    @Override
    public void sendMail() {
   
        SimpleMailMessage message = new SimpleMailMessage();
        message.setFrom(from+"(小甜甜)");
        message.setTo(to);
        message.setSubject(subject);
        message.setText(context);
        javaMailSender.send(message);
    }
}
```

​ 将发送邮件的必要信息（发件人、收件人、标题、正文）封装到SimpleMailMessage对象中，可以根据规则设置发送人昵称等。


​ 发送简单邮件仅需要提供对应的4个基本信息就可以了，如果想发送复杂的邮件，需要更换邮件对象。使用MimeMessage可以发送特殊的邮件。

**发送网页正文邮件**

```java
@Service
public class SendMailServiceImpl2 implements SendMailService {
   
    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    private String from = "test@qq.com";
    //接收人
    private String to = "test@126.com";
    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "<img src='ABC.JPG'/><a href='https://www.itcast.cn'>点开有惊喜</a>";

    public void sendMail() {
   
        try {
   
            MimeMessage message = javaMailSender.createMimeMessage();
            MimeMessageHelper helper = new MimeMessageHelper(message);
            helper.setFrom(to+"(小甜甜)");
            helper.setTo(from);
            helper.setSubject(subject);
            helper.setText(context,true);		//此处设置正文支持html解析

            javaMailSender.send(message);
        } catch (Exception e) {
   
            e.printStackTrace();
        }
    }
}
```

**发送带有附件的邮件**

```java
@Service
public class SendMailServiceImpl2 implements SendMailService {
   
    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    @Value("${spring.mail.username}")
    private String from;
    //接收人
    private String to = "2564661125@qq.com";

    private String[] tos = {
   "2564661125@qq.com", "bingomail@qq.com"};

    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "<a href='https://blog.csdn.net/qq_42324086'>点开有惊喜</a>";

    @Override
    public void sendMail() {
   
        try {
   
            MimeMessage mimeMessage = javaMailSender.createMimeMessage();
            //MimeMessageHelper helper = new MimeMessageHelper(mimeMessage);
            MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
            helper.setFrom(from + "(小甜甜)");
            //helper.setTo(to);
            //设置多个接收人
            helper.setTo(tos);
            helper.setSubject(subject);
            helper.setText(context, true); //此处设置正文支持html解析

            //添加附件
            File f1 = new File("D:\\code\\Java\\IdeaProjects\\springboot-study\\springboot_23_mail\\target\\springboot_23_mail-0.0.1-SNAPSHOT.jar");
            File f2 = new File("D:\\code\\Java\\IdeaProjects\\springboot-study\\springboot_23_mail\\src\\main\\resources\\logo.png");

            helper.addAttachment(f1.getName(), f1);
            helper.addAttachment("样图.png", f2);

            javaMailSender.send(mimeMessage);
        } catch (Exception e) {
   
            e.printStackTrace();
        }

    }
}
```

**总结**

1. springboot整合javamail其实就是简化了发送邮件的客户端对象JavaMailSender的初始化过程，通过配置的形式加载信息简化开发过程


从广义角度来说，消息其实就是信息，但是和信息又有所不同。信息通常被定义为一组数据，而消息除了具有数据的特征之外，还有消息的来源与接收的概念。通常发送消息的一方称为消息的生产者，接收消息的一方称为消息的消费者

-  消息发送方 
 <ul> 
  - 生产者 
 </ul>  
-  消息接收方 
 <ul> 
  - 消费者 
 </ul>  
-  同步消息 同步消息就是生产者发送完消息，等待消费者处理，消费者处理完将结果告知生产者，然后生产者继续向下执行业务   
-  异步消息 生产者发送完消息，无需等待消费者处理完毕，生产者继续向下执行其他动作  


![img](https://img-blog.csdnimg.cn/img_convert/e94bddb5931ac5c2b3ff4cb199a25844.png)

#### Java处理消息的标准规范

​ 目前企业级开发中广泛使用的消息处理技术共三大类，具体如下：

- JMS 
- AMQP 
- MQTT

​ 为什么是三大类，而不是三个技术呢？因为这些都是规范，就想JDBC技术，是个规范，开发针对规范开发，运行还要靠实现类，例如MySQL提供了JDBC的实现，最终运行靠的还是实现。并且这三类规范都是针对异步消息进行处理的，也符合消息的设计本质，处理异步的业务。对以上三种消息规范做一下普及

##### JMS

-  JMS（Java Message Service）：一个规范，等同于JDBC规范，提供了与消息服务相关的API接口  
-  JMS消息模型 
 <ul> 
  - peer-2-peer：点对点模型，消息发送到一个队列中，队列保存消息。队列的消息只能被一个消费者消费，或超时 
  - **pub**lish-**sub**scribe：发布订阅模型，消息可以被多个消费者消费，生产者和消费者完全独立，不需要感知对方的存在 
 </ul>  
-  JMS消息种类 
 <ul> 
  - TextMessage 
  - MapMessage 
  - **BytesMessage** 
  - StreamMessage 
  - ObjectMessage 
  - Message （只有消息头和属性） 
 </ul>  
-  JMS实现：ActiveMQ、Redis、HornetMQ、RabbitMQ、RocketMQ（没有完全遵守JMS规范） 

##### AMQP

-  AMQP（advanced message queuing protocol）：一种协议（高级消息队列协议，也是消息代理规范），规范了网络交换的数据格式，兼容JMS  
-  优点：具有跨平台性，服务器供应商，生产者，消费者可以使用不同的语言来实现  
-  AMQP消息模型 
 <ul> 
  -  direct exchange  
  -  fanout exchange  
  -  topic exchange  
  -  headers exchange  
  -  system exchange  
 </ul>  
-  AMQP消息种类：byte[]  
-  AMQP实现：RabbitMQ、StormMQ、RocketMQ 

##### MQTT

- MQTT（Message Queueing Telemetry Transport）消息队列遥测传输，专为小设备设计，是物联网（IOT）生态系统中主要成分之一

##### KafKa

​ Kafka，一种高吞吐量的分布式发布订阅消息系统，提供实时消息功能。Kafka技术并不是作为消息中间件为主要功能的产品，但是其拥有发布订阅的工作模式，也可以充当消息中间件来使用，而且目前企业级开发中其身影也不少见。

小结:

1.  消息概念与作用  
2.  JMS  
3.  AMQP  
4.  MQTT 


​ 为了便于下面演示各种各样的消息中间件技术，我们创建一个购物过程生成订单时为用户发送短信的案例环境，模拟使用消息中间件实现发送手机短信的过程。

​ 手机验证码案例需求如下：

-  执行下单业务时（模拟此过程），调用消息服务，将要发送短信的订单id传递给消息中间件  
-  消息处理服务接收到要发送的订单id后输出订单id（模拟发短信） 由于不涉及数据读写，仅开发业务层与表现层，其中短信处理的业务代码独立开发，代码如下： 

**订单业务**

​ **业务层接口**

```java
public interface OrderService {
   
    void order(String id);
}
```

​ 模拟传入订单id，执行下订单业务，参数为虚拟设定，实际应为订单对应的实体类

​ **业务层实现**

```java
@Service
public class OrderServiceImpl implements OrderService {
   
    @Autowired
    private MessageService messageService;
    
    @Override
    public void order(String id) {
   
        //一系列操作，包含各种服务调用，处理各种业务
        System.out.println("订单处理开始");
        //短信消息处理
        messageService.sendMessage(id);
        System.out.println("订单处理结束");
        System.out.println();
    }
}
```

​ 业务层转调短信处理的服务MessageService

​ **表现层服务**

```java
@RestController
@RequestMapping("/orders")
public class OrderController {
   

    @Autowired
    private OrderService orderService;

    @PostMapping("{id}")
    public void order(@PathVariable String id){
   
        orderService.order(id);
    }
}
```

​ 表现层对外开发接口，传入订单id即可（模拟）

**短信处理业务**

​ **业务层接口**

```java
public interface MessageService {
   
    void sendMessage(String id);
    String doMessage();
}
```

​ 短信处理业务层接口提供两个操作，发送要处理的订单id到消息中间件，另一个操作目前暂且设计成处理消息，实际消息的处理过程不应该是手动执行，应该是自动执行，到具体实现时再进行设计

​ **业务层实现**

```java
@Service
public class MessageServiceImpl implements MessageService {
   
    private ArrayList<String> msgList = new ArrayList<String>();

    @Override
    public void sendMessage(String id) {
   
        System.out.println("待发送短信的订单已纳入处理队列，id：" + id);
        msgList.add(id);
        System.out.println("当前短信队列" + msgList.toString());
    }

    @Override
    public String doMessage() {
   
        String id = msgList.remove(0);
        System.out.println("已完成短信发送业务，id：" + id);
        System.out.println("当前短信队列" + msgList.toString());
        return id;
    }
}
```

​ 短信处理业务层实现中使用集合先模拟消息队列，观察效果

​ **表现层服务**

```java
@RestController
@RequestMapping("/msgs")
public class MessageController {
   

    @Autowired
    private MessageService messageService;

    @GetMapping
    public String doMessage(){
   
        String id = messageService.doMessage();
        return id;
    }
}
```

​ 短信处理表现层接口暂且开发出一个处理消息的入口，但是此业务是对应业务层中设计的模拟接口，实际业务不需要设计此接口。

​ 下面开启springboot整合各种各样的消息中间件，从严格满足JMS规范的ActiveMQ开始


​ windows版安装包下载地址： [https://activemq.apache.org/components/classic/download](https://activemq.apache.org/components/classic/download/) [/](https://activemq.apache.org/components/classic/download/)

​ 下载的安装包是解压缩就能使用的zip文件，解压缩完毕后会得到如下文件


![img](https://img-blog.csdnimg.cn/img_convert/5b992ec70e831ce6ede608f746a5a13e.png)

**启动服务器**

```java
activemq.bat
```

​ 运行bin目录下的win32或win64目录下的activemq.bat命令即可，根据自己的操作系统选择即可，默认对外服务端口61616。

**访问web管理服务**

​ ActiveMQ启动后会启动一个Web控制台服务，可以通过该服务管理ActiveMQ。

```java
http://127.0.0.1:8161/
```

​ web管理服务默认端口8161，访问后可以打开ActiveMQ的管理界面，如下：


![img](https://img-blog.csdnimg.cn/410d42a710ce40248d8431b9bac74528.png)

​ 首先输入访问用户名和密码，初始化用户名和密码相同，均为：admin，成功登录后进入管理后台界面，如下：


![img](https://img-blog.csdnimg.cn/img_convert/c4398eaa48fcdf456a0c53f42e145f86.png)

​ 看到上述界面视为启动ActiveMQ服务成功。

**服务端口：61616，管理后台端口：8161**

**启动失败**

​ 在ActiveMQ启动时要占用多个端口，以下为正常启动信息：

>wrapper | --&gt; Wrapper Started as Console<br> wrapper | Launching a JVM…<br> jvm 1 | Wrapper (Version 3.2.3) http://wrapper.tanukisoftware.org<br> jvm 1 | Copyright 1999-2006 Tanuki Software, Inc. All Rights Reserved.<br> jvm 1 |<br> jvm 1 | Java Runtime: Oracle Corporation 1.8.0_172 D:\soft\jdk1.8.0_172\jre<br> jvm 1 | Heap sizes: current=249344k free=235037k max=932352k<br> jvm 1 | JVM args: -Dactivemq.home=…/… -Dactivemq.base=…/… -Djavax.net.ssl.keyStorePassword=password -Djavax.net.ssl.trustStorePassword=password -Djavax.net.ssl.keyStore=…/…/conf/broker.ks -Djavax.net.ssl.trustStore=…/…/conf/broker.ts -Dcom.sun.management.jmxremote -Dorg.apache.activemq.UseDedicatedTaskRunner=true -Djava.util.logging.config.file=logging.properties -Dactivemq.conf=…/…/conf -Dactivemq.data=…/…/data -Djava.security.auth.login.config=…/…/conf/login.config -Xmx1024m -Djava.library.path=…/…/bin/win64 -Dwrapper.key=7ySrCD75XhLCpLjd -Dwrapper.port=32000 -Dwrapper.jvm.port.min=31000 -Dwrapper.jvm.port.max=31999 -Dwrapper.pid=9364 -Dwrapper.version=3.2.3 -Dwrapper.native_library=wrapper -Dwrapper.cpu.timeout=10 -Dwrapper.jvmid=1<br> jvm 1 | Extensions classpath:<br> jvm 1 | […\lib,…\lib\camel,…\lib\optional,…\lib\web,…\lib\extra]<br> jvm 1 | ACTIVEMQ_HOME: …<br> jvm 1 | ACTIVEMQ_BASE: …<br> jvm 1 | ACTIVEMQ_CONF: …\conf<br> jvm 1 | ACTIVEMQ_DATA: …\data<br> jvm 1 | Loading message broker from: xbean:activemq.xml<br> jvm 1 | INFO | Refreshing org.apache.activemq.xbean.XBeanBrokerFactory$1@5f3ebfe0: startup date [Mon Feb 28 16:07:48 CST 2022]; root of context hierarchy<br> jvm 1 | INFO | Using Persistence Adapter: KahaDBPersistenceAdapter[D:\soft\activemq\bin\win64…\data\kahadb]<br> jvm 1 | INFO | KahaDB is version 7<br> jvm 1 | INFO | PListStore:[D:\soft\activemq\bin\win64…\data\localhost\tmp_storage] started<br> jvm 1 | INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10434-1646035669595-0:1) is starting<br> jvm 1 | INFO | Listening for connections at: tcp://CZBK-20210302VL:61616?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600<br> jvm 1 | INFO | Connector openwire started<br> jvm 1 | INFO | Listening for connections at: amqp://CZBK-20210302VL:5672?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600<br> jvm 1 | INFO | Connector amqp started<br> jvm 1 | INFO | Listening for connections at: stomp://CZBK-20210302VL:61613?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600<br> jvm 1 | INFO | Connector stomp started<br> jvm 1 | INFO | Listening for connections at: mqtt://CZBK-20210302VL:1883?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600<br> jvm 1 | INFO | Connector mqtt started<br> jvm 1 | INFO | Starting Jetty server<br> jvm 1 | INFO | Creating Jetty connector<br> jvm 1 | WARN | ServletContext@o.e.j.s.ServletContextHandler@7350746f{/,null,STARTING} has uncovered http methods for path: /<br> jvm 1 | INFO | Listening for connections at ws://CZBK-20210302VL:61614?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600<br> jvm 1 | INFO | Connector ws started<br> jvm 1 | INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10434-1646035669595-0:1) started<br> jvm 1 | INFO | For help or more information please see: http://activemq.apache.org<br> jvm 1 | WARN | Store limit is 102400 mb (current store usage is 0 mb). The data directory: D:\soft\activemq\bin\win64…\data\kahadb only has 68936 mb of usable space. - resetting to maximum available disk space: 68936 mb<br> <strong>jvm 1 | INFO | ActiveMQ WebConsole available at http://127.0.0.1:8161/</strong><br> <strong>jvm 1 | INFO | ActiveMQ Jolokia REST API available at http://127.0.0.1:8161/api/jolokia/</strong>

==


![img](https://img-blog.csdnimg.cn/img_convert/1a6c99ef2a29933b7771b2b465433549.png)

​ 其中占用的端口有：61616、5672、61613、1883、61614，如果启动失败，请先管理对应端口即可。以下就是某个端口占用的报错信息，可以从抛出异常的位置看出，启动5672端口时端口被占用，显示java.net.BindException: Address already in use: JVM_Bind。Windows系统中终止端口运行的操作参看 [【命令行启动常见问题及解决方案】](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%90%AF%E5%8A%A8%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E5%8F%8A%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)

```java
wrapper  | --> Wrapper Started as Console
wrapper  | Launching a JVM...
jvm 1    | Wrapper (Version 3.2.3) http://wrapper.tanukisoftware.org
jvm 1    |   Copyright 1999-2006 Tanuki Software, Inc.  All Rights Reserved.
jvm 1    |
jvm 1    | Java Runtime: Oracle Corporation 1.8.0_172 D:\soft\jdk1.8.0_172\jre
jvm 1    |   Heap sizes: current=249344k  free=235038k  max=932352k
jvm 1    |     JVM args: -Dactivemq.home=../.. -Dactivemq.base=../.. -Djavax.net.ssl.keyStorePassword=password -Djavax.net.ssl.trustStorePassword=password -Djavax.net.ssl.keyStore=../../conf/broker.ks -Djavax.net.ssl.trustStore=../../conf/broker.ts -Dcom.sun.management.jmxremote -Dorg.apache.activemq.UseDedicatedTaskRunner=true -Djava.util.logging.config.file=logging.properties -Dactivemq.conf=../../conf -Dactivemq.data=../../data -Djava.security.auth.login.config=../../conf/login.config -Xmx1024m -Djava.library.path=../../bin/win64 -Dwrapper.key=QPJoy9ZoXeWmmwTS -Dwrapper.port=32000 -Dwrapper.jvm.port.min=31000 -Dwrapper.jvm.port.max=31999 -Dwrapper.pid=14836 -Dwrapper.version=3.2.3 -Dwrapper.native_library=wrapper -Dwrapper.cpu.timeout=10 -Dwrapper.jvmid=1
jvm 1    | Extensions classpath:
jvm 1    |   [..\..\lib,..\..\lib\camel,..\..\lib\optional,..\..\lib\web,..\..\lib\extra]
jvm 1    | ACTIVEMQ_HOME: ..\..
jvm 1    | ACTIVEMQ_BASE: ..\..
jvm 1    | ACTIVEMQ_CONF: ..\..\conf
jvm 1    | ACTIVEMQ_DATA: ..\..\data
jvm 1    | Loading message broker from: xbean:activemq.xml
jvm 1    |  INFO | Refreshing org.apache.activemq.xbean.XBeanBrokerFactory$1@2c9392f5: startup date [Mon Feb 28 16:06:16 CST 2022]; root of context hierarchy
jvm 1    |  INFO | Using Persistence Adapter: KahaDBPersistenceAdapter[D:\soft\activemq\bin\win64\..\..\data\kahadb]
jvm 1    |  INFO | KahaDB is version 7
jvm 1    |  INFO | PListStore:[D:\soft\activemq\bin\win64\..\..\data\localhost\tmp_storage] started
jvm 1    |  INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10257-1646035577620-0:1) is starting
jvm 1    |  INFO | Listening for connections at: tcp://CZBK-20210302VL:61616?maximumConnections=1000&wireFormat.maxFrameSize=104857600
jvm 1    |  INFO | Connector openwire started
jvm 1    | ERROR | Failed to start Apache ActiveMQ (localhost, ID:CZBK-20210302VL-10257-1646035577620-0:1)
jvm 1    | java.io.IOException: Transport Connector could not be registered in JMX: java.io.IOException: Failed to bind to server socket: amqp://0.0.0.0:5672?maximumConnections=1000&wireFormat.maxFrameSize=104857600 due to: java.net.BindException: Address already in use: JVM_Bind
jvm 1    |      at org.apache.activemq.util.IOExceptionSupport.create(IOExceptionSupport.java:28)
jvm 1    |      at org.apache.activemq.broker.BrokerService.registerConnectorMBean(BrokerService.java:2288)
jvm 1    |      at org.apache.activemq.broker.BrokerService.startTransportConnector(BrokerService.java:2769)
jvm 1    |      at org.apache.activemq.broker.BrokerService.startAllConnectors(BrokerService.java:2665)
jvm 1    |      at org.apache.activemq.broker.BrokerService.doStartBroker(BrokerService.java:780)
jvm 1    |      at org.apache.activemq.broker.BrokerService.startBroker(BrokerService.java:742)
jvm 1    |      at org.apache.activemq.broker.BrokerService.start(BrokerService.java:645)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerService.afterPropertiesSet(XBeanBrokerService.java:73)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeCustomInitMethod(AbstractAutowireCapableBeanFactory.java:1748)
jvm 1    |      at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1685)
jvm 1    |      at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1615)
jvm 1    |      at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:553)
jvm 1    |      at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:481)
jvm 1    |      at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:312)
jvm 1    |      at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
jvm 1    |      at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:308)
jvm 1    |      at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:197)
jvm 1    |      at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:756)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:867)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:542)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:64)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:52)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory$1.<init>(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createApplicationContext(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createBroker(XBeanBrokerFactory.java:67)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:71)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:54)
jvm 1    |      at org.apache.activemq.console.command.StartCommand.runTask(StartCommand.java:87)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.runTask(ShellCommand.java:154)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.main(ShellCommand.java:104)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.apache.activemq.console.Main.runTaskClass(Main.java:262)
jvm 1    |      at org.apache.activemq.console.Main.main(Main.java:115)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.tanukisoftware.wrapper.WrapperSimpleApp.run(WrapperSimpleApp.java:240)
jvm 1    |      at java.lang.Thread.run(Thread.java:748)
jvm 1    | Caused by: java.io.IOException: Failed to bind to server socket: amqp://0.0.0.0:5672?maximumConnections=1000&wireFormat.maxFrameSize=104857600 due to: java.net.BindException: Address already in use: JVM_Bind
jvm 1    |      at org.apache.activemq.util.IOExceptionSupport.create(IOExceptionSupport.java:34)
jvm 1    |      at org.apache.activemq.transport.tcp.TcpTransportServer.bind(TcpTransportServer.java:146)
jvm 1    |      at org.apache.activemq.transport.tcp.TcpTransportFactory.doBind(TcpTransportFactory.java:62)
jvm 1    |      at org.apache.activemq.transport.TransportFactorySupport.bind(TransportFactorySupport.java:40)
jvm 1    |      at org.apache.activemq.broker.TransportConnector.createTransportServer(TransportConnector.java:335)
jvm 1    |      at org.apache.activemq.broker.TransportConnector.getServer(TransportConnector.java:145)
jvm 1    |      at org.apache.activemq.broker.TransportConnector.asManagedConnector(TransportConnector.java:110)
jvm 1    |      at org.apache.activemq.broker.BrokerService.registerConnectorMBean(BrokerService.java:2283)
jvm 1    |      ... 46 more
jvm 1    | Caused by: java.net.BindException: Address already in use: JVM_Bind
jvm 1    |      at java.net.DualStackPlainSocketImpl.bind0(Native Method)
jvm 1    |      at java.net.DualStackPlainSocketImpl.socketBind(DualStackPlainSocketImpl.java:106)
jvm 1    |      at java.net.AbstractPlainSocketImpl.bind(AbstractPlainSocketImpl.java:387)
jvm 1    |      at java.net.PlainSocketImpl.bind(PlainSocketImpl.java:190)
jvm 1    |      at java.net.ServerSocket.bind(ServerSocket.java:375)
jvm 1    |      at java.net.ServerSocket.<init>(ServerSocket.java:237)
jvm 1    |      at javax.net.DefaultServerSocketFactory.createServerSocket(ServerSocketFactory.java:231)
jvm 1    |      at org.apache.activemq.transport.tcp.TcpTransportServer.bind(TcpTransportServer.java:143)
jvm 1    |      ... 52 more
jvm 1    |  INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10257-1646035577620-0:1) is shutting down
jvm 1    |  INFO | socketQueue interrupted - stopping
jvm 1    |  INFO | Connector openwire stopped
jvm 1    |  INFO | Could not accept connection during shutdown  : null (null)
jvm 1    |  INFO | Connector amqp stopped
jvm 1    |  INFO | Connector stomp stopped
jvm 1    |  INFO | Connector mqtt stopped
jvm 1    |  INFO | Connector ws stopped
jvm 1    |  INFO | PListStore:[D:\soft\activemq\bin\win64\..\..\data\localhost\tmp_storage] stopped
jvm 1    |  INFO | Stopping async queue tasks
jvm 1    |  INFO | Stopping async topic tasks
jvm 1    |  INFO | Stopped KahaDB
jvm 1    |  INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10257-1646035577620-0:1) uptime 0.426 seconds
jvm 1    |  INFO | Apache ActiveMQ 5.16.3 (localhost, ID:CZBK-20210302VL-10257-1646035577620-0:1) is shutdown
jvm 1    |  INFO | Closing org.apache.activemq.xbean.XBeanBrokerFactory$1@2c9392f5: startup date [Mon Feb 28 16:06:16 CST 2022]; root of context hierarchy
jvm 1    |  WARN | Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.activemq.xbean.XBeanBrokerService#0' defined in class path resource [activemq.xml]: Invocation of init method failed; nested exception is java.io.IOException: Transport Connector could not be registered in JMX: java.io.IOException: Failed to bind to server socket: amqp://0.0.0.0:5672?maximumConnections=1000&wireFormat.maxFrameSize=104857600 due to: java.net.BindException: Address already in use: JVM_Bind
jvm 1    | ERROR: java.lang.RuntimeException: Failed to execute start task. Reason: java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext
jvm 1    | java.lang.RuntimeException: Failed to execute start task. Reason: java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext
jvm 1    |      at org.apache.activemq.console.command.StartCommand.runTask(StartCommand.java:91)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.runTask(ShellCommand.java:154)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.main(ShellCommand.java:104)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.apache.activemq.console.Main.runTaskClass(Main.java:262)
jvm 1    |      at org.apache.activemq.console.Main.main(Main.java:115)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.tanukisoftware.wrapper.WrapperSimpleApp.run(WrapperSimpleApp.java:240)
jvm 1    |      at java.lang.Thread.run(Thread.java:748)
jvm 1    | Caused by: java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext
jvm 1    |      at org.springframework.context.support.AbstractRefreshableApplicationContext.getBeanFactory(AbstractRefreshableApplicationContext.java:164)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1034)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:555)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:64)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:52)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory$1.<init>(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createApplicationContext(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createBroker(XBeanBrokerFactory.java:67)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:71)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:54)
jvm 1    |      at org.apache.activemq.console.command.StartCommand.runTask(StartCommand.java:87)
jvm 1    |      ... 16 more
jvm 1    | ERROR: java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext
jvm 1    | java.lang.IllegalStateException: BeanFactory not initialized or already closed - call 'refresh' before accessing beans via the ApplicationContext
jvm 1    |      at org.springframework.context.support.AbstractRefreshableApplicationContext.getBeanFactory(AbstractRefreshableApplicationContext.java:164)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.destroyBeans(AbstractApplicationContext.java:1034)
jvm 1    |      at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:555)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:64)
jvm 1    |      at org.apache.xbean.spring.context.ResourceXmlApplicationContext.<init>(ResourceXmlApplicationContext.java:52)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory$1.<init>(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createApplicationContext(XBeanBrokerFactory.java:104)
jvm 1    |      at org.apache.activemq.xbean.XBeanBrokerFactory.createBroker(XBeanBrokerFactory.java:67)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:71)
jvm 1    |      at org.apache.activemq.broker.BrokerFactory.createBroker(BrokerFactory.java:54)
jvm 1    |      at org.apache.activemq.console.command.StartCommand.runTask(StartCommand.java:87)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.runTask(ShellCommand.java:154)
jvm 1    |      at org.apache.activemq.console.command.AbstractCommand.execute(AbstractCommand.java:63)
jvm 1    |      at org.apache.activemq.console.command.ShellCommand.main(ShellCommand.java:104)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.apache.activemq.console.Main.runTaskClass(Main.java:262)
jvm 1    |      at org.apache.activemq.console.Main.main(Main.java:115)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
jvm 1    |      at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
jvm 1    |      at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
jvm 1    |      at java.lang.reflect.Method.invoke(Method.java:498)
jvm 1    |      at org.tanukisoftware.wrapper.WrapperSimpleApp.run(WrapperSimpleApp.java:240)
jvm 1    |      at java.lang.Thread.run(Thread.java:748)
wrapper  | <-- Wrapper Stopped
请按任意键继续. . .
```

小结:

1.  ActiveMQ下载与安装  
2.  ActiveMQ服务启动（控制台） 


**步骤①**：导入springboot整合ActiveMQ的starter

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

**步骤②**：配置ActiveMQ的服务器地址

```java
spring:
  activemq:
    broker-url: tcp://localhost:61616
```

**步骤③**：使用JmsMessagingTemplate操作ActiveMQ

```java
@Service
public class MessageServiceActivemqImpl implements MessageService {
   
    @Autowired
    private JmsMessagingTemplate messagingTemplate;

    @Override
    public void sendMessage(String id) {
   
        System.out.println("待发送短信的订单已纳入处理队列，id："+id);
        messagingTemplate.convertAndSend("order.queue.id",id);
    }

    @Override
    public String doMessage() {
   
        String id = messagingTemplate.receiveAndConvert("order.queue.id",String.class);
        System.out.println("已完成短信发送业务，id："+id);
        return id;
    }
}
```

​ 发送消息需要先将消息的类型转换成字符串，然后再发送，所以是convertAndSend，定义消息发送的位置，和具体的消息内容，此处使用id作为消息内容。

​ 接收消息需要先将消息接收到，然后再转换成指定的数据类型，所以是receiveAndConvert，接收消息除了提供读取的位置，还要给出转换后的数据的具体类型。

**步骤④**：使用消息监听器在服务器启动后，监听指定位置，当消息出现后，立即消费消息

```java
@Component
public class MessageListener {
   
    @JmsListener(destination = "order.queue.id")
    @SendTo("order.other.queue.id")
    public String receive(String id){
   
        System.out.println("已完成短信发送业务，id："+id);
        return "new:"+id;
    }
}
```

​ 使用注解@JmsListener定义当前方法监听ActiveMQ中指定名称的消息队列。

​ 如果当前消息队列处理完还需要继续向下传递当前消息到另一个队列中使用注解@SendTo即可，这样即可构造连续执行的顺序消息队列。

**步骤⑤**：切换消息模型由点对点模型到发布订阅模型，修改jms配置即可

```java
spring:
  activemq:
    broker-url: tcp://localhost:61616
  jms:
    pub-sub-domain: true
```

​ pub-sub-domain默认值为false，即点对点模型，修改为true后就是发布订阅模型。

**总结**

1. springboot整合ActiveMQ提供了JmsMessagingTemplate对象作为客户端操作消息队列 
2. 操作ActiveMQ需要配置ActiveMQ服务器地址，默认端口61616 
3. 企业开发时通常使用监听器来处理消息队列中的消息，设置监听器使用注解@JmsListener 
4. 配置jms的pub-sub-domain属性可以在点对点模型和发布订阅模型间切换消息模型


​ RabbitMQ是MQ产品中的目前较为流行的产品之一，它遵从AMQP协议。RabbitMQ的底层实现语言使用的是Erlang，所以安装RabbitMQ需要先安装Erlang。

**Erlang安装**

​ windows版安装包下载地址： [https](https://www.erlang.org/downloads) [😕/www.erlang.org/downloads](https://www.erlang.org/downloads)

​ 下载完毕后得到exe安装文件，一键傻瓜式安装，安装完毕需要重启，需要重启，需要重启。

​ 安装的过程中可能会出现依赖Windows组件的提示，根据提示下载安装即可，都是自动执行的，如下：


![img](https://img-blog.csdnimg.cn/img_convert/8b9019212b61b837f1d3021bd20c593c.png)

​ Erlang安装后需要配置环境变量，否则RabbitMQ将无法找到安装的Erlang。需要配置项如下，作用等同JDK配置环境变量的作用。

-  ERLANG_HOME   
-  PATH 在系统变量的path里添加 %ERLANG_HOME%\bin 

##### 安装

​ windows版安装包下载地址： [https://](https://rabbitmq.com/install-windows.html) [rabbitmq.com/install-windows.html](https://rabbitmq.com/install-windows.html)

​ 下载完毕后得到exe安装文件，一键傻瓜式安装，安装完毕后会得到如下文件


![img](https://img-blog.csdnimg.cn/64f0770d97554eca9bac425b593565d5.png)

**启动服务器**

```java
rabbitmq-service.bat start		# 启动服务
rabbitmq-service.bat stop		# 停止服务
rabbitmqctl status				# 查看服务状态
```

​ 运行sbin目录下的rabbitmq-service.bat命令即可(cmd命令行要有管理员权限)，start参数表示启动，stop参数表示退出，默认对外服务端口5672。

​ 注意：启动rabbitmq的过程实际上是开启rabbitmq对应的系统服务，需要管理员权限方可执行。

​ 说明：有没有感觉5672的服务端口很熟悉？activemq与rabbitmq有一个端口冲突问题，学习阶段无论操作哪一个？请确保另一个处于关闭状态。

​ 说明：不喜欢命令行的小伙伴可以使用任务管理器中的服务页，找到RabbitMQ服务，使用鼠标右键菜单控制服务的启停。


![img](https://img-blog.csdnimg.cn/070cec357a8b4164a2734dde958d45a0.png)

**访问web管理服务**

​ RabbitMQ也提供有web控制台服务，但是此功能是一个插件，需要先启用才可以使用,在**sbin目录**下运行下面的命令

```java
rabbitmq-plugins.bat list							# 查看当前所有插件的运行状态
rabbitmq-plugins.bat enable rabbitmq_management		# 启动rabbitmq_management插件
```

​ 启动插件后可以在插件运行状态中查看是否运行，运行后通过浏览器即可打开服务后台管理界面

```java
http://localhost:15672
```

​ web管理服务默认端口15672，服务端口：5672，访问后可以打开RabbitMQ的管理界面，如下：


![img](https://img-blog.csdnimg.cn/img_convert/cb8406067a6ea660fd1841a5feea6dd7.png)

​ 首先输入访问用户名和密码，初始化用户名和密码相同，均为：guest，成功登录后进入管理后台界面，如下：


![img](https://img-blog.csdnimg.cn/img_convert/d2a7c4433b2e8a69e9b22e465df07aa6.png)

小结:

1.  Erlang下载与安装（环境变量配置）  
2.  RabbitMQ下载与安装  
3.  RabbitMQ服务启动（服务）  
4.  RabbitMQ服务管理 


RabbitMQ满足AMQP协议，因此不同的消息模型对应的制作不同，先使用最简单的direct模型开发。

**步骤①**：导入springboot整合amqp的starter，amqp协议默认实现为rabbitmq方案

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

**步骤②**：配置RabbitMQ的服务器地址

```java
spring:
  rabbitmq:
    host: localhost
    port: 5672
```

**步骤③**：初始化直连模式系统设置

​ 由于RabbitMQ不同模型要使用不同的交换机，因此需要先初始化RabbitMQ相关的对象，例如队列，交换机等

```java
@Configuration
public class RabbitConfigDirect {
   
    @Bean
    public Queue directQueue(){
   
        return new Queue("direct_queue");
    }
    @Bean
    public Queue directQueue2(){
   
        return new Queue("direct_queue2");
    }
    @Bean
    public DirectExchange directExchange(){
   
        return new DirectExchange("directExchange");
    }
    @Bean
    public Binding bindingDirect(){
   
        return BindingBuilder.bind(directQueue()).to(directExchange()).with("direct");
    }
    @Bean
    public Binding bindingDirect2(){
   
        return BindingBuilder.bind(directQueue2()).to(directExchange()).with("direct2");
    }
}
```

​ 队列Queue与直连交换机DirectExchange创建后，还需要绑定他们之间的关系Binding，这样就可以通过交换机操作对应队列。

**步骤④**：使用AmqpTemplate操作RabbitMQ

```java
@Service
public class MessageServiceRabbitmqDirectImpl implements MessageService {
   
    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
   
        System.out.println("待发送短信的订单已纳入处理队列（rabbitmq direct），id："+id);
        amqpTemplate.convertAndSend("directExchange","direct",id);
    }
    
    @Override
    public String doMessage() {
   
        return null;
    }
}
```

​ amqp协议中的操作API接口名称看上去和jms规范的操作API接口很相似，但是传递参数差异很大。

**步骤⑤**：使用消息监听器在服务器启动后，监听指定位置，当消息出现后，立即消费消息

```java
@Component
public class MessageListener {
   
    @RabbitListener(queues = "direct_queue")
    public void receive(String id){
   
        System.out.println("已完成短信发送业务(rabbitmq direct)，id："+id);
    }
}
```

​ 使用注解@RabbitListener定义当前方法监听RabbitMQ中指定名称的消息队列。

小结:

1. SpringBoot整合RabbitMQ直连交换机模式


**步骤①**：同上

**步骤②**：同上

**步骤③**：初始化主题模式系统设置

```java
@Configuration
public class RabbitConfigTopic {
   
    @Bean
    public Queue topicQueue(){
   
        return new Queue("topic_queue");
    }
    @Bean
    public Queue topicQueue2(){
   
        return new Queue("topic_queue2");
    }
    @Bean
    public TopicExchange topicExchange(){
   
        return new TopicExchange("topicExchange");
    }
    @Bean
    public Binding bindingTopic(){
   
        return BindingBuilder.bind(topicQueue()).to(topicExchange()).with("topic.*.id");
    }
    @Bean
    public Binding bindingTopic2(){
   
        return BindingBuilder.bind(topicQueue2()).to(topicExchange()).with("topic.orders.*");
    }
}
```

​ 主题模式支持routingKey匹配模式，*表示匹配一个单词，#表示匹配任意内容，这样就可以通过主题交换机将消息分发到不同的队列中，详细内容请参看RabbitMQ系列课程。


**步骤④**：使用AmqpTemplate操作RabbitMQ

```java
@Service
public class MessageServiceRabbitmqTopicImpl implements MessageService {
   
    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
   
        System.out.println("待发送短信的订单已纳入处理队列（rabbitmq topic），id："+id);
        amqpTemplate.convertAndSend("topicExchange","topic.orders.id",id);
    }
    
    @Override
    public String doMessage() {
   
        return null;
    }
}
```

​ 发送消息后，根据当前提供的routingKey与绑定交换机时设定的routingKey进行匹配，规则匹配成功消息才会进入到对应的队列中。

**步骤⑤**：使用消息监听器在服务器启动后，监听指定队列

```java
@Component
public class MessageListener {
   
    @RabbitListener(queues = "topic_queue")
    public void receive(String id){
   
        System.out.println("已完成短信发送业务(rabbitmq topic 1)，id："+id);
    }
    @RabbitListener(queues = "topic_queue2")
    public void receive2(String id){
   
        System.out.println("已完成短信发送业务(rabbitmq topic 22222222)，id："+id);
    }
}
```

​ 使用注解@RabbitListener定义当前方法监听RabbitMQ中指定名称的消息队列。

**总结**

1. springboot整合RabbitMQ提供了AmqpTemplate对象作为客户端操作消息队列 
2. 操作ActiveMQ需要配置ActiveMQ服务器地址，默认端口5672 
3. 企业开发时通常使用监听器来处理消息队列中的消息，设置监听器使用注解@RabbitListener 
4. RabbitMQ有5种消息模型，使用的队列相同，但是交换机不同。交换机不同，对应的消息进入的策略也不同


RocketMQ由阿里研发，后捐赠给apache基金会，目前是apache基金会顶级项目之一，也是目前市面上的MQ产品中较为流行的产品之一，它遵从AMQP协议。

##### 安装

​ windows版安装包下载地址： [https://rocketmq.apache.org](https://rocketmq.apache.org/) [/](https://rocketmq.apache.org/)

​ 下载完毕后得到zip压缩文件，解压缩即可使用，解压后得到如下文件


![img](https://img-blog.csdnimg.cn/img_convert/531c32486baab1b702f4761b4e93c064.png)

​ RocketMQ安装后需要配置环境变量，具体如下：

-  ROCKETMQ_HOME   
-  PATH 在系统变量的path里添加 %ROCKETMQ_HOME%\bin  
-  NAMESRV_ADDR （建议）： 127.0.0.1:9876  

​ 关于NAMESRV_ADDR对于初学者来说建议配置此项，也可以通过命令设置对应值，操作略显繁琐，建议配置。系统学习RocketMQ知识后即可灵活控制该项。

**RocketMQ工作模式**

​ 在RocketMQ中，处理业务的服务器称为broker，生产者与消费者不是直接与broker联系的，而是通过命名服务器进行通信。broker启动后会通知命名服务器自己已经上线，这样命名服务器中就保存有所有的broker信息。当生产者与消费者需要连接broker时，通过命名服务器找到对应的处理业务的broker，因此命名服务器在整套结构中起到一个信息中心的作用。并且broker启动前必须保障命名服务器先启动。


![img](https://img-blog.csdnimg.cn/773cb136625a45a4b291fa30d98410a2.png)

**启动服务器**

-  先启动命名服务器 mqnamesrv		# 启动命名服务器   
-  启动broker mqbroker		# 启动broker 


![img](https://img-blog.csdnimg.cn/img_convert/f62ab970c1762465a9f1b50fb4f7d051.png)

​ 运行bin目录下的mqnamesrv命令即可启动命名服务器，默认对外服务端口9876。

​ 运行bin目录下的mqbroker命令即可启动broker服务器，如果环境变量中没有设置NAMESRV_ADDR则需要在运行mqbroker指令前通过set指令设置NAMESRV_ADDR的值，并且每次开启均需要设置此项。

**测试服务器启动状态**

​ RocketMQ提供有一套测试服务器功能的测试程序，运行bin目录下的tools命令即可使用。

```java
tools org.apache.rocketmq.example.quickstart.Producer		# 生产消息
tools org.apache.rocketmq.example.quickstart.Consumer		# 消费消息
```

小结:

1.  RocketMQ下载与安装（环境变量配置）  
2.  命名服务器启动（控制台）  
3.  broker服务启动（控制台）  
4.  消息生产消费测试 


**步骤①**：导入springboot整合RocketMQ的starter，此坐标不由springboot维护版本

```java
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-spring-boot-starter</artifactId>
    <version>2.2.1</version>
</dependency>
```

**步骤②**：配置RocketMQ的服务器地址

```java
rocketmq:
  name-server: localhost:9876
  producer:
    group: group_rocketmq
```

​ 设置默认的生产者消费者所属组group。

**步骤③**：使用RocketMQTemplate操作RocketMQ

```java
@Service
public class MessageServiceRocketmqImpl implements MessageService {
   

    @Autowired
    private RocketMQTemplate rocketMQTemplate;


    @Override
    public void sendMessage(String id) {
   
        //同步
        // rocketMQTemplate.convertAndSend("order_sm_id", id);
        
        //异步
        SendCallback callback = new SendCallback() {
   
            @Override
            public void onSuccess(SendResult sendResult) {
   
                System.out.println("消息发送成功");
            }

            @Override
            public void onException(Throwable e) {
   
                System.out.println("消息发送失败！！！！！");
            }
        };
        rocketMQTemplate.asyncSend("order_id", id, callback);
        System.out.println("使用Rabbitmq将待发送短信的订单纳入处理队列，id：" + id);
    }

    @Override
    public String doMessage() {
   
        return null;
    }
}
```

​ 使用asyncSend方法发送异步消息。

**步骤④**：使用消息监听器在服务器启动后，监听指定位置，当消息出现后，立即消费消息

```java
@Component
@RocketMQMessageListener(topic = "order_id",consumerGroup = "group_rocketmq")
public class MessageListener implements RocketMQListener<String> {
   
    @Override
    public void onMessage(String id) {
   
        System.out.println("已完成短信发送业务(rocketmq)，id："+id);
    }
}
```

​ RocketMQ的监听器必须按照标准格式开发，实现RocketMQListener接口，泛型为消息类型。

​ 使用注解@RocketMQMessageListener定义当前类监听RabbitMQ中指定组、指定名称的消息队列。

**总结**

1. springboot整合RocketMQ使用RocketMQTemplate对象作为客户端操作消息队列 
2. 操作RocketMQ需要配置RocketMQ服务器地址，默认端口9876 
3. 企业开发时通常使用监听器来处理消息队列中的消息，设置监听器使用注解@RocketMQMessageListener


##### 安装

​ windows版安装包下载地址： [https://](https://kafka.apache.org/downloads) [kafka.apache.org/downloads](https://kafka.apache.org/downloads)

​ 下载完毕后得到tgz压缩文件，使用解压缩软件解压缩即可使用，解压后得到如下文件


![img](https://img-blog.csdnimg.cn/img_convert/d0dc7eeed86d1c00da745d0ecd0e67b8.png)

​ 建议使用windows版2.8.1版本。

**启动服务器**

​ kafka服务器的功能相当于RocketMQ中的broker，kafka运行还需要一个类似于命名服务器的服务。在kafka安装目录中自带一个类似于命名服务器的工具，叫做zookeeper，它的作用是注册中心，相关知识请到对应课程中学习。

```java
zookeeper-server-start.bat ..\..\config\zookeeper.properties		# 启动zookeeper
kafka-server-start.bat ..\..\config\server.properties				# 启动kafka
```

​ 运行**bin目录下的windows目录**下的zookeeper-server-start命令即可启动注册中心，默认对外服务端口2181。

​ 运行bin目录下的windows目录下的kafka-server-start命令即可启动kafka服务器，默认对外**服务端口9092**。

**创建主题**

​ 和之前操作其他MQ产品相似，kakfa也是基于主题操作，操作之前需要先初始化topic。

```java
# 创建topic
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic testTopic
# 查询topic
kafka-topics.bat --zookeeper 127.0.0.1:2181 --list					
# 删除topic
kafka-topics.bat --delete --zookeeper localhost:2181 --topic testTopic
```

**测试服务器启动状态**

​ Kafka提供有一套测试服务器功能的测试程序，运行bin目录下的windows目录下的命令即可使用。

```java
kafka-console-producer.bat --broker-list localhost:9092 --topic testTopic						# 测试生产消息
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic testTopic --from-beginning	# 测试消息消费
```


![img](https://img-blog.csdnimg.cn/img_convert/ad2e1e8cedafd553b7ddf659607b7257.png)


**步骤①**：导入springboot整合Kafka的starter，此坐标由springboot维护版本

```java
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

**步骤②**：配置Kafka的服务器地址

```java
spring:
  kafka:
    bootstrap-servers: localhost:9092
    consumer:
      group-id: order
```

​ 设置默认的生产者消费者所属组id。

**步骤③**：使用KafkaTemplate操作Kafka

```java
@Service
public class MessageServiceKafkaImpl implements MessageService {
   
    @Autowired
    private KafkaTemplate<String,String> kafkaTemplate;

    @Override
    public void sendMessage(String id) {
   
        System.out.println("待发送短信的订单已纳入处理队列（kafka），id："+id);
        kafkaTemplate.send("testTopic",id);
    }
    @Override
    public String doMessage() {
   
        return null;
    }
}
```

​ 使用send方法发送消息，需要传入topic名称。

**步骤④**：使用消息监听器在服务器启动后，监听指定位置，当消息出现后，立即消费消息

```java
@Component
public class MessageListener {
   
    @KafkaListener(topics = "testTopic")
    public void onMessage(ConsumerRecord<String,String> record){
   
        System.out.println("已完成短信发送业务(kafka)，id："+record.value());
    }
}
```

​ 使用注解@KafkaListener定义当前方法监听Kafka中指定topic的消息，接收到的消息封装在对象ConsumerRecord中，获取数据从ConsumerRecord对象中获取即可。

**小结**

1. springboot整合Kafka使用KafkaTemplate对象作为客户端操作消息队列 
2. 操作Kafka需要配置Kafka服务器地址，默认端口9092 
3. 企业开发时通常使用监听器来处理消息队列中的消息，设置监听器使用注解@KafkaListener。接收消息保存在形参ConsumerRecord对象中

总结:

1.  消息  
2.  ActiveMQ  
3.  RabbitMQ  
4.  RocketMQ  
5.  Kafka 


监控的意义

-  监控服务状态是否宕机  
-  监控服务运行指标（内存、虚拟机、线程、请求等）  
-  监控日志  
-  管理服务（服务下线） 

监控的实施方式

-  显示监控信息的服务器：用于获取服务信息，并显示对应的信息  
-  运行的服务：启动时主动上报，告知监控服务器自己需要受到监控 


![img](https://img-blog.csdnimg.cn/img_convert/c092098bdc913123fd197536a082dd46.png)

小结:

1. 监控是一个非常重要的工作，是保障程序正常运行的基础手段 
2. 监控的过程通过一个监控程序进行，它汇总所有被监控的程序的信息集中统一展示 
3. 被监控程序需要主动上报自己被监控，同时要设置哪些指标被监控


Spring Boot Admin，这是一个开源社区项目，用于管理和监控SpringBoot应用程序。这个项目中包含有客户端和服务端两部分，而监控平台指的就是服务端。我们做的程序如果需要被监控，将我们做的程序制作成客户端，然后配置服务端地址后，服务端就可以通过HTTP请求的方式从客户端获取对应的信息，并通过UI界面展示对应信息。

​ 下面就来开发这套监控程序，先制作服务端，其实服务端可以理解为是一个web程序，收到一些信息后展示这些信息。

## 服务端开发

**步骤①**：导入springboot admin对应的starter，版本与当前使用的springboot版本保持一致，并将其配置成web工程

```java
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-server</artifactId>
    <version>2.5.4</version>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

​ 上述过程可以通过创建项目时使用勾选的形式完成。


![img](https://img-blog.csdnimg.cn/89cdd8948a5a4eac9821556a3191ff40.png)

**步骤②**：在引导类上添加注解@EnableAdminServer，声明当前应用启动后作为SpringBootAdmin的服务器使用

```java
@SpringBootApplication
@EnableAdminServer
public class Springboot25AdminServerApplication {
   
    public static void main(String[] args) {
   
        SpringApplication.run(Springboot25AdminServerApplication.class, args);
    }
}
```

​ 做到这里，这个服务器就开发好了，启动后就可以访问当前程序了，界面如下。


![img](https://img-blog.csdnimg.cn/aa5c11cb9f9048feab7ff23e3cdcbf15.png)

​ 由于目前没有启动任何被监控的程序，所以里面什么信息都没有。下面制作一个被监控的客户端程序。

## 客户端开发

​ 客户端程序开发其实和服务端开发思路基本相似，多了一些配置而已。

**步骤①**：导入springboot admin对应的starter，版本与当前使用的springboot版本保持一致，并将其配置成web工程

```java
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.5.4</version>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

​ 上述过程也可以通过创建项目时使用勾选的形式完成，不过一定要小心，端口配置成不一样的，否则会冲突。

**步骤②**：设置当前客户端将信息上传到哪个服务器上，通过yml文件配置

```java
spring:
  boot:
    admin:
      client:
        url: http://localhost:8080
```

​ 做到这里，这个客户端就可以启动了。启动后再次访问服务端程序，界面如下。


![img](https://img-blog.csdnimg.cn/8c4c14cdba584cd08fb60a2307581f2b.png)

​ 可以看到，当前监控了1个程序，点击进去查看详细信息。


![img](https://img-blog.csdnimg.cn/b0bf26da66ed43aa9e61c38ac84ebd18.png)

​ 由于当前没有设置开放哪些信息给监控服务器，所以目前看不到什么有效的信息。下面需要做两组配置就可以看到信息了。

1.  开放指定信息给服务器看  
2.  允许服务器以HTTP请求的方式获取对应的信息 配置如下： 

```java
server:
  port: 80
spring:
  boot:
    admin:
      client:
        url: http://localhost:8080
management:
  endpoint:
    health:
      show-details: always
  endpoints:
    web:
      exposure:
        include: "*"
```

​ 上述配置对于初学者来说比较容易混淆。简单解释一下，到下一节再做具体的讲解。springbootadmin的客户端默认开放了13组信息给服务器，但是这些信息除了一个之外，其他的信息都不让通过HTTP请求查看。所以你看到的信息基本上就没什么内容了，只能看到一个内容，就是下面的健康信息。


![img](https://img-blog.csdnimg.cn/15e94ca504504c95aa87e2c862a8ca4e.png)

​ 但是即便如此我们看到健康信息中也没什么内容，原因在于健康信息中有一些信息描述了你当前应用使用了什么技术等信息，如果无脑的对外暴露功能会有安全隐患。通过配置就可以开放所有的健康信息明细查看了。

```java
management:
  endpoint:
    health:
      show-details: always
```

​ 健康明细信息如下：


![img](https://img-blog.csdnimg.cn/a376b670a3c24723a429df08acd581c7.png)

​ 目前除了健康信息，其他信息都查阅不了。原因在于其他12种信息是默认不提供给服务器通过HTTP请求查阅的，所以需要开启查阅的内容项，使用*表示查阅全部。记得带引号。

```java
endpoints:
  web:
    exposure:
      include: "*"
```

​ 配置后再刷新服务器页面，就可以看到所有的信息了。


![img](https://img-blog.csdnimg.cn/1b1c062cf02c47debcbd32f095b3c68b.png)

​ 以上界面中展示的信息量就非常大了，包含了13组信息，有性能指标监控，加载的bean列表，加载的系统属性，日志的显示控制等等。

**配置多个客户端**

​ 可以通过配置客户端的方式在其他的springboot程序中添加客户端坐标，这样当前服务器就可以监控多个客户端程序了。每个客户端展示不同的监控信息。


![img](https://img-blog.csdnimg.cn/f8b2ea64c0c940df97423579033b8034.png)

​ 进入监控面板，如果你加载的应用具有功能，在监控面板中可以看到3组信息展示的与之前加载的空工程不一样。

- 类加载面板中可以查阅到开发者自定义的类，如左图



​ ![img](https://img-blog.csdnimg.cn/8f4942def3c64164afa85232b65b8aeb.png) ![img](https://img-blog.csdnimg.cn/732a1071253c40c98788c57c68517175.png)

- 映射中可以查阅到当前应用配置的所有请求



​ ![img](https://img-blog.csdnimg.cn/6b593447cd80436da5af6e672a4ea8e6.png) ![img](https://img-blog.csdnimg.cn/921dbaf0011143b7a633507c750b0209.png)

- 性能指标中可以查阅当前应用独有的请求路径统计数据



​ ![img](https://img-blog.csdnimg.cn/cde7fb13f4274ba08fcf0e34746cef17.png) ![img](https://img-blog.csdnimg.cn/6ff01778066e4086b455b7fb09b172f5.png)

**总结**

1. 开发监控服务端需要导入坐标，然后在引导类上添加注解@EnableAdminServer，并将其配置成web程序即可 
2. 开发被监控的客户端需要导入坐标，然后配置服务端服务器地址，并做开放指标的设定即可 
3. 在监控平台中可以查阅到各种各样被监控的指标，前提是客户端开放了被监控的指标


-  Actuator提供了SpringBoot生产就绪功能，通过端点的配置与访问，获取端点信息  
-  端点描述了一组监控信息，SpringBoot提供了多个内置端点，也可以根据需要自定义端点信息  
-  访问当前应用所有端点信息：/actuator  
-  访问端点详细信息：/actuator**/** 端点名称 

通过查阅监控中的映射指标，可以看到当前系统中可以运行的所有请求路径，其中大部分路径以/actuator开头


![img](https://img-blog.csdnimg.cn/1d3105c4971f4660a182bfd6cf5db5c6.png)

​ 首先这些请求路径不是开发者自己编写的，其次这个路径代表什么含义呢？既然这个路径可以访问，就可以通过浏览器发送该请求看看究竟可以得到什么信息。


![img](https://img-blog.csdnimg.cn/img_convert/a3a6e8ee08fa8ec2b8521b62afd04712.png)

​ 通过发送请求，可以得到一组json信息，如下

```java
{
   
    "_links": {
   
        "self": {
   
            "href": "http://localhost:81/actuator",
            "templated": false
        },
        "beans": {
   
            "href": "http://localhost:81/actuator/beans",
            "templated": false
        },
        "caches-cache": {
   
            "href": "http://localhost:81/actuator/caches/{cache}",
            "templated": true
        },
        "caches": {
   
            "href": "http://localhost:81/actuator/caches",
            "templated": false
        },
        "health": {
   
            "href": "http://localhost:81/actuator/health",
            "templated": false
        },
        "health-path": {
   
            "href": "http://localhost:81/actuator/health/{*path}",
            "templated": true
        },
        "info": {
   
            "href": "http://localhost:81/actuator/info",
            "templated": false
        },
        "conditions": {
   
            "href": "http://localhost:81/actuator/conditions",
            "templated": false
        },
        "shutdown": {
   
            "href": "http://localhost:81/actuator/shutdown",
            "templated": false
        },
        "configprops": {
   
            "href": "http://localhost:81/actuator/configprops",
            "templated": false
        },
        "configprops-prefix": {
   
            "href": "http://localhost:81/actuator/configprops/{prefix}",
            "templated": true
        },
        "env": {
   
            "href": "http://localhost:81/actuator/env",
            "templated": false
        },
        "env-toMatch": {
   
            "href": "http://localhost:81/actuator/env/{toMatch}",
            "templated": true
        },
        "loggers": {
   
            "href": "http://localhost:81/actuator/loggers",
            "templated": false
        },
        "loggers-name": {
   
            "href": "http://localhost:81/actuator/loggers/{name}",
            "templated": true
        },
        "heapdump": {
   
            "href": "http://localhost:81/actuator/heapdump",
            "templated": false
        },
        "threaddump": {
   
            "href": "http://localhost:81/actuator/threaddump",
            "templated": false
        },
        "metrics-requiredMetricName": {
   
            "href": "http://localhost:81/actuator/metrics/{requiredMetricName}",
            "templated": true
        },
        "metrics": {
   
            "href": "http://localhost:81/actuator/metrics",
            "templated": false
        },
        "scheduledtasks": {
   
            "href": "http://localhost:81/actuator/scheduledtasks",
            "templated": false
        },
        "mappings": {
   
            "href": "http://localhost:81/actuator/mappings",
            "templated": false
        }
    }
}
```

​ 其中每一组数据都有一个请求路径，而在这里请求路径中有之前看到过的health，发送此请求又得到了一组信息

```java
{
    "status": "UP",
    "components": {
        "diskSpace": {
            "status": "UP",
            "details": {
                "total": 297042808832,
                "free": 72284409856,
                "threshold": 10485760,
                "exists": true
            }
        },
        "ping": {
            "status": "UP"
        }
    }
}
```

​ 当前信息与监控面板中的数据存在着对应关系


![img](https://img-blog.csdnimg.cn/3f93e9ce7b7e418bacd84ea8119576db.png)

​ 原来监控中显示的信息实际上是通过发送请求后得到json数据，然后展示出来。按照上述操作，可以发送更多的以/actuator开头的链接地址，获取更多的数据，这些数据汇总到一起组成了监控平台显示的所有数据。

​ 到这里我们得到了一个核心信息，监控平台中显示的信息实际上是通过对被监控的应用发送请求得到的。那这些请求谁开发的呢？打开被监控应用的pom文件，其中导入了springboot admin的对应的client，在这个资源中导入了一个名称叫做actuator的包。被监控的应用之所以可以对外提供上述请求路径，就是因为添加了这个包。


![img](https://img-blog.csdnimg.cn/img_convert/1622b6e2b32703a30bb6655229420539.png)

​ 这个actuator是什么呢？这就是本节要讲的核心内容，监控的端点。

​ Actuator，可以称为端点，描述了一组监控信息，SpringBootAdmin提供了多个内置端点，通过访问端点就可以获取对应的监控信息，也可以根据需要自定义端点信息。通过发送请求路劲**/actuator**可以访问应用所有端点信息，如果端点中还有明细信息可以发送请求**/actuator/端点名称**来获取详细信息。以下列出了所有端点信息说明：


​ 上述端点每一项代表被监控的指标，如果对外开放则监控平台可以查询到对应的端点信息，如果未开放则无法查询对应的端点信息。通过配置可以设置端点是否对外开放功能。使用enable属性控制端点是否对外开放。其中health端点为默认端点，不能关闭。

```java
management:
  endpoint:
    health:						# 端点名称
      show-details: always
    info:						# 端点名称
      enabled: true				# 是否开放
```

​ 为了方便开发者快速配置端点，springboot admin设置了13个较为常用的端点作为默认开放的端点，如果需要控制默认开放的端点的开放状态，可以通过配置设置，如下：

```java
management:
  endpoints:
    enabled-by-default: true	# 是否开启默认端点，默认值true
```

​ 上述端点开启后，就可以通过端点对应的路径查看对应的信息了。但是此时还不能通过HTTP请求查询此信息，还需要开启通过HTTP请求查询的端点名称，使用“*”可以简化配置成开放所有端点的WEB端HTTP请求权限。

```java
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

​ 整体上来说，对于端点的配置有两组信息，一组是endpoints开头的，对所有端点进行配置，一组是endpoint开头的，对具体端点进行配置。

```java
management:
  endpoint:		# 具体端点的配置
    health:
      show-details: always
    info:
      enabled: true
  endpoints:	# 全部端点的配置
    web:
      exposure:
        include: "*"
    enabled-by-default: true
```

**总结**

1.  被监控客户端通过添加actuator的坐标可以对外提供被访问的端点功能  
2.  端点功能的开放与关闭可以通过配置进行控制  
3.  web端默认无法获取所有端点信息，通过配置开放端点功能 


info端点描述了当前应用的基本信息，可以通过两种形式快速配置info端点的信息

-  配置形式 在yml文件中通过设置info节点的信息就可以快速配置端点信息 info:
  appName: @project.artifactId@
  version: @project.version@
  company: 传智教育
  author: itheima 配置完毕后，对应信息显示在监控平台上  也可以通过请求端点信息路径获取对应json信息 


![img](https://img-blog.csdnimg.cn/c3d6e2861f57415dbd376a64bd68c5d3.png)

-  编程形式 通过配置的形式只能添加固定的数据，如果需要动态数据还可以通过配置bean的方式为info端点添加信息，此信息与配置信息共存 <pre><code class="prism language-java"><span class="token annotation punctuation">@Component</span>
<span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">InfoConfig</span> <span class="token keyword">implements</span> <span class="token class-name">InfoContributor</span> <span class="token punctuation">{
     
    <!-- --></span>
    <span class="token annotation punctuation">@Override</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">contribute</span><span class="token punctuation">(</span><span class="token class-name">Info<span class="token punctuation">.</span>Builder</span> builder<span class="token punctuation">)</span> <span class="token punctuation">{
     
    <!-- --></span>
        <span class="token comment">//添加单个信息</span>
        builder<span class="token punctuation">.</span><span class="token function">withDetail</span><span class="token punctuation">(</span><span class="token string">"runTime"</span><span class="token punctuation">,</span> <span class="token keyword">new</span> <span class="token class-name">SimpleDateFormat</span><span class="token punctuation">(</span><span class="token string">"yyyy年MM月dd日 HH:mm:ss"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">format</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token class-name">Map</span> infoMap <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">HashMap</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        infoMap<span class="token punctuation">.</span><span class="token function">put</span><span class="token punctuation">(</span><span class="token string">"buildTime"</span><span class="token punctuation">,</span> <span class="token string">"2006"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        builder<span class="token punctuation">.</span><span class="token function">withDetails</span><span class="token punctuation">(</span>infoMap<span class="token punctuation">)</span><span class="token punctuation">;</span>      <span class="token comment">//添加一组信息</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre> 


​ health端点描述当前应用的运行健康指标，即应用的运行是否成功。通过编程的形式可以扩展指标信息。

```java
@Component
public class HealthConfig extends AbstractHealthIndicator {
   
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
   
        boolean condition = true;
        if(condition) {
   
            builder.status(Status.UP);					//设置运行状态为启动状态
            builder.withDetail("runTime", System.currentTimeMillis());
            Map infoMap = new HashMap();
            infoMap.put("buildTime", "2006");
            builder.withDetails(infoMap);
        }else{
   
            builder.status(Status.OUT_OF_SERVICE);		//设置运行状态为不在服务状态
            builder.withDetail("上线了吗？","你做梦");
        }
    }
}
```

​ 当任意一个组件状态不为UP时，整体应用对外服务状态为非UP状态。


![img](https://img-blog.csdnimg.cn/e603a4cb75734deb9a6d2a45191711e9.png)


​ metrics端点描述了性能指标，除了系统自带的监控性能指标，还可以自定义性能指标。

```java
@Service
public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
   
    @Autowired
    private BookDao bookDao;

    private Counter counter;

    public BookServiceImpl(MeterRegistry meterRegistry){
   
        counter = meterRegistry.counter("用户付费操作次数：");
    }

    @Override
    public boolean delete(Integer id) {
   
        //每次执行删除业务等同于执行了付费业务
        counter.increment();
        return bookDao.deleteById(id) > 0;
    }
}
```

​ 在性能指标中就出现了自定义的性能指标监控项


![img](https://img-blog.csdnimg.cn/bbefd51e1f3747619361f3b6bdfcf499.png)


可以根据业务需要自定义端点，方便业务监控

```java
@Component
@Endpoint(id="pay",enableByDefault = true)
public class PayEndpoint {
   
    @ReadOperation
    public Object getPay(){
   
        Map payMap = new HashMap();
        payMap.put("level 1","300");
        payMap.put("level 2","291");
        payMap.put("level 3","666");
        return payMap;
    }
}
```

​ 由于此端点数据spirng boot admin无法预知该如何展示，所以通过界面无法看到此数据，通过HTTP请求路径可以获取到当前端点的信息，但是需要先开启当前端点对外功能，或者设置当前端点为默认开发的端点。


![img](https://img-blog.csdnimg.cn/a57475c3bcee43d0992645fc73da74bc.png)

**小结**

1. 端点的指标可以自定义，但是每种不同的指标根据其功能不同，自定义方式不同 
2. info端点通过配置和编程的方式都可以添加端点指标 
3. health端点通过编程的方式添加端点指标，需要注意要为对应指标添加启动状态的逻辑设定 
4. metrics指标通过在业务中添加监控操作设置指标 
5. 可以自定义端点添加更多的指标

**总结:**

1.  监控的意义  
2.  可视化监控平台————Spring Boot Admin  
3.  监控原理————Actuator  
4.  自定义监控指标 
 <ul> 
  4.  系统端点添加监控指标  
  4.  自定义端点  
 </ul> 

