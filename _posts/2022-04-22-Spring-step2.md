---
title: Spring-step2
date: 2022-04-22 +/-TTTT
categories: [Spring,造轮子]
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

在step1中我们总结过Spring Ioc容器的主要工作，包括Bean定义、Bean注册、Bean初始化、依赖注入；而现在这些功能都被耦合在同一个BeanFactory类中，这样不便于后期扩展，为了提供更好的可扩展性，我们应该将其分解，一个类做一件事