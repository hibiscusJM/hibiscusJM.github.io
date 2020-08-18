---
title: Spring && SpringBoot
tags: Spring  SpringBoot
renderNumberedHeading: true
grammar_cjkRuby: true
---


# 一、SpringBoot
   Spring尽管已经利用IOC和AOP实现了轻量级的java开发，但其组件是轻量级的，配置仍然是重量级的，尽管可以使用组件扫描和自动装配实现自动配置，但这仍然是部分，某些功能仍然需要借助XML或Java进行显式配置，比如事务管理和SpringMVC、或者使用第三方库时仍然需要进行显式配置；另外项目的依赖管理也很麻烦，比如需要决定使用哪些库，还需要判断使用哪个版本，如果版本不兼容会出现很大问题，这些问题仍然很麻烦，因此在Spring之上构建了全新的开发模型SpringBoot，移除了开发Spring应用中很多单调乏味的内容。
   SpringBoot中主要提供了四个主要的功能：
 1. 自动配置：
    Spring Boot会为常见配置场景进行自动配置，比如数据库、安全、SpringMVC等。
 2. starter起步依赖：
    Spring Boot通过起步依赖为项目的依赖管理提供帮助，起步依赖借助于传递依赖解析把常用库聚合在一起，组成了几个为特定功能而定制的依赖。我们在开发中需要使用某项功能时，可以直接在构建文件中添加依赖项，不用考虑这种功能具体要用什么库，也不用考虑版本。
 3. 命令行接口：
    Spring Boot CLI利用了起步依赖和自动配置，可以快速开发Spring应用程序，它是非必要组成部分。
 4. Actuator：
    该模块可以提供在运行时检视应用程序内部情况的能力。

# 二、Spring Boot说明
  可以使用Maven或Gradle构建应用程序，这两类项目在构建Spring Boot应用程序时都包含：
 - 构建说明文件，其中Gradle项目对应build.gradle文件，Maven项目对应pom.xml文件；
 - Application.java：引导启动应用程序；
 - ApplicationTests.java:测试类；
 - application.properties：也可以改为.yaml文件，在这个文件里可以根据需要添加配置属性。
  其中Application.java文件中的@SpringBootApplication开启了Spring的组件扫描和Spring Boot的自动配置功能，实际上该注解将三个注解组合在了一起：
 - Spring的@Configuration：表明该类使用Spring基于Java的配置；
 - Spring的@ComponentScan：启用组件扫描；
 - SpringBoot的@EnableAutoConfiguration：该注解开启了SpringBoot的自动配置。
  Spring Boot为Gradle和Maven提供了构建插件，以便辅助构建项目，在构建说明文件中应用了Spring Boot的Gradle插件或Maven插件，构建插件的主要功能是把项目打包成一个可执行的JAR，包括把所有依赖打入JAR文件内，并为Jar添加一个描述文件；Gradle没有Maven的依赖管理功能，build.gradle里没有为各项依赖指定版本，而pom.xml文件中将spring-boot-starter-parent作为上一级，这样就可以利用Maven的依赖管理功能，继承很多常用库的依赖版本，就不用指定版本号了。

