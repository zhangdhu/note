类层次关系如下：
Collection﻿
├List
│├LinkedList
│├ArrayList
│└Vector
│　└Stack
└Set
Map
├Hashtable
├HashMap
└WeakHashMap


Collection 层次结构 中的根接口。Collection 表示一组对象，这些对象也称为 collection 的元素。

构造方法：
所有通用的 Collection 实现类（通常通过它的一个子接口间接实现 Collection）应该提供两个“标准”构造方法：
一个是 void（无参数）构造方法，用于创建空 collection；
另一个是带有 Collection 类型单参数的构造方法，用于创建一个具有与其参数相同元素新的 collection。

遍历Collection：　　　　
	Iterator it = collection.iterator(); // 获得一个迭代子
　　 while(it.hasNext()) {
　　　　　Object obj = it.next(); // 得到下一个元素
　　 }

由Collection接口派生的两个接口是List和Set。
（1）List
List是有序的Collection，使用此接口能够精确的控制每个元素插入的位置。用户能够使用索引（元素在List中的位置，类似于数组下标）来访问List中的元素，这类似于Java的数组。

List也会生成一个ListIterator（列表反复器），利用它可在一个列表里朝两个方向遍历，同时插入和删除位于列表中部的元素（同样地，只建议对LinkedList这样做）

实现List接口的常用类有LinkedList，ArrayList，Vector和Stack。
(1.1) LinkedList类
LinkedList 提供优化的顺序访问性能，同时可以高效率地在列表中部进行插入和删除操作。但在进行随机访问时，速度却相当慢
(1.2)ArrayList
允许我们快速访问元素，但在从列表中部插入和删除元素时，速度却嫌稍慢。
不要用它删除和插入元素；与LinkedList相比，它的效率要低许多
(1.3)Vector
Vector非常类似ArrayList，但是Vector是同步的。
(1.4)Stack
Stack继承自Vector，实现一个后进先出的堆栈。
set
Set是一种不包含重复的元素的Collection
HashSet＊ 用于除非常小的以外的所有Set。对象也必须定义hashCode()
ArraySet 由一个数组后推得到的Set。面向非常小的Set设计，特别是那些需要频繁创建和删除的。对于小Set，与HashSet相比，ArraySet创建和反复所需付出的代价都要小得多。但随着Set的增大，它的性能也会大打折扣。不需要HashCode()


Map接口

Hashtable类
Hashtable继承Map接口，实现一个key-value映射的哈希表。

HashMap和Hashtable类似，不同之处在于HashMap是非同步的，并且允许null

WeakHashMap是一种改进的HashMap，它对key实行“弱引用”，


HashMap＊ 基于一个散列表实现（用它代替Hashtable）。针对“键－值”对的插入和检索，这种形式具有最稳定的性能。可通过构建器对这一性能进行调整，以便设置散列表的“能力”和“装载因子”
ArrayMap 由一个ArrayList后推得到的Map。对反复的顺序提供了精确的控制。面向非常小的Map设计，特别是那些需要经常创建和删除的。对于非常小的Map，创建和反复所付出的代价要比HashMap低得多。但在Map变大以后，性能也会相应地大幅度降低



问题：
1、Hashtable和HashMap的区别?
最重要的不同是Hashtable的方法是同步的，而HashMap的方法不是.
还有一点不同是，只有HashMap可以让你将空值作为一个表的条目的key或value。HashMap中只有一条记录可以是一个空的key，但任意数量的条目可以是空的value
一些资料建议，当需要同步时，用Hashtable，反之用HashMap。但是，因为在需要时，HashMap可以被同步，HashMap的功能比Hashtable的功能更多，而且它不是基于一个陈旧的类的，所以有人认为，在各种情况下，HashMap都优先于Hashtable。

2、ArrayList和Vector的区别
　　 1>同步性：Vector是线程安全的，也就是说是同步的，而ArrayList是线程序不安全的，不是同步的
	2>数据增长：当需要增长时，Vector默认增长为原来一培，而ArrayList却是原来的一半。

       首先看这两类都实现List接口，而List接口一共有三个实现类，分别是ArrayList、Vector和LinkedList。List用于存放多个元素，能够维护元素的次序，并且允许元素的重复。3个具体实现类的相关区别如下：

    1、ArrayList是最常用的List实现类，内部是通过数组实现的，它允许对元素进行快速随机访问。数组的缺点是每个元素之间不能有间隔，当数组大小不满足时需要增加存储能力，就要讲已经有数组的数据复制到新的存储空间中。当从ArrayList的中间位置插入或者删除元素时，需要对数组进行复制、移动、代价比较高。因此，它适合随机查找和遍历，不适合插入和删除。
    2、Vector与ArrayList一样，也是通过数组实现的，不同的是它支持线程的同步，即某一时刻只有一个线程能够写Vector，避免多线程同时写而引起的不一致性，但实现同步需要很高的花费，因此，访问它比访问ArrayList慢。
    3、LinkedList是用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和遍历速度比较慢。另外，他还提供了List接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆栈、队列和双向队列使用。
    4、查看Java源代码，发现当数组的大小不够的时候，需要重新建立数组，然后将元素拷贝到新的数组内，ArrayList和Vector的扩展数组的大小不同。

3、Collection 和Collections的区别。
　　Collections是个java.util下的类，它包含有各种有关集合操作的静态方法。
　　Collection是个java.util下的接口，它是各种集合结构的父接口。

4、数组(Array)和列表(ArrayList)有什么区别？
下面列出了Array和ArrayList的不同点： 
    1）、Array可以包含基本类型和对象类型，ArrayList只能包含对象类型。 
    2）、Array大小是固定的，ArrayList的大小是动态变化的。 
    3）、ArrayList提供了更多的方法和特性，比如：addAll()，removeAll()，iterator()等等。 
    4）、对于基本类型数据，集合使用自动装箱来减少编码工作量。但是，当处理固定大小的基本数据类型的时候，这种方式相对比较慢。


















