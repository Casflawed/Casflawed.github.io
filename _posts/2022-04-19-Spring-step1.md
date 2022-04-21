---
title: Spring-step1
date: 2022-04-19 +/-TTTT
categories: [Spring,造轮子]
tags: [设计模式]     # TAG names should always be lowercase
---

## Spring IoC的主要功能

1.在实际Spring中，Spring IoC容器做的主要工作分为

- Bean定义
- Bean注册，所谓的注册就像DriveManger对数据库驱动进行注册的那样，实际就是将Bean或者与Bean直接关联的信息用容器进行保存，待要使用时就用索引（可以是名称、id、或其他任何能够唯一对应Bean的事务）取出
- Bean初始化
- 依赖注入

## 我们为什么会需要Spring Ioc

1.在了解到Spring Ioc的功能时，我又会有这样的问题：问题1，为什么Spring Ioc要按照Bean定义、Bean注册、Bean初始化、依赖注入的流程去管理Bean；问题2，我们最初选择使用Spring IoC容器是为了什么？

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