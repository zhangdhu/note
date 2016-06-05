大多数 JVM 将内存区域划分为 
Method Area（Non-Heap）（方法区） ,
Heap（堆） , 
Program Counter Register（程序计数器） ,   
VM Stack（虚拟机栈，也有翻译成JAVA 方法栈的）,
Native Method Stack  （ 本地方法栈 ），

其中Method Area 和  Heap 是线程共享的  ，VM Stack，Native Method Stack  和Program Counter Register  是非线程共享的。为什么分为 线程共享和非线程共享的呢?请继续往下看。