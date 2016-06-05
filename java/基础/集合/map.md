HashMap、HashTable、ConcurrentHashMap的区别
 
1、HashMap和HashTable都实现了Map接口，里面存放的元素不保证有序，并且不存在相同元素；
    参考HashMap与HasTable的区别.md
2、TreeMap、HashMap、LinkedHashMap的区别
    关于Map集合，前面几篇都有讲过，可以去回顾一下。而TreeMap、HashMap、LinkedHashMap都是Map的一些具体实现类，其关系图如下：

    （1）LinkedHashMap保存了数据的插入顺序，底层是通过一个双链表的数据结构来维持这个插入顺序的。key和value都可以为null；
    （2）TreeMap实现了SortMap接口，它保存的记录是根据键值key排序，默认是按key升序排列。也可以指定排序的Comparator。





