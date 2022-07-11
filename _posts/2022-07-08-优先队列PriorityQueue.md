---
title: 优先队列PriorityQueue
date: 2022-07-08 +/-TTTT
categories: [算法与数据结构]
tags: []     # TAG names should always be lowercase
---

# 优先队列
## 概述
优先队列PriorityQueue是Queue接口的实现，可以对其中元素进行排序，可以放基本数据类型的包装类（如：Integer，Long等）或自定义的类，对于基本数据类型的包装器类，优先队列中元素默认排列顺序是升序排列，但对于自己定义的类来说，需要自己定义比较器，**虽说它被称为优先队列，但是它的底层数据结构实际上是我们熟知的堆结构，而且默认情况下，即`new PriorityQueue<>()`是小根堆**，所以很多时候我们不用自己手写堆，使用PriorityQueue就可以了

## 常用方法

```java
peek()//返回队首元素
poll()//返回队首元素，队首元素出队列
add()//添加元素
offer()//添加元素
size()//返回队列元素个数
isEmpty()//判断队列是否为空，为空返回true,不空返回false
```

**注意：在java1.5中add()实际上调用的offer()**<br>
![add()与offer()](/blog/202207081542452.png "add()与offer()")

## 优先队列的使用

1.队列保存的是基本数据类型的包装类<br>
```java
public class PriorityQueueSort {
  public static void priorityQueueSort(int[] arr){
    PriorityQueue<Integer> smallHeap = new PriorityQueue<>(); // 默认小根堆，且升序
    for (int num : arr) {
      smallHeap.add(num);
    }
    for (int i = 0; i < arr.length; i++) {   // 我们发现PriorityQueue每次需要Poll输出元素，最终的数组序列才是有序的
      Integer poll = smallHeap.poll();
      System.out.print(poll + " ");
    }
  }


  public static void main(String[] args) {
    int[] arr = new int[]{38, 43 , 45, 20, 23, 100, 1, 4, 19 };
    priorityQueueSort(arr);
  }

}
```

**理解优先队列：<br>
1.默认情况下的优先队列其实就是小根堆，每次poll的过程其实包含：从堆中去除根元素，然后heapify，在这样反复的poll，输出的元素就是有序的，因为每次输出了小根堆的根元素<br>
2.如果让我自己手写小根堆，思路和大根堆一样，不过最后需要排序出来后是倒叙的，所以需要首位交换元素**

2.队列保存的是自定义类<br>
```java
//矩形类
class Node{
    public Node(int chang,int kuan)
    {
        this.chang=chang;
        this.kuan=kuan;
    }
    int chang;
    int kuan;
}

public class Test {
　　　　//自定义比较类，先比较长，长升序排列，若长相等再比较宽，宽降序
    static Comparator<Node> cNode=new Comparator<Node>() {
        public int compare(Node o1, Node o2) {
            if(o1.chang!=o2.chang)
                return o1.chang-o2.chang;
            else
                return o2.kuan-o1.kuan;
        }
        
    };
    public static void main(String[] args) {
        Queue<Node> q=new PriorityQueue<>(cNode);
        Node n1=new Node(1, 2);
        Node n2=new Node(2, 5);
        Node n3=new Node(2, 3);
        Node n4=new Node(1, 2);
        q.add(n1);
        q.add(n2);
        q.add(n3);
        Node n;
        while(!q.isEmpty())
        {
            n=q.poll();
            System.out.println("长: "+n.chang+" 宽：" +n.kuan);
        }
　　　　　/**
　　　　　　* 输出结果
　　　　　　* 长: 1 宽：2
　　　　　　* 长: 2 宽：5
　　　　　　* 长: 2 宽：3
　　　　　　*/
    }
}
```

