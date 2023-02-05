---
title: 迁移Postgres的Sequence（序列）
date: 2023-01-29 +/-TTTT
categories: [数据库, pgsql]
tags: []     # TAG names should always be lowercase
---

# 如何在迁移数据库时导出 SEQUENCE
navicat 转储数据和结构 sql 时无法生成自增序列的 sql，但 pgAdmin4 做到了，下面是 pgAdmin 导入和导出 sql 的操作演示：

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291445455.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291446283.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291451733.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291452872.png)

下面是导入操作：

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291454666.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291456011.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291458826.png)

![](https://cdn.jsdelivr.net/gh/Casflawed/img-host@master/blog/202301291459900.png)

# 如何创建 SEQUENCE
1. 创建序列：CREATE SEQUENCE my_sequence INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 99999999 CACHE 1;
2. 为序列赋予操作权限：ALTER SEQUENCE my_sequence OWNER TO postgres;
3. 关联到表主键：alter table my_table alter column my_id set default nextval('my_sequence');

# 如何正确修改 SEQUENCE  
> 序列（Sequence）的当前值（Currval）无法通过 pg_dump导出，又不能对源实例做修改，得这么办才行。

在结构导出时，序列（Sequence）的当前值无法通过pg_dump导出，只能通过事后查询该序列的当前值并写入目标库。

查询序列的当前值，有两种办法：

1. select currval('seqname') 仅获得当前会话最后一次生成的值。实际执行中，必须先执行 nextval 后才能执行currval，这样会修改源数据库，不可取
2. select last_value from seqname 获得所有会话中最后一次生成的值

修改目标库序列的当前值，也有两种办法：

1. select setval('seqname', val) 修改序列当前值（原子操作）
2. alter sequence seqname restart with val 修改序列当前值（阻塞性事务，会阻塞其他会话的nextval操作）

## 建议采用的方案

既可以干净地获取源值，又能低成本地设置到目标。

1. select last_value from seqname 获得源库当前值
2. select setval('seqname', val) 在目标库设置目标值