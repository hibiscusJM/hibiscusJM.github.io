---
title: SpringBoot中的各种依赖
tags: javaProject 
        SpringBoot
renderNumberedHeading: true
grammar_cjkRuby: true
---


# pom.xml中的各种依赖
根据项目的需求，在IDEA中搭建好项目环境后在pom.xml中添加各种依赖：
1. <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
	这是pom.xml文件中默认的父级依赖，这样当前的项目就是一个springBoot项目了，而且可以提供相关的Maven默认依赖，使用它之后，常用的包依赖就可以省掉version信息也可以做到版本兼容
2. 为了使用数据库并进行操作需要添加以下几个依赖：
   <dependency>
		   <groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
   </dependency>
    <dependency>
		   <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
   </dependency>
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
     </dependency>
	 另外需要在application.yml文件中添加相应的数据库信息;
3. 因为这是一个web项目，所以需要添加web依赖
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
4. 添加yaml依赖，默认的配置文件是application.properties文件，这里改成yaml文件，更具备可读性：
   <dependency>
            <groupId>org.yaml</groupId>
            <artifactId>snakeyaml</artifactId>
            <version>1.10</version>
    </dependency>
5. 添加配置依赖，实现对象属性的自动配置
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
    </dependency>
6. 添加lambok依赖，为了方便实体类bean快速生成get set方法,从而不用手动添加
   <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
7. 添加json依赖，实现序列化与反序列化
   <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.31</version>
        </dependency>
8. 添加自动配置jar包依赖
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-autoconfigure</artifactId>
        </dependency>
9. 添加kafka依赖
    <dependency>
            <groupId>org.springframework.kafka</groupId>
            <artifactId>spring-kafka</artifactId>
            <version>1.1.1.RELEASE</version>
        </dependency>
10. 添加test依赖，完善测试用例
    <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
11. 添加工具包
    <dependency>
            <groupId>commons-lang</groupId>
            <artifactId>commons-lang</artifactId>
            <version>2.2</version>
        </dependency>