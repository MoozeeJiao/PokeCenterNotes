# Java Service Provider Interface

JDK 内置的一种服务提供发现机制。是一种动态替换发现的机制，比如一个接口想在运行时动态给他添加实现，只需要添加一个实现然后把他描述给 JDK 即可（通过改一个文本文件）。Dubbo，[[01_Flink#自定义connector| Flink加载connector]] 就使用了 SPI。

## 使用

1. 需要1个目录
	* META/services
	* 放到 ClassPath 下面
2. 目录下面放置一个配置文件
	* 文件名是扩展接口的全名（com.abc.HelloInterface）
	* 文件内部为接口的实现类
	* 文件必须为 UTF-8 编码
3. 使用
	* ServiceLoad\<HelloInterface\>  loads = ServiceLoad.load(HelloInterface.class)