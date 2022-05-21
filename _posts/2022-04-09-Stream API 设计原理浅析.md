---
title: Stream API 设计原理浅析
date: 2022-04-09 +/-TTTT
categories: [编程语言, Java, Java8特性, Stream API]
tags: [函数式接口, lambda表达式, 匿名类]     # TAG names should always be lowercase
---

## Stream API 基本执行流程

![Stream API基本执行流程](/blog/202204092227514.png "Stream API基本执行流程")

如何理解stage
首先我们们看看抽象类ReferencePipeline的继承链

![ReferencePipeline的继承链](/blog/202204092239811.png "ReferencePipeline的继承链")

ReferencePipeline 实现Stream接口，实现了各个Stream API 操作，同时继承了PipelineHelper，根据JDK的描述，PipelineHelper是一个执行 Stream pipelines的helper，它能够捕获所以Stream相关的信息（意思是里面定义了可以获取到Stream信息的方法，不过都是都是抽象方法，具体都交由它的子类AbstractPipeline和ReferencePipeline实现了），所以实际上ReferencePipeline包含了所有Stream的信息和操作，而在Stream中用stage来描述一个完整的操作（中间操作、结束操作等等），所以其实Stream可看作是ReferencePipeline的一个实例，然而源码也确实是这么干的。正如下图：

![AbstractPipeline的stage属性](/blog/202204100910098.png "AbstractPipeline的stage属性")

## 中间操作的stage初始化做了什么

以peek()为例，由于中间操作的各个实现都在ReferencePipeline中，如下：

![无状态中间操作的初始化](/blog/202204100926095.png "无状态中间操作的初始化")

另外中间操作的初始化会记录上个stage，上图stage的构造，this指的就是上个stage也就是upstream，之所以this是上个stage，是因为每个中间操作以上个stage进行调用，所以this自然指的是上个stage，而在代码中上个stage用`previousStage`表示

下面介绍Stream API:

Stream API 分两大类，中间操作和结束操作

- 中间操作：中间操作的返回值依然是Stream对象，也就是一个stage，中间操作又分为无状态操作和有状态操作
    + 无状态操作如：filter、map等，即元素的操作只与自身相关，与其他元素无关
    + 有状态操作如：sorted、limit、distinct等，即元素的操作与其他元素关联，例如sorted，元素与其他元素比较才能确定自己的位置

- 结束操作：返回值不再是Stream对象，它会触发之前的中间操作，**正如“无状态中间操作的初始化”所述，最初的初始化只是记录操作，并未真正执行，只有在遇到结束操作时才会触发**，结束操作又分短路操作和非短路操作
    + 短路操作指不用处理所有元素就能返回结果，如findFirst
    + 非短路操作则必须处理完所有元素才能返回结果，如collect
    
在介绍一下ReferencePipeline的三大静态内部类：

这三大内部类都继承了ReferencePipeline

![ReferencePipeline的三大静态内部类](/blog/202204100947377.png "ReferencePipeline的三大静态内部类")

以如下的Stream API 为例：

`list.stream().filter(e -> e.startsWith("A")).sorted((c1,c2) -> c1.length() - c2.length()).collect(Collectors.toList());`

`List.stream()`会被实例化为Head对象，`.filter()`会被实例化为StatelessOp对象，`.sorted()`会被实例化为StatefulOp对象

## 链接stage

上图“AbstractPipeline的stage属性”中，每个stage用`previousStage`保存upstream，这就形成了一条反向链表，把每个stage作为链表中的node的话，就有下图：

![stage反向链](/blog/202204101022430.png "stage反向链")

## 链接Sink

Stream API 通过Sink链记录各个操作的顺序，而每个Sink记录了各个操作传递的lambda表达式；**前面所过结束操作会触发中间操作的实际执行，实际上Sink的链接也是由结束操作触发的，毕竟先要确定操作的执行顺序然后才会正式执行操作**，以collect()为例：我们进入了AbstractPipeline的`wrapAndCopyInto()`，这个方法方法返回Sink，并且内部调用了`copyInto()`

![wrapAndCopyInto()](/blog/202204101046235.png "wrapAndCopyInto()")

而copyInto需要接收Sink类型的参数，而它传入了`wrapSink()`，我们进入它，**发现它正是在链接Sink**

![链接Sink](/blog/202204101042529.png "链接Sink")

也就是说对于Sink链我们有下图：

![Alt text](/blog/202204101100159.png "Optional title")

对比stage链和Sink链，我们发现Head是没有Sink的，终止操作也没有Sink，而每个Sink用`downstream`记录下个stage的Sink，到这就对应上我们最开始的那张图“Stream API基本执行流程”

## Sink链的执行
前面说过Sink链接完成就准备执行了，我们关注AbstractPipeline#copyInto()函数，它接收一个Sink参数，这个参数由wrapAndCopyInto()传入，而传入的就是经过链接后的Sink链头，所以进入`copyInto()`，如下图：

![copyInto操作执行函数](/blog/202204101158105.png "copyInto操作执行函数")

最后我们研究`<R, A> R collect(Collector<? super T, A, R> collector);`发现，**其中T，也就是Stream&lt;T&gt;中的T，代表的是Stream中元素的类型，而A实际是Sink类型，R实际就是collect返回值类型**

到此整个Stream API的执行力流程就分析完毕了。

## 如果让自己来设计Stream API

在研究Stream API时会发现一个很奇怪很有意思的现象，在调用Stream API时，按理应该按照函数的语义执行，例如filter就应该执行过滤的操作，然而实际上，这些API的实现并没有如它语义样立即执行，而是将操作剥离交给了Sink，而它真正做的其实是生成了流结构（可以将其与链表类比）

而将这些操作剥离之后，就形成了一整套有序的处理流的办法也就是Sink链

这样就从最开始的将整个数据集统一处理到后面的foreach，一个个的在Sink链中处理；

而从建模来看，我们把操作再集中，形成一整套的新的处理办法，对数据集进行操作，从而减少了重复遍历，类似一个电子组件，把微小的改变某个状态的多个这样的组件封装成一个新的组件从而达到我们的目的，因为我们的目的就是为了得到被这些操作统统处理之后的结果

其中涉及到**惰性求值（延迟计算）**的技巧：程序中事件发生的逻辑顺序与机器中事件发生的实际顺序解耦开来，我们并没有让机器按照事物的逻辑顺序来了。这也就是我们最开始提到的很奇怪很有意思的现象，这种技巧能再一定程度上缓解机器的执行压力。正如一个盒子我们知道输入，也大概猜的出输出，只需要按需拉取结果就行了

![盒子模型](/blog/202204141850830.png "盒子模型")


## 总结
1.Sink链的链接和执行都是在结束操作中完成的

2.stage实例化的同时也完成了执行操作的记录，通过lambda表达式传递给Sink，并由`accept()`记录，在这里其实用到了**闭包**的技术，也就是lambda作为参数其生命周期本应再函数执行结束后就结束，但因为被匿名类拷贝，赋值给了内部的私有成员也就是downStream，它的生命周期也因此得到了延长


