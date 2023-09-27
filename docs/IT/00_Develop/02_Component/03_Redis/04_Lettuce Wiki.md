# Lettuce Wiki

# 快速开始

1、

# 连接池化

lettuce连接是线程安全的并且默认会自动重连，这使得多个线程可以共享同一个连接。这使得大多数场景下都无需使用连接池。当然，为了少数需要连接池的场景，lettuce提供了通用的连接池支持。

## 真的有必要用连接池吗？

lettuce的线程安全设计可以覆盖绝大部分的使用场景。且redis是单线程执行用户指令的。使用多线程并不一定会提高性能，线程获取专属的连接往往需要进行阻塞操作。Redis事务就是一个典型的使用动态连接池的场景，需要使用同一个连接（*待确认，事务需要同一个连接?*）的多个线程数量会变化。也就是说动态连接池的需求是有限的而引入连接池会增加复杂度和维护成本。

## 执行模式

lettuce支持两种池化模式：
* 同步/阻塞，通过 Apache Commons Pool 2 实现
* 异步/非阻塞，通过 Lettuce-specific pool 实现 [[version5]]

## 同步连接池化

同步连接池化使用声明式编程模型，使得线程上的所有代码都会被执行。（*？*）

### 依赖

依赖于 2.2 版本以上的 Apache common-pool2 来提供池化能力。

### 连接池支持

Lettuce 提供了通用的连接池实现。使用 *Supplier* 来创建各种类型的连接（Redis Standalone，Pub/Sub，Sentinel，Master/Replica，RedisCluster）。*ConnectionPoolSupport* 将根据你的需要创建 *GenericObjectPool* 或者 *SoftReferenceObjectPool* 。池子可以分配包装的或直接的连接。
* 包装的连接通过调用 *StatefulConnection.close()* 可以将连接返还给池子。
* 常规的连接需要通过 *GenericObjectPool.returnObject(...)* 返还。

#### 基本使用方法

``` Java
RedisClient client = RedisClient.create(RedisURI.create(host, port));

GenericObjectPool<StatefulRedisConnection<String, String>> pool = ConnectionPoolSupport.createGenericObjectPool(() -> client.connect(), new GenericObjectPoolConfig());

// executing work
try (StatefulRedisConnection<String, String> connection = pool.borrowObject) {
	RedisCommands<String, String> commands = connection.sync();
    commands.multi();
    commands.set("key", "value");
    commands.set("key2", "value2");
    commands.exec();
}

// terminating
pool.close();
client.shutdown();
```

#### 集群模式使用方法

``` Java
RedisClusterClient clusterClient = RedisClusterClient.create(RedisURI.create(host, port));

GenericObjectPool<StatefulRedisClusterConnection<String, String>> pool = ConnectionPoolSupport
               .createGenericObjectPool(() -> clusterClient.connect(), new GenericObjectPoolConfig());

// execute work
try (StatefulRedisClusterConnection<String, String> connection = pool.borrowObject()) {
    connection.sync().set("key", "value");
    connection.sync().blpop(10, "list");
}

// terminating
pool.close();
clusterClient.shutdown();
```

## 异步连接池化

异步/非阻塞编程模型需要一个非阻塞的API来获取Redis连接。但是一个阻塞的线程池很容易阻塞事件循环，使得应用无法进一步处理。

Lettuce不依赖任何外部依赖，实现了一个异步的，非阻塞的池子，来支持lettuce的一部接接。

### 异步连接池支持

Lettuce提供了异步连接池的实现，这需要一个提供各种连接的*Supplier*，*AsyncConnectionPoolSupport*将会创建一个*BoundedAsyncPool*这个池子可以分配包装的或者直接的连接。
* 包装的连接可以通过调用*StatefulConnection.closeAsync()* 可以将连接返还给池子。
* 常规的连接需要调用*AsyncPool.release(...)* 返还。

#### 基础使用方法

``` Java
RedisClient client = RedisClient.create();

CompletionStage<AsyncPool<StatefulRedisConnection<String, String>>> poolFuture = AsyncConnectionPoolSupport.createBoundedObjectPoolAsync(() -> client.connectAsync(StringCodec.UTF8, RedisURI.create(host, port)), BoundedPoolConfig.create());
 
// await poolFuture initialization to avoid NoSuchElementException: Pool exhausted when starting your application

// execute work
CompletableFuture<TransactionResult> transactionResult = pool.acquire().thenCompose(connection -> {

    RedisAsyncCommands<String, String> async = connection.async();

    async.multi();
    async.set("key", "value");
    async.set("key2", "value2");
    return async.exec().whenComplete((s, throwable) -> pool.release(connection));
});

// terminating
pool.closeAsync();

// after pool completion
client.shutdownAsync();
```

#### 集群模式使用方法

``` Java
RedisClusterClient clusterClient = RedisClusterClient.create(RedisURI.create(host, port));

CompletionStage<AsyncPool<StatefulRedisClusterConnection<String, String>>> poolFuture = AsyncConnectionPoolSupport.createBoundedObjectPoolAsync(
        () -> clusterClient.connectAsync(StringCodec.UTF8), BoundedPoolConfig.create());

// execute work
CompletableFuture<String> setResult = pool.acquire().thenCompose(connection -> {

    RedisAdvancedClusterAsyncCommands<String, String> async = connection.async();

    async.set("key", "value");
    return async.set("key2", "value2").whenComplete((s, throwable) -> pool.release(connection));
});

// terminating
pool.closeAsync();

// after pool completion
clusterClient.shutdownAsync();
```
