---
title: wait、notify、notifyAll方法的使用注意事项
date: 2022-09-01 +/-TTTT
categories: [多线程]
tags: []     # TAG names should always be lowercase
---

# 为什么wait方法必须在 synchronized 保护的同步代码中使用？
**wait方法的使用原则**

线程在调用wait方法之前，必须先持有对象的monitor锁，也就是synchronized锁

**wait为什么要这样设计**

为了验证这个问题，我们从反面来看，假设现在有一个阻塞队列：

```java
class BlockingQueue {
    Queue<String> buffer = new LinkedList<String>();
    public void give(String data) {
        buffer.add(data);
        notify();  // Since someone may be waiting in take
    }
    public String take() throws InterruptedException {
        while (buffer.isEmpty()) {
            wait();
        }
        return buffer.remove();
    }
}
```

从代码看：

1. 方法give()是生产者，每次往队列中添加一个元素，就去唤醒正在等待的线程
2. 方法take()是消费者，它会进行循环判断，如果队列为空，就进入等待状态，否则从队列中取出一个元素

由于消费者代码块没有被synchronized修饰，所以就容易出现下面的情况：

1. 消费者判断循环，true，进入循环，此时因为cpu调度，生产者方法开始执行，而wait()方法没来的及执行
2. 由于生产者已经执行，那么队列不为空，当cpu占用权回到消费者时，while条件已经失效，此时生产者会进行无效的等待
3. 而如果没有其他生产者运行，消费者就不会得到唤醒的通知，那么就会无限期的等待

**总结**

消费者while语句块，判断和执行不是一个原子操作，所以整个程序就很容易出错

**加了synchronized之后**

```java
public void give(String data) {
   synchronized (this) {
      buffer.add(data);
      notify();
  }
}

public String take() throws InterruptedException {
   synchronized (this) {
    while (buffer.isEmpty()) {
         wait();
       }
     return buffer.remove();
  }
}
```

我们知道先要进入synchronized修饰的语句块必须首先获得对象的monitor锁，那么当消费者进入到synchronized语句块后，就已经持有了monitor锁，那么在消费者释放monitor锁之前，生产者一定不会执行

另外由于wait会释放monitor锁，这也要求我们必须首先进入到 synchronized 内持有这把锁。

# 为什么 wait/notify/notifyAll 被定义在 Object 类中，而 sleep 定义在 Thread 类中？

1. wait方法调用时会释放monitor锁，notify、notifyAll在调用前必须持有monitor锁，它们都是与monitor锁相关的，而monitor锁是对象级别的，而非线程级别的，所以把wait/notify/notifyAll 定义在 Object 类是最合适的，因为 Object 类是所有对象的父类。
2. 如果把 wait/notify/notifyAll 方法定义在 Thread 类中，会带来很大的局限性，假设此时wait在Thread中，那么线程如何明确释放哪把锁，而线程又该如何持有多把锁。
3. 既然我们是让当前线程去等待某个对象的锁，自然应该通过操作对象来实现，而不是操作线程。

# wait/notify 和 sleep 方法的异同？

**主要对比 wait 和 sleep 方法**

相同点：

1. 都可以让线程阻塞
2. 都可以响应interrupt中断：在等待的过程中如果收到中断信号，都可以进行响应，并抛出 InterruptedException 异常。

不同点：

1. wait 方法必须在 synchronized 保护的代码中使用，而 sleep 方法并没有这个要求。
2. 在同步代码中执行 sleep 方法时，并不会释放 monitor 锁，但执行 wait 方法时会主动释放 monitor 锁。
3. leep 方法中会要求必须定义一个时间，时间到期后会主动恢复，而对于没有参数的 wait 方法而言，意味着永久等待，直到被中断或被唤醒才能恢复，它并不会主动恢复。
4. wait/notify 是 Object 类的方法，而 sleep 是 Thread 类的方法。