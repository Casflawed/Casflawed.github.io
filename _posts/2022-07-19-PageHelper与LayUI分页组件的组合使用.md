---
title: PageHelper与LayUI分页组件的组合使用
date: 2022-07-19 +/-TTTT
categories: [项目,牛客网讨论区]
tags: []     # TAG names should always be lowercase
---

# 同步分页
相比与异步分页，同步分页的数据是和页面一起返回给前端的，它的特点是：每次页面切换会刷新页面，因此它的体验比不上异步分页，但是我们依然需要掌握

# PageHelper的使用
1. 导入依赖

```xml
<!-- MyBatis 分页插件 -->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.4.3</version>
</dependency>
```
这是pageHelper的Spring Boot依赖，无需做任何配置，只要引入该依赖就可以使用，另外pageHelper的配合MyBatis使用的

## 如果自定义Page类
如果不使用pageHelper，我们就需要自定义Page类，像下面这样：

```java
/**
 * page 分页模型
 * @param <T> 具体模块的 JavaBean
 */
@Data
public class Page<T> {
  public static final int PAGE_CAPACITY = 4;
  private Integer pageNo;                           //当前页码
  private Integer pagesTotal;                       //总页码
  private Integer pageCapacity = PAGE_CAPACITY;     //当前页显示数量
  private Integer itemTotalCount;                   //总记录数
  private List<T> items;                            //当前页数据
  private Integer from;                             //分页条页码的起点
  private Integer to;                               //分页条页码的终点
  private String url;                               //处理页面的前后台 url
}
```

从属性来看，我们分页需要用到这些数据：1.当前页码，2.总页码，3.每页的记录数，4.总记录数，5.分页条页码的起点，6.分页条页码的终点，这些数据的作用：

1. 当前页码和每页的记录数，是分页查询的条件
2. 总页码需要用总记录数和每页记录数计算
3. from和to是为了简化分页条的生成，如果分页条的功能要做完整的话，需要的分页条算法还是蛮复杂的
4. url就是为了复用，同时前端不好获取应用上下文，这个属性存在让分页切换的url更加容易获取

可见如果自己设计的话需要考虑的东西还蛮多的，并且还不太方便，因此我们使用pageHelper

## 上手pageHelper
pageHelper的上手非常简单：

```java
PageHelper.startPage(pageNum, pageSize);        //开启分页查询

PageInfo<DiscussPost> discussPostPageInfo = new PageInfo<>(discussPostMapper.selectDiscussPosts());       //pageHelper自动分页
```

1. 开启分页，`PageHelper.startPage(pageNum, pageSize);`，pageNum是当前页码，pageSize是每页的记录数
2. pageInfo封装需要分页的数据，selectDiscussPosts对应的SQL如下：

```xml
<sql id="Base_Column_List" >
id, user_id, title, type, status, create_time, comment_count, score
</sql>
<sql id="Blob_Column_List" >
content
</sql>

<select id="selectDiscussPosts" resultType="DiscussPost">
select
<include refid="Base_Column_List" />
,
<include refid="Blob_Column_List" />
from `discuss_post`
where `status` != 2
order by `type` desc
</select>
```

从这里就能看出pageHelper与自定义Page的不同点了：

1. 不需要自定义分页查询，我们只需要查询需要分页的所用数据，并用PageInfo类封装，然后pageHelper就会自动生成分页查询的SQL，还有查询总数据量的SQL，就像下面这样：

![pageHelper的自动sql生成](/blog/202207191703472.png "Optional title")

这两条SQL都是在我们最初的SQL的基础之上自动生成的，这样我们就少写了几句SQL，但是真正让我们方便的是这个PageInfo类：

![PageInfo类](/blog/202207191710414.png "Optional title")

像这样有了pageInfo，只需把它传给前端，前端就可以通过pageInfo里面的属性，像total（总数据量）、pageNum（当前页码）、pageSize（每页的记录数）自动生成分页条了，需要注意的是：

1. 前端不需要处理当前页，pageHelper会自动处理页码-1，执行分页查询
2. 后端应该向前端传递的是pageInfo的JSON字符串而不是Java对象

    > 如果你使用的是Thymeleaf模板渲染引擎，可能会直接通过Model向它传递java对象，这样通过模板获取到的数据是无法被js解析的，你也无法提取到需要的属性，
    > 
    > 但如果是通过json工具像fastjson、gson将Java对象转换成json字符串，前端将json字符串解析成json对象就可以顺利提取属性了

3. 由于js提取模板引擎的数据比较困难，我们可以使用表单的隐藏域来实现

```html
<input type="hidden" name="pageInfo" th:value="${pageInfo}">
```

```js
$('input[name="pageInfo"]').val()   //js通过这条语句就可以获取value了
```

# LayUI分页组件使用
1. 引入依赖

```html
<link rel="stylesheet" th:href="@{/layui/css/layui.css}">
<script th:src="@{/layui/layui.js}"></script>
```

2. 在分页条容器中加载分页条

```js
/**
 * 分页条渲染函数，在页面加载时执行
 */
layui.use(['laypage', 'layer'], function () {
    var laypage = layui.laypage, layer = layui.layer;
    var pageInfo = getPageInfoJsonObject()

    // elem和count是必须项，elem是挂载的容器Id，注意不需要加#，count是需要分页的数据量
    laypage.render({
        elem: 'pagination',
        count: pageInfo.total,                              //数据总数
        limit: pageInfo.pageSize,                           //每页的数量
        curr: pageInfo.pageNum,
        theme: 'pagination',                                //自定义样式
        jump: function (laypage, first) {                   //切换分页的回调
            if (!first) {                                   //如果不加这个条件判断，回调会反复触发执行
                window.location.href = getUrl() + "?pageNum=" + laypage.curr
            }
        }
    });
})
```

## LayUI分页组件的特点

1. 相比与 [pagination.js](https://pagination.js.org/) ，laypage不需要以页面数据为数据源

    >如果我们使用的是pagination.js，那么我们需要从后端获取所有的分页数据，这样和pagehelper的结合使用就会显得及其不优雅，
    >而且由于是同步分页，那么每次页面刷新都会执行庞大的数据查询，效率很低

2. 而LayUI有了分页的数据量就能生成分页条，这样就省了不少事<br>
3. 自动生成的分页条的html代码<br>
![分页条的html代码](/blog/202207191524263.png "Optional title")

    > 自定义样式由theme属性指定，theme属性的可选值：
    > 
    > 1. theme: '#c00'，定义每个切换按钮的背景颜色，这时它的位置在a标签中
    > 2. theme: 'xxx'，将会生成 class="layui-laypage-xxx" 的CSS类，以便自定义主题，这时它的位置在分页条的div中

## laypage组件使用的注意点

laypage能为我们自动生成分页条，但是不能帮我们设定页面切换的请求url，需要我们手动设置，目前有两种方法：

1. laypage的jump参数定义了页面切换的回调，在该函数中我们可以通过window.location，替换地址栏的url，但是使用它，需要注意url不能写死，下面是window.location的用法：

    > 1. window.location.href （当前url）—— http://www.myurl.com:8866/test?id=123&username=xxx
    > 2. window.location.protocol（协议）—— http:
    > 3. window.location.host（域名 + 端口）—— www.myurl.com:8866
    > 4. window.location.hostname（域名）—— www.myurl.com
    > 5. window.location.port（端口）—— 8866
    > 6. window.location.pathname（路径）—— /test
    > 7. window.location.search （请求的参数）—— ?id=123&username=xxx
    > 8. window.location.origin（路径前面的url）——  http://www.myurl.com:8866

通过上面的特性就可以动态获取url，这样在不同的开发环境下，就算url发生变化，程序也能正常运行

2. 第二种就是为我们的元素绑定点击事件，在点击事件中我们可以发送ajax请求，请求获取到的数据在通过html拼接成html字符串，加载到html中就可以实现了，当然也可以同样调用window.location请求页面和数据，这样能够避免html拼接的痛苦，当然ajax请求应该也可以直接接收页面内容，只不过这个我还没有尝试过（不过使用Thymeleaf之后感觉vue还是方便太多）