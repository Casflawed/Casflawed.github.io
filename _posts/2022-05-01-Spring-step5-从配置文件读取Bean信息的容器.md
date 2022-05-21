---
title: Spring-step5-从配置文件读取Bean信息的容器
date: 2022-05-01 +/-TTTT
categories: [框架,Spring]
tags: [系统设计,封装,反射]     # TAG names should always be lowercase
---

## 回顾
到目前为止spring-bean容器也来越自动化，它能够为客户端做的事情越来越多，包括自动创建Bean对象、对象属性自动注入；我们前面说过的一个Bean容器应该具备的能力：

- Bean定义
- Bean注册，所谓的注册就像DriveManger对数据库驱动进行注册的那样，实际就是将Bean或者与Bean直接关联的信息用容器进行保存，待要使用时就用索引（可以是名称、id、或其他任何能够唯一对应Bean的事务）取出
- Bean对象创建
- 依赖注入

目前该容器已经全部具备，但是与实际的Spring-Bean相比，它还有个地方很有违和感：客户端每次都需要依靠Java代码把BeanDefinition和PropertyValues给准备好，并且注册进入容器，但实际上这样操作比较麻烦，毕竟记住API是件非常烦人的事情，所以实际的Spring容器采用配置文件记录bean信息的方法，通过读取配置文件解析成BeanDefinition和PropertyValues，这样容器就将BeanDefinition和PropertyValues创建工作也包揽在自己手里，这样客户端的工作就更加轻松了；

## 目标
所以本step的目标就是实现读取xml配置文件，实现容器自动创建BeanDefinition和PropertyValues！

## 当前的Bean容器
![当前的容器和期望的容器](/blog/202205021443694.png "当前的容器和期望的容器")

可以看到客户端不用管BeanDefinition和PropertyValues的实例化，XML配置文件彻底接管了这个任务，这下我们其实可以把XML配置文件和Bean容器合并一下作为最新的容器，**从客户端的角度来看只需要从Bean容器中get，而不用set了**，这样客户端差不多把对象的控制权完全交给了Bean容器，也就实现了对象实例化逻辑和客户端核心业务解耦的目的，而从容器的角度来看，生产对象实例的原料由XML配置文件提供，Bean容器负责制造，整个合在一起构造了一个严谨的对象实例化工厂；

![实例化工厂支持客户端核心业务](/blog/202205021449454.png "实例化工厂支持客户端核心业务")

## 怎么从原始容器——>期望容器
当前容器，Bean定义和Bean注册还需要客户端操劳，应该为了让客户端轻松点，就让Bean容器来代劳吧；

也就是说Bean容器现在要做的工作就有：Bean定义 ——> Bean注册 ——> Bean实例化 ——> Bean属性注入；不过在这之前得准备原料，才能准备生产得事情吧，哈哈哈，不急慢慢来！所以工作有点多啊：

准备原料 ——> Bean定义 ——> Bean注册 ——> Bean实例化 ——> Bean属性注入

## 合理规划生产
所谓思考建设得时候不仅要考虑当前得情况，还要给未来留有余地，以便建设的扩展优化，所以我们是否要把所有的生产流程放在一个流水线上呢？当然不是，分部门，各司其职分而治之才是王道，因为这样各个流程不会杂糅在一起，要是针对其中一个流程做优化，也不会影响到其他的生产流程，**总之生产线分解再分解就对了**

### 原料引进部门
所以针对生产流程，成立专门的部门，原料引进部门专门处理XML配置文件读取，解析BeanDefinition的任务，毕竟BeanDefiniton就是我们需要的原料，下面看看原料加工厂需要做那些工作吧：

![原料加工成的工作](/blog/202205021733589.png "原料加工成的工作")

### 给原料来源分渠道
由于XML配置文件可能来自本地，classpath，或者云文件，所以实际上XML配置文件的读取是有多种策略的，因此依照策略模式，建立XML配置文件的不同读取策略

```java
public interface Resource {

    InputStream getInputStream() throws IOException;

}
```

```java
public class ClassPathResource implements Resource {

    // 为什么要定义path和classLoader两个属性
    // 1.原本让我来写，classLoader是写死的（方便客户端指定特定的classLoader，毕竟classLoader与资源类型有点关系？）
    // 2.path也可以直接传递给方法（延长path的生命周期？）

    private final String path;
    private ClassLoader classLoader;

    public ClassPathResource(String path) {
        this(path, (ClassLoader) null);
    }

    public ClassPathResource(String path, ClassLoader classLoader) {
        Assert.notNull(path, "Path must not be null");
        this.path = path;
        this.classLoader = (classLoader != null ? classLoader : ClassUtils.getDefaultClassLoader());
    }

    @Override
    public InputStream getInputStream() throws IOException {
        InputStream is = classLoader.getResourceAsStream(path);
        if (is == null) {
            throw new FileNotFoundException(
                    this.path + " cannot be opened because it does not exist");
        }
        return is;
    }
}
```

```java
public class FileSystemResource implements Resource {

    private final File file;

    private final String path;

    public FileSystemResource(File file) {
        this.file = file;
        this.path = file.getPath();
    }

    public FileSystemResource(String path) {
        this.file = new File(path);
        this.path = path;
    }

    @Override
    public InputStream getInputStream() throws IOException {
        return new FileInputStream(this.file);
    }

    public final String getPath() {
        return this.path;
    }

}
```

```java
public class UrlResource implements Resource{

    private final URL url;

    public UrlResource(URL url) {
        Assert.notNull(url,"URL must not be null");
        this.url = url;
    }

    @Override
    public InputStream getInputStream() throws IOException {
        URLConnection con = this.url.openConnection();
        try {
            return con.getInputStream();
        }
        catch (IOException ex){
            if (con instanceof HttpURLConnection){
                ((HttpURLConnection) con).disconnect();
            }
            throw ex;
        }
    }

}
```

### 读取资源时首先要判断是什么类型的资源
```java
public interface ResourceLoader {

    /**
     * Pseudo URL prefix for loading from the class path: "classpath:"
     */
    String CLASSPATH_URL_PREFIX = "classpath:";

    Resource getResource(String location);

}
```

```java
public class DefaultResourceLoader implements ResourceLoader {

    @Override
    public Resource getResource(String location) {
        Assert.notNull(location, "Location must not be null");
        if (location.startsWith(CLASSPATH_URL_PREFIX)) {
            return new ClassPathResource(location.substring(CLASSPATH_URL_PREFIX.length()));
        }
        else {
            try {
                URL url = new URL(location);
                return new UrlResource(url);
            } catch (MalformedURLException e) {
                return new FileSystemResource(location);
            }
        }
    }

}
```

### 从资源中解析BeanDefiniton
```java
/**
 * Simple interface for bean definition readers.
 */
public interface BeanDefinitionReader {

    BeanDefinitionRegistry getRegistry();

    ResourceLoader getResourceLoader();

    void loadBeanDefinitions(Resource resource) throws BeansException;

    void loadBeanDefinitions(Resource... resources) throws BeansException;

    void loadBeanDefinitions(String location) throws BeansException;

}
```

```java
/**
 * Abstract base class for bean definition readers which implement
 * the {@link BeanDefinitionReader} interface.
 */
public abstract class AbstractBeanDefinitionReader implements BeanDefinitionReader {

    private final BeanDefinitionRegistry registry;

    private ResourceLoader resourceLoader;

    protected AbstractBeanDefinitionReader(BeanDefinitionRegistry registry) {
        this(registry, new DefaultResourceLoader());
    }

    public AbstractBeanDefinitionReader(BeanDefinitionRegistry registry, ResourceLoader resourceLoader) {
        this.registry = registry;
        this.resourceLoader = resourceLoader;
    }

    @Override
    public BeanDefinitionRegistry getRegistry() {
        return registry;
    }

    @Override
    public ResourceLoader getResourceLoader() {
        return resourceLoader;
    }

}
```

```java
/**
 * Bean definition reader for XML bean definitions.
 */
public class XmlBeanDefinitionReader extends AbstractBeanDefinitionReader {

    public XmlBeanDefinitionReader(BeanDefinitionRegistry registry) {
        super(registry);
    }

    public XmlBeanDefinitionReader(BeanDefinitionRegistry registry, ResourceLoader resourceLoader) {
        super(registry, resourceLoader);
    }

    @Override
    public void loadBeanDefinitions(Resource resource) throws BeansException {
        try {
            try (InputStream inputStream = resource.getInputStream()) {
                doLoadBeanDefinitions(inputStream);
            }
        } catch (IOException | ClassNotFoundException e) {
            throw new BeansException("IOException parsing XML document from " + resource, e);
        }
    }

    @Override
    public void loadBeanDefinitions(Resource... resources) throws BeansException {
        for (Resource resource : resources) {
            loadBeanDefinitions(resource);
        }
    }

    @Override
    public void loadBeanDefinitions(String location) throws BeansException {
        ResourceLoader resourceLoader = getResourceLoader();
        Resource resource = resourceLoader.getResource(location);
        loadBeanDefinitions(resource);
    }

    protected void doLoadBeanDefinitions(InputStream inputStream) throws ClassNotFoundException {
        Document doc = XmlUtil.readXML(inputStream);
        Element root = doc.getDocumentElement();
        NodeList childNodes = root.getChildNodes();

        for (int i = 0; i < childNodes.getLength(); i++) {
            // 判断元素
            if (!(childNodes.item(i) instanceof Element)) continue;
            // 判断对象
            if (!"bean".equals(childNodes.item(i).getNodeName())) continue;
            
            // 解析标签
            Element bean = (Element) childNodes.item(i);
            String id = bean.getAttribute("id");
            String name = bean.getAttribute("name");
            String className = bean.getAttribute("class");

            // 获取 Class，方便获取类中的名称
            Class<?> clazz = Class.forName(className);
            // 优先级 id > name
            String beanName = StrUtil.isNotEmpty(id) ? id : name;
            if (StrUtil.isEmpty(beanName)) {
                beanName = StrUtil.lowerFirst(clazz.getSimpleName());
            }

            // 定义Bean
            BeanDefinition beanDefinition = new BeanDefinition(clazz);

            // 读取属性并填充
            for (int j = 0; j < bean.getChildNodes().getLength(); j++) {
                if (!(bean.getChildNodes().item(j) instanceof Element)) continue;
                if (!"property".equals(bean.getChildNodes().item(j).getNodeName())) continue;
                // 解析标签：property
                Element property = (Element) bean.getChildNodes().item(j);
                String attrName = property.getAttribute("name");
                String attrValue = property.getAttribute("value");
                String attrRef = property.getAttribute("ref");

                // 获取属性值：引入对象、值对象
                Object value = StrUtil.isNotEmpty(attrRef) ? new BeanReference(attrRef) : attrValue;
                // 创建属性信息
                PropertyValue propertyValue = new PropertyValue(attrName, value);
                beanDefinition.getPropertyValues().addPropertyValue(propertyValue);
            }
            if (getRegistry().containsBeanDefinition(beanName)) {
                throw new BeansException("Duplicate beanName[" + beanName + "] is not allowed");
            }
            // 注册 BeanDefinition
            getRegistry().registerBeanDefinition(beanName, beanDefinition);
        }
    }

}
```

## 总结
像spring这样的精妙设计一定是经过无数次修改，因此对于我自己来说想要一次性就写出这么完美的设计是很难的，不过认识到自己的上限，勇敢接受自己的不足；目前我已经掌握了流程图对功能进行分解，但是真正将文字描述的功能转化成代码，还有一段路要走；不过在设计并实践的过程中：

1.保证功能得到实现，不要妄想一次性达到官方那种完美的状态
2.由有缺陷的代码不断精进，不断完善才是一段设计精妙的代码该有的过程，同时可以借助流程图，类图等UML工具辅助设计