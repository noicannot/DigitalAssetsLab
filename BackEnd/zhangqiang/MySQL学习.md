<a name="pbjcs"></a>
# 164.数据库的三范式是什么？
第一范式：强调的是列的原子性，即数据库表的每一列都是不可分割的原子数据项。<br />第二范式：要求实体的属性完全依赖于主关键字。所谓完全依赖是指不能存在仅依赖主关键字一部分的属性。<br />第三范式：任何非主属性不依赖于其它非主属性。
<a name="if33t"></a>
# 165.一张自增表里面总共有 7 条数据，删除了最后 2 条数据，重启 mysql 数据库，又插入了一条数据，此时 id 是几？
数据库引擎如果是 MyISAM ，那 id 就是 8。<br />数据库引擎如果是 InnoDB，那 id 就是 6。<br />InnoDB 表只会把自增主键的最大 id 记录在内存中，所以重启之后会导致最大 id 丢失。
<a name="N8cfQ"></a>
# 166.如何获取当前数据库版本？
使用 select version() 获取当前 MySQL 数据库版本。
<a name="voyUq"></a>
# 167. 说一下 ACID 是什么？
Atomicity（原子性）：一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被恢复（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。即，事务不可分割、不可约简。<br />Consistency（一致性）：在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设约束、触发器、级联回滚等。依赖于应用程序，就是当前对数据库的操作要符合系统约束<br />Isolation（隔离性）：数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。<br />Durability（持久性）：事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。
<a name="ResvK"></a>
# 168. char 和 varchar 的区别是什么？
char(n) ：固定长度类型，比如订阅 char(10)，当你输入"abc"三个字符的时候，它们占的空间还是 10 个字节，其他 7 个是空字节。<br />char 优点：效率高；缺点：占用空间；适用场景：存储密码的 md5 值，固定长度的，使用 char 非常合适。<br />varchar(n) ：可变长度，存储的值是每个值占用的字节再加上一个用来记录其长度的字节的长度。<br />所以，从空间上考虑 varcahr 比较合适；从效率上考虑 char 比较合适，二者使用需要权衡。
<a name="Sqs1h"></a>
# 169. float 和 double 的区别是什么？
float 最多可以存储 8 位的十进制数，并在内存中占 4 字节。<br />double 最可可以存储 16 位的十进制数，并在内存中占 8 字节。
<a name="ZL675"></a>
# 170. MySQL 的内连接、左连接、右连接有什么区别？
内连接关键字：inner join；左连接：left join；右连接：right join。<br />内连接是把匹配的关联数据显示出来；左连接是左边的表全部显示出来，右边的表显示出符合条件的数据；右连接正好相反。
<a name="fABJA"></a>
# 171. MySQL 索引是怎么实现的？
索引是满足某种特定查找算法的数据结构，而这些数据结构会以某种方式指向数据，从而实现高效查找数据。<br />具体来说 MySQL 中的索引，不同的数据引擎实现有所不同，但目前主流的数据库引擎的索引都是 B+ 树实现的，B+ 树的搜索效率，可以到达二分法的性能，找到数据区域之后就找到了完整的数据结构了，所有索引的性能也是更好的。
<a name="Y4fDd"></a>
# 172. 怎么验证 MySQL 的索引是否满足需求？
使用 explain 查看 SQL 是如何执行查询语句的，从而分析你的索引是否满足需求。<br />explain 语法：explain select * from table where type=1。
<a name="ZI1a0"></a>
# 173. 说一下数据库的事务隔离？
MySQL 的事务隔离是在 MySQL. ini 配置文件里添加的，在文件的最后添加：transaction-isolation = REPEATABLE-READ<br />可用的配置值：READ-UNCOMMITTED、READ-COMMITTED、REPEATABLE-READ、SERIALIZABLE。<br />READ-UNCOMMITTED：未提交读，最低隔离级别、事务未提交前，就可被其他事务读取（会出现幻读、脏读、不可重复读）。<br />READ-COMMITTED：提交读，一个事务提交后才能被其他事务读取到（会造成幻读、不可重复读）。<br />REPEATABLE-READ：可重复读，默认级别，保证多次读取同一个数据时，其值都和事务开始时候的内容是一致，禁止读取到别的事务未提交的数据（会造成幻读）。<br />SERIALIZABLE：序列化，代价最高最可靠的隔离级别，该隔离级别能防止脏读、不可重复读、幻读。<br />脏读 ：表示一个事务能够读取另一个事务中还未提交的数据。比如，某个事务尝试插入记录 A，此时该事务还未提交，然后另一个事务尝试读取到了记录 A。<br />不可重复读 ：是指在一个事务内，多次读同一数据。<br />幻读 ：指同一个事务内多次查询返回的结果集不一样。比如同一个事务 A 第一次查询时候有 n 条记录，但是第二次同等条件下查询却有 n+1 条记录，这就好像产生了幻觉。发生幻读的原因也是另外一个事务新增或者删除或者修改了第一个事务结果集里面的数据，同一个记录的数据内容被修改了，所有数据行的记录就变多或者变少了。
<a name="OsmyN"></a>
# 174. 说一下 MySQL 常用的引擎？
InnoDB 引擎：mysql 5.1 后默认的数据库引擎，提供了对数据库 acid 事务的支持，并且还提供了行级锁和外键的约束，它的设计的目标就是处理大数据容量的数据库系统。MySQL 运行的时候，InnoDB 会在内存中建立缓冲池，用于缓冲数据和索引。但是该引擎是不支持全文搜索，同时启动也比较的慢，它是不会保存表的行数的，所以当进行 select count(*) from table 指令的时候，需要进行扫描全表。由于锁的粒度小，写操作是不会锁定全表的,所以在并发度较高的场景下使用会提升效率的。<br />MyIASM 引擎：不提供事务的支持，也不支持行级锁和外键。因此当执行插入和更新语句时，即执行写操作的时候需要锁定这个表，所以会导致效率会降低。不过和 InnoDB 不同的是，MyIASM 引擎是保存了表的行数，于是当进行 select count(*) from table 语句时，可以直接的读取已经保存的值而不需要进行扫描全表。所以，如果表的读操作远远多于写操作时，并且不需要事务的支持的，可以将 MyIASM 作为数据库引擎的首选。
<a name="c8RPx"></a>
# 175. 说一下 MySQL 的行锁和表锁？
MyISAM 只支持表锁，InnoDB 支持表锁和行锁，默认为行锁。<br />表级锁：开销小，加锁快，不会出现死锁。锁定粒度大，发生锁冲突的概率最高，并发量最低。<br />行级锁：开销大，加锁慢，会出现死锁。锁力度小，发生锁冲突的概率小，并发度最高。
<a name="KWmET"></a>
# 176. 说一下乐观锁和悲观锁？
乐观锁：每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在提交更新的时候会判断一下在此期间别人有没有去更新这个数据。<br />悲观锁：每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻止，直到这个锁被释放。<br />数据库的乐观锁需要自己实现，在表里面添加一个 version 字段，每次修改成功值加 1，这样每次修改的时候先对比一下，自己拥有的 version 和数据库现在的 version 是否一致，如果不一致就不修改，这样就实现了乐观锁。
<a name="NzHXR"></a>
# 177. MySQL 问题排查都有哪些手段？
使用 show processlist 命令查看当前所有连接信息。<br />使用 explain 命令查询 SQL 语句执行计划。<br />开启慢查询日志，查看慢查询的 SQL。
<a name="pkgYx"></a>
# 178. 如何做 MySQL 的性能优化？
为搜索字段创建索引。<br />避免使用 select *，列出需要查询的字段。<br />垂直分割分表。<br />选择正确的存储引擎。
<a name="oUNcO"></a>
# MySQL逻辑架构介绍
<a name="G7vIz"></a>
## 总体概览：
<a name="hifz0"></a>
### 1、连接层
最上层是一些客户端和连接服务，包含本地sock通信和大多数基于客户端/服务端工具实现的类似于tcp/ip的通信。主要完成一些类似于连接处理、授权认证、及相关的安全方案。在该层上引入了线程池的概念，为通过认证安全接入的客户端提供线程。同样在该层上可以实现基于SSL的安全链接。服务器也会为安全接入的每个客户端验证它所具有的操作权限。
<a name="WMm7n"></a>
### 2、服务层
第二层架构主要完成大多数的核心功能，如SQL接口，并完成缓存的查询，SQL的分析和优化及部分内置函数的执行。所有跨存储引擎的功能也在这一层实现，如过程、函数等。在该层，服务器会解析查询并创建相应的内部解析树，并对其完成相应的优化如确定查询表的顺序，是否理由索引等，最后生成相应的执行操作。如果是select语句服务器还会查询内部的缓存。如果缓存空间足够大，这样在解决大量读操作的环境中能够很好地提升系统的性能。
<a name="SvW27"></a>
### 3、引擎层
存储引擎层，存储引擎真正的负责了MySQL中数据的存储和提取，服务器通过API与存储引擎进行通信。不同的存储引擎具有的功能不同，这样我们可以根据自己的实际需要进行选取
<a name="ANLW9"></a>
### 4、存储层
数据存储层，主要是将数据存储在运行于裸设备的文件系统之上，并完成与存储引擎的交互。
<a name="vNlEj"></a>
# 存储引擎
<a name="r705E"></a>
## 查看当前mysql的默认存储引擎
```sql
show variables like '%storage_engine%';
```
<a name="h7vqy"></a>
## MyISAM和InnoDB对比
| 对比项 | MyISAM | InnoDB |
| --- | --- | --- |
| 主外键 | 不支持 | 支持 |
| 事务 | 不支持 | 支持 |
| 行表锁 | 表锁，即使操作一条记录也会锁住整个表，不适合高并发操作 | 行锁，操作时只锁某一行，不对其他行有影响，适合高并发操作 |
| 缓存 | 只缓存索引，不缓存真实数据 | 缓存索引和真实数据，对内存要求较高，而且内存大小对性能有决定性的影响 |
| 表空间 | 小 | 大 |
| 关注点 | 性能（偏读） | 事务 |
| 默认安装 | Y | Y |

<a name="FVWxF"></a>
# 七种join的SQL编写
```sql
---合并查询出两表公共部分数据
select * from table1 t1 inner join table2 t2 on t1.id=t2.id
---合并查询出左表全部和右表部分和左表相同数据，缺失以NULL填充
select * from table1 t1 left join table2 t2 on t1.id=t2.id
---合并查询出右表全部和左表部分和右表相同数据，缺失以NULL填充
select * from table1 t1 right join table2 t2 on t1.id=t2.id
---合并查询左表和右表，排除左右表相同的数据及右表其他不同数据只要左表独有信息
select * from table1 t1 left join table2 t2 on t1.id=t2.id where t2.id is null
---合并查询左表和右表，排除左右表相同的数据及左表其他不同数据只要右表独有信息
select * from table1 t1 right join table2 t2 on t1.id=t2.id where t1.id is null
---合并查询左表和右表的全部信息
select * from table1 t1 left join table2 t2 on t1.id=t2.id
union
select * from table1 t1 right join table2 t2 on t1.id=t2.id
---合并查询左表和右表的独有信息
select * from table1 t1 left join table2 t2 on t1.id=t2.id where t2.id is null
union
select * from table1 t1 right join table2 t2 on t1.id=t2.id where t1.id is null
```
<a name="ZtcsK"></a>
# 事务与ACID：
事务是由一组SQL语句组成的逻辑处理单元，事务具有以下4个属性，通常简称为事务的ACID属性。<br />原子性（Atomicity）：事务是一个原子操作单元，其对数据的修改，要么全部执行，要么你全都不执行。<br />一致性（Consistent）：在事务开始和完成时，数据都必须保持一致状态。这意味着所有相关的数据规则都必须应用于事务的修改，以保持数据的完整性；事务结束时，所有的内部数据结构（如B树索引或双向链表）也都必须是正确的。<br />隔离性（lsolation）：数据库系统提供一定的隔离机制，保证事务在不受外部并发操作影响的“独立”环境执行。这意味着事务处理过程中的中间状态对外部是不可见的。反之亦然。<br />持久性（Durable）：事务完成之后，它对于数据的修改是永久性，即使出现系统故障也能够保持。
<a name="ZzpRC"></a>
## 并发事务带来的问题
<a name="HUeyY"></a>
### 更新丢失：
当两个或多个事务选择同一行，然后基于最初选定的值更新该行时，由于每个事务都不知道其他事务的存在，就会发生丢失更新问题
<a name="PpQZs"></a>
### 脏读（读到其他事务已修改但未提交的数据）：
事务A读取到了事务B已修改但尚未提交的数据，还在这个数据基础上做了操作。此时，如果B事务回滚，A读取的数据无效，不符合一致性要求。
<a name="Q6svm"></a>
### 不可重复读：
事务A读取到了事务B已经提交的修改数据，不符合隔离性
<a name="Uh5TQ"></a>
### 幻读（读到其他事务的新增数据）：
事务A读到了事务B提交的新增数据，不符合隔离性（和脏读类似）
<a name="GrOUN"></a>
## 事务的隔离级别：
| 读数据一致性及允许的并发副作用隔离级别 | 读数据一致性 | 脏读 | 不可重复读 | 幻读 |
| --- | --- | --- | --- | --- |
| 未提交读（Read uncommitted） | 最低级别，只能保证不读取物理上损坏的数据 | 是 | 是 | 是 |
| 已提交读（Read committed） | 语句级 | 否 | 是 | 是 |
| 可重复读（Repetable read） | 事务级 | 否 | 否 | 是 |
| 可序列化（Serialzable） | 最高级别，事务级 | 否 | 否 | 否 |

**数据库的事务隔离越严格，并发副作用越小，但付出的代价也就越大，因为事务隔离实质上就是使事务一定程度上“串行化”进行，这显然与“并发”是矛盾的。同时，不同的应用对读一致性和事务隔离程度的要求也是不同的，比如许多应用对“不可重复读”和“幻读”并不敏感，可能更关系数据并发访问的能力。**
<a name="ujx3K"></a>
### 查看当前数据库事务的隔离级别：
```sql
show variables like 'tx_isolation'
```
<a name="bQ6Dg"></a>
# MySQL的索引：
帮助MySQL获取数据的数据结构，索引本身也会占用内存<br />当没有索引时，查询会进行全表扫描
<a name="SlfQW"></a>
## 什么是索引：
1、排好序的快速查找结构<br />2、索引会影响where后面的查找和order by后面的排序<br />3、平常所说的索引，如果没有特别指明，都是指B树（多路搜索树，并不一定是二叉树）结构组织的索引。其中聚集索引，次要索引，复合索引，前缀索引，唯一索引默认都是使用B+树索引，统称索引。除了B+树这种类型还有哈希索引（hash index）
<a name="Pmw61"></a>
### 那些情况需要建立索引：
1、主键自动建立唯一索引<br />2、频繁作为查找条件的字段应该创建索引<br />3、查询中与其它表关联的字段，外键关系建立索引<br />4、单值/复合索引（高并发下倾向创建复合索引）<br />5、查询中排序的字段，排序字段若通过索引去访问将大大提高排序速度（order by）<br />6、查询中统计或者分组字段（group by分组前必order by）
<a name="mnQ9A"></a>
### 那些情况不需要建立索引：
1、频繁更新的字段不创建索引<br />2、表记录太少<br />3、where条件里用不到的字段不创建索引<br />4、数据重复且分布平均的表字段，因此应该只为最经常查询和最经常排序的数据列建立索引，注：如果某个数据列包含许多重复的内容，为它建立索引就没有太大的实际效果<br />​<br />
<a name="Ce6yv"></a>
## 索引优势：
通过索引对数据排序，降低数据排序成本，降低数据库IO成本，降低CPU消耗
<a name="WHmDG"></a>
## 索引劣势：
1、实际索引也是一张表，该表保存了主键与索引字段，并指向实体表的记录，所以索引列也要占用空间<br />2、提高了查询速度，但是会降低更新表的速度，如对表INSERT、UPDATE和DELETE，因为更新表时，MySQL不仅要保存数据，还要保存一下索引文件每次更新添加了索引列的字段，都会调整因为更新所带来的的键值变化后的索引信息<br />3、索引只是提高效率的一个因素，如果MySQL有大数据量的表，就需要花时间研究建立最优秀的索引，或优化查询
<a name="FM42M"></a>
## 
<a name="vw2yn"></a>
## 全文索引（用于搜索很长一篇文章的时候，效果最好）：
<a name="IGVvr"></a>
## 单值索引：
一个索引只包含单个列，一个表可以用多个单列索引（一个表最好不要多于五个）
<a name="uP1YT"></a>
## 唯一索引（UNIQUE）：
索引列的值必须唯一，但允许有空值
<a name="cgSuY"></a>
## 复合索引：
一个索引包含多个列
<a name="Vbilw"></a>
## 覆盖索引：
select的数据列只用从索引中就能够取得，不必读取数据行，MySQL可以利用索引返回select列表中的字段，而不必根据索引再次读取数据文件，查询列要被所建索引覆盖
<a name="x7GOD"></a>
## 创建索引基本语法
```sql
---CREATE方式，[UNIQUE]建唯一索引加这个，不建不加，mytable后面可以加多个列，就成为符合索引
CREATE [UNIQUE] INDEX indexName ON mytable(columnnname(length)) 
---ALTER普通方式
ALTER mytable ADD [UNIQUE] INDEX [indexName] ON (columnnname(length))
---该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL
ALTER TABLE tbl_name ADD PRIMARY KEY(column_list)
---这条语句创建索引的值必须是唯一的(除了NULL外，NULL可能会出现多次)
ALTER TABLE tbl_name ADD UNQUE index_name(column_list)
---添加普通索引，索引值可出现多次
ALTER TABLE tbl_name ADD INDEX index_name(column_list)
---该语句指定了索引为FULLTEXT，用于全文索引
ALTER TABLE tbl_name ADD FULLTEXT index_name(column_list)
```
<a name="OdhqD"></a>
## 删除索引基本语法
```sql
DROP INDEX [indexName] ON mytable;
```
<a name="cnSxQ"></a>
## 查看索引基本语法
```sql
SHOW INDEX FROM table_name
```
<a name="kXO5v"></a>
## 索引的结构
<a name="aQRGo"></a>
### B+Tree索引
<a name="h3OhG"></a>
#### 检索原理
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622615682030-8799c60b-d82a-47dd-b0cd-37ee318eeb4c.png#clientId=u13134f26-c93a-4&from=paste&height=349&id=ue7c0664f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=349&originWidth=722&originalType=binary&ratio=1&size=251932&status=done&style=none&taskId=u0b408bca-8d5f-40e5-ac7c-cbd1e4a6ea8&width=722)<br />**初始化介绍：**<br />一颗b+树，浅蓝色的块称之为一个磁盘块，每个磁盘块包含几个数据项（深蓝色所示）和指针（黄色所示），如磁盘块1包含数据项17和35，包含指针P1（小于17的数据）、P2（大于17小于35的数据）、P3（大于35的数据）。<br />真实的数据项存在于叶子节点即3、5、9、10、13、15、28、29、36、60、75、79、90、99。<br />非叶子节点不存储真实的数据，只存储指引搜索方向的数据项，如17、35并不真实存在于数据表中<br />**查找过程：**<br />如果要查找数据项29，那么首先会把磁盘块1由磁盘加载到内存，此时发生一次IO，在内存中用二分查找确定29在17和35直接，锁定磁盘块1的P2指针，内存时间因为非常短（相比磁盘的IO）可以忽略不计，通过磁盘块1的P2指针的磁盘地址把磁盘块3由磁盘加载到内存，发生第二次IO，29在26和30直接，锁定磁盘块3的P2指针，通过指针加载磁盘块8到内存，发生第三次IO，同时内存中做二分查找找到29，结束查询，总计三次IO。<br />真实情况，3层的B+树可以表示上百万的数据，如果上百万的数据查找只需要三次IO，性能提高将是巨大的，如果没有索引，每个数据项都要发生一次IO，那么总共需要百万次IO，成本很高
<a name="Dmfdo"></a>
### Hash索引
<a name="nskwt"></a>
### full-text全文索引
<a name="XGi8f"></a>
### R-Tree索引
<a name="WU9aM"></a>
## 索引的原理：
<a name="F79Xs"></a>
### 二叉树
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622611694021-e8b831b2-8c85-4a69-adeb-107e5dacb69a.png#clientId=u13134f26-c93a-4&from=paste&height=305&id=uVij1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=305&originWidth=666&originalType=binary&ratio=1&size=133708&status=done&style=none&taskId=u310e7233-4153-4de0-abfe-5850838e1f3&width=666)<br />为了加快col2查找，可以维护一个右边所示的二叉查找树，每个节点分别包含索引键值和一个指向对应数据记录物理地址的指针，这样就可以运用二叉查找树在一定的复杂度内获取到相应数据，从而快速的检索出符合条件的记录
<a name="q3FJP"></a>
# explain使用简介
使用EXPLAIN关键字可以模拟优化器执行SQL查询语句，从而知道MySQL是如何处理你的SQL语句的。分析你的查询语句或是表结构的性能瓶颈。
<a name="Xn7To"></a>
## 可以做的事情：
1、表的读取顺序<br />2、数据读取操作的操作类型<br />3、那些索引可以使用<br />4、哪些索引被实际使用<br />5、表之间的引用<br />6、每张表有多少行被优化器查询
<a name="rkrN0"></a>
## 用法
```sql
explain 所要检测的SQL
```
执行得到结果<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622618454327-57accb3a-58d0-4f8f-bf06-ba204e0e745b.png#clientId=u13134f26-c93a-4&from=paste&height=28&id=uf700181c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=28&originWidth=839&originalType=binary&ratio=1&size=3730&status=done&style=none&taskId=u1203dc05-326a-42c1-9b8e-2f762edde0f&width=839)<br />**id（**select查询的序列号**）（重点查看）：**<br />包含一组数字，表示查询中执行select子句或操作表的顺序（表的读取/加载顺序）。<br />三种情况：<br />1、id相同，执行顺序由上至下<br />2、id不同，如果是子查询，id序号会递增，id值越大优先级越高，越先被执行<br />3、id相同不同，同时存在<br />**select_type（查询的类型）（重点查看）：**

| SIMPLE | 简答的select查询，查询中不包含子查询或者UNION |
| --- | --- |
| PRIMARY | 查询中若包含任何复杂的子部分，最外层查询则被标记为这个 |
| SUBQUERY | 在select或where列表中包含了子查询 |
| DERIVED | 在from列表中包含的子查询被标记为DERIVED（衍生）MySQL会递归执行这些子查询，把结果放在临时表里 |
| UNION | 若第二个SELECT出现在UNION之后，则被标记为UNION；<br />若UNION包含在from子句的子查询中，外层select将被标记为：DERIVED |
| UNION RESULT | 从UNION表获取结果的SELECT |

**table：**<br />显示这一行数据是关于那张表的<br />**partitions：**<br />匹配的分区<br />**type（显示查询使用了何种类型）（重点查看）：**<br />从最好到最差依次是：system>const>eq_ref>ref>range>index>ALL

| system | 表只有一行记录（等于系统表），这是const类型的特例，平时不会出现，这个也可以忽略不计 |
| --- | --- |
| const | 表示通过索引一次就找到了，const用户比较主键或者unique索引。因为只匹配一行数据，所以很快如将主键置于where列表中，MySQL就能将该查询转换为一个常量 |
| eq_ref | 唯一性索引扫描，对于每个索引键，表中只有一条记录与之匹配。常见于主键或唯一索引扫描 |
| ref | 非唯一性索引扫描，返回匹配某个单独值的所有行。<br />本质上也是一种索引访问，它返回所有匹配某个单独值的行，然而，它可能会找到多个符合条件的行，所以他应该属于查找和扫描的混合体 |
| range | 只检索给定范围的行，使用一个索引来选择行。key列显示使用了那个索引，一般就是在你的where语句中出现了between、<、>、in等的查询，这种范围扫描索引比全表扫描要好，因为它只需要开始于索引的某一点，而结束于另一点，不用扫描全表 |
| index | Full Index Scan，index与ALL区别为index类型只遍历索引树。这通常比ALL块，因为索引文件通常比数据文件小（虽然all和index都是读全表，但index是从索引中读取的，而all是从硬盘中读的） |
| ALL | 全表扫描，将遍历全表以找到匹配的行 |

注：一般来说，得保证查询至少达到range级别，最好能达到ref<br />**possible_keys：**<br />显示可能应用在这张表的索引，一个或多个。<br />查询涉及到的字段若存在索引，则该索引将被列出，但不一定被查询实际使用<br />**key（重点查看）：**<br />实际使用的索引。如果为NULL，则没有使用索引。<br />若查询中使用了覆盖索引，则该索引仅出现在key列表中。<br />**key_len：**<br />表示索引中使用的字节数，可通过该列计算查询中使用的索引的长度。在不损失精确性的情况下，长度越短越好。<br />key_len显示的值为索引字段的最大可能长度，并非实际使用长度，即key_len是根据表定义计算而得，不是通过表内检索出的<br />**ref：**<br />显示索引的哪一列被使用了，如果可能的话，是一个常数。哪些列或常量被用于查找索引列上的值。<br />**rows：**<br />根据表统计信息及索引选用情况，大致估算出找到所需的记录所需要读取的行数（数值越小越好）<br />**filtered：**<br />按表条件过滤的行百分比<br />**Extra（执行情况的描述和说明）（重点查看）：**

| Using filesort | 说明mysql会对数据使用一个外部的索引排序，而不是按照表内的索引顺序进行读取。MySQL中无法利用索引完成排序操作称为“文件排序”（需优化） |
| --- | --- |
| Using temporary | 使用了临时表保存中间结果，MySQL在对查询结果排序时使用临时表。常见于排序order by和分组查询group by（必需优化） |
| Using index | 表示相应的select操作中使用了覆盖索引（Covering Index），避免了访问了表的数据行，效率不错！<br />如果同时出现using where，表明索引被用来执行索引键值的查找；<br />如果没有同时出现using where，表明索引用来读取数据而非执行查找动作。 |
| Using index condition | 却是命中了索引，但不是所有列数据都在索引树上，还需要访问实际的行记录 |
| Using where | 使用了where过滤 |
| using join buffer | 使用了连接缓存（join），配置文件join buffer可以调大一点 |
| impossible where | where子句的值总是false，不能用来获取任何元组 |
| select tables optimized away | 在没有group by子句的情况下，基于索引优化MIN/MAX操作或者对于MyISAM存储引擎优化COUNT(*)操作，不必等到执行阶段再进行计算，查询执行计划生成的阶段即完成优化 |
| distinct | 优化distinct操作，在找到第一匹配的元组后即停止找同样值的动作 |

<a name="pxvPm"></a>
# 索引优化
注意：<br />按照MySQL B+树的查找策略，索引中的列如果在SQL中是范围条件后面的索引将不能生效。例如下
<a name="cfOBb"></a>
## 单表索引优化示例
```sql
---示例SQL此时comments为范围条件
explain select id,author_id from article where category_id = 1 and comments > 1 
order by views desc limit 1
```
示例SQL只有主键索引时，性能分析全表扫描和文件排序，需要优化<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622639418706-f36c13a9-61a2-4dd6-ad02-8ab48bc57540.png#clientId=u906ff8a7-42f7-4&from=paste&height=47&id=u51836597&margin=%5Bobject%20Object%5D&name=image.png&originHeight=47&originWidth=957&originalType=binary&ratio=1&size=7224&status=done&style=none&taskId=u2a5f912d-cf51-4adc-87bc-bdf113e3624&width=957)<br />为category_id，comments，views建立索引
```sql
create index sy_ccv on article(category_id,comments,views)
```
查询结果，优化了全表扫描但文件排序依旧存在，这个索引不合适<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622639346936-b3afe498-f97e-4d20-8c79-61426cc4081f.png#clientId=u906ff8a7-42f7-4&from=paste&height=124&id=u5266be0b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=124&originWidth=1057&originalType=binary&ratio=1&size=16287&status=done&style=none&taskId=u05f374fb-ba2f-410c-81bb-ecc93ee89db&width=1057)<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622639369446-b73855cf-347e-4619-92ef-804208cdd455.png#clientId=u906ff8a7-42f7-4&from=paste&height=46&id=u5c3ca3c4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=46&originWidth=1079&originalType=binary&ratio=1&size=7593&status=done&style=none&taskId=ud264a810-9407-440c-9ca0-772cf0e18e4&width=1079)<br />考虑到索引列（comments）的字段在SQL中存在范围查询会使他后面的（views）索引失效，所以可以尝试只给category_id和views两列创建索引
```sql
---删除原有索引
drop index sy_ccv on article
---为category_id和views两列创建索引
create index sy_cv on article(category_id,views)
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622639833895-ed6ef5c6-be89-49f0-95b9-2ee3614e5707.png#clientId=u906ff8a7-42f7-4&from=paste&height=90&id=u1d81fa71&margin=%5Bobject%20Object%5D&name=image.png&originHeight=90&originWidth=1061&originalType=binary&ratio=1&size=13472&status=done&style=none&taskId=u024611dc-e237-4fd2-a46b-83f98b4c838&width=1061)<br />文件排序消失，优化成功<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622639850465-9685db3e-0cde-4c5c-8cfa-df52c33048ff.png#clientId=u906ff8a7-42f7-4&from=paste&height=56&id=u6561fa4d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=56&originWidth=938&originalType=binary&ratio=1&size=7367&status=done&style=none&taskId=ub59b47e7-3c58-46a8-a243-41b7ce3d7a5&width=938)
<a name="C3Jys"></a>
## 两表索引优化示例
```sql
EXPLAIN select * from class left join book on class.card = book.card
```
目前两表索引都只有主键索引，SQL诊断为全表扫描<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622640385581-21a214ea-52cc-486a-af1a-e0aab9eeb00a.png#clientId=u906ff8a7-42f7-4&from=paste&height=73&id=ucd23c19b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=73&originWidth=1149&originalType=binary&ratio=1&size=11025&status=done&style=none&taskId=u48aa69c2-f83e-45a9-8eaa-85f939e6c91&width=1149)<br />先给book的card字段加上索引
```sql
create index bc on book(card)
show index from book
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622640531752-ad54c1e4-9a15-4c07-af3e-a75540aabbce.png#clientId=u906ff8a7-42f7-4&from=paste&height=68&id=u7e1be28c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=68&originWidth=1183&originalType=binary&ratio=1&size=10349&status=done&style=none&taskId=u4f521f87-f1ee-4377-bab5-fa504bbffd9&width=1183)<br />SQL诊断发现book表的全表扫描没有了，但class表依旧存在全表扫描<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622640604521-19b4b897-3a63-44d3-b75e-f030dd675742.png#clientId=u906ff8a7-42f7-4&from=paste&height=88&id=u255786c9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=88&originWidth=912&originalType=binary&ratio=1&size=10031&status=done&style=none&taskId=u81ae9827-ca5a-4bd8-9930-5d3ec5d6611&width=912)<br />此时删除book的索引给class表的card加上索引<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622640826356-dad923e2-16e3-4f2f-880c-20596be4a702.png#clientId=u906ff8a7-42f7-4&from=paste&height=80&id=u4205228b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=80&originWidth=1182&originalType=binary&ratio=1&size=10650&status=done&style=none&taskId=u6869b74c-0024-47fd-9ac9-3d33ce0c391&width=1182)<br />此时class表的查询方式为index，book表加有索引查询方式为ref，ref好于index，rows也没有变化<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622640846416-fd47b412-224b-4557-855b-51fdd4c911bf.png#clientId=u906ff8a7-42f7-4&from=paste&height=70&id=u59fde097&margin=%5Bobject%20Object%5D&name=image.png&originHeight=70&originWidth=1219&originalType=binary&ratio=1&size=11506&status=done&style=none&taskId=u5af123b8-0dde-4964-9ee8-4850c9358de&width=1219)
<a name="QTjgU"></a>
## 索引失效情况：
1、最佳左前缀法则（如果索引了多列，要遵循最左前缀法则。指的是查询从索引的最左前列开始并且不跳过索引中的列,如创建了a,b,c三个索引，查询条件也要有这三个且顺序不能乱）<br />2、不在索引列上做任何操作（计算、函数、（自动or手动）类型转换），会导致索引失效而转向全表扫描<br />3、存储引擎不能使用索引中范围条件右边的列（索引中条件用了范围，后面索引都失效）<br />4、尽量使用覆盖索引（只访问索引的查询（索引列和查询列一致）），减少select *<br />5、mysql在使用不等于（！=或<>）时无法使用索引导致全表扫描<br />6、is null,is not null也无法使用索引<br />7、like以通配符开头（'%abc...'）会导致索引失效变成全表扫描（最好在值的右边加通配符，根据规则3单值右边通配符索引仍可用。2、如果必须用两边百分号才能生效，可以建立覆盖索引来使索引生效）<br />8、字符串不加单引号索引失效（隐式类型转换）<br />9、少用or，用它来连接时索引失效
<a name="CyD9m"></a>
## 索引优化结论：
1、这是由左连接特性决定的。LEFT JOIN条件用于确定如何从右表搜索行，左边一定都有，所以右表是关键，一定要建立索引，右连接则反之<br />2、尽可能减少Join语句中的嵌套循环，永远用小结果集驱动大的结果集。<br />3、优先优化嵌套循环的内层循环<br />4、保证Join语句中被驱动表上Join条件已被索引<br />5、当无法保证被驱动表的Join条件字段被索引且内存资源充足的前提下，不要太吝惜JoinBuffer的设置
<a name="jSk2y"></a>
# SQL优化套路
1、开启慢查询日志，设置阈值，比如超过5秒钟就是慢SQL，并将它抓取出来。<br />2、explain+慢SQL分析<br />3、show profile查询SQL在MySQL服务器里面的执行细节和生命周期情况<br />4、SQL数据库服务器的参数调优<br />
<br />
<br />5、永远小表驱动大表<br />当A表数据大于B表时，用in合适
```sql
select * from A where id in (select id from B)
等价于
for select id from B
for select * from A where A.id=B.id
```
当A表数据小于于B表时，用exists合适（将主查询的数据放到子查询中做验证，用exists）
```sql
select * from A where exists (select 1 from B where B.id = A.id)
```
<a name="BRAZW"></a>
# order by优化
1、ORDER BY语句使用索引最左前列<br />2、使用WHERE子句于ORDER BY子句条件组合满足索引最左前列<br />3、当查询字段大小总和小于max_length_for_sort_data而且排序字段不是TEXT|BLOB类型时，会用改进后的算法----单路排序，否则用老算法，多路排序。<br />4、两种算法的数据都有可能超出sort_buffer的容量，超出之后，会创建tmp文件进行合并排序，导致多次I/O，但是用单路排序算法的风险会更大一些，所以要提高sort_buffer_size。<br />5、增大sort_buffer_size参数的设置，不管用哪种算法，提高这个参数都会提高效率，要根据系统的能力去提高，因为这个参数是针对每个进程的<br />6、增大max_length_for_sort_data参数的设置，提高这个参数，会增加用改进算法的概率。但是如果设的太高，数据总容量超出sort_buffer_size的概率就增大，明显症状是高的磁盘I/O活动和低的处理器使用率。
<a name="cDfVK"></a>
## filesort排序算法
<a name="eiQJy"></a>
### 双路排序：
MySQL4.1之前使用双路排序，字面意思就是两次扫描磁盘，最终得到数据，读取行指针和orderby列，对他们进行排序，然后扫描已经排序好的列表，按照列表中的值重新从列表中读取对应的数据输出。<br />从磁盘取排序字段，在buffer进行排序，再从磁盘取其他字段。<br />取一批数据，要对磁盘进行两次扫描，总所周知，I/O很耗时，所以在mysql4.1后，出现了第二种改进算法，就是单路排序。
<a name="i12Ui"></a>
### 单路排序
从磁盘读取查询需要的所有列，按照order by列在buffer对它们进行排序，然后扫描排序后的列表进行输出，它的效率更快一些，避免了第二次读取数据。并且把随机IO变成了顺序IO，但是它会使用更多的空间，因为它把每一行都保存在内存中了。
<a name="usaol"></a>
#### 单路排序的缺点
在sort_buffer中，方法B比方法A要多占用很多空间，因为方法B是把所有字段都取出，所以有可能去除的数据总大小超出了sort_buffer的容量，导致每次只能取sort_buffer容量大小的数据，进行排序（创建tmp文件，多路合并），排完再去取sort_buffer容量大小，再排。。。从而导致多次I\O<br />本想省一次I/O操作，反而导致大量I/O操作，得不偿失。
<a name="FWpLP"></a>
# group by优化
1、group by实质是先排序后进行分组，遵照索引建的最佳左前缀<br />2、当无法使用索引列，增大max_length_for_sort_data参数的设置+增大sort_buffer_size参数的设置<br />3、where高于having，能写在where限定的条件就不要去having限定了
<a name="B2r0a"></a>
# 慢查询日志
MySQL的慢查询日志是MySQL提供的一种日志记录，它用来记录在MySQL中响应时间超过阈值的语句，具体指运行时间超过long_query_time值的SQL，则会被记录到慢查询日志中。<br />具体指运行时间超过long_query_time值的SQL，则会被记录到慢查询日志中。long_query_time的默认值为10，意思是运行10秒以上的语句。<br />由他来查看哪些SQL超出了我们的最大忍耐时间值，比如一条sql执行超过5秒钟，<br />我们就算慢SQL，希望能手机超过5秒的sql，结合之前explain进行全面分析。<br />**注意：**<br />默认情况下。MySQL数据库没有开启慢查询日志，需要我们手动来设置这个参数。如果不是调优需要，一般不建议开启该参数，因为开启慢查询日志会或多或少带来一定性能影响。慢查询日志支持将日志记录写入文件。
<a name="EUEgD"></a>
## 查看是否开启慢查询及慢查询的开启
```sql
---查看慢查询日志状态
SHOW VARIABLES like '%slow_query_log%'
---开启慢查询，只对当前数据库生效，如果mysql重启则会失效
set global slow_query_log=1
```
<a name="cGjg1"></a>
## 设置慢SQL阈值时间（秒级）
```sql
set global long_query_time=3
---查看设置的阈值
show global variables like 'long_query_time'
```
<a name="CEGdX"></a>
## 慢SQL日志查询相关Linux命令
```java
//得到返回记录最多的10个SQL
mysqldumpslow -s r -t 10 /var/lib/mysql/atguigu-slow.log
//得到访问次数最多的10个SQL
mysqldumpslow -s c -t 10 /var/lib/mysql/atguigu-slow.log
//得到按照时间排序的前10条里面含有左连接的查询语句
mysqldumpslow -s t -t 10 -g "left join" /var/lib/mysql/atguigu-slow.log
//建议在使用这些命令是结合|和more使用，否则有可能出现爆屏情况
mysqldumpslow -s r -t 10 /var/lib/mysql/atguigu-slow.log | more
```
<a name="j4JoZ"></a>
### mysqldumpslow帮助信息
S：表示按照何种方式排序<br />C：访问次数<br />l：锁定时间<br />r：返回记录<br />t：查询时间<br />al：平均锁定时间<br />ar：平均返回记录数<br />at：平均查询时间<br />t：返回前面多少条的数据<br />g：后面搭配一个正则匹配模式，大小写不敏感
<a name="UogPu"></a>
# Show Profile（可以看到一个SQL的完整生命周期和每一步消耗的时间）
**查询最近执行的SQL及其耗时**
```sql
show PROFILES
```
**根据show PROFILES结果查看最耗时的SQL的cpu和io情况**
```sql
---140为show PROFILES查询结果最慢的SQL的编号
show PROFILE cpu,block io for query 140
```
**show PROFILE status出现需要注意的结果提示**<br />converting HEAP to MyISAM 查询结果太大，内存都不够用了往磁盘上搬<br />Creating tmp table 创建临时表<br />Copying to tmp table on disk 把内存中临时表复制到磁盘，危险<br />locked 锁表
<a name="GkqyI"></a>
# 全局查询日志（不在生产开启）
**配置开启**<br />在mysql的my.cnf中，设置如下：<br />#开启<br />general_log=1<br />#记录日志文件的路径<br />general_log_file=/path/logfile<br />#输出格式<br />log_output=FILE<br />**命令开启**
```sql
set global general_log=1;
set global log_output='TABLE';
```
开启之后所执行的SQL都会记录到mysql库里的general_log表，使用下面命令查看
```sql
select * from mysql.general_log
```
<a name="nXrY1"></a>
# MySQL锁机制
<a name="Q4hk2"></a>
## 概述
锁是计算机协调多个进程或线程并发访问某一资源的机制。<br />在数据库中，除传统的计算资源（如CPU、RAM、I/O等）等争用以外，数据也是一种供许多用户共享的资源。如何保证数据并发访问的一致性、有效性是所有数据库必须解决的一个问题，锁冲突也是影响数据库并发访问性能的一个重要因素。从这个角度来说，锁对数据库而言显得尤其重要，也更加复杂。
<a name="H1dVp"></a>
## 读锁（共享锁）
针对同一份数据，多个读操作可以同时进行而不会互相影响<br />在MyISAM引擎下当一个用户对一个表加了读锁之后该用户<br />只能读这个表，不能对这个表进行修改，也不能读其他表<br />其他用户可以读该表，对该表的修改操作会进入阻塞状态
<a name="y08F3"></a>
## 写锁（排他锁）
当前写操作没有完成前，它会阻断其他写锁和读锁<br />在MyISAM引擎下用户给表加了写锁<br />可以读当前表、可以修改当前表、不可读其他表<br />其他用户不可修改该表，不可读该表都会进入阻塞<br />​

MyISAM的读写锁调度是写优先，这也是MyISAM不适合做写为主表的引擎。因为写锁后，其他线程不能做任何操作，大量的更新会使查询很难得到锁，从而造成永远阻塞
<a name="wf7sK"></a>
## 如何分析表锁定
可以通过检查table_locks_waited和table_locks_immediate状态变量来分析系统上的表锁定
```sql
show status like '%table%'
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622731917983-42d84205-8102-43e4-bfcf-913e21090745.png#clientId=u972161cd-8800-4&from=paste&height=158&id=ub0852254&margin=%5Bobject%20Object%5D&name=image.png&originHeight=158&originWidth=288&originalType=binary&ratio=1&size=40657&status=done&style=none&taskId=ua9b20703-9e31-4404-a55e-d0fd842be28&width=288)<br />**table_locks_immediate**：产生表级锁定的次数，表示可以立即获取锁的查询次数，每立即获取锁值加1；<br />**table_locks_waited**：出现表级锁定争用而发生等待的次数（不能立即获取锁的次数，每等待一次锁值加1），此值高则说明存在着较严重的表级锁争用情况
<a name="qIrLS"></a>
## 表锁（偏读）
偏向MyISAM存储引擎，开销小，加锁快；无死锁；锁定粒度大，发生锁冲突的概率最高，并发度最低。
```sql
---手动增加表锁
lock table 表名 read(write), 表名2 read(write), 其他;
---查看表上加过的锁
show open tables
---释放表锁
unlock tables
```
<a name="SKhi0"></a>
## 行锁（偏写）
偏向InnoDB存储引擎，开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低，并发度也最高。<br />InnoDB与MyISAM的最大不同有两点：一是支持事务（TRANSACTION）；二是采用行级锁
<a name="SujLc"></a>
### 注意点
在对数据进行操作时**切勿使用MySQL的自动类型转换机制**，如字段是varchar类型却要插入int型这样做是可以修改成功但是**会使该列索引失效**，**导致本来的行锁会变成表锁**。
<a name="UOq93"></a>
### 间隙锁危害
**间隙锁概念：**<br />当我们用范围条件而不是相等条件检索数据，并请求共享或排他锁时，InnoDB会给符合条件的已有数据记录的索引项加锁；对于键值在条件范围内但并不存在的记录，叫做“间隙”，这种锁机制就叫做间隙锁<br />**危害：**<br />查询过程中通过范围查找的话，他会锁定整个范围内所有的索引键值，即使这个键值并不存在。<br />间隙锁有一个比较致命的弱点，就是当锁定一个范围键值之后，即使某些不存在的<br />键值也会被无辜的锁定，而造成在锁定的时候无法插入锁定键值范围内的任何数据。在某些场景下这可能会对性能造成很大的危害
<a name="NKRdm"></a>
### MySQK锁定一行记录
```sql
---首先开始标记
begin;
---假设要锁定8号记录这一行sql后加for update，锁定期间其他操作都会被阻塞
---知道锁定行的会话提交commit;
select * from table where a=8 for update;
---提交结束
commit;
```
<a name="BZYrv"></a>
### 分析行锁定的命令
```sql
---通过检查InnoDB_row_lock状态变量来分析系统上上的行锁争夺情况
show status like 'innodb_row_lock%'
---对各个状态量的说明如下
Innodb_row_lock_current_waits：当前正在等待锁定的数量
Innodb_row_lock_time（重要）：从系统启动到现在锁定总时间长度
Innodb_row_lock_avg（重要）：每次等待所花平均时间
Innodb_row_lock_time_max：从系统启动到现在等待最长的一次所花的时间
Innodb_row_lock_waits（重要）：系统启动后到现在总共等待的次数
```
<a name="UlPlY"></a>
### 总结
Innodb存储引擎由于实现了行级锁定，虽然在锁定机制的实现方面所带来的性能损耗可能比表级锁定会更高一些，但是在整体并发处理能力方法要远远优于MyISAM的表级锁定。当系统并发量较高的时候，Innodb的整体性能和MyISAM相比就会有比较明显的优势了。<br />但是Innodb的行级锁定同样也有其脆弱的一面，当我们使用不当的时候，可能会让Innodb的整体性能表现不仅不能比MyISAM高，甚至可能会更差。
<a name="XKdos"></a>
### 优化建议
1、尽可能让所有数据检索都通过索引来完成，避免无索引行锁升级为表锁。<br />2、合理设计索引，尽量缩小锁的范围。<br />3、尽可能较少检索条件，避免间隙锁。<br />4、尽量控制事务大小，减少锁定资源量和时间长度。<br />5、尽可能低级别事务隔离。
<a name="VT1ZV"></a>
## 页锁
开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般
<a name="DrIp1"></a>
# 主从复制
主机新建库、新建表、insert记录，从机复制<br />**好处：**<br />1、数据更安全：做了数据冗余，不会因为单台服务器的宕机而丢失数据<br />2、性能大大提升：一主多从，不同用户从不同数据库读取，性能提升<br />3、扩展性更优：流量增大时，可以方便增加从服务器，不影响系统使用<br />4、负载均衡：一主多从相当于分担了主机任务，做了负载均衡
<a name="g0TNq"></a>
## 原理：
从机会从主机读取二进制日志文件log-bin来进行数据同步<br />MySQL复制过程分成三步：<br />1、主机将改变记录到二进制日志（binary log）。这些记录过程叫做二进制日志事件，binary log events；<br />2、从机将主机的binary log事件拷贝到它的中继日志（relay log）<br />3、从机重做中继日志中的事件，将改变应用到自己的数据库中。MySQL复制是异步且串行化的
<a name="G7QU9"></a>
## 复制的基本原则：
1、每个**从机**只有一个**主机**<br />2、每个**从机**只能有一个唯一的服务器ID<br />3、每个**主机**可以有多个**从机**
<a name="S2PvC"></a>
## 一主一从常见配置：
mysql版本一致且后台以服务运行，同一网络可以互通<br />主从都配置在[mysqld]结点下，都是小写
<a name="aBjZz"></a>
### 主机修改（windos）my.ini配置文件：
```java
主服务器唯一ID（必须）
server-id=1 
启用二进制日志（必须）
log-bin=自己本地路径/mysqlbin 例：D:/devsoft/MySQLServer5.5/data/mysqlbin
启用错误日志（可选）
log-err=自己本地路径/mysqlerr 例：D:/devsoft/MySQLServer5.5/data/mysqlerr
根目录（可选）
basedir="自己本地路径"  例：D:/devsoft/MySQLServer5.5
临时目录（可选）
tmpdir="自己本地路径"   例：D:/devsoft/MySQLServer5.5
数据目录（可选）
datadir="自己本地路径/Data"  例：datadir="D:/devsoft/MySQLServer5.5/Data"
主机设置读写都可以
read-only=0
设置不要复制的数据库（可选）
binlog-ignore-db=mysql
设置需要复制的数据库（可选）
binlog-do-db=需要复制的主数据库名字
```
<a name="DiN45"></a>
### 从机修改（Linux）my.cnf配置文件
```java
从服务器唯一ID（必须）
server-id=1 
启用二进制日志（可选）
log-bin=自己本地路径/mysqlbin 例：D:/devsoft/MySQLServer5.5/data/mysqlbin
```
主机从机都必须关闭防火墙
<a name="PkEKN"></a>
### 主机上建立账户并授权给从机
```java
GRANT REPLICATION SLAVE ON *.* TO 'zhangsan'@'从机数据库IP' IDENTIFIED BY '123456';
flush privileges;
---查询master状态，记录下File和Position的值
show master status;
```
<a name="mWSCM"></a>
### 在从机上配置需要复制的主机
```java
CHANGE MASTER TO MASTER_HOST='主机IP',MASTER_USER='zhangsan',MASTER_PASSWORD='123456',
MASTER_LOG_FILE='mysqlbin.具体数字',MASTER_LOG-POS=Position具体值
---查询从机状态,必须同时看到Slave_IO_Running:Yes,Slave_SQL_Running:Yes
show slave status
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/12668119/1622884655772-a802bace-abea-4a50-8ff7-e494ce5b8dfa.png#clientId=u95a89684-8c16-4&from=paste&height=103&id=u0c0cad35&margin=%5Bobject%20Object%5D&name=image.png&originHeight=103&originWidth=702&originalType=binary&ratio=1&size=46697&status=done&style=none&taskId=uab0cf0b9-0b3a-477d-8cd8-61149133944&width=702)
<a name="qilTD"></a>
### 停止从机复制功能
```java
stop slave
```
