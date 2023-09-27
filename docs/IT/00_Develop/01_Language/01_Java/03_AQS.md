# AbstractQueuedSynchronizer

## 功能介绍

锁和同步器（信号量、事件等）的实现框架，这些组件都依赖于一个 FIFO 的等待队列。AQS 用单一的原子 int 来表示状态，代表对象被获取或者释放。子类需要定义 protected 方法来实现状态的转换。有了这些，AQS 中的其他方法就能实现排队和阻塞机制。子类可以维护其他状态变量，但只有通过 *getState*, *setState*, *compareAndSetState* 方法操作的原子 int 值会被用来控制同步功能。

