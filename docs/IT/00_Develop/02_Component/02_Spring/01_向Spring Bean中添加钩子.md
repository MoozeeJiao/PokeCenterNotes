
# 向Spring Bean中添加钩子

## Spring Bean

Bean 是由 ApplicationContext 创建、编排、销毁的实例。根据 Bean 的不同生命周期，我们可以在不同的阶段加入钩子以实现不同的目的。

## Bean 的生命周期

### Bean 的创建阶段

* **Instantiation（实例化）**: bean最初始的阶段，实例化就像创建一个java实体一样。
* **Populating Properties（填充属性）**: Spring扫描实现了 Aware 接口的 bean，通过回调函数设置相关参数。
* **Pre-Initialization（预初始化）**: BeanPostProcessor开始调用 postProcessBeforeInitialization() 方法，之后 @PostConstruct 注解的方法也会立即运行。
* **AfterPropertiesSet（标准初始化）**: 执行实现了 InitializingBean 接口的 bean 的 afterPropertiesSet() 方法。
* **Custom Initialization（自定义初始化）**: 触发 @Bean 注解中定义的 initMethod 方法。
* **Post-Initialization（后初始化）**: BeanPostProcessor再次工作，调用 postProcessAfterInitialization() 方法。

### Bean 的销毁阶段

* **Pre-Destory（预销毁）**: Spring 触发 @Pre-Destory 注解标注的方法。
* **Destory（销毁）**:  执行实现了 DisposableBean 接口的 bean 的 destroy() 方法。
* **Custom Destruction（自定义初始化）**: 触发 @Bean 注解中定义的的 destory 方法。

## 加入钩子函数

### 1、使用spring提供的回调接口

在标准初始化阶段自定义操作

```java
@Component
class MyStringBean implements InitializingBean {
	@Override
	public void afterPropertiesSet() {
	}
}
```

在标准销毁阶段操作

```java
@Component
class MyStringBean implements DisposableBean {
	@Override
	public void destory() {
	}
}
```

### 2、使用JSR-250注解

使用 @PostConstruct 和 @PreDestory 注解，在预初始化和预销毁阶段加入函数

```java
@Component
class MyStringBean {
	@PostConstruct
	public void pc() {
	}

	@PreDestory
	public void pd() {
	}
}
```

### 3、使用@Bean注解的属性

使用@Bean注解的 initMethod 和 destoryMethod 方法

```java
@Configuration
class MyStringBeanConf {
	@Bean(initMethod = "onInit", destoryMethod = "onDestory")
	public MySpringBean nySPringBean() {
	}
}
```

如果bean中由名为 close() 或 shutdown() 的方法，那么它们会被默认当作自定义销毁方法。如果我们不希望这样，可以用 destoryMethod="" 来禁用这种默认

### 4、使用Bean后处理器 BeanPostProcessor

利用 BeanPostProcessor 接口在 bean 初始化之前或之后运行自定义操作，甚至返回修改后的 bean

```java
class MyBeanPostProcessor implements BeanPostProcessor {

	@Override
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
	//...
	return bean;
	}

	public Object postProcessAfterInitialization(Object bean, String beanName) throw BeansException {
	//...
	return bean;
	}
}
```

*注意：BeanPostProcessor 是针对 spring 上下文中的所有 bean*

### 5、Aware 接口

```java
@Component
class MySpringBean implements BeanNameAware, ApplicationContextAware {

	@Override
	public void setBeanName(String name) {
		//...
	}

	public void setApplicationContext(ApplicationCOntext applicationContext) throws BeansException {
		//...
	}
}
```

## 执行顺序

--- setBeanName executed --- 
--- setApplicationContext executed --- 
--- postProcessBeforeInitialization executed --- -
-- @PostConstruct executed --- 
--- afterPropertiesSet executed --- 
--- init-method executed --- 
--- postProcessAfterInitialization executed --- 
... 
--- @PreDestroy executed --- 
--- destroy executed --- 
--- destroy-method executed ---



