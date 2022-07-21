---
title: 在Spring和SpringBoot中优雅的进行参数校验
date: 2022-07-21 +/-TTTT
categories: [框架, SpringBoot]
tags: []     # TAG names should always be lowercase
---

# 前言
数据的校验的重要性就不用说了，即使在前端对数据进行校验的情况下，我们还是要对传入后端的数据再进行一遍校验，避免用户绕过浏览器直接通过一些 HTTP 工具直接向后端请求一些违法数据。

最普通的做法就像下面这样。我们通过 `if/else` 语句对请求的每一个参数一一校验。

```java
@RestController
@RequestMapping("/api/person")
public class PersonController {

    @PostMapping
    public ResponseEntity<PersonRequest> save(@RequestBody PersonRequest personRequest) {
        if (personRequest.getClassId() == null
                || personRequest.getName() == null
                || !Pattern.matches("(^Man$|^Woman$|^UGM$)", personRequest.getSex())) {

        }
        return ResponseEntity.ok().body(personRequest);
    }
}
```

这样的代码，小伙伴们在日常开发中一定不少见，很多开源项目都是这样对请求入参做校验的。

但是，不太建议这样来写，这样的代码明显违背了 **单一职责原则**。大量的非业务代码混杂在业务代码中，非常难以维护，还会导致业务层代码冗杂！

实际上，我们是可以通过一些简单的手段对上面的代码进行改进的！这也是本文主要要介绍的内容！

**注意：本文主要讲解基于Sping Boot的注解校验，Spring Boot版本依赖如下：**

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.1</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
```


# 添加相关依赖

基于 Spring Boot 的话，只需要给项目添加上下面这些依赖：

```xml
<dependencies>
    <!--参数校验依赖-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>

    <!--测试依赖-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <version>2.2.4.RELEASE</version>
        <scope>test</scope>
    </dependency>

    <!--Spring Web依赖-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!--lombok工具-->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

在Spring Boot 2.3 1 之前，`spring-boot-starter-validation` 包括在了 `spring-boot-starter-web` 中，但如果你使用的Spring Boot版本大于2.3.1，比如我当前使用的是2.7.1，那么就必须手动添加依赖`spring-boot-starter-validation`

# 验证 Controller 的输入

## 验证请求体

验证请求体即是验证被 `@RequestBody` 注解标记的方法参数。

我们在需要验证的参数上加上了`@Valid`注解，如果验证失败，它将抛出`MethodArgumentNotValidException`。默认情况下，Spring 会将此异常转换为 HTTP Status 400（错误请求）。

**`PersonController`**

```java
@RestController
@RequestMapping("/api/person")
public class PersonController {

    @PostMapping
    public ResponseEntity<PersonRequest> save(@RequestBody @Valid PersonRequest personRequest) {
        return ResponseEntity.ok().body(personRequest);
    }
}
```

**注意：这里开启Spring数据校验使用@Validated也可以**

**`PersonRequest`**

我们使用校验注解对请求的参数进行校验！

```java
@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class PersonRequest {

    @NotNull(message = "classId 不能为空")
    private String classId;

    @Size(max = 33)
    @NotNull(message = "name 不能为空")
    private String name;

    @Pattern(regexp = "(^Man$|^Woman$|^UGM$)", message = "sex 值不在可选范围")
    @NotNull(message = "sex 不能为空")
    private String sex;

}

```

正则表达式说明：

- `^string` : 匹配以 string 开头的字符串
- `string$` ：匹配以 string 结尾的字符串
- `^string$` ：精确匹配 string 字符串
- `(^Man$|^Woman$|^UGM$)` : 值只能在 Man,Woman,UGM 这三个值中选择

### 自定义全局异常处理器捕获数据校验异常

自定义异常处理器可以帮助我们捕获异常，并进行一些简单的处理。

**`GlobalExceptionHandler`**

```java
@Slf4j
@RestControllerAdvice
public class GlobalExceptionHandler {
    /**
     * 处理参数校验失败异常
     * @param exception 异常类
     * @return 响应
     */
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResultBean exceptionHandler(MethodArgumentNotValidException exception){
      //我们主要获取这个接口BindingResult的数据，它就包含了我们使用@RequestBody绑定的参数的所有信息，无论是校验异常错误信息还是JavaBean参数的属性信息
      BindingResult bindingResult = exception.getBindingResult();
      
      Map<String, String> errorMap = new HashMap<>();
      StringBuffer buffer = new StringBuffer();
      if(bindingResult.getFieldErrors() != null){
        for (FieldError fieldError : bindingResult.getFieldErrors()) {
          String field = fieldError.getField();
          Object rejectedValue = fieldError.getRejectedValue();
          String defaultMessage = fieldError.getDefaultMessage();
          errorMap.put(field, defaultMessage);
          String msg = String.format("错误字段：%s, 错误值：%s, 原因：%s", field, rejectedValue, defaultMessage);
          buffer.append(msg);
          log.warn("错误字段：[{}], 错误值：[{}], 原因：[{}]", field, rejectedValue, defaultMessage);
        }
      }
      return ResultBean.error(buffer.toString(), errorMap, 400);
    }
}
```

### 通过Postman测试验证

**验证成功的情况**

![顺利接收JavaBean](/blog/202207211924515.png "Optional title")

**验证失败的情况**

![三个参数都错误](/blog/202207211923143.png "Optional title")


顺便一提，如何在PostMan发送请求体json数据，也就是说后端用@RequestBody接收的参数：

1. 设置请求头`Content-Type:application/json`，content-type首字母小写也是可行的

![设置Content-Type](/blog/202207211928769.png "Optional title")

2. 传递json参数

![传递json参数](/blog/202207211929071.png "Optional title")

## 验证请求参数

这些参数通常被 `@PathVariable` 以及 `@RequestParam`标记，并且相对于JavaBean的参数，我们往往将其称为平铺参数

**注意：这里适用@Valid注解是不行的，因为它要求待校验的入参是JavaBean，所以如果需要校验平铺参数，请使用@Validated开启Spring自动参数校验**

**`PersonController`**

```java
@RestController
@RequestMapping("/api/person")
@Validated
public class PersonController {
  @GetMapping("/{id}")
  public ResponseEntity<Integer> getPersonByID(@PathVariable("id") @Max(value = 5, message = "超过 id 的范围了") Integer id) {
    return ResponseEntity.ok().body(id);
  }

  @PutMapping("/{name}")
  public ResponseEntity<String> getPersonByName(@RequestParam("name") @Size(max = 6, message = "超过 name 的范围了") String name) {
    return ResponseEntity.ok().body(name);
  }
}
```

**`ExceptionHandler`**

```java
/**
* 处理平铺参数校验失败
*/
@ExceptionHandler(ConstraintViolationException.class)
public ResultBean exceptionHandler(ConstraintViolationException exception){
    log.warn(exception.getMessage());
    return ResultBean.error(exception.getMessage(), 400);
}
```

### 通过Postman测试验证

**验证成功的情况**

![顺利接收JavaBean](/blog/202207212015566.png "Optional title")

**验证失败的情况**

![三个参数都错误](/blog/202207212015953.png "Optional title")


# 验证 Service 中的方法
我们不仅可以使用@Validated和@Valid验证Controller组件，也可以验证其他Spring管理的组件，比如Service，**不过Controller一般不提供接口，而Service一般是面向接口编程**，而这个地方有坑，需要注意下面几点：

1. 在实现类中重定义接口方法的参数校验配置会失败且会报错：`javax.validation.ConstraintDeclarationException: HV000151: A method overriding another method must not redefine the parameter constraint configuration`，这个异常信息也告诉我们：参数的校验配置应该写在接口方法中，并且实现类不能修改配置，要么保持一样，要么可以不用写参数校验配置
2. 在非Controller组件中，像Service，必须组合使用@Validated和@Valid，其中@Validated作为类注解、@Valid作为方法参数注解javaBean，这样参数校验才会生效，并且它产生的异常是`ConstraintViolationException`，这个跟之前Controller中的平铺参数校验产生的异常是相同的，这个异常没有继承`BindException`接口，相对而言它的错误不好像`BindException`和`MethodArgumentNotValidException`那样处理
3. 如果方法参数是平铺参数，那么只要加@Validated就行了
```java
@Service
@Validated
public class PersonServiceImpl implements PersonService {

  @Override
  public PersonRequest insertPerson(@NotNull @Min(10) Integer id, @NotNull String name) {
    return null;
  }
}

```
4. @Validated可以放在接口中，也可以放在实现类中，不过我一般放在实现类中

**PersonService**

```java
public interface PersonService {
  PersonRequest insertPerson(@Valid PersonRequest person);
}
```

**PersonServiceImpl**

```java
@Service
@Validated
public class PersonServiceImpl implements PersonService {
  @Override
  public PersonRequest insertPerson(PersonRequest person) {
    return person;
  }
}
```

**ExceptionHandler**

```java
@ExceptionHandler(ConstraintViolationException.class)
public ResultBean exceptionHandler(ConstraintViolationException exception){
    log.warn(exception.getMessage());
    return ResultBean.error(exception.getMessage(), 400);
}
```

## 通过Postman测试验证

**参数校验失败**

![classId为null](/blog/202207212236355.png "Optional title")

# 级联校验
级联校验关键点在于@Valid，级联校验的意思是JavaBean内部有其他JavaBean需要验证，那么这个JavaBean就需要加@Valid注解，并且只能用@Valid，因为它可以标记字段，@Validatd不行

**PersonRequest**

```java
@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class PersonRequest {

  @NotNull(message = "classId 不能为空")
  private String classId;

  @Pattern(regexp = "(^Man$|^Woman$|^UGM$)", message = "sex 值不在可选范围")
  @NotNull(message = "sex 不能为空")
  private String sex;

  @Valid //让InnerChild的属性也参与校验
  @NotNull
  private InnerChild child;     //内部的JavaBean

  @Getter
  @Setter
  @ToString
  public static class InnerChild {
    @Size(max = 33)
    @NotNull(message = "name 不能为空")
    private String name;

    @NotNull(message = "年龄不能为空")
    @Positive(message = "年龄只能为正数")
    private Integer age;
  }
}
```

# Validator 编程方式手动进行参数验证

某些场景下可能会需要我们手动校验并获得校验结果。

我们通过 `Validator` 工厂类获得的 `Validator` 示例。另外，如果是在 Spring Bean 中的话，还可以通过 `@Autowired` 直接注入的方式。

```java
@Autowired
Validator validate
```

具体使用情况如下：

```java
/**
 * 手动校验对象
 */
@Test
public void check_person_manually() {
    ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
    Validator validator = factory.getValidator();
    PersonRequest personRequest = PersonRequest.builder().sex("Man22")
            .classId("82938390").build();
    Set<ConstraintViolation<PersonRequest>> violations = validator.validate(personRequest);
    violations.forEach(constraintViolation -> System.out.println(constraintViolation.getMessage()));
}
```

输出结果如下：

```
sex 值不在可选范围
name 不能为空
```

# 自定义 Validator(实用)

如果自带的校验注解无法满足你的需求的话，你还可以自定义实现注解。

## 案例一:校验特定字段的值是否在可选范围

比如我们现在多了这样一个需求：`PersonRequest` 类多了一个 `Region` 字段，`Region` 字段只能是`China`、`China-Taiwan`、`China-HongKong`这三个中的一个。

**第一步，你需要创建一个注解 `Region`。**

```java
@Target({FIELD})
@Retention(RUNTIME)
@Constraint(validatedBy = RegionValidator.class)
@Documented
public @interface Region {

    String message() default "Region 值不在可选范围内";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};
}
```

**第二步，你需要实现 `ConstraintValidator`接口，并重写`isValid` 方法。**

```java
public class RegionValidator implements ConstraintValidator<Region, String> {

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        HashSet<Object> regions = new HashSet<>();
        regions.add("China");
        regions.add("China-Taiwan");
        regions.add("China-HongKong");
        return regions.contains(value);
    }
}

```

现在你就可以使用这个注解：

```java
@Region
private String region;
```

**通过测试验证**

```java
PersonRequest personRequest = PersonRequest.builder()
     .region("Shanghai").build();
mockMvc.perform(post("/api/person")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(personRequest)))
  .andExpect(MockMvcResultMatchers.jsonPath("region").value("Region 值不在可选范围内"));
```

**使用 `Postman` 验证**

![](https://img-blog.csdnimg.cn/20210421203330978.png)

## 案例二:校验电话号码

校验我们的电话号码是否合法，这个可以通过正则表达式来做，相关的正则表达式都可以在网上搜到，你甚至可以搜索到针对特定运营商电话号码段的正则表达式。

`PhoneNumber.java`

```java
@Documented
@Constraint(validatedBy = PhoneNumberValidator.class)
@Target({FIELD, PARAMETER})
@Retention(RUNTIME)
public @interface PhoneNumber {
    String message() default "Invalid phone number";
    Class[] groups() default {};
    Class[] payload() default {};
}
```

`PhoneNumberValidator.java`

```java
public class PhoneNumberValidator implements ConstraintValidator<PhoneNumber, String> {

    @Override
    public boolean isValid(String phoneField, ConstraintValidatorContext context) {
        if (phoneField == null) {
            // can be null
            return true;
        }
        //  大陆手机号码11位数，匹配格式：前三位固定格式+后8位任意数
        // ^ 匹配输入字符串开始的位置
        // \d 匹配一个或多个数字，其中 \ 要转义，所以是 \\d
        // $ 匹配输入字符串结尾的位置
        String regExp = "^[1]((3[0-9])|(4[5-9])|(5[0-3,5-9])|([6][5,6])|(7[0-9])|(8[0-9])|(9[1,8,9]))\\d{8}$";
        return phoneField.matches(regExp);
    }
}

```

搞定，我们现在就可以使用这个注解了。

```java
@PhoneNumber(message = "phoneNumber 格式不正确")
@NotNull(message = "phoneNumber 不能为空")
private String phoneNumber;
```

**通过测试验证**

```java
PersonRequest personRequest = PersonRequest.builder()
    .phoneNumber("1816313815").build();
mockMvc.perform(post("/api/person")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(personRequest)))
  .andExpect(MockMvcResultMatchers.jsonPath("phoneNumber").value("phoneNumber 格式不正确"));
```

![](https://img-blog.csdnimg.cn/20210421204116640.png)

# 使用验证组

验证组我们基本是不会用到的，也不太建议在项目中使用，理解起来比较麻烦，写起来也比较麻烦。简单了解即可！

当我们对对象操作的不同方法有不同的验证规则的时候才会用到验证组。

我写一个简单的例子，你们就能看明白了！

**1.先创建两个接口，代表不同的验证组**

```java
public interface AddPersonGroup {
}
public interface DeletePersonGroup {
}
```

**2.使用验证组**

```java
@Data
public class Person {
    // 当验证组为 DeletePersonGroup 的时候 group 字段不能为空
    @NotNull(groups = DeletePersonGroup.class)
    // 当验证组为 AddPersonGroup 的时候 group 字段需要为空
    @Null(groups = AddPersonGroup.class)
    private String group;
}

@Service
@Validated
public class PersonService {

    @Validated(AddPersonGroup.class)
    public void validatePersonGroupForAdd(@Valid Person person) {
        // do something
    }

    @Validated(DeletePersonGroup.class)
    public void validatePersonGroupForDelete(@Valid Person person) {
        // do something
    }

}
```

通过测试验证：

```java
  @Test(expected = ConstraintViolationException.class)
  public void should_check_person_with_groups() {
      Person person = new Person();
      person.setGroup("group1");
      service.validatePersonGroupForAdd(person);
  }

  @Test(expected = ConstraintViolationException.class)
  public void should_check_person_with_groups2() {
      Person person = new Person();
      service.validatePersonGroupForDelete(person);
  }
```

验证组使用下来的体验就是有点反模式的感觉，让代码的可维护性变差了！尽量不要使用！

# 常用校验注解总结

`JSR303` 定义了 `Bean Validation`（校验）的标准 `validation-api`，并没有提供实现。`Hibernate Validation`是对这个规范/规范的实现 `hibernate-validator`，并且增加了 `@Email`、`@Length`、`@Range` 等注解。`Spring Validation` 底层依赖的就是`Hibernate Validation`。

**JSR 提供的校验注解**:

- `@Null` 被注释的元素必须为 null
- `@NotNull` 被注释的元素必须不为 null
- `@AssertTrue` 被注释的元素必须为 true
- `@AssertFalse` 被注释的元素必须为 false
- `@Min(value)` 被注释的元素必须是一个数字，其值必须大于等于指定的最小值
- `@Max(value)` 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
- `@DecimalMin(value)` 被注释的元素必须是一个数字，其值必须大于等于指定的最小值
- `@DecimalMax(value)` 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
- `@Size(max=, min=)` 被注释的元素的大小必须在指定的范围内
- `@Digits (integer, fraction)` 被注释的元素必须是一个数字，其值必须在可接受的范围内
- `@Past` 被注释的元素必须是一个过去的日期
- `@Future` 被注释的元素必须是一个将来的日期
- `@Pattern(regex=,flag=)` 被注释的元素必须符合指定的正则表达式

**Hibernate Validator 提供的校验注解**：

- `@NotBlank(message =)` 验证字符串非 null，且长度必须大于 0
- `@Email` 被注释的元素必须是电子邮箱地址
- `@Length(min=,max=)` 被注释的字符串的大小必须在指定的范围内
- `@NotEmpty` 被注释的字符串的必须非空
- `@Range(min=,max=,message=)` 被注释的元素必须在合适的范围内

# 拓展

1. “`@NotNull` 和 `@Column(nullable = false)` 两者有什么区别？”

    > - `@NotNull`是 JSR 303 Bean 验证批注,它与数据库约束本身无关。
    > - `@Column(nullable = false)` : 是 JPA 声明列为非空的方法。

    > 总结来说就是即前者用于验证，而后者则用于指示数据库创建表的时候对表的约束。

2. 对校验进行分类
    + 基础校验，空字符串，null，字符串长短，数值大小等
    + 业务校验，比如传了用户id要检查该用户是否存在，购买的数量是否超库存。是有业务逻辑的。
    + 权限校验，比如有没有权限给用户添加订单

    > 对于基础校验，建议在Controller做<br>
    > 对于业务校验应该放在Service中做，Service应该是集中业务逻辑的<br>
    > 对于权限校验，要看权限是怎么设计的。我一般是在controller做的。<br>

# 总结@Validated和@Valid的区别
1. @Valid：标准JSR-303规范的标记型注解，用来标记验证属性和方法返回值，进行级联和递归校验
2. @Validated：Spring的注解，是标准JSR-303的一个变种（补充），提供了一个分组功能，可以在入参验证时，根据不同的分组采用不同的验证机制
3. 在Controller中校验方法参数时，使用@Valid和@Validated并无特殊差异（若不需要分组校验的话）
4. 相比于@Validated，@Valid可以用在字段级别约束，用来表示级联校验。
5. 相比与@Valid，@Validated可以用于提供分组功能
6. 在非Controller组件中校验方法参数时，@Valid和@Validated必须配合使用，其中@Validated标记组件类，@Valid标记方法参数，如果方法参数是平铺参数，那么只需要用@Validated标记类组件就行了
7. @Valid和@Validated作为类注解都有一个共同作用：开启Spring自动参数校验；但@Valid作为类注解只能标记Controller组件，而@Validated可以标记除Controller组件的其他组件比如@Service

# 参考链接
- [@Validated和@Valid的区别？校验级联属性（内部类）](https://www.cnblogs.com/yourbatman/p/11272939.html)
- [Spring方法级别数据校验：@Validated + MethodValidationPostProcessor优雅的完成数据校验动作](https://blog.csdn.net/f641385712/article/details/97402946)
- [如何在 Spring/Spring Boot 中做参数校验？你需要了解的都在这里！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485783&idx=1&sn=a407f3b75efa17c643407daa7fb2acd6&chksm=cea2469cf9d5cf8afbcd0a8a1c9cc4294d6805b8e01bee6f76bb2884c5bc15478e91459def49&token=292197051&lang=zh_CN)
