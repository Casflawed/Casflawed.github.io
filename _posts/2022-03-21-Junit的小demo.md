---
title: Junit的小demo
date: 2022-03-21 +/-TTTT
categories: [Junit, Demo]
tags: [反射, 注解]     # TAG names should always be lowercase
---

# 目标
- 模拟Junit中@Test、@Before、@After的实现方式
- 练习自定注解实现
- 探索注解的底层实现

# 方法
1.定义自定义注解@MyTest、@MyBefore、@MyAfter
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyTest {
}
```
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyBefore {
}
```
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAfter {
}
```

2.使用注解
```java
public class MainClass {

  @MyTest
  public void testSave(){
    System.out.println("保存成功");
  }

  @MyTest
  public void testUpdate(){
    System.out.println("更新成功");
  }

  @MyBefore
  public void init(){
    System.out.println("初始化");
  }

  @MyAfter
  public void destroy(){
    System.out.println("销毁");
  }
}
```

3.读取并执行测试方法
```java
public class TestClass {
  public static void main(String[] args) throws IllegalAccessException, InstantiationException, InvocationTargetException {
    // 1.获取测试类的Class对象和实例对象
    Class<MainClass> clazz = MainClass.class;
    MainClass instance = clazz.newInstance();

    // 2.获取带有注解的方法
    Method[] methods = clazz.getMethods();

    // 3.并用map存储
    Map<String, List<Method>> annotationListMap = new HashMap<>(20);

    // 4.遍历方法
    for (Method method : methods) {

      // 5.获取方法上的注解信息
      Annotation[] methodAnnotations = method.getAnnotations();
      // 6.遍历注解
      for (Annotation annotation : methodAnnotations){

        // 7.获取带了这种注解的方法数组，注意：由于注解底层有jdk动态代理实现接口的实现，所以getClass是获取不到原类型的类对象的
        // 但Annotation提供了annotationType()方法用于获取注解的类型对象
        List<Method> methodList = annotationListMap.get(annotation.annotationType().getName());

        // 8.如果数组不存在，新创建
        if (methodList == null){
          List<Method> list = new ArrayList<>();
          // 并将方法对象存入数组
          list.add(method);
          // 将注解：方法数组的键值对存入map
          annotationListMap.put(annotation.annotationType().getName(), list);
        }else {
          // 9.如果存在，直接在方法数组中添加该方法
          methodList.add(method);
        }
      }

    }

    // 10.执行方法
    List<Method> myBeforeList = annotationListMap.get(MyBefore.class.getName());
    List<Method> myTestList = annotationListMap.get(MyTest.class.getName());
    List<Method> myAfterList = annotationListMap.get(MyAfter.class.getName());

    // 11.按流程执行方法
    for (Method method1 : myTestList){
      // 首先执行MyBefore标注的方法
      for (Method method0 : myBeforeList){
        method0.invoke(instance, (Object[]) null);
      }
      // 再执行MyTest标注的方法
      method1.invoke(instance, (Object[]) null);
      // 最后执行带MyAfter标注的方法
      for (Method method2 : myAfterList){
        method2.invoke(instance, (Object[]) null);
      }
    }
  }
}
```

# 结论与发现
1.注解本质上是接口，而注解内部属性会在底层被解析为同名的抽象方法

2.Method对象通过getAnnotations()获取的注解对象是jdk代理对象，因为jdk底层通过动态代理对注解做了实现，所以通过getClass(),我们获取不到Class<? extends Annotation>的类对象，而是Proxy类对象；但是Annotation内部定义了一个annotationType()的方法，该方法可以帮助我们获取到注解的Class对象