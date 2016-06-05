1、
静态include主要是对静态页面的引入，不会检查所包含文件的变化
<% @ include file="include.html" %>
2、
<jsp：include>动作包含的属性：
page：指定所包含资源的相对url路径，该资源必须时同一web应用程序的组成部分。
flush：指定在执行include动作后是否应刷新缓冲区，在jsp1.1中，该属性必须设置为真。


