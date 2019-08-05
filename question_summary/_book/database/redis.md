# redis

* 哨兵机制？

    是用来监控redis集群中master状态的工具，是实现redis高可用的一种解决方案。

* redis默认端口号？ 6379

* 支持的数据类型？

    String

    Hash

    List

    Set

    ZSet

* 什么是redis持久化?有哪几种持久化机制？
  
  持久化就是将数据写入磁盘，防止数据丢失。
  
  redis持久化机制有AOF和RDB(默认)


* 什么是缓存穿透？如何解决？

    一般的系统按照key去缓存，如果找不到key，就去数据库查，一些恶意请求会估计查询不存在的key,就会对数据库造成很大压力，这就是缓存穿透。

    解决方案： 1. 对结果为空的查询进行缓存，缓存时间可以短一点 2. 对一定不存在的key进行过滤。可以把所有可能存在的key放到一个大的bitMap中，查询时通过bitmap过滤

* 什么时缓存雪崩？如何解决？

    缓存数据集中在同一时间段失效，这时会对后端系统造成很大压力，这就是缓存雪崩。

    解决方案： 1. 不同的key设置不同的缓存时间。 2 做二级缓存