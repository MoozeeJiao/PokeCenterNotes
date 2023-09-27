# 《HBase 不睡觉》

![[hbase01.jpg]]

Region是表的一部分，类似于一个分区。RegionService中有多个Region，Region包含多个Store,每个Store对应一个列族

![[hbase02.jpg]]

WAL预写日志: 数据到达Region后，先写进WAL再写进Memstore。解决宕机恢复问题。

WAL可以关闭，也可以改异步ASYNC_WAL，数据先写入Memstore隔一段时间后在写入WAL。

WAL是一个环状体滚动日志结构（写入效率高，空间不会扩大），每隔一段时间会将WAL与HDFS数据比较，已经持久化的操作会移动到.oldlogs。块快满了也会滚动。如果没有服务引用旧的WAL就会被删除。


每个Store都有个Memstore内存存储对象，如果写满了就flush到HFile。Store中有多个HFile，直接跟HDFS打交道，是数据的存储实体。

Memstore的意义: HDFS文件只能创建、追加、删除，不能修改。数据库，需要数据有序来保障性能，因此需要在内存中把数据整理成顺序存放。Memstore维持数据按照Rowkey排序，而不是缓存。

LSM B+树的改进，如果在频繁数据改动的情况下维护读取速度的稳定。

![[hbase03.jpg]]
![[hbase04.jpg]]
![[hbase05.jpg]]
增加一个单元格: HDFS新增一条数据

修改一个单元格: HDFS新增一条数据，版本号比之前大

删除一个单元格: 新增一条墓碑数据

每隔一段时间进行Compaction，将多个HFile合并成一个。

![[hbase06.jpg]]

客户端会缓存meta信息

Mini Compaction: store中多个HFile合并为一个，只删过ttl的

Major Compaction: store中所有HFile合并为一个，墓碑也删，不要在业务高峰执行