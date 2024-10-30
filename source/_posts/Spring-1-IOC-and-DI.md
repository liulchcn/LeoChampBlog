---
title: "\x96Spring(1):IOC and DI"
date: 2024-10-30 08:35:27
tags:
   - 技术
   - Spring
categories:
  - article
author:
 - LeoChamp
---

# 1. IOC 与 DI 概念

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1711624410909-01121db0-4a5a-4598-94ff-307df7ea5e7c.png)

降低依赖

- 使用对象时，在程序中不要主动使用new产生对象，转换为由**外部**提供对象

在传统的编程模式下，对象的创建和依赖的管理通常由开发者手动完成，这意味着类需要主动去创建它所依赖的其他对象。这种方式会导致代码之间的耦合度很高，尤其是在项目规模较大时，管理对象的创建和生命周期变得复杂且难以维护。

**IOC**的核心思想是将对象的创建和依赖关系的管理权交给Spring容器，也就是通过依赖注入（Dependency Injection, DI）来实现。这种“反转”指的是对象不再主动去寻找它的依赖对象，而是由Spring容器在程序运行时，按照配置或注解，自动将依赖注入到对象中。

## 1.1. IOC 容器

Spring 为 IOC 提供了一个容器，称为 **IOC 容器**，充当 IOC 的外部。

IOC 思想中的外部就是 Spring 的 IOC 容器。

- IOC 容器负责对象的创建，初始化。
- 被创建的或则管理的对象在 IOC 中统称 **Bean**。
- IOC 容器中放的就是一个个 Bean 对象。



Bean 其实就是包装了的 Object，无论是控制反转还是依赖注入，它们的主语都是 object，而 bean 就是由第三方包装好了的 object。Bean 是 Spring 的主角，有种说法叫 Spring 就是面向 bean 的编程。



当容器中创建好 service 和 dao 对象后缺少依赖。

- 因为service运行需要依赖dao对象
- IOC容器中虽然有service和dao对象
- 但是service对象和dao对象没有任何关系
- 需要把dao对象交给service,也就是说要绑定service和dao对象之间的关系

绑定 service 和 dao 的关系就要用到依赖注入



## 1.2. DI 依赖注入

在容器中建立bean与bean之间的依赖关系的整个过程，称为**依赖注入**

- 业务层要用数据层的类对象，以前是自己new的
- 现在自己不new了，靠别人[外部其实指的就是IOC容器]来给注入进来
- 这种思想就是依赖注入



IOC和DI这两个概念的最终目标就是:==充分解耦==，具体实现靠:

- 使用IOC容器管理bean（IOC)
- 在IOC容器内将有依赖关系的bean进行关系绑定（DI）
- 最终结果为:使用对象时不仅可以直接从IOC容器中获取，并且获取到的bean已经绑定了所有的依赖关系.



# 2. IOC 相关内容

## 2.1. Bean的属性 scope

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1711628247528-965b0969-5a99-4b3b-a5f7-c247fdf111ef.png)



scope 可以确定 bean 是否单例

- 为什么bean默认为单例?

- bean为单例的意思是在Spring的IOC容器中只会有该类的一个对象
- bean对象只有一个就避免了对象的频繁创建与销毁，达到了bean对象的复用，性能高

- bean在容器中是单例的，会不会产生线程安全问题?

- 如果对象是有状态对象，即该对象有成员变量可以用来存储数据的，
- 因为所有请求线程共用一个bean对象，所以会存在线程安全问题。
- 如果对象是无状态对象，即该对象没有成员变量没有进行数据存储的，
- 因方法中的局部变量在方法调用完成后会被销毁，所以不会存在线程安全问题。

- 哪些bean对象适合交给容器进行管理?

- 表现层对象
- 业务层对象
- 数据层对象
- 工具对象

- 哪些bean对象不适合交给容器进行管理?

- 封装实例的域对象，因为会引发线程安全问题，所以不适合。

# 3. Bean 生命周期

### Bean生命周期的关键阶段

1. **实例化（Instantiation）**：Spring通过构造函数（无参或有参）创建Bean的实例。在这个阶段，如果使用的是构造函数注入，Spring会调用相应的构造函数，并传递所需的依赖。
2. **依赖注入（Dependency Injection）**：在Bean实例化之后，Spring容器会自动处理依赖注入，包括Setter方法注入和字段注入。此时，Spring会根据注解和配置，注入必要的依赖。
3. **初始化（Initialization）**：依赖注入完成后，Spring会调用`@PostConstruct`注解标注的方法，或者执行自定义的初始化方法（如`InitializingBean`接口的`afterPropertiesSet()`方法）。这一步确保Bean在使用前已完成所有必要的初始化工作。
4. **销毁（Destruction）**：当容器关闭或Bean的生命周期结束时，Spring会调用`@PreDestroy`注解标注的方法，或者执行自定义的销毁方法（如`DisposableBean`接口的`destroy()`方法）。





# 4. 注入类型

Spring 依赖注入有三种类型：

- 字段注入
- 构造器注入
- Setter 注入

## 4.1. 字段注入

```java
public class A{
	@Aurowird
	private BService b;
	public void action(){
		b.find();
	}
}
```

我们常用的`@Autowird`就是字段注入。

1. 对象的外部可见性。我们在 A 类中定义的私有变量 b，只能在 a 类中使用，脱离了容器环境就无法访问。

```
A a = new A(); A.action();
```

![img](https://cdn.nlark.com/yuque/0/2024/png/40540759/1712986791284-f69f0494-3542-4533-a6f5-ea14b4b0ebf0.png)

执行这段代码的结果就是抛出一个 NullPointerException 空指针异常，无法在在 A 的外部实例化 b 对象。想要 使用 b 对象只能通过反射的方式

1. 存在潜在的循环依赖。

```
public class ClassA{ @Autowird private ClassB classB; } public class ClassB{ @Autowird private ClassA classA; }
```

1. 我们无法设置需要的注入的对象为 final，也无法注入那些不可变对象。

## 4.2. 构造器注入

```java
public class A{
	private BService b;
	@Autowird
	public A(BService b){
		this.b=b;
	}
	public void action(){
		b.find();
	}	
}
```

构造器注入能**解决对象外部的可见性问题**。

构造器注入能够保证注入的组件不可变，并且确保需要的依赖不为空。

组件不可变就意味着我们可以使用 final 关键词修饰所依赖的对象。依赖不为空是指所传入的依赖对象肯定是一个实例对象，从而避免空指针异常。

一旦采用构造器注入，循环依赖的时候就会抛出循环依赖异常。

## 4.3. Setter 方法注入

```java
public class A{
	pivate ClassB classB;
	@Autowird
	public void setClassB(ClassB classB){
		this.classB=classB;
	}
	public void action(){
		classB.find();
	}
}
```

 Setter方法注入可以在类实例化后再注入依赖项。这种方式灵活，但不如构造函数注入那样具有强制性，可能导致未注入依赖时的空指针异常。  

# 5. Spring 注入依赖分析

无论采用哪种依赖注入机制，前提都是 SpringIOC 容器的正常启动。IOC 的初始化为两大步骤：Bean 的注册和 Bean 的实例化。

## 5.1. Bean 的注册

在使用 Spring 的时候，可以通过获取一个应用上下文（ApplicationContext）对象来操作 Bean。

```java
AnnotationConfigApplicationContext annotationConfigApplicationContext = new AnnotationConfigApplicationContext(B.class);
    
    public AnnotationConfigApplicationContext(Class<?>... componentClasses) {
        this();
        this.register(componentClasses);
        this.refresh();
    }

    public AnnotationConfigApplicationContext(String... basePackages) {
        this();
        this.scan(basePackages);
        this.refresh();
    }
```



这两个构造函数很明确，一个注册，一个根据包的路径配置扫描 Bean。

我们层层追踪 register 可以看到：

```java
    private <T> void doRegisterBean(Class<T> beanClass, @Nullable String name, @Nullable Class<? extends Annotation>[] qualifiers, @Nullable Supplier<T> supplier, @Nullable BeanDefinitionCustomizer[] customizers) {
        AnnotatedGenericBeanDefinition abd = new AnnotatedGenericBeanDefinition(beanClass);
        if (!this.conditionEvaluator.shouldSkip(abd.getMetadata())) {
            abd.setAttribute(ConfigurationClassUtils.CANDIDATE_ATTRIBUTE, Boolean.TRUE);
            abd.setInstanceSupplier(supplier);
            ScopeMetadata scopeMetadata = this.scopeMetadataResolver.resolveScopeMetadata(abd);
            abd.setScope(scopeMetadata.getScopeName());
            String beanName = name != null ? name : this.beanNameGenerator.generateBeanName(abd, this.registry);
            AnnotationConfigUtils.processCommonDefinitionAnnotations(abd);
            int var10;
            int var11;
            if (qualifiers != null) {
                Class[] var9 = qualifiers;
                var10 = qualifiers.length;

                for(var11 = 0; var11 < var10; ++var11) {
                    Class<? extends Annotation> qualifier = var9[var11];
                    if (Primary.class == qualifier) {
                        abd.setPrimary(true);
                    } else if (Lazy.class == qualifier) {
                        abd.setLazyInit(true);
                    } else {
                        abd.addQualifier(new AutowireCandidateQualifier(qualifier));
                    }
                }
            }

            if (customizers != null) {
                BeanDefinitionCustomizer[] var13 = customizers;
                var10 = customizers.length;

                for(var11 = 0; var11 < var10; ++var11) {
                    BeanDefinitionCustomizer customizer = var13[var11];
                    customizer.customize(abd);
                }
            }

            BeanDefinitionHolder definitionHolder = new BeanDefinitionHolder(abd, beanName);
            definitionHolder = AnnotationConfigUtils.applyScopedProxyMode(scopeMetadata, definitionHolder, this.registry);
            BeanDefinitionReaderUtils.registerBeanDefinition(definitionHolder, this.registry);
        }
    }
```

1. 创建一个**AnnotatedGenericBeanDefinition**对象，它是Spring中的一个类，用于存储bean的元数据信息。
2. 检查是否应跳过此bean的注册。这通常是通过检查bean的条件注解（如**@Conditional**）来决定的。
3. 设置bean的属性和实例提供者（如果有的话）。
4. 解析bean的作用域（如singleton，prototype等）。
5. 生成bean的名称。如果提供了名称，就使用提供的名称，否则会自动生成一个。
6. 处理bean的公共定义注解，如**@Lazy**, **@Primary**, **@DependsOn**等。
7. 如果提供了限定符注解，会根据注解类型进行相应的处理。
8. 如果提供了自定义器，会调用自定义器对bean定义进行自定义处理。
9. 创建一个**BeanDefinitionHolder**对象，它是一个bean定义的包装器，包含了bean定义和bean名称。
10. 应用作用域代理模式，这通常用于处理**@ScopedProxy**注解。
11. 最后，将bean定义注册到bean定义注册表中。



该代码块主要是三步骤：

- 构建 BeanDefinition
- 设置 BeanDefinition 属性
- 注册 BeanDefinition



## 5.2. Bena 的实例化

SpringIOC 容器对 Bean 的创建过程并没有完成，只是将 Bean 加载到容器中。容器本身可能存在这些 Bean的定义，所以我们还需要 `refresh()`方法刷新容器。

在此仅仅列出了相关代码

```java
	@Override
	public void refresh() throws BeansException, IllegalStateException {
		this.startupShutdownLock.lock();
		try {
			this.startupShutdownThread = Thread.currentThread();

			StartupStep contextRefresh = this.applicationStartup.start("spring.context.refresh");

			// Prepare this context for refreshing.
			prepareRefresh();

			// Tell the subclass to refresh the internal bean factory.
			ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

			。。。。。。

			try {
				。。。。。
				
				// Instantiate all remaining (non-lazy-init) singletons.
				finishBeanFactoryInitialization(beanFactory);

				// Last step: publish corresponding event.
				finishRefresh();
			}
			。。。。
		}
		finally {
			this.startupShutdownThread = null;
			this.startupShutdownLock.unlock();
		}
	}
```

1. **获取Bean工厂**：调用**obtainFreshBeanFactory()**方法，完成 BeanDefinition 注册并返回一个 BeanFactory。对于 AnnotationConfigApplication 而言就是将 BeanDefinition 注册到 `DefaultListableFactory`。
2. **完成Bean工厂的初始化**：调用**finishBeanFactoryInitialization(beanFactory)**方法，实例化所有剩余的（非延迟初始化）单例。

```java
protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) throws BeanCreationException {
       。。。
            instanceWrapper = (BeanWrapper)this.factoryBeanInstanceCache.remove(beanName);
        }

        if (instanceWrapper == null) {
            instanceWrapper = this.createBeanInstance(beanName, mbd, args);
        }

        Object bean = instanceWrapper.getWrappedInstance();
。。。。。

        Object exposedObject = bean;

        try {
            this.populateBean(beanName, mbd, instanceWrapper);
            exposedObject = this.initializeBean(beanName, exposedObject, mbd);
             。。。。。
        }
```

三个核心方法：

- createBeanInstance：实例化

根据配置生成具体的 Bean，最终通过基于构造器的反射方法实现这一目标。Bean 被创建了但是不完整，属性还没有被注入

- populateBean：填充属性

用于实现属性的自动注入，包含 byName，byType 类型的自动装配，基于@Autowird，@value注解的属性设值。这里的 Bean 可以说是算是完整的了。

- initializeBean：扩展

这个更多的是一种扩展性的实现机制，用于 Bean 初始化完成之后执行一些定制化操作。

# 6. 循环依赖分析

为什么 setter 方法注入可以解决循环依赖问题，而构造器不能。

对于单例作用域来说，Spring 容器在整个生命周期内，有且只有一个 Bean 对象，这个对象应该存在缓存中。Spring 为了解决单例 Bean 的循环以来问题，会使用三级缓存。

## 6.1. 三级缓存结构

```java
	/** Cache of singleton objects: bean name to bean instance. */
	private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256);

	/** Cache of singleton factories: bean name to ObjectFactory. */
	private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16);

	/** Cache of early singleton objects: bean name to bean instance. */
	private final Map<String, Object> earlySingletonObjects =
                                               new ConcurrentHashMap<>(16);
```

- singletonObjects 是一级缓存，用来持有完整的 Bean 实例。
- earlySingletonObjects 存放的是那些提前暴露的对象。也就是已经创建还没有注入的对象，属于二级缓存。
- singletonFactories 存放用来创建 earlySingletonObjects 的工厂对象属于三级缓存。





```java
@Nullable
	protected Object getSingleton(String beanName, boolean allowEarlyReference) {
		// Quick check for existing instance without full singleton lock
		Object singletonObject = this.singletonObjects.get(beanName);
		if (singletonObject == null && isSingletonCurrentlyInCreation(bean Name)) {
			singletonObject = this.earlySingletonObjects.get(beanName);
			if (singletonObject == null && allowEarlyReference) {
				synchronized (this.singletonObjects) {
					// Consistent creation of early reference within full singleton lock
					singletonObject = this.singletonObjects.get(beanName);
					if (singletonObject == null) {
						singletonObject = this.earlySingletonObjects.get(beanName);
						if (singletonObject == null) {
							ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
							if (singletonFactory != null) {
								singletonObject = singletonFactory.getObject();
								this.earlySingletonObjects.put(beanName, singletonObject);
								this.singletonFactories.remove(beanName);
							}
						}
					}
				}
			}
		}
		return singletonObject;
	}
```

1. **singletonObjects**：这是一个存储已经创建的单例对象的Map。首先，方法会尝试从这个Map中获取指定名称的单例对象。
2. **isSingletonCurrentlyInCreation**：这个方法用来检查指定名称的单例对象是否正在创建中。如果正在创建中，那么就会尝试从**earlySingletonObjects**这个Map中获取对象。
3. **earlySingletonObjects**：这是一个存储提前暴露的单例对象的Map，也就是还未完成创建的单例对象（例如，当一个单例Bean的构造器中又依赖了自己，就需要提前暴露）。
4. **allowEarlyReference**：这个参数决定了是否允许获取提前暴露的单例对象。如果允许，那么就会尝试从**earlySingletonObjects**中获取对象。
5. **singletonFactories**：这是一个存储单例对象工厂的Map。如果在**singletonObjects**和**earlySingletonObjects**中都没有获取到对象，那么就会尝试从**singletonFactories**中获取对象工厂，然后通过工厂创建对象。
6. 在创建新的单例对象后，会将其添加到**earlySingletonObjects**中，并从**singletonFactories**中移除相应的工厂。

![img](https://cdn.nlark.com/yuque/0/2024/jpeg/40540759/1722825939379-8265e47a-49d8-48e3-83d9-0dd3b4eec580.jpeg)



## 6.2. 循环依赖解决方案

### 6.2.1. 概括

Spring引入了"早期引用"的概念。当一个单例Bean被创建时，Spring会先将这个尚未完全初始化的Bean实例（属性还未全部注入）放入**earlySingletonObjects**这个Map中，这样如果后续有其他Bean依赖于它，就可以直接使用这个早期引用，从而打破循环依赖。

在这段代码中，如果**allowEarlyReference**参数为**true**，那么就允许获取提前暴露的单例对象，也就是允许获取尚未完全初始化的Bean实例。这就是这段代码如何处理循环依赖的关键。

### 6.2.2. 详细

```java
	/**
	 * Add the given singleton factory for building the specified singleton
	 * if necessary.
	 * <p>To be called for eager registration of singletons, e.g. to be able to
	 * resolve circular references.
	 * @param beanName the name of the bean
	 * @param singletonFactory the factory for the singleton object
	 */
	protected void addSingletonFactory(String beanName, ObjectFactory<?> singletonFactory) {
		Assert.notNull(singletonFactory, "Singleton factory must not be null");
		synchronized (this.singletonObjects) {
			if (!this.singletonObjects.containsKey(beanName)) {
				this.singletonFactories.put(beanName, singletonFactory);
				this.earlySingletonObjects.remove(beanName);
				this.registeredSingletons.add(beanName);
			}
		}
	}
```

这段代码执行时机是在已经通过构造函数创建 Bean，但还没有完成对 Bean 中完整属性的注入。Bean 已经可以被暴露进行识别了，但还不能使用。



```java
public class A{
	private ClassB b;
	@Autowird
	public void setClassB(ClassB b){
		this.b=b;
	}
}
public class B{
	private ClassA a;
	@Autowird
	public void setClassA(ClassA a){
		this.a=a;
	}
}
```

1. 先初始化 ClassA。ClassA 首先通过 `createBeanInstacne()`方法创建实例，并且将实例提前暴露到第三级缓存 `singletonFactories`中。
2. ClassA 尝试通过 populateBean()注入属性，发现依赖 ClassB，就去回去 ClassB 的实例。
3. ClassB 没创建，走创建流程。发现依赖 ClassA，就尝试从第一级缓存 `singletonObjects` 去获取 ClassA 的实例。因为没创建完，一级二级缓存不存在，在第三级中，通过 `singletonFactories`工厂拿出 ClassA，并生成 ClassA 对象，把 ClassA 的三级缓存删除加入二级缓存。
4. 完成ClassB的初始化，并把ClassB对象加入到一级缓存，二级缓存删除
5. ClassA此时就可以正常的填充属性值了，因为ClassB已经初始化完成
6. ClassA初始化完成并把ClassA添加到一级缓存中，删除二级缓存

构造器无法解决循环依赖问题。这是因为构造器注入过程中是发生在 Bean 初始化的第一个步骤`createBeanInstance()`中,而这个方法还没调用 `addSingleFactory()`方法完成第三级缓存的构建。

## 6.3. 循环依赖问题

1. **不就是存一下半成品的对象吗，有必要弄三个缓存吗？一个不行？两个足够了吧？**

如果是单纯的解决循环依赖的问题（其他啥也不管，就解决依赖的事）！那其实用一个缓存或者两个缓存都行。



1. **如果在ClassA把半成品对象放入缓存后，另一个地方也要用这个对象，直接从缓存拿出来了怎么办？**

其实对于这个问题在大部分对象上可能发生的概率不大。

如果非要解决。

那么可以加锁的方式，在对象创建完成之前不允许获取对象。

1. **如果是这个流程，那就意味着实例化的时候就要生成代理对象并放入缓存，这可就和原来的非循环依赖流程不一样了。**

   

对于这个问题。

我个人认为就有点偏设计思路方面的问题了。
如果是我的话，不到万不得已，我是绝对不会改变原流程的。



**用两个缓存的流程：**

其实和上面差不多。

只是可以把半成品对象放入二级缓存，创建完成的对象放入一级缓存。

这样就不会出现用一个缓存时候的问题。

但是问题2依然存在。

具体可以自己串下流程。





**4. 这三个缓存到底有啥用啊，难道就只是为了解决循环依赖问题？**

准确的来说二级缓存和三级缓存就是为了解决循环依赖问题而存在的。

但是一级缓存不是！

| 缓存级别 | 缓存内容                                   | 作用                                                         |
| -------- | ------------------------------------------ | ------------------------------------------------------------ |
| 一级缓存 | 创建完成的对象                             | 提升对象获取速度保证Singleton类型对象的全局唯一性            |
| 二级缓存 | 半成品对象（执行三级缓存的逻辑生成的对象） | 保证代理对象的唯一性，比如对象A依赖B和C，并且B和C都依赖A，那么如果没有二级缓存的话。B，C两个可能会调用两次三级缓存中的逻辑生成对象，也就生成了两个代理对象。当然最终目的也是为了和三级缓存配合解决循环依赖问题。 |
| 三级缓存 | 创建代理对象的工厂                         | 三级缓存的存在其实就是因为Spring的开发者不想要改变原来的生成代理对象的流程（在初始化阶段生成代理对象），而为解决循环依赖问题加的一个补丁，所以如果没有循环依赖的时候用不到三级缓存，自然也就用不到二级缓存。但是一旦有了循环依赖，就利用二级和三级提前生成代理对象。 |

- 第一层缓存：最基础的缓存，创建完并初始化（createBean）后的bean实例会放入，项目启动完成后获取bean实例时从此获取
- 第三层缓存：创建bean过程中用于处理循环依赖的临时缓存，由于只有在初始化时才知道有没有循环依赖，所以通过ObjectFactory临时“存储”刚创建完的bean，并延迟触发循环依赖时被引用的bean需要赋值当前bean时去获取当前bean的逻辑，且获取对象会作为当前bean的最终对象
- 第二级缓存：创建bean过程中用于处理循环依赖的临时缓存，搭配第[三层缓存](https://www.zhihu.com/search?q=三层缓存&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A2443911807})，用于其ObjectFactory返回对象的缓存，保证多个关联对象对当前bean的引用为同一个


 

# 7. 添加中间层

1. 提取中介者
2. 转移 业务逻辑
3. 引入回调





# 8. 实战经验

要了解熟悉这几个注解

```
@Scop``@Primary
@Qualifier
```



当 Bean 的范围被设为 **prototype** 的时候，每次请求 Bean，SpringIOC 容器都会创建一个新的对象实例。所以使用原型模式在创建过程中会对性能产生影响。对于网络连接对象，数据库连接对象在初始化过程中消耗巨大资源的，应避免使用原型模式。



Spring IOC 容器的延迟加载和预加载机制。通过`@Autowird`注解注入的 Bean 都是在 SpringIOC 启动的时候被创建和初始化，这个过程称为预加载。

添加`@Lazy`注解的效果是只有使用到这个 Bean 时才会去初始化。



**有状态会话bean**   ：每个用户有自己特有的一个实例，在用户的生存期内，bean保持了用户的信息，即“有状态”；一旦用户灭亡（调用结束或实例结束），bean的生命期也告结束。即每个用户最初都会得到一个初始的bean。简单来说，有状态就是有数据存储功能。有状态对象(Stateful Bean)，就是有实例变量的对象 ，可以保存数据，是**非线程安全**的。
**无状态会话bean**   ：bean一旦实例化就被加进会话池中，各个用户都可以共用。即使用户已经消亡，bean   的生命期也不一定结束，它可能依然存在于会话池中，供其他用户调用。由于没有特定的用户，那么也就不能保持某一用户的状态，所以叫无状态bean。但无状态会话bean   并非没有状态，如果它有自己的属性（变量），那么这些变量就会受到所有调用它的用户的影响，这是在实际应用中必须注意的。简单来说，无状态就是一次操作，不能保存数据。无状态对象(Stateless Bean)，就是没有实例变量的对象 .不能保存数据，是不变类，是**线程安全**的。



# 9. 面试题

1. 对于某个接口，需要提供的多个实现类，且都能够被注入到 SpringIOC 容器中怎么办

1. `@Primary`设置主实现类。
2. 使用`@Qualifier`注解来为不同的的实现类命名，根据不同名称来注入目标对象。

1. 缩短 IOC 容器启动时间怎么办

1. `@ComponentScan`注解来控制组件的扫描范围
2. 合理设置 Bean 的作用域来降低对象的创建成本
3. 使用延时加载机制来控制 Bean 的初始化时机。

1. Spring 中 Bean 的实例化包括哪些步骤

1. 基于构造器的反射方法创建 Bean
2. 通过属性注入实例化 Bean
3. 通过回调机制扩展 Bean

1. 解决循环依赖的步骤

1. 使用@Lazy注解：@Lazy注解可以延迟Bean的实例化，从而避免循环依赖的问题。
2. @Autowired注解的required属性：将required属性设置为false，以避免出现循环依赖问题。
3. 三级缓存：Spring使用三级缓存解决循环依赖，这也是一个重要的知识点。
