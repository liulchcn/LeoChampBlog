---
title: Spring(3):AOP
date: 2024-10-30 08:51:44
tags:
   - 技术
   - Spring
categories:
  - article
author:
 - LeoChamp
---

## 一、代理模式

-  代理类（代理主题） 
- ⽬标类（真实主题） 
- 代理类和⽬标类的公共接⼝（抽象主题）：客户端在使⽤代理类时就像在 使⽤⽬标类，不被客户端 所察觉，所以代理类和⽬标类要有共同的⾏为，也就是实现共同的接⼝  

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1724753145508-bb4f4a45-ef9d-4f7a-b97b-8345f01ee60f.png)

### 静态代理

AOP 底层是动态代理实现的。

Spring 的 AOP 的动态代理时 JDK 动态代理和 CGLIB 动态代理技术

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1724771556638-ea108af0-264b-4e59-bddb-052c7258487a.png)

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1724771574031-354964f1-dc20-4903-9998-3008b831213b.png)

### 动态代理

-  JDK动态代理技术：**只能代理接⼝。**
-  CGLIB动态代理技术：CGLIB(Code Generation Library)是⼀个开源项⽬。是⼀个强⼤的，⾼性 能，⾼质量的Code⽣成类库，它可以在运⾏期扩展Java类与实现Java接⼝**。它既可以代理接⼝，⼜ 可以代理类**，底层是通过继承的⽅式实现的。性能⽐JDK动态代理要好。（底层有⼀个⼩⽽快的字 节码处理框架ASM。） 
- Javassist动态代理技术：Javassist是⼀个开源的分析、编辑和创建Java字节码的类库。是由东京⼯ 业⼤学的数学和计算机科学系的 Shigeru Chiba （千叶 滋）所创建的。它已加⼊了开放源代码 JBoss 应⽤服务器项⽬，通过使⽤Javassist对字节码操作为JBoss实现动态"AOP"框架。  

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1724771669267-4207a611-df1c-4a28-b87c-3f69164deb38.png)

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1724771685404-dc66de9b-7d80-44fc-af06-c21b1812c99f.png)

 我们在静态代理的时候，除了以上⼀个接⼝和⼀个实现类之外，是不是要写⼀个代理类 UserServiceProxy呀！在动态代理中UserServiceProxy代理类是可以动态⽣成的。这个类不需要写。我 们直接写客户端程序即可  

```java
public class Client {
	public static void main(String[] args) {
		// 创建⽬标对象
		OrderService target = new OrderServiceImpl();
		// 创建代理对象
		OrderService orderServiceProxy = (OrderService) Proxy
						.newProxyInstance(targt.getClass().getClassLoader(),
										  target.getClass().getInterfaces(),
										  new TimerInvocationHandler(target));
		// 调⽤代理对象的代理⽅法
		orderServiceProxy.detail();
		orderServiceProxy.modify();
		orderServiceProxy.generate();
	}
}
 OrderService orderServiceProxy = Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), 调⽤处理器对象); 
```

这⾏代码做了两件事： 第⼀件事：在内存中⽣成了代理类的字节码 第⼆件事：创建代理对象 Proxy类全名：java.lang.reflect.Proxy。这是JDK提供的⼀个类（所以称为JDK动态代理）。主要是通过 这个类在内存中⽣成代理类的字节码  。

 其中newProxyInstance()⽅法有三个参数： 

- 第⼀个参数：类加载器。在内存中⽣成了字节码，要想执⾏这个字节码，也是需要先把这个字节码 加载到内存当中的。所以要指定使⽤哪个类加载器加载。 
- 第⼆个参数：接⼝类型。代理类和⽬标类实现相同的接⼝，所以要通过这个参数告诉JDK动态代理 ⽣成的类要实现哪些接⼝。 
- 第三个参数：调⽤处理器。这是⼀个JDK动态代理规定的接⼝，接⼝全名： java.lang.reflect.InvocationHandler。显然这是⼀个回调接⼝，也就是说调⽤这个接⼝中⽅法的程 序已经写好了，就差这个接⼝的实现类了。  



```java
public class TimerInvocationHandler implements InvocationHandler {
	//目标对象
	private Object target;
	// 通过构造⽅法来传⽬标对象
	public TimerInvocationHandler(Object target) {
		this.target = target;
	}
    @Override
 public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
	 // ⽬标执⾏之前增强。
	 long begin = System.currentTimeMillis()；
	 // 调⽤⽬标对象的⽬标⽅法
	 Object retValue = method.invoke(target, args);
	 // ⽬标执⾏之后增强。
	 long end = System.currentTimeMillis();
	 System.out.println("耗时"+(end - begin)+"毫秒");
	 return retValue;
 }
}
```

 ⼤家可能会⽐较好奇：那个InvocationHandler接⼝中的invoke()⽅法没看⻅在哪⾥调⽤呀？ 注意：当你调⽤代理对象的代理⽅法的时候，注册在InvocationHandler接⼝中的invoke()⽅法会被调⽤。所以不用每次都去使用了。  



```java
 public class ProxyUtil {
	 public static Object newProxyInstance(Object target) {
		 return Proxy.newProxyInstance(target.getClass().getClassLoader(),
									   target.getClass().getInterfaces(), 
									   new TimerInvocationHandler(target));
	 }
 }


public class Client {
	public static void main(String[] args) {
		// 创建⽬标
		OrderService target = new OrderServiceImpl()‘
		// 创建代理对象
		OrderService orderServiceProxy = (OrderService) ProxyUtil
										  .newProxyInstance(target);
		// 调⽤代理对象的代理⽅法
		orderServiceProxy.detail();
		orderServiceProxy.modify();
		orderServiceProxy.generate();
	}
}
```



### CGLIB 动态代理

如下是一个没有接口的类，

```java
public class UserService {
	public void login(){
		 System.out.println("");
	}
	public void logout(){
		System.out.println("");
	}
}
```

使用 CGLIB 在内存中为 UserService 类生成代理类，并创建对象：

```java
 public class Client {
	 public static void main(String[] args) {
		 // 创建字节码增强器
		 Enhancer enhancer = new Enhancer();
		 // 告诉cglib要继承哪个类
		 enhancer.setSuperclass(UserService.class);
		 // 设置回调接⼝,⽅法拦截器对象
		 enhancer.setCallback(new TimerMethodInterceptor());
		 // ⽣成源码，编译class，加载到JVM，并创建代理对象
		 UserService userServiceProxy = (UserService)enhancer.create();
		 userServiceProxy.login();
		 userServiceProxy.logout();
	 }
 }
```

 和JDK动态代理原理差不多，在CGLIB中需要提供的不是InvocationHandler，⽽是： net.sf.cglib.proxy.MethodInterceptor  。

```java
public class TimerMethodInterceptor implements MethodInterceptor {
	// 第⼀个参数：⽬标对象
	// 第⼆个参数：⽬标⽅法
	// 第三个参数：⽬标⽅法调⽤时的实参
	// 第四个参数：代理⽅法
    @Override
	public Object intercept(Object target, Method method, Object[] objects, 
							MethodProxy methodProxy) throws Throwable {
		 // 前增强
		long begin = System.currentTimeMillis();
		// 调⽤⽬标
		Object retValue = methodProxy.invokeSuper(target, objects);
		// 后增强
		long end = System.currentTimeMillis();
		System.out.println("耗时" + (end - begin) + "毫秒");
		// ⼀定要返回
		return retValue;
	}
}
```





## 二、面向切面编程

动态代理就是面向编程的思想实现。

对于业务逻辑无关的代码单独做一个模块。



 Spring的AOP使⽤的动态代理是：JDK动态代理 + CGLIB动态代理技术。Spring在这两种动态代理中灵 活切换，如果是代理接⼝，会默认使⽤JDK动态代理，如果要代理某个类，这个类没有实现接⼝，就会 切换使⽤CGLIB。当然，你也可以强制通过⼀些配置让Spring只使⽤CGLIB。  



### (一) AOP 的七大术语

#### 1. 连接点 Jointpoint

在**程序整个流程**，可以织入切面位置。描述的是一种位置

#### 2. 切点 Pointcut

本质上就是真正织入切面方法。

#### 3. 通知 Adivice

通知又叫增强，通知描述的是：具体代码

#### 4. 切面

切点+通知就是切面

如果你是面试官，我会这样讲述CGLIB和JDK动态代理：

### (二)  什么是动态代理？

动态代理是在程序运行时生成代理类，而不是在编译时生成。代理类可以用来增强目标对象的功能，比如在方法调用前后添加日志、权限检查、事务管理等。

#### JDK动态代理

JDK动态代理基于Java的反射机制，只能代理实现了接口的类。其核心是`java.lang.reflect.Proxy`类和`InvocationHandler`接口。

- **实现原理**：

- JDK动态代理通过实现目标对象的接口，并在方法调用时通过反射来调用目标对象的方法。
- `Proxy.newProxyInstance()`方法用于创建代理对象，参数包括类加载器、接口和调用处理器（`InvocationHandler`）。
- `InvocationHandler`接口中定义了`invoke`方法，当代理对象调用方法时，`invoke`方法会被调用，可以在此处进行额外操作（如日志、权限等）。

- **优点**：

- 简单易用，直接基于接口。
- 不依赖第三方库，JDK原生支持。

- **缺点**：

- 只能代理实现了接口的类，无法代理没有接口的类。

- **应用场景**：

- 适用于代理实现了接口的类，比如Spring AOP中的面向接口编程。

#### CGLIB动态代理

CGLIB（Code Generation Library）是一种强大的字节码生成库，它通过**继承**目标类的方式来实现代理，因此可以代理没有实现接口的类。

- **实现原理**：

- CGLIB通过生成目标类的子类，并在子类中拦截方法调用来实现代理。
- 它通过继承目标类，并重写其方法，在方法调用前后添加增强逻辑。
- 核心类是`net.sf.cglib.proxy.Enhancer`和`MethodInterceptor`接口。

- **优点**：

- 可以代理没有接口的类，适用范围更广。
- 性能比JDK动态代理更高，尤其在大量代理对象时表现明显。

- **缺点**：

- 代理的类不能是`final`类，目标方法不能是`final`或`private`方法，因为这些都不能被继承或重写。
- 需要依赖CGLIB库，增加了一些复杂性。

- **应用场景**：

- 适用于代理没有实现接口的类，或者希望通过继承来代理类的场景。Spring AOP中，当目标类没有实现接口时，默认使用CGLIB动态代理。

####  JDK动态代理 vs CGLIB动态代理

- **实现方式**：

- JDK动态代理是基于接口实现的，通过反射调用目标对象的方法。
- CGLIB动态代理是基于继承目标类，通过生成子类并重写方法实现代理。

- **使用场景**：

- JDK动态代理适合有接口的场景，代理的是接口的方法调用。
- CGLIB动态代理适合无接口的场景，可以代理普通类。

- **性能**：

- CGLIB动态代理通常性能更高，因为它直接生成字节码并调用，但创建代理对象的时间稍慢。
- JDK动态代理在小规模代理时性能差异不明显，但大量代理对象时性能稍逊于CGLIB。

- **Spring中的应用**：

- Spring AOP默认使用JDK动态代理，如果目标类没有实现接口，则使用CGLIB动态代理。





- **JDK动态代理**适合接口代理，简单直接，Java原生支持。
- **CGLIB动态代理**适合普通类代理，功能强大，适用范围广，但需要第三方库支持。

通过这两种代理机制，Java可以实现强大的AOP编程，使得代码在不改变原有逻辑的情况下增强功能。两者各有优劣，选择时应根据具体应用场景做出决定。

### (三) 具体使用 AOP

- Spring 框架结合 AspectJ 框架实现 AOP，基于注解方式。
- Spring 框架结合 AspectJ 框架实现 AOP，基于 XML 方式



Spring 容器在扫描类的时候，查看该类上是否有@Aspect注解，如果有，则给这个类生成代理对象。

### (四) 切面顺序

通过@Order来控制

### (五) JoinPoint 和**ProceedingJoinPoint**，连接点

连接点是方法，切点也是方法，每个方法都是连接点，但只有要增强功能即被切点表达式涵盖的叫切入点；所有切入点一定是连接点，连接点不一定是切入点。。



可以根据 JointPoint 得到目标方法签名。通过方法的签名可以获取到方法的具体信息。



`ProceedingJoinPoint` 是 `JoinPoint` 的子接口，增加了 `proceed()` 方法，可以控制目标方法的执行。通常用于环绕通知（Around Advice）中，你可以通过 `proceed()` 方法调用目标方法，并在调用前后执行一些逻辑。它允许你在方法执行前后进行操作，**比如修改参数或返回值，甚至阻止目标方法的执行**。  



### (六) 全注解式开发

```java
 @Configuration
 @ComponentScan("com.powernode.spring6.service")
 @EnableAspectJAutoProxy(proxyTargetClass = true)
 public class Spring6Configuration {
 
```
