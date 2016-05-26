HashTable的应用非常广泛，HashMap是新框架中用来代替HashTable的类，也就是说建议使用HashMap，不要使用HashTable。可能你觉得HashTable很好用，为什么不用呢？这里简单分析他们的区别。 

1.HashTable的方法是同步的，HashMap未经同步，所以在多线程场合要手动同步HashMap这个区别就像Vector和ArrayList一样。
2.HashTable不允许null值(key和value都不可以),HashMap允许null值(key和value都可以)。
3.HashTable有一个contains(Object value)，功能和containsValue(Object value)功能一样。
4.HashTable使用Enumeration，HashMap使用Iterator。

以上只是表面的不同，它们的实现也有很大的不同。

5.HashTable中hash数组默认大小是11，增加的方式是 old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数。

6.哈希值的使用不同，HashTable直接使用对象的hashCode，代码是这样的：
int hash = key.hashCode();
int index = (hash & 0x7FFFFFFF) % tab.length;
而HashMap重新计算hash值，而且用与代替求模：
int hash = hash(k);
int i = indexFor(hash, table.length);

static int hash(Object x) {
　　int h = x.hashCode();

　　h += ~(h << 9);
　　h ^= (h >>> 14);
　　h += (h << 4);
　　h ^= (h >>> 10);
　　return h;
}
static int indexFor(int h, int length) {
　　return h & (length-1);
}
以上只是一些比较突出的区别，当然他们的实现上还是有很多不同的，比如
HashMap对null的操作