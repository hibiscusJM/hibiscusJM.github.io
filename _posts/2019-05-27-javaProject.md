---
title: javaProject
tags:
       javaProject
renderNumberedHeading: true
grammar_cjkRuby: true
---
**Java卡包项目**
==环境需求 #03A9F4==：
 

 1. ==<i class="fas fa-coffee"></i> #FF9800==java1.8
 2. ==<i class="fas fa-feather-alt"></i> #4CAF50==Springboot
 3. ==<i class="far fa-hand-point-right"></i> #FF5722==Hbase
 4. ==<i class="fas fa-sitemap"></i> #00BCD4==Mysql
 5. ==<i class="fas fa-piggy-bank"></i> #80004c==Redis(缓存框架）
 6. ==<i class="far fa-comments"></i> #E91E63==Kafka(消息队列）

==技术分层 #03A9F4==：

 1. 框架层：java1.8+Springboot
 	 Springboot：实现自动配置、内置tomcat
 2. 存储层：Mysql+Hbase+Redis
 3. 消息队列：Kafka
 
==基础工具 #03A9F4==：

 1. Maven：规范项目、实现持续集成
 2. PostMan：接口测试
 3. TextLab：代码、文本验证、格式化工具，主要用来验证json文件格式