## MVCC原理
### 什么是MVCC
> MVCC，全称Multi-Version Concurrency Control，即多版本并发控制。MVCC是一种并发控制的方法，一般在数据库管理系统中，实现对数据库的并发访问，在编程语言中实现事务内存。

### MVCC解决了什么问题
MVCC在MySQL InnoDB中的实现主要是为了提高数据库并发性能，用更好的方式去处理读-写冲突，做到即使有读写冲突时，也能做到不加锁，非阻塞并发读
### MySQL版本链
![MySQL版本链](https://img-blog.csdnimg.cn/20210709225948254.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xfQmxvZw==,size_16,color_FFFFFF,t_70#pic_center)
### Read View
* m_ids：在生成ReadView时，当前系统中活跃的读写事务的事务id列表
* min_trx_id：在生成ReadView时，当前系统中活跃的读写事务中最小的事务id；也就是m_ids中最小值。
* max_trx_id：在生成ReadView时，系统应该分配下一个事务的事务id值。
* creator_trx_id：生成该ReadView的事务的事务id。

#### ReadView判断记录可见的条件
 <img src="https://img-blog.csdnimg.cn/20210708234404693.jpg"   width="45%">
 <img src="https://img-blog.csdnimg.cn/20210709220018294.jpg"   width="45%">
 <img src="https://img-blog.csdnimg.cn/20210709220526421.jpg"   width="45%">
 <img src="https://img-blog.csdnimg.cn/20210709221401840.jpg"   width="45%">

### 什么是当前读和快照读
* 当前读

像select lock in share mode(共享锁), select for update ; update, insert ,delete(排他锁)这些操作都是一种当前读，为什么叫当前读？就是它读取的是记录的最新版本，读取时还要保证其他并发事务不能修改当前记录，会对读取的记录进行加锁。

* 快照读

像不加锁的select操作就是快照读，即不加锁的非阻塞读；快照读的前提是隔离级别不是串行级别，串行级别下的快照读会退化成当前读；之所以出现快照读的情况，是基于提高并发性能的考虑，快照读的实现是基于多版本并发控制，即MVCC,可以认为MVCC是行锁的一个变种，但它在很多情况下，避免了加锁操作，降低了开销；既然是基于多版本，即快照读可能读到的并不一定是数据的最新版本，而有可能是之前的历史版本
> MVCC就是为了实现读-写冲突不加锁，而这个读指的就是快照读, 而非当前读，当前读实际上是一种加锁的操作，是悲观锁的实现



参考资料

> 《MySQL是怎样运行的-从根儿上理解MySQL》
