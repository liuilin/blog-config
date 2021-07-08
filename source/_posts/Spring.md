---
title: Spring
date: 2021-03-08 15:16:13
tags:
---
# Spring

### IOC

程序的耦合：程序间的依赖关系
包括：类之间的依赖、方法间的依赖
解耦：降低程序间的依赖关系
实际开发中应该做到：编译期不依赖，运行时才依赖。

> 就是要做到要new的类删掉以后，编译期不让它报错

解耦的思路：
第一步：使用反射来创建对象，而避免使用new关键字

> private IAccountDao accountDao=new AccountDaoImpl();

第二步：通过读取配置文件来获取要创建的对象全限定类名

Bean：在计算机英语中，有可重用组件的含义。
JavaBean：用java语言编写的可重用组件。javabean>实体类
一个创建Bean对象的工厂，它就是创建我们的service和dao对象的，两种方式：
i.需要一个配置文件来配置我们的service和dao配置的内容：唯一标识=全限定类名（key=value）
ii.通过读取配置文件中配置的内容，反射创建对象

我的配置文件可以是xml也可以是properties