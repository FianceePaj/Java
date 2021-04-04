# Springboot

## 1.AOP（Aespect Oriented Programming）面向切片编程

分离应用的业务逻辑和系统级服务进行内聚性的开发。

AOP是OOP的补充和完善。

OOP对于分散对象的公共行为没有太多的把握，OOP中对象的关系一般都是从上到下的，但是对于从左到右的关系并不适合定义。这样重复的横切代码造成了大量代码的重复。

AOP则是利用横切技术将<u>影响多个类的公共行为封装到可重用模块</u>，并命名为Aespect。

核心关注点（业务主要的处理流程）和横切关注点（发生在核心关注点的多处，各处相似，例如权限认证，日志，事务处理）。

## 2.IOC（Inverse Of Control）依赖反转

一个对象依赖的其他对象会通过被动的方式传递进来，而不是对象自己创建或者查找依赖对象。

利用“第三方”实现具有依赖关系的对象之间的解耦。

**叫IOC的原因：**利用依赖注入DI（Denpendency Injection），本来一个类依赖的类需要自己创建或者使用，但是采用IOC之后，依赖的对象被注入到需要的地方



# MyBatis

## 1.几种分页方式

数组分页，sql分页，拦截器分页，RowBounds分页

## 2.和Hibernate

Mybatis不完全是ORM框架，可以编写原生的sql语句，灵活性高



# Redis

## 1.Redis？

可以基于内存也可以持久化的日志型，Key-Value数据库

## 2.Redis支持的数据类型

string，list，hash，set，zset

## 3.持久化的方式

**RDF（Redis Database）：**指定时间间隔对数据库进行快照存储

**AOF（Append Only File）：**每一个收到的写命令都通过write函数追加到文件中













