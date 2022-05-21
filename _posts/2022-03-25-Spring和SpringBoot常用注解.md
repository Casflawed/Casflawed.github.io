---
title: Spring和SpringBoot常用注解
date: 2022-03-25 +/-TTTT
categories: [框架, Spring]
tags: [注解]     # TAG names should always be lowercase
---

## 使用@Value("${property}")读取简单的配置信息
```java
@Value("${name}")
String name;
```

## JPA相关注解
### 使用@Table标注表名

```java
@Entity
@Table("name = person")
public class Person{
    private String name;
    private Integer age;
    private Boolean gender;
}
```

表名一致性，如大小写，下划线请看：

[JPA映射数据库mysql表名,字段名大小写转化,下划线分割.](https://blog.csdn.net/kaige8312/article/details/103372084)

[JPA中自动使用@Table(name = "userTab")后自动将表名、列名添加了下划线的问题](https://www.cnblogs.com/songxingzhu/p/9835683.html)