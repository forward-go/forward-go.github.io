---
title: Spring Boot
date: 2018-08-02 11:41:10
tags:
categories: Spring Boot
description: "Spring Boot"
---

# Spring Boot

## 一、配置类

使用@Configuration注解类

### 1. 导入额外的配置类

不需要把所有的配置放入单独的一个类中。

#### 额外配置导入方式

+ 使用@Import注解导入额外的配置类
+ 使用@ComponentScan注解自动扫描Spring components，包括@Configuration类

### 2. 配置方法

+ XML配置

如必须使用XML配置，则建议新建一个@Configuration类，然后使用@ImportResource注解加载XML配置文件

+ 基于Java的配置（推荐）

### 3. 自动配置

Spring Boot会根据你引入的jar包依赖自动配置你的Spring应用。

***启动方式***：添加@EnableAutoConfiguration或者@SpringBootApplication注解到你的@Configuration类之一

#### 3.1 替代自动配置

可以通过加入"--debug"参数开启调试日志输出到控制台查看目前应用的自动配置

#### 3.2 禁用特定的自动配置类

+ 查找到你不需要应用的自动配置类，通过配置@EnableConfiguration的"exclude"参数禁用它。

~~~java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration(proxyBeanMethods = false)
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
~~~



***注意：*** 如果指定的配置类不在classpath路径中，需指定类的全限定路径

+ 还可以通过spring.autoconfigure.exclude属性排除

## 二、Spring Beans和依赖注入

在使用Spring Boot时可以自由使用符合Spring框架标准的Bean和依赖注入技术。简单来说，我们可以通过@Component注解发现所有Bean和用@Autowired注解做构造函数注入

## 三、@SpringBootApplication的使用

单个@SpringBootApplication注解相当于启用了以下三个注解：

+ @EnableAutoConfiguration
+ @ComponentScan
+ @Configuration