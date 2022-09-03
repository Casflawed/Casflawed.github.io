---
title: 在Linux系统上安装Oracle JDK8
date: 2022-09-03 +/-TTTT
categories: [Linux]
tags: []     # TAG names should always be lowercase
---

# Linux版本
`uname -a`，查看Linux版本如下：

Linux VM-12-14-centos 3.10.0-1160.71.1.el7.x86_64 #1 SMP Tue Jun 28 15:37:28 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux

# 官网下载JDK8
[JDK8下载链接](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)
可以下载的版本：

![下载版本](/blog/202209032154785.png "Optional title")

**版本x86和x64**

x86对应32的机器，x64对应64为的机器，我的机器是64位的，现在一般的机器应该都是64位的

# 使用Xftp7发送文件
使用Xftp7将之前下载到Windows系统上的JDK压缩包，发送给远程服务器，如下图所示：

![Xftp发送文件到远程服务器](/blog/202209032156474.png "Optional title")
我在Linux系统上，目录/opt下，创建了一个jdk的目录用于存放jdk压缩包，创建命令：`mkdir /opt/jdk`

# 使用Xshell远程链接服务器
Xshell远程连接服务器后，如下图所示：

![Xshell连接远程服务器](/blog/202209032200553.png "Optional title")

下面就是在Xshell上的一系列操作：

1. 解压jdk压缩包，命令：`tar -zxvf jdk-8u341-linux-x64.tar.gz`，-zxvf的`z`指的就是.tar.gz这种压缩格式
2. 创建/usr/local/java目录，命令：`mkdir /usr/local/java`
3. 将解压后的jdk文件移动到java目录下，命令：`mv jdk1.8.0_341/ /usr/local/java`，即将jdk1.8.0_341/目录下的所有文件移动到java目录下
4. 此时在java目录下，进入jdk1.8.0_341/bin目录，通过命令`./java -version`可以查看jdk版本，但这还不够，我们要设置环境变量，使得命令能在其他目录下执行
5. 配置环境变量的配置文件，命令：vim /etc/profile，键入：insert，开始编辑，编辑内容如下：

在末尾添加：

export JAVA_HOME=/usr/local/java/jdk1.8.0_341
export PATH=$JAVA_HOME/bin:$PATH

其中`$PATH`是指原本已经存在的环境变量，如果不加这个就会覆盖掉其他环境变量配置，造成严重的后果，编辑完毕后的效果如图所示：
![环境变量配置文件](/blog/202209032209579.png "Optional title")

7. 编辑完成，键入ESC退出编辑，然后输入`:wq`，保存配置并推出，当然如果不保存，命令是：`:q!`
8. 此时输入命令：`echo $PATH`，我们发现环境变量并没有添加成功，这是因为没有刷新环境变量配置文件，输入命令：`source /etc/profile`，然后输入命令：`echo $PATH`，此时环境变量添加成功
9. 编写一个简单的Hello.java文件，测试是否能运行成功
10. 输入命令，`cd ~`，进入用户主目录，创建目录workspace，命令：`mkdir workspace`，进入到workspace目录，输入命令：`vim Hello.java`，开始编写Java代码，如下图所示：
![Hello.java](/blog/202209032219505.png "Optional title")

11. 输入命令：`javac Hello.java`，然后输入命令：`java Hello`，运行Java程序，你会得到下面的结果：
![运行结果](/blog/202209032220019.png "Optional title")

至此jdk8安装完成