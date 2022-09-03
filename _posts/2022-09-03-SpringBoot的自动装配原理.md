---
title: SpringBoot的自动装配原理
date: 2022-09-03 +/-TTTT
categories: [框架, SpringBoot]
tags: [注解]     # TAG names should always be lowercase
---

# SpringBoot的自动装配解决了什么问题

减少了Spring的xml等繁琐的配置

# 怎么利用自动装配便利
通过注解和一些简单的配置，就能直接使用外部依赖的某些功能，或Spring内部的某些功能

# SpringBoot的自动装配是如何实现的
@SpringBootApplication ==> @EnableAutoConfiguration

首先自动装配是从注解@EnableAutoConfiguration开始

## @EnableAutoConfiguration
@EnableAutoConfiguration是一个合成注解，它的里面包含两个重要的注解：

1. @AutoConfigurationPackage，用来自动导入我们的项目根目录下，添加了@Configuration、@Component等注解的类到Spring IoC容器的
2. @Import({AutoConfigurationImportSelector.class})，用来导入在spring-boot-autoconfigure包下，META-INF/spring.factories中指定的自动配置类

## 条件装配，按需配置
1. 每个自动配置类会按照条件进行生效，并且默认绑定配置文件指定的值，这个配置文件就是SpringBoot的全局配置文件application.yml
2. 常见的按条件配置，比如，某个Bean是否存在，如果存在就不生效，或者某个类是否存在，如果不存在就不生效
3. 生效的配置类最终会通过@EnableAutoConfiguration中的Import，将配置类中定义的Bean全部注入到IoC容器中

## 定制化配置
两种方式：

1. 用户直接自己在自定义配置类中通过@Bean替换底层的组件
2. 用户通过修过SpringBoot全局配置文件中的值

# 如何实现一个 Starter
1. 新疆工程，artifactId应该符合规范： XXXX-spring-boot-starter
2. 引入SpringBoot Starter基础库
3. 创建XXXXAutoConfiguration自动配置类，用于往容器中注入Bean
4. 在工程的 resources 包下创建META-INF/spring.factories文件，里面的一行为自动配置类全限定名
5. 最后新建其他工程，引入XXXX-spring-boot-starter

# 总结
SpringBoot 通过@EnableAutoConfiguration开启自动装配，通过 SpringFactoriesLoader 最终加载META-INF/spring.factories中的自动配置类实现自动装配，自动配置类其实就是通过@Conditional按需加载的配置类