今天在看Spring的源码的时候不知道从什么地方开启应该合适，因为不太清楚实现类所在的具体Jar包，就从网上找了些，可是网上有的说的是不清不楚，甚至是有些错误的，所以就把相关Jar包的大致作用给整理了一遍，做个笔记吧。

1.spring-aop-3.2.2.jar  

包含在应用中使用Spring的AOP特性时所需的类。

2.spring-aspects-3.2.2.jar  

提供对AspectJ的支持，以便可以方便的将面向方面的功能集成进IDE中

3.spring-beans-3.2.2.jar 

springIoC（依赖注入）的基础实现，所有应用都要用到的，它包含访问配置文件、创建和管理bean以及进行Inversion of Control / Dependency Injection（IoC/DI）操作相关的所有类。但是这个是个基础实现，一般我们在实际的开发过程中很少直接用到，它是对起到支撑作用的。

4.spring-context-3.2.2.jar

为Spring核心提供了大量扩展。可以找到使用Spring ApplicationContext特性时所需的全部类，JDNI所需的全部类，UI方面的用来与模板(Templating)引擎如 Velocity、FreeMarker、JasperReports集成的类，以及校验Validation方面的相关类，还有ejb,cache,format,jms等等。

5.spring-context-support-3.2.2.jar  

spring-context 的扩展支持，用于 MVC 方面

6.spring-core-3.2.2.jar 

spring的核心包，包含Spring框架基本的核心工具类，Spring其它组件要都要使用到这个包里的类，是其它组件的基本核心。包括ASM，CGLIB以及相关的工具类

7.spring-expression-3.2.2.jar 

spring表达式语言。

8.spring-instrument-3.2.2.jar 

spring对服务器的代理接口。

9.spring-instrument-tomcat-3.2.2.jar 

spring对tomcat连接池的集成。

10.spring-jdbc-3.2.2.jar 

spring对jdbc的简单封装

11.spring-jms-3.2.2.jar 

spring对jms(java message service)的封装，为了简化对JMS API的使用

12.spring-orm-3.2.2.jar 

包含Spring对DAO特性集进行了扩展，使其支持 iBATIS、JDO、OJB、TopLink，因为Hibernate已经独立成包了，现在不包含在这个包里了。这个jar文件里大部分的类都要依赖spring-dao.jar里的类，用这个包时你需要同时包含spring-dao.jar包。spring 整合第三方的 ORM 映射支持，如 Hibernate 、Ibatis、Jdo 以及spring的JPA的支持。

13.spring-oxm-3.2.2.jar

spring 对Object/XMI 的映射的支持，可以让JAVA与XML之间来回切换。

14.spring-struts-3.2.2.jar

Struts框架支持，可以更方便更容易的集成Struts框架。

15.spring-test-3.2.2.jar

spring对JUnit框架的简单封装。

16.spring-tx.3.2.2.jar

spring提供对事务的支持，事务的相关处理以及实现类就在这个Jar包中

17.spring-web-3.2.2.jar

包含Web应用开发时，用到Spring框架时所需的核心类，包括自动载入WebApplicationContext特性的类、Struts与JSF集成类、文件上传的支持类、Filter类和大量工具辅助类。

18.spring-webmvc-3.2.2.jar 

spring mvc相关，实现SpringMVC的操作。

19.spring-webmvc-portlet-3.2.2.jar

spring mvc的增强扩展。

