![image](https://github.com/Ray3260/Blog/assets/41173822/32ac419e-084e-44c8-a7db-331f89354234)

* java集合，容器，主要是由两大接口派生而来，一个是Collection接口，用于存储单一元素， 另一个是Map接口，用于存放键值对。
* Collections，有List、Set、Queue三个子接口
* Map，有HashMap、HashTable、SortedMap(接口)

##  ArrayList扩容机制
* 底层是动态数组，使用无参构造方法会赋值一个空数组，默认容量为10，当add触发自动扩容时调用grow()方法，默认扩容1.5倍。

## Comparable 和 Comparator 区别
* 都是java中用于排序的接口。
* Comparable 来自java.lang包，提供compareTo(Object obj)方法用来排序。
* Comparator 来自java.util包，提供compare(Object o1, Object o2)方法用来排序。

## HashSet、LinkedHashSet和TreeSet
* 都是Set接口的实现类，都能保证元素唯一性，并且都不是线程安全的。
* 底层数据结构不同，HashSet基于HashMap实现，LinkedHashSet基于链表和哈希表实现，
元素的添加和拿出满足FIFO，TreeSet基于红黑树实现，元素是有序的，有自然排序和定制排序。

## Queue 和 Deque
* Queue是单端队列，遵循FIFO规则，扩展了Collections接口。
* Deque是双端队列，在队列两端均可以插入和删除元素，扩展了Queue接口。

## ArrayDeque 和 LinkedList
* 都实现了Deque接口，都具有队列的功能。
* ArrayDeque是基于可变长的数组和双指针来实现，LinkedList通过链表来实现。
* ArrayDeque不支持存储null数据，LinkedList可以。
* ArrayList虽然有扩容机制但是比LinkedList性能要好，LinkedList每次插入数据需要申请新的堆空间。

## PriorityQueue
* 利用二叉堆的数据结构来实现，底层使用可变长的数组来存储数据。
* 线程非安全的，不支持null和non-comparable对象。
* 默认是最小堆，可以自定义排序方式（new comparato）

## HashMap 和 HashTable
|区别|线程是否安全|效率|对null key和null value的支持|初始容量、扩容|底层数据结构|
|:--:|:--:|:--:|:--:|:--:|:--:|
|HashMap|线程不安全|高|可以存储null，作为key只能有一个|初始16，扩容为2倍，若创建时给初始值，则会扩充其为2的幂次方大小|数组+链表，当链表长度大于8时转为红黑树（先判断数组是否大于64，否则先扩容）|
|HashTable|线程安全|低（基本淘汰）|不允许null出现|默认11，扩容为2n+1|数组+链表|

## HashMap的线程不安全
* 扩容机制会造成死循环和数据丢失问题，不适合多线程下使用。
* 死循环例子（1.7之前头插法）
    * 当一个桶位中有多个元素需要进行扩容时，多个线程同时对链表进行操作，头插法导致节点指向错误的位置，从而形成一个环形链表，陷入死循环。
    * 1.8之后采用尾插法是的插入元素永远在链表的尾部，避免了环形结构。
* 数据覆盖例子：
    * 当两个线程1、2同时进行put操作，并且发生了hash冲突
    * 不同的线程可能在不同的时间片获得CPU执行的机会，当线程1执行完哈希冲突判断后，由于时间片耗尽挂起。线程2先完成了插入操作。
    * 随后，线程1获得时间片，由于之前已经判断过hash冲突，所以此时直接进行插入，导致线程2插入的数据被线程1覆盖。

## ConcurrentHashMap
* 线程安全的HashMap，1.7使用分段数组+链表，1.8之后使用数组+链表/红黑树
* 实现线程安全的方式
    * 1.7时对整个桶数组进行了分割分段（segment，分段锁）
    * 1.8直接使用node数组+链表+红黑树，并发控制使用synchronized和CAS来操作。
