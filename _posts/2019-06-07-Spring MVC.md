---
title:Spring MVC
tags: Spring   MVC
renderNumberedHeading: true
grammar_cjkRuby: true
---

# 一、Spring MVC web框架
 Spring  MVC基于模型-视图-控制器模式实现，当用户提交请求时，其Spring MVC会将请求传送至每个组件，从离开浏览器到获取响应返回，其过程如下：
1. “DispatcherServlet”:
       在请求离开浏览器时，会先到达DispatcherServlet，即前端控制器，它的任务就是将请求发送给Spring MVC控制器，控制器是处理请求的Spring组件；
2.  处理器映射：
     因为在一个应用中会有很多控制器组件，DispatcherServlet需要知道应该将请求发送给哪个控制器，所以会查询一个或多个处理器映射来确定请求的下一站在哪里，处理器映射会根据请求携带的URL信息来进行决策；
3.  控制器：
    选择好合适的控制器后，DispatcherServlet会将请求发送给选中的控制器，到了控制器，请求就会卸下用户提交的信息并耐心等待控制器处理这些信息，一般控制器会将业务逻辑的实现委托给服务对象处理；
4. 模型及逻辑视图名：
   控制器完成逻辑处理后会产生一些信息，这些信息需要返回给用户并在浏览器上显示，这些信息就被称为模型（Model)，一般来说这些信息还需要进行格式化，所以需要将信息发送给一个视图（view,通常是JSP页面），所以控制器会将模型数据打包并标识出用于渲染输出的视图名，然后将请求连同模型和视图名发送回DispatcherServlet。
5. 视图解析器：
   控制器传递给DispatcherServlet的视图名并不直接表示某个特定的JSP，仅仅传递了一个逻辑名称，使用这个名称去查找产生结果的真正视图，所以DispatcherServlet会使用视图解析器将逻辑视图名匹配为一个特定的视图实现。
6. 视图：
   经过第5步，DispatcherServlet已经知道由哪个视图渲染结果，此时就将模型数据交付给它，视图将使用模型数据渲染输出。
7. 响应
   最后渲染完成的输出通过响应对象传递给客户端。

# 二、实现Spring MVC
1.  配置DispatcherServlet
   DispatcherServlet（前端控制器）是SpringMVC的核心。
   servlet：是运行在Web服务器或应用服务器上的程序，是作为来自Web浏览器或其他HTTP客户端的请求和HTTP服务器上的数据库或应用程序之间的中间层，服务器具体对接收请求作出响应的工作是由Servlet完成的，但是Servlet配置过于繁琐，且HTTP协议传输的数据都是文本形式，需要进行大量的数据类型转换，因此Servlet显得非常低效和落后，因此对servlet做了很多改进。
 - 演进1：GenericServlet抽象类，在该类的帮助下，只需要重写service方法即可，不需要将servlet接口的所有方法实现；
 - 演进2：HTTPServlet抽象类覆盖了GenericServlet类；
 - 演进3：JSP的加入，避免了在servlet类中编写大量复杂的HTML代码；
 - 演进4：Spring
 - 演进5：Spring Web模块-Spring MVC，使用Servlet完成复杂的功能时，需要编写多个Servlet类，并且还要在xml中进行注册，配置过于繁琐，而SpringMVC实现了简单配置。
  DispatcherServlet的配置方式：
 - 传统方法：使用web.xml文件
 - 使用java配置；
 
2. 启用Spring MVC
   可以有多种方式启用Spring MVC：
   （1）使用XML；
   （2）使用<mvc：annotation-driven>启用注解驱动的Spring MVC；
   （3）基于Java进行配置：使用@EnableWebMvc注解，但仅仅使用该注解没有配置视图解析器、没有启用组件扫描、同时DispatcherServlet会映射为应用的默认Servlet则会处理所有请求包括对静态资源的请求，因此还要在该配置类中添加@ComponentScan 注解开启自动扫描，再添加一个视图解析器的bean，同时扩展方法处理静态资源将静态资源转发到Servlet容器中默认的Servlet上，而不是DispatcherServlet本身处理此类请求。
   
3.  编写控制器
   在类上添加@Controller注解，声明该类是控制器，与@Compoent注解相差不大，辅助实现组件扫描。控制器只是在方法上添加了@RequestMapping注解，这个注解就表明了它们索要处理的请求，其中注解内可使用value属性指定方法所要处理的请求，method属性细化了所使用的HTTP方法，比如Get\post。@RequestMapping注解还可以放在类级别上，会应用到所有处理器方法上，当类级别上的注解属性与方法级别属性合并后，该方法执行对应的请求。也可以在控制器类中将模型数据传入到视图中。

# 三、SpringMVC接受请求
Spring MVC允许以多种方式将客户端中的数据传送到控制器的处理器方法中，包括：
 1. 查询参数
   在方法中的参数前添加@RequestParam，即请求中需要填写对应的查询参数，通过这种方式可以向控制器中传递信息，另外一种方式就是将传递参数作为请求路径的一部分；
 2. 路径变量
   上一种方式中，处理器方法将会处理如“/user/show?id=123”这样的请求，这种方式也可以正常工作，但从面向资源的角度看这并不理想，要识别的资源应该通过URL路径进行标识即“user/123”发起请求，实现这种路径变量：
   在@RequestMapping路径中添加占位符，同时在方法的参数上添加@PathVariable注解，表明在请求路径中不管占位符部分的值是什么都会传递给处理器方法的参数中
 3. 表单参数
   处理注册表单的POST请求，控制器接受表单数据并将表单数据保存为对象，还可以为表单提交添加校验

