---
title: Spring-step2-掌握Bean对象自动创建的容器
date: 2022-04-22 +/-TTTT
categories: [框架, Spring]
tags: [设计模式,系统设计]     # TAG names should always be lowercase
---

## 回顾step1

step1我们实现了一个非常单纯的Bean容器---BeanFactory，里面提供方法registerBeanDefinition()，getBean()，并且维护一个ConcurrentHashMap的实例，用于存储Bean对象

![step1程序类图](/blog/202204212141036.png "step1程序类图")

这个容器提供的Bean的注册、获取功能，但对用户而言，用户却需要自行创建、自行注册、同时自行提取；**这与我们最初的设想：将创建对象的控制权从用户手中夺回**，因此我们应该让容器自行创建对象才是，那么如何实现呢？

![当前用户和容器的关系](/blog/202204221117021.png "当前用户和容器的关系")

## 掌控对象控制权

我们知道将创建对象和业务功能解耦，可以使用工厂设计模式或者抽象工厂，但是由于对象的类型不确定，我们不可能在未知对象类型的情况下new出对象，所以说用户必须告诉我们的工厂我们该实例化哪个类型？用户不能自己创建，又必须告诉工厂创建什么，大家想到了什么？对，就是反射！通过反射获取Class对象就可以创建实例对象，用户只要告诉我么类型的全类名就可以了；所以现在用户和容器的关系应该是下面这样的：

![新的关系](/blog/202204221129943.png "新的关系")

而原来容器维护的是实例对象，现在维护的应该是Class对象，这样容器就能真正掌握对象的创建权力，这样什么时候需要对象，容器就可以为其创建，或者单例对象

所以我们的BeanDefinition看起来应该是这样的：

```java
public class BeanDefinition{
    private Class beanClass;

    public BeanDefinition(){}

    public BeanDefinition(Class beanClass){
        this.beanClass = beanClass;
    }

    public void setBeanClass(Class beanClass){
        this.beanClass = beanClass;
    }

    public Class getBeanClass(Class beanClass){
        return this.beanClass
    }
}
```

## 拆分容器

在step1中我们总结过Spring Ioc容器的主要工作，包括Bean定义、Bean注册、Bean初始化、依赖注入；而现在这些功能都被耦合在同一个BeanFactory类中，这样不便于后期扩展，为了提供更好的可扩展性，我们应该将其分解，一个类做一件事；经分析我们发现，容器的真正起作用时是当我们需要从中获取Bean对象的时候，那么容器需要能够自己创建Bean对象，并且暂存起来，那么我们看下BeanFactory的继承链是如何的：

![BeanFactory的继承链](/blog/202204251710776.png "BeanFactory的继承链")

然后我们在以getBean为目标，看看它是如何执行的：
![getBean](/blog/202204271635434.png "getBean")

可见因为getBean的需要，诞生了getBeanDefinition和createBean方法，并且我们发现这次的容器增加了单例对象缓存，使得不是每次getBean都重新创建对象，AbstractBeanFactory确定了getBean()的执行框架，使得该容器会默认返回对象的单例，同样单例缓存功能也实现在另一个类DefaultSingletonRegistry中，这样每个功能之间保持独立，类与类之间实现解耦，整个框架更容易扩展

## 完整的类图
![完整的类图](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202204271715202.png "完整的类图")

## 为什么无论是BeanDefinition容器还是singletonObject容器都要用final修饰呢？
因为这样让属性更安全，因为被final修饰后，容器就很难被替换，也就是说属性只能初始化一次；

## 当前容器存在的问题
先看一段代码，这段代码测试单例缓存是否成功：

```java
public class DefaultSingletonBeanRegistryTest {

  @Test
  public void testGetSingleton() {
    // 我的bean容器
    DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();

    // 创建我的BeanDefinition
    BeanDefinition beanDefinition = new BeanDefinition(UserService.class);

    //BeanDefinition注册进容器
    beanFactory.registerBeanDefinition("userService", beanDefinition);

    //获取Bean对象
    UserService userService = (UserService)beanFactory.getBean("userService");

    //再次获取Bean对象
    Object anotherUserService = beanFactory.getBean("userService");

    // 判断两者是否为同一对象
    System.out.println(userService == anotherUserService);
  }
}
```

问题：

1.很明显，相较于step1我们的容器确实能够自己创建对象，并且还能进行单例缓存，但是对于用户来说，依然需要手动注册Definition，也就是说还是要由程序主动管理对象的生成
2.每次取出Bean需要用户显式进行强转，有没有如泛型那样容器帮我们自动强转的方法
3.容器创建Bean，**使用反射的newInstance()方法，而它的底层实际上调用的是无参构造函数**，所以如果面对这样的一个类：

```java
public class UserService {
  private String name;

  public UserService(String name) {
    this.name = name;
  }

  public void queryUserInfo(){
    System.out.println("查询用户信息");
  }
}
```

就会报错，因为它压根就没有无参构造函数

那么如何解决这些问题呢？Spring-step3继续