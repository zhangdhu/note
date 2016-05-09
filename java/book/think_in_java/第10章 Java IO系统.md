第10章 Java IO系统

具有讽刺意味的是，Java的IO设计初衷实际要求避免过多的类。

三种不同的种类的IO需要考虑（文件、控制台、网络连接），而且需要通过大量不同的方式与它们通信（顺序、随机访问、二进制、字符、按行、按字等等）

InputStream（输入流）衍生的所有类都拥有名为read()的基本方法，用于读取单个字节或者字节数组。类似地，从OutputStream衍生的所有类都拥有基本方法write()，用于写入单个字节或者字节数组。

10.1.1 InputStream的类型
(1) 字节数组
(2) String对象
(3) 文件
(4) “管道”，它的工作原理与现实生活中的管道类似：将一些东西置入一端，它们在另一端出来。 (5) 一系列其他流，以便我们将其统一收集到单独一个流内。
(6) 其他起源地，如Internet连接等（将在本书后面的部分讲述）。

ByteArrayInputStream，StringBufferInputStream，FileInputStream，PipedInputString ，SequenceInputStream，FilterInputStream

10.1.2 OutputStream的类型
ByteArrayOutputStream，FileOutputStream，PipedOutputStream，FilterOutputStream

10.2 增添属性和有用的接口
装饰器方案规定封装于初始化对象中的所有对象都拥有相同的接口，以便利用装饰器的“透明”性质——我们将相同的消息发给一个对象，无论它是否已被“装饰”。

抽象的“过滤器”类是所有装饰器的基础类