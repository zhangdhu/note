#ServletConfig

容器初始化一个servlet时，会为这个servlet建一个唯一的ServletConfig。容器从DD读出Servlet初始化参数，并把这些参数交给ServletConfig，然后把ServletConfig传递给servlet的init(ServletConfig config)方法。也就是说容器只有在创建servlet实例时才会读DD文件中的init-param，并且在servlet一生中只读一次。

在实际应用过程中，为了便于修改我们并不希望直接把某一变量硬编码到servlet类中，这个时候就会用到ServletConfig接口。我们可以把某些变量放在DD(web.xml)中,这样如果我们要修改某一值，可以直接改动DD文件即可。

在DD文件(web.xml)中：

    <servlet>
        <servlet-name>ServletConfigTest</servlet-name>
        <servlet-class>com.guo.ServletConfigTest</servlet-class>
        <init-param>
            <param-name>color</param-name>
            <param-value>red</param-value>
        </init-param>
     </servlet>
在servlet代码中:

 out.println(getServletConfig().getInitParameter("color"));

在这里先屡屡他们之间的关系，首先HttpServlet继承自GenericServlet类，而GenericServlet类又继承自Servlet接口，Servlet接口有方法getServletConfig() ，所以HttpServlet肯定有方法getServletConfig() 。

而GenericServlet类又实现了ServletConfig 接口，也就是他肯定实现了ServletConfig接口中的所有方法，所以以上代码我们还可以这样写：


out.println(getInitParameter("color"));

 

在这里我们来看看ServletConfig中的方法：

getInitParameter(String   name)：根据给定的初始化参数，返回匹配的初始化参数值。
getInitParameterNames()：返回一个Enumeration对象，里面包含了所有的初始化参数。
getServletContext()：返回一个servletContext()对象.
getServletName()：返回servlet的名字，即web.xml中的<servlet-name>的子元素的值。如果没有配置这个子元素，则返回servlet类的名字。




