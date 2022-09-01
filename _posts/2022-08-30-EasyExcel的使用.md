---
title: EasyExcel的使用
date: 2022-08-30 +/-TTTT
categories: [Office办公软件, Excel]
tags: []     # TAG names should always be lowercase
---

# EasyExcel简介
对于apache提供的Apache poi，它非常容易造成内存泄露，因为是一次性将Excel文件都读到内存，而EasyExcel是按照一个Sheet的一行一行读取到内存当中，这样便于后期处理，就能避免内存泄露

# 使用EasyExcel导入.xls或.xlsx文件
## 普通导入并输出
第一种：稍微复杂的写法，不过很标准

```java
public class ReadComplex {
  public static void main(String[] args) {
    ExcelReaderBuilder builder = EasyExcel.read();
    //读取的文件绝对路径
    builder.file("C:\\Users\\wangwei\\Documents\\excel\\demo.xlsx");
    //读取的表格
    builder.sheet("模板");
    builder.autoCloseStream(true);
    //读取的文件类型
    builder.excelType(ExcelTypeEnum.XLSX);
    //注册读取监听器
    builder.registerReadListener(new AnalysisEventListener() {
      @Override
      public void invoke(Object o, AnalysisContext analysisContext) {
        //监听者模式，每读完一行就会调用的方法
        System.out.println(o);
      }

      @Override
      public void doAfterAllAnalysed(AnalysisContext analysisContext) {
        //所有数据读完后调用
        System.out.println("====读取完成====");
      }
    });
    //获取读取器
    ExcelReader build = builder.build();
    build.readAll();
    //完成所有的读取，并且关闭流
    build.finish();
  }
}
```

第二种是简便的写法：

```java
public class ReadExcel {
  public static void main(String[] args) {
    EasyExcel.read("C:\\Users\\wangwei\\Documents\\excel\\demo.xlsx")
            //如果不指定sheetName，默认读取所有的表格
            .sheet("模板")
            .registerReadListener(new AnalysisEventListener() {
              @Override
              public void invoke(Object o, AnalysisContext analysisContext) {
                System.out.println(o.toString());
              }

              @Override
              public void doAfterAllAnalysed(AnalysisContext analysisContext) {
                System.out.println("====读取完成====");
              }
            })
            .doRead();
  }
}
```

这种方法采用链式编程的方式，并且只设置关键的参数：sheet名、文件名和监听器，最后调用doRead方法就可以读取数据了

## 使用JavaBean接收Excel表格每行的数据
首先说明，通过debug，我们得知在监听器内部的invoke()的参数O，实际读取时的类型是LinkedHashMap，并且key为Integer，value为String

但是通常我们会用JavaBean去接收数据，具体步骤如下：

1.首先是我们的Excel文件数据
![文件数据](/blog/202208311337044.png "Optional title")

2.然后是JavaBean类

```java
@Data
public class ExcelData {
  @ExcelProperty("排名")
  private Integer rank;

  @ExcelProperty("选项ID")
  private String itemId;

  @ExcelProperty("标题")
  private String title;

  @ExcelProperty("编号")
  private Long code;

  @ExcelProperty("描述")
  private String desc;

  @ExcelProperty("得票数")
  private Integer voteCount;

  @ExcelProperty("活动ID")
  private String activityId;

  @ExcelProperty("创建时间")
  private Date createTime;

}
```

3.第三部，开始读取

```java
public class ReadExcelByObj {
  public static void main(String[] args) {
    //用来保存接收到的数据
    ArrayList<ExcelData> list = new ArrayList<>();
    EasyExcel.read("C:\\Users\\wangwei\\Documents\\excel\\demo.xlsx")
            //接收数据的JavaBean类型
            .head(ExcelData.class)
            .sheet("模板")
            .registerReadListener(new AnalysisEventListener<ExcelData>() {
              @Override
              public void invoke(ExcelData excelData, AnalysisContext analysisContext) {
                list.add(excelData);
              }

              @Override
              public void doAfterAllAnalysed(AnalysisContext analysisContext) {
                System.out.println("====读取完成====");
              }
            })
            .doRead();
    for (ExcelData excelData : list) {
      System.out.println(excelData);
    }
  }
}
```

也很简单，相比于简便写法，就多出了用head()指定JavaBean的类型

# 使用EasyExcel导出Excel文件
写数据也非常简单，这里就演示如何将JavaBean导出到Excel，直接上代码：

```java
public class WriteExcel {
  public static void main(String[] args) {
    List dataList = getExcelDataList();
    EasyExcel.write("C:\\Users\\wangwei\\Documents\\excel\\demo_副本.xlsx")
            .head(ExcelData.class)
            .excelType(ExcelTypeEnum.XLSX)
            .sheet("list")
            .doWrite(dataList);
  }
  public static List getExcelDataList(){
    ArrayList<ExcelData> list = new ArrayList<>();
    EasyExcel.read("C:\\Users\\wangwei\\Documents\\excel\\demo.xlsx")
            //接收数据的JavaBean类型
            .head(ExcelData.class)
            .sheet("模板")
            .registerReadListener(new AnalysisEventListener<ExcelData>() {
              @Override
              public void invoke(ExcelData excelData, AnalysisContext analysisContext) {
                list.add(excelData);
              }

              @Override
              public void doAfterAllAnalysed(AnalysisContext analysisContext) {
                System.out.println("====读取完成====");
              }
            })
            .doRead();
    return list;
  }
}
```

从代码中看出，写出文件也非常简单，同样用head()指定JavaBean的类型，然后是文件类型、文件保存的位置和Sheet名，最后调用doWrite写出就完成了

