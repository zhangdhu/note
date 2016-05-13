Servlet.md

Servlet 是什么？
Java Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。
使用 Servlet，您可以收集来自网页表单

Servlet 生命周期

Servlet 生命周期可被定义为从创建直到毁灭的整个过程。以下是 Servlet 遵循的过程：
Servlet 通过调用 init () 方法进行初始化。
Servlet 调用 service() 方法来处理客户端的请求。
Servlet 通过调用 destroy() 方法终止（结束）。
最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。