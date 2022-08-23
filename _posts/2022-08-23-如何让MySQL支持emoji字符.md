---
title: 如何让MySQL支持emoji字符
date: 2022-08-23 +/-TTTT
categories: [数据库, MySQL]
tags: []     # TAG names should always be lowercase
---

> 以Windows系统，MySQL5.7.33版本为例

# 第一种方法：修改数据库配置文件（已经实践有效）
在MySQL文件目录下，找到mysql.ini配置文件，将其中的内容替换为下面的内容：

```xml
[client]

default-character-set = utf8mb4

[mysql]

# 设置mysql客户端默认字符集
default-character-set = utf8mb4

[mysqld]

#设置3306端口
port = 3306 

# 设置mysql的安装目录
basedir=C:\Users\wangwei\Documents\mysql-5.7.33-winx64

# 设置mysql数据库的数据的存放目录
datadir=C:\Users\wangwei\Documents\mysql-5.7.33-winx64\data

# 允许最大连接数
max_connections=200

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server = utf8mb4

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB

character-set-client-handshake = FALSE

collation-server = utf8mb4_unicode_ci

init_connect='SET NAMES utf8mb4'
```

这个配置文件的修改会让MySQL服务端、客户端默认的字符集编程utf8mb4

## 重新启动MySQL，让配置文件生效
重启之前需要修改注册表：`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL`下的ImagePath

![ImagePath](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202208230841611.png "Optional title")

修改值为：`"C:\Users\wangwei\Documents\mysql-5.7.33-winx64\bin\mysqld" --defaults-file="C:\Users\wangwei\Documents\mysql-5.7.33-winx64\mysql.ini" MySQL`，其中--defaults-file后面的部分是自己添加上去的，目的是为了让MySQL在启动的时候加载配置文件mysql.ini

## 查看MySQL配置变量
使用命令：`show variables where variable_name like 'character_set_%' or variable_name like 'collation%';`，结果如下，说明配置文件加载成功

![配置文件加载成功](/blog/202208230853408.png "Optional title")

## 修改原来的库、表、字段的字符集
昨晚上面的步骤，以后自己新建的表、字段的默认字符集就是utfmb4了，但如果自己原来的数据库、表、字段不是utfmb4，则需要手动修改：

```sql
-- 修改数据库的字符集
ALTER DATABASE 数据库名 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
-- 修改表的字符集
ALTER TABLE 表名 CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
-- 修改表字段的字符集
ALTER TABLE 表名 MODIFY 字段名 字段类型 CHARSET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

按理到这步就应该成了，最后就能在数据库中插入emoji字符了

## 提高MySQL-connector-java驱动版本
![数据库可以插入emoji](/blog/202208230902081.png "Optional title")

如上图数据库已经可以插入emoji字符了，但是在程序中却依然插入不了，这时候就是你的mysql-connector-java驱动存在版本问题，我最开始的版本是5.1.8，结果程序插入不利啊emoji字符，换成更加高的版本6.0.6就可以了

# 第二种方法，改字段级别的字符集
字符集规则有下面的优先级：字段 > 表 > 数据库，因此按理仅仅修改某个需要插入emoji字符的字段的字符集就可以了