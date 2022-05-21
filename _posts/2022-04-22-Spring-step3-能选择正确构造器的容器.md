---
title: Spring-step3-能选择正确构造器的容器
date: 2022-04-22 +/-TTTT
categories: [框架, Spring]
tags: [设计模式,CGLIB]     # TAG names should always be lowercase
---

## 目标
由于上一步骤我们将对象创建的方式限制在用无参构造函数创建，因为Class.newInstance()，本质上是调用无参构造函数，那么对于没有无参构造的类就会报错，所以step3就是为了实现：

**使得没有无参构造器的类也能正常创建**

## 如何让容器具备选择正确构造器的能力
为了让对象能够正常创建，而非默认由无参构造器创建，因此需要选择正确的构造器器；如何选择正确构造器？

对于重载的构造器，我们根据参数类型和参数顺序就能判断，那么参数哪里来呢？

对于容器来说，它可以自主创建对象，但是它毕竟也不知道该使用哪个构造器，或者说究竟使用哪个构造器应该由用户创建，我们只需把判断构造器的逻辑封装进容器即可；**我们知道容器对外提供了提取对象的方法：getBean()，我们可以由它传入参数**

## 将构造器选择逻辑封装进容器
### JDK反射获取
```java
public class JDKInitializeBeanStrategy implements InitializeBeanStrategy{
  @Override
  public Object initializeBean(BeanDefinition beanDefinition, Object[] args) throws IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchMethodException {
    // 1.获取Class对象
    Class beanClass = beanDefinition.getBeanClass();
    // 2.获取构造器组
    Constructor[] constructors = beanClass.getDeclaredConstructors();
    // 3.遍历构造器组，选择合适的构造器
    if (args != null) {
      for (Constructor constructor : constructors) {
        // 4.获取方法参数列表
        Class<?>[] parameterTypes = constructor.getParameterTypes();
        // 5.比较参数长度
        if (parameterTypes.length == args.length) {
          int i;
          // 6.比较参数类型是否相同
          for (i = 0; i < parameterTypes.length; i++) {
            if (parameterTypes[i] != args[i].getClass()) {
              break;
            }
          }
          // 7.如果参数长度相同，类型相同，说明构造器匹配
          if (i == parameterTypes.length) {
            try {
              // 传入参数，创建bean对象，并返回
              return constructor.newInstance(args);
            } catch (InstantiationException | IllegalAccessException | InvocationTargetException e) {
              e.printStackTrace();
            }
          }
        }
      }
    }
    // 8.args为null
    Constructor constructor = null;
    // 9.获取无参构造函数
    constructor = beanClass.getDeclaredConstructor();
    // 10.返回bean对象
    return constructor.newInstance(null);
  }
```

### 抽取构造器选择逻辑
```java
protected Object createBeanInstance(BeanDefinition beanDefinition, Object... args) {
    // 抽取构造器选择逻辑
    Constructor constructor = null;

    // 1.获取Class对象
    Class beanClass = beanDefinition.getBeanClass();

    if (args == null) {
      try {
        constructor = beanClass.getDeclaredConstructor();
      } catch (NoSuchMethodException e) {
        e.printStackTrace();
      }
    } else {
      // 2.获取构造器组
      Constructor[] constructors = beanClass.getDeclaredConstructors();

      // 3.遍历构造器组，选择合适的构造器
      for (Constructor cons : constructors) {

        // 4.获取方法参数列表
        Class<?>[] parameterTypes = cons.getParameterTypes();

        // 5.比较参数长度
        if (parameterTypes.length == args.length) {
          int i;

          // 6.比较参数类型是否相同
          for (i = 0; i < parameterTypes.length; i++) {
            if (parameterTypes[i] != args[i].getClass()) {
              break;
            }
          }

          // 7.如果参数长度相同，类型相同，说明构造器匹配
          if (i == parameterTypes.length) {
            constructor = cons;
          }
        }
      }
    }

    return initializeBeanStrategy.initializeBean(constructor, beanDefinition, args);

  }
```

### CGLIB动态创建对象（不熟）
```java
public class CglibInitializeBeanStrategy implements InitializeBeanStrategy{
  @Override
  public Object initializeBean(Constructor constructor, BeanDefinition beanDefinition, Object[] args) {
    Enhancer enhancer = new Enhancer();
    enhancer.setSuperclass(beanDefinition.getBeanClass());
    enhancer.setCallback(new NoOp() {
      @Override
      public int hashCode() {
        return super.hashCode();
      }
    });
    if (constructor.getParameterTypes().length == 0){
      return enhancer.create();
    }
    return enhancer.create(constructor.getParameterTypes(),args);
  }
}
```

## 总结：步骤流程图
![流程图](/blog/202204301936841.png "流程图")

## 扩展
通过一步步优化扩展，我们的spring容器已经具备了自主创建对象的能力，但是相比正统的Spring容器，我们的容器还无法对对象属性进行赋值，那么下一步就让我们解决对象属性注入的问题吧