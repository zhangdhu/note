ServletContext.md


1.Servlet接口实现类的内容：
    Servlet接口SUN公司定义了两个默认实现类，分别为：GenericServlet、HttpServlet
　
HttpServlet指能够处理HTTP请求的servlet，它在原有Servlet接口上添加了一些与HTTP协议处理方法，它比Servlet接口的功能更为强大。因此开发人员在编写Servlet时，通常应继承这个类，而避免直接去实现Servlet接口。

　　HttpServlet在实现Servlet接口时，覆写了service方法，该方法体内的代码会自动判断用户的请求方式，如为GET请求，则调用HttpServlet的doGet方法，如为Post请求，则调用doPost方法。因此，开发人员在编写Servlet时，通常只需要覆写doGet或doPost方法，而不要去覆写service方法。

。对于每次访问请求，Servlet引擎都会创建一个新的HttpServletRequest请求对象和一个新的HttpServletResponse响应对象，然后将这两个对象作为参数传递给它调用的Servlet的service()方法，service方法再根据请求方式分别调用doXXX方法。

阅读ServletConfig API，并举例说明该对象的作用：

获得字符集编码

获得数据库连接信息

获得配置文件，查看struts案例的web.xml文件

４.ServletContext的内容：

WEB容器在启动时，它会为每个WEB应用程序都创建一个对应的ServletContext对象，它代表当前web应用。

ServletConfig对象中维护了ServletContext对象的引用，开发人员在编写servlet时，可以通过ServletConfig.getServletContext方法获得ServletContext对象。




WEB容器在启动时，它会为每个WEB应用程序都创建一个对应的ServletContext对象，它代表当前web应用。
   ServletConfig对象中维护了ServletContext对象的引用，开发人员在编写servlet时，可以通过ServletConfig.getServletContext方法获得ServletContext对象。

由于一个WEB应用中的所有Servlet共享同一个ServletContext对象，因此Servlet对象之间可以通过ServletContext对象来实现通讯。ServletContext对象通常也被称之为context域对象。

1.多个Servlet通过ServletContext对象实现数据共享。

在InitServlet的Service方法中利用ServletContext对象存入需要共享的数据

/*获取ServletContext对象*/  

ServletContext context = this.getServletContext();   

//存入共享的数据    

context.setAttribute("name", "haha"); 

2.获取WEB应用的初始化参数。

在web.xml文件中配置需要初始化的参数信息。

<web-app>   

 <context-param>   

<param-name>url</param-name>   

<param-value>jdbc:MySQL://localhost:3306/4g</param-value>   

 </context-param>   

<context-param>   

2.实现Servlet的转发：

在测试的Servlet中实现转发的步骤如下:  

/*要利用ServletContext对象实现转发获取对象*/  

ServletContext context = this.getServletContext();   

 //在request对象中存入name属性    

request.setAttribute("name", "haha");   

 /*根据转发的地址获取 RequestDispatcher对象*/  

RequestDispatcher  rd  = context.getRequestDispatcher("/index.jsp");   

3.利用ServletContext对象读取资源文件。  

读取资源文件(properties文件（属性文件）)的三种方式

配置的properties的内容如下:   

url=jdbc\:mysql\://localhost\:3306/3g ; 







