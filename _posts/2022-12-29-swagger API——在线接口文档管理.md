---
title: swagger API——在线接口文档管理
date: 2022-12-29 +/-TTTT
categories: [项目, 商场停车]
tags: []     # TAG names should always be lowercase
---

# 如何配置
## 引入依赖
```xml
<dependency>
    <groupId>com.spring4all</groupId>
    <artifactId>swagger-spring-boot-starter</artifactId>
    <version>1.9.0.RELEASE</version>
</dependency>
```

## application 配置
```yml
swagger:
  enabled: true
  base-package: com.flameking.parking.member
  base-path: /**
  authorization:
    key-name: Authorization
  docket:
    v1:
      title: 会员服务
#      description: 会员服务Api
      base-package: com.flameking.parking.member
      version: 1.0
```

## 启动类开启注解
```java
@EnableSwagger2Doc
public class ParkingMemberApplication {
    public static void main(String[] args) {
        SpringApplication.run(ParkingMemberApplication.class, args);
    }
}
```