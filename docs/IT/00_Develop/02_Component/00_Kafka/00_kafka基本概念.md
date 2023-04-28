# Kafka基本概念

### Leader Epoch

#### follower LEO 更新

kafka 有*两套 follower LEO*：
+ 一套保存在 follower 副本所在 broker 的副本管理机中（1）；
+ 一套在 leader 所在 broker 的副本管理机中（2）。

follwer 端的 follower LEO 在写入一条新消息时更新；

leader 端的 follower LEO 在处理 follwer 的 fetch 请求时，它会先从自己的 log 中读取相应的数据，但在将数据返回给 follower 之前（根据 fetch 请求中的 offset）更新 follower LEO。

#### follower HW 更新

写完消息后，followr 会更新自己的 HW = min( leader HW, follower LEO)

#### leader LEO 更新

在写入一条新消息时更新。

#### leader HW 更新

以下4情况会尝试更新：

+ 成为 leader 副本时；（异常）
+ broker 崩溃导致副本被踢出 ISR 时；（异常）
+ 写入消息时；（正常）
+ 处理 fetch 请求时。（正常）

正常时，leader 会根据自己和保存的符合条件的 follower LEO 选一个最小的 LEO 当作 HW。满足两条件之一即可：

+ 在 ISR 中；
+ LEO 落后 leader LEO 的时常不小于 replica.lag.time.max.ms （某些恢复的副本，不在ISR里但是追上了进度）

![[hw_update_1.png]]

*HW 需要额外一轮 fetch 才能更新，这种设计是有问题的*。

可能引起：

1. 数据丢失
2. 数据不一致

典型场景都是 min.insync.replicas = 1，宕机未完成同步或更新 HW，切换leader。根因在 HW 被用于衡量副本同步成功与否和日志截断。

#### kafka 0.11 版本解决方案

leader epoch 取代 HW，是一对值 (epoch, offset)。epoch 表示 leader 版本号， offset 表示该版本写入的第一条消息位移。

broker 中会保存这样的一个缓存，并定期写入 checkpoint 文件中。保存自己当leader时开始写入的第一条消息的offset以及leader版本。这样在恢复的时候完全使用这些信息而非水位来判断是否需要截断日志。













