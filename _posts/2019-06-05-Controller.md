---
title: Controller
tags: Java  MVC
renderNumberedHeading: true
grammar_cjkRuby: true
---


# Controller层
 1.  首先Controller层是表示层，也就是接收用户请求以及返回请求结果，该层不包含业务逻辑，功能有以下五点：
   
 - （1）参数校验
 -    （2）调用service层接口
 -    （3）转换数据对象
 -    （4）组装返回对象
 -    （5）异常处理
 2.  controller层常用的注解：
   
 - （1）@RestController：相当于@Controller+@Responsebody，@Controller注解表明这是一个控制器类，还需要在spring容器中创建该类的实例才能注入bean；
 -    （2）@RequestMapping：将控制器类注入到Spring容器中后还需要添加注解@RequestMapping，这个注解时用来映射请求的，即指明处理器可以用来处理哪些URL请求；该注解可以用在类上，也可以用在方法上
 -    （3）@PathVariable：@RequestMapping的地址可以是url变量，通过该注解可以获取作为方法的参数；
 -    （4）@Reponsebody：前面说到@RestController=@Conller+@Reponsebody，@ReponseBody就是表示方法的返回值以指定的格式写入http response body中，而不是解析为跳转路径。
 -    所以当要求方法返回json数据，而不是跳转页面时，可以直接标注@RestController。
 -    （5）@RequestBody：该注解用来接收前端传递给后端的json字符串中的数据（请求体中的数据），因为GET方式无请求体，所以使用@RequestBody接收数据时，前端不能用GET方式提交数据，而是用POST方式提交。
 -    （6）@GetMapping、@PostMapping、@PutMapping、@DeleteMapping、@PatchMapping：看这几个注解的名字肯定和@RequestMapping有关系，实际上早期只有@RequestMapping来处理请求，为了区分不同的请求方式通常需要在注解中添加参数method=RequestMethod.GET；那么有了这几种mapping注解后，就可以在不同的方法上根据请求方式使用不同的注解。
 3.   http请求的几种方式：
   因为controller层对应前端发送的请求，如上文所示，一些注解也根据请求不同而使用，因此这里对http的几种请求方式做一下简单总结，网上查到http的请求方式很多都写8种，但是目前已经增加到15种：
   
 - （1）GET：请求指定的页面信息，并返回主体；
 -    （2）POST：向指定资源提交数据进行处理请求，数据被包含在请求体中，POST请求可能会导致新的资源建立或修改；

   POST和GET是最常见的两种请求方法，二者在使用上也有所不同：
  

 - a)安全性： GET是不安全的，因为它直接将数据放到请求的URL中；post是安全的，它将其放在请求体中，就相当于运送货物的卡车，get方法是直接将货物绑在车顶，而post是放在车厢里的；但是二者都是http的请求方式，而http本身就是不安全，因此安全的唯一手段就是使用https.
 -    b)数据量：get传送的数据量较小，受到URL的长度限制，而post一般不受限制；
 -    c)编码限制：get中必须为ASCII字符，post不受限制；
 -    d)执行效率：get是表单默认的提交方法。

   但是get和post的这些区别又都不能算作标准，这个链接中的回答很详细的从更广的层面上区分了get和post: https://www.zhihu.com/question/28586791
   

 - （3）HEAD：类似于GET请求，只不过返回的响应中没有具体的内容，用于获取报头；
 -    （4）PUT：从客户端向服务器传送的数据取代指定的文档的内容；
 -    （5）DELETE：请求服务器删除指定的页面；
 -    （6）CONNECT：http1.1中预留给能够将连接改为管道方式的代理服务器；
 -    （7）OPTIONS：允许客户端查看服务器的性能；
 -    （8）TRACE：回显服务器收到的请求，主要用于测试或诊断；
 -    （9）PATCH：对PUT方法的补充，用来对已知资源进行局部更新；
 -    （10）MOVE：请求服务器将指定页面移动至另一个网络地址；
 -    （11）COPY：请求服务器将制定的页面拷贝至另一个网络地址；
 -    （12）LINK：请求服务器建立连接关系；
 -    （13）UNLINK：断开连接关系；
 -    （14）WTAPPED：允许客户端发送经过封装的请求；
 -    （15）Extension-mothed：在不改动协议的前提下，可增加另外的方法。