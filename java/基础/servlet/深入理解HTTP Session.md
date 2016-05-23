server端程序调用 HttpServletRequest.getSession(true)这样的语句时才被创建

Session删除的时间是：
1）Session超时：超时指的是连续一定时间服务器没有收到该Session所对应客户端的请求，并且这个时间超过了服务器设置的Session超时的最大时间。
2）程序调用HttpSession.invalidate()
3）服务器关闭或服务停止

session保存在服务器内存中。

session会因为浏览器的关闭而删除吗？
不会，session只会通过上面提到的方式去关闭。
