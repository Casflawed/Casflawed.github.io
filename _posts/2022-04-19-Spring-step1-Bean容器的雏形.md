---
title: Spring-step1-Bean容器的雏形
date: 2022-04-19 +/-TTTT
categories: [框架, Spring]
tags: [设计模式]     # TAG names should always be lowercase
---

# Spring 容器是什么？
作为一名 Java 工程师，在工作中少不了接触 Spring，我对它最大的印象就是：只需要在类上面标注几个注解，像 @Component，@Service，@Controller 就再也不用去操心这些 Bean 对象的创建，使用的时候它们就已经创建好了。所以在我眼里 Spring 容器就是一个大的对象工厂。实际上：

Spring 包含并管理**应用对象的配置和生命周期**，你可以配置你的每个 Bean 对象是如何被创建的，这些 Bean 在创建时可以是一个单独的实例 or 每次都生成一个新的实例，以及它们是如何相互构建和使用的。

在 Spring 容器中，被管理的 Bean 对象并不是直接存在容器中，它会被拆解保存到 Bean 的定义中，然后由 Spring 容器统一进行装配，最终我们就可以使用到实例化后的对象了。

# 目标
定义一个简单的 Spring 容器，用于**定义、存放和获取 Bean 对象**。


在实际Spring中，Spring IoC容器做的主要工作分为

- Bean定义
- Bean注册，所谓的注册就像DriveManger对数据库驱动进行注册的那样，实际就是将Bean或者与Bean直接关联的信息用容器进行保存，待要使用时就用索引（可以是名称、id、或其他任何能够唯一对应Bean的事务）取出
- Bean对象创建
- 依赖注入

## 我们为什么会需要Spring Ioc

1.在了解到Spring Ioc的功能时，我又会有这样的问题：问题1，为什么Spring Ioc要按照Bean定义、Bean注册、Bean对象创建、依赖注入的流程去管理Bean；问题2，我们最初选择使用Spring IoC容器是为了什么？

首先解答问题2：

- 举一个古老的例子

```java
public class UserService{
  private UserDao userDao = new UserOracleDao();
  // private UserDao userDao = new UserMysqlDao();
  // private UserDao userDao = new UserSqlServerDao();
  .....
}
```
我们与数据库交互的接口会随着数据库的改变而改变，这导致每次数据库发生变化，我们就需要修改代码，但当程序中有大量这样的代码，修改的成本就会很大；因而除了设置接口，我们还应该让客户能够主导我们的程序，也就是说要使用UserDao的哪一个实现由客户决定，于是：

```java
public class UserFactory {
  private static UserDao userDao;

  static {
    InputStream inputStream = UserFactory.class.getClassLoader().getResourceAsStream("application.properties");
    Properties prop = new Properties();
    try {
      prop.load(inputStream);
    } catch (IOException e) {
      e.printStackTrace();
    }
    String userDaoClassName = prop.getProperty("userDao");
    try {
      Class<?> clazz = Class.forName(userDaoClassName);
      userDao = (UserDao)clazz.newInstance();
    } catch (Exception e) {
      System.out.println("类不存在");
      e.printStackTrace();
    }
  }

  public static UserDao getUserDao() {
    return userDao;
  }
}
```

这样通过读取外界配置文件，就能实现要使用哪一个UserDao由用户自己决定，其实SpringIoc就相当于一个大大的工厂类，它帮助我们创建对象，注入对象，将对对象的控制权完全掌握在自己手里；避免了业务代码和创建对象耦合

2.对于第二个问题，首先为什么要对Bean定义

Bean定义，即对Bean重新定义，由于容器内部管理的Bean可能是不同类型的，同时我们还会对Bean做各种初始化，因此重新定义为统一的类是合理的

然后是Bean注册，将每个Bean打好标记，并存入容器

前两步做好后，为什么使用这些对象我们就的对其初始化，同时在需要使用Bean对象的地方注入

## step1程序类图

![step1程序类图](/blog/202204212141036.png "step1程序类图")

## 缺陷

1.在这一阶段最明显的问题就是：我们需要自己创建对象并注册到容器中，那么如何让容器能够自己创建Bean，定义Bean、注册Bean呢？

答案是反射，我们都知道获取Class对象有三种方式，例如：String.class，str.getClass()，Class.forName();显然最后一种方式是目前我们用的上的，也就是说，我们想要实例化哪个Bean，只要获取它的全类名就可以了，那么怎么获取到全类名呢？是配置文件、注解、还是说有什么其他的办法？下一章节细讲！