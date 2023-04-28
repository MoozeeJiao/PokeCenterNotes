
分布式的分布式应用程序协同服务。ZooKeeper目标是将复杂的分布式一致性服务能力封装起来，提供易用的接口。

使用zk的应用：
* Hdoop 的 NameNode 高可用；
* HBase 的 master，保存 hbase:meta 表，保存 RegionSerever 列表；
* Kafka 管理集群成员，controller 选举。

适用于存储和协同的关键数据，不适合存储大量数据。

## master-woker 架构

master 负责监控 woker 状态，并为 woker 分配任务。

|  特性 | zk实现 |
|----|----|
|任何时刻只能有1个 master，多个会导致脑裂。|使用临时的 znode /master，创建成功则为master。|
| 除了激活的 master，还有 backup 的可以很快进入激活状态。|创建 /master znode失败后，会watch这个节点，如果节点被删除，则继续尝试创建。|
|master 实时监控 woker 状态，收到状态变化通知，进行任务分配。|woker 通过在 /wokers 下创建临时节点介入集群，master会 watch /woker 下面的列表。|


## 数据模型

Data tree，每个节点叫做 znode。不同于文件系统，每个节点都可以保存数据，每个节点都有一个版本（从0开始）。
* 使用 UNIX 风格路径名定位 znode，/A/X；
* znode 数据只支持全量读写；
* 所有 API 都是wait-free的。

### znode 分类

1. 持久性的（PERSISTENT）：一旦创建就不会丢失；
2. 临时性的（EPHEMERAL）：zk宕机，或client在指定timeout时间内没有连接server，都会被认为丢失；
3. 持久顺序的（PERSISTENT_SEQUENTIAL）：名字关联一个唯一的单调递增的整数后缀。
4. 临时顺序的（EPHEMERAL_SEQUENTIAL）


## zk架构

* standalone
* quorum（多个节点）

