# Redis 介绍

## 是什么？

开源内存数据存储系统，可用作数据库、缓存、消息中间件。

支持多种数据结构 String，Hash，Set，List，ZSet，Bitmap，Hyperloglog，geo

内置了复制（repliaction），LUA脚本，LRU驱动事件（LRU eviction），事务（transactions）和不同级别的磁盘持久化（presistence）；

通过哨兵 Sentinel 和自动分区 Cluster 提供高可用性。