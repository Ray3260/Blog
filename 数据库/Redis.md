## Redis 简介
* Redis是一个基于C语言开发的开源NoSQL数据库，他的数据是保存在内存中的，读写速度快，被广泛用于分布式缓存方向，存储键值对数据。
* Redis提供了多种数据类型实现（String、List、Set、Hash、zset、HyperLogLog、Bitmap、GeoSpatial）。

## Redis为什么快
* 基于内存，访问速度快。
* 基于Reactor模式设计开发了一套高效的事件处理模型，单线程事件循环和IO多路复用。
* 多种优化过后的数据类型/结构，性能高。
![image](https://github.com/Ray3260/Blog/assets/41173822/ca65a39f-772f-4f9a-a02b-4f645f4b22d6)

## Redis 和 Memcached
* 相同点：1. 基于内存的数据库，一般用来当做缓存使用。2. 都有过期策略。3. 两者的性能都很高
* Redis支持更加丰富的数据类型
* Redis支持数据的持久化，可以将内存中的数据保持在磁盘上。
* Redis有灾难恢复机制。
* Redis在服务器内存使用完之后，可以将不同的数据放到磁盘上。
* memcached没有原生的集群模式，需要依靠客户端来实现往集群中分片写入数据。Redis目前是原生支持Cluster模式的。
* Memcached是多线程，非阻塞IO复用的网络模型。Redis是单线程的多路IO复用模型。
* Redis支持发布订阅模型、Lua脚本、事务等功能。
* Redis同时使用了惰性删除与定期删除。

## Redis除了缓存，还可以应用于
* 分布式锁，基于Redisson来实现分布式锁。
* 限流：一般使用Redis+Lua脚本的方式来限流。
* 消息队列：Redis自带的List数据结构可以作为一个简单的队列使用。
* 延时队列：Ression内置了延时队列（基于Sorted Set实现的）。
* 分布式Session：利用String或者Hash数据类型保存Session数据，所有服务器都可以访问。
* 复杂业务场景：通过Redis以及redis扩展提供的数据结构，可以方便的完成很多复杂的业务场景。

## Redis持久化机制
* 支持三种持久化机制：快照（RDB）、只追加文件（AOF）、RDB和AOF混合持久化
* RDB持久化：通过创建快照来获取存储在内存的数据在某个时间点的副本，redis默认持久化方法。生成快照命令：1.save：同步保存操作，会阻塞redis主进程。2.bgsave：fork出子进程不阻塞，默认选项。
* AOF持久化：持久化的实时性更好，开启后每执行一条更改redis数据的命令，该命令会被写到AOF缓冲区中，然后再写到AOF文件中。
![image](https://github.com/Ray3260/Blog/assets/41173822/4af7e823-fa62-48a0-8f36-09c8b6453dfa)

## Redis线程模型
* Redis基于Reactor模式设计开发了一套高效的事件处理模型。
* 单线程模型如何监听大量客户端连接：IO多路复用程序。
![image](https://github.com/Ray3260/Blog/assets/41173822/2d86a183-e1da-48b7-bcf9-c0eaad36c014)
