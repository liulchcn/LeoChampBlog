---
title: Spring(2):Bean
date: 2024-10-30 08:49:00
tags:
   - 技术
   - Spring
categories:
  - article
author:
 - LeoChamp
---

# 一、Bean 的生命周期

 Bean⽣命周期的管理，可以参考Spring的源码：`AbstractAutowireCapableBeanFactory`类的 `doCreateBean()`⽅法。  



- **第一步：实例化 Bean**
- **第二步：Bean 的属性赋值**

- 检查 Bean 是否实现了 Aware 的相关接口，并设置相关依赖。

- Bean 后处理器 Beafore 执行

- 检查 Bean 是否实现了 InitialBean 接口**，**并且调用接口方法

- **第三步：初始化 Bean**

- Bean 后处理器 after 执行

- **第四步：使用 Bean**

- 检查是否实现了 DisposableBean 的接口，并调用接口方法

- **第五步：销毁 Bean**



### (一) Bean 实现 Aware。

- 当Bean实现了BeanNameAware，Spring会将**Bean的名字**传递给Bean。
-  当Bean实现了BeanClassLoaderAware，Spring会将加载该**Bean的类加载器**传递给Bean。 
- 当Bean实现了BeanFactoryAware，Spring会将**Bean⼯⼚对象**传递给Bean。  

### (二) Bean 实现 InitialBean 接口

- **资源初始化**：你可以在 `afterPropertiesSet()` 方法中初始化一些资源，比如打开文件、连接数据库等。
- **数据校验**：在 Bean 准备好之前，可以对注入的属性或依赖进行校验，确保它们符合预期。
- **启动任务**：例如启动后台任务、定时器等。

 要使用 `InitializingBean` 接口，你需要让你的 Bean 类实现该接口，并重写 `afterPropertiesSet()` 方法。下面是一个简单的示例：  

```java
import org.springframework.beans.factory.InitializingBean;
import org.springframework.stereotype.Component;

@Component
public class MyBean implements InitializingBean {

    private String name;

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        // 初始化逻辑
        System.out.println("InitializingBean: 所有属性设置完成后执行初始化逻辑");
        if (name == null || name.isEmpty()) {
            throw new IllegalArgumentException("name 属性不能为空");
        }
        // 其他初始化操作
    }
}
```

#### 1. 与 `@PostConstruct` 的对比

`InitializingBean` 是一种基于接口的初始化方式，Spring 还提供了基于注解的方式，即使用 `@PostConstruct` 注解。二者的功能类似，但有一些区别：

- **代码耦合**：`InitializingBean` 是 Spring 特定的接口，如果你使用这个接口，类会与 Spring 框架产生耦合。而 `@PostConstruct` 是 Java 的标准注解，可以在 Spring 外的容器中复用，因此解耦性更强。
- **优先级**：如果一个类同时实现了 `InitializingBean` 并且定义了 `@PostConstruct` 方法，那么 `@PostConstruct` 会先执行，之后才会执行 `afterPropertiesSet()` 方法。

### (三) 检查是否实现了 DisposableBean 的接口

 在 Spring 框架中，`DisposableBean` 接口用于在 Spring 容器销毁 Bean 时执行一些清理操作。通过实现这个接口，你可以在应用程序关闭或上下文销毁时对 Bean 进行资源释放、关闭连接、停止线程等操作。  

1. DisposableBean 接口概述
   接口作用：DisposableBean 接口提供了一个 destroy() 方法，该方法会在 Spring 容器销毁 Bean 时被调用，用于执行自定义的销毁逻辑。
   执行时机：当 Spring 容器关闭或销毁 Bean 时（例如应用程序关闭时），Spring 会自动调用 destroy() 方法。这是释放资源、关闭连接等操作的好时机。
2. 使用 DisposableBean 的场景
   资源释放：如果你的 Bean 持有一些外部资源，如**文件、数据库连接、网络连接等，应该在 destroy() 方法中关闭或释放这些资源。**
   后台任务终止：如果你的 **Bean 启动了后台线程或定时任务，应该在销毁时终止这些任务，以避免资源泄漏。**
   缓存清理：在应用关闭时，**可以清理 Bean 中的缓存数据**，确保资源不会被占用。
3. DisposableBean 接口的实现
   要使用 DisposableBean 接口，你需要让你的 Bean 类实现该接口，并重写 destroy() 方法。下面是一个简单的示例：

```java
import org.springframework.beans.factory.DisposableBean;
import org.springframework.stereotype.Component;

@Component
public class MyBean implements DisposableBean {

    // 假设有一个资源需要在销毁时释放
    private SomeResource resource;

    public MyBean(SomeResource resource) {
        this.resource = resource;
    }

    @Override
    public void destroy() throws Exception {
        // 销毁逻辑
        System.out.println("DisposableBean: Bean 被销毁，执行清理操作");
        if (resource != null) {
            resource.close(); // 关闭资源
        }
        // 其他清理操作
    }
}
```

#### 1. 与 `@PreDestroy` 的对比

与 `InitializingBean` 类似，Spring 还提供了基于注解的销毁方法，即使用 `@PreDestroy` 注解。二者的功能类似，但有一些区别：

- **代码耦合**：`DisposableBean` 是 Spring 特定的接口，使用它会使类与 Spring 框架产生耦合。而 `@PreDestroy` 是 Java 的标准注解，可以在 Spring 外的容器中复用，解耦性更强。
- **优先级**：如果一个类同时实现了 `DisposableBean` 并且定义了 `@PreDestroy` 方法，那么 `@PreDestroy` 方法会先执行，之后才会执行 `destroy()` 方法。





# 二、Bean 的作用域

 在Spring的实际开发中，合理选择Bean的作用域（Scope）对于优化性能、提升系统稳定性至关重要。下面我通过几个具体场景，介绍Spring Bean的不同作用域及其应用场景。

### (一)  **Singleton (单例作用域)**

#### 1. 场景：服务类和无状态组件

大部分情况下，Spring Bean使用默认的单例作用域。单例Bean在整个应用程序生命周期中只会被创建一次，并且由所有请求共享。例如，一个业务服务类或工具类不需要保存任何状态信息时，使用单例作用域是最佳选择。

**应用场景：**

- **服务类**：如用户服务类（`UserService`）、订单服务类（`OrderService`）等。
- **工具类**：如字符串操作工具类、日期处理工具类等。

**优势：**

- 节省内存：共享同一个实例。
- 简化管理：不需要处理实例化的复杂性。

### (二)  **Prototype (原型作用域)**

#### 1. 场景：有状态组件或需要频繁创建销毁的对象

当你需要每次请求都创建一个新的Bean实例，并且每个实例独立于其他实例时，使用Prototype作用域。例如，在一个系统中，每次需要处理一个新任务时创建一个新的任务处理对象，这样可以确保任务之间的隔离。

**示例代码：**

```plain
java
复制代码
@Component
@Scope("prototype")
public class TaskProcessor {
    private String taskId;

    public TaskProcessor(String taskId) {
        this.taskId = taskId;
    }

    public void process() {
        System.out.println("Processing task: " + taskId);
    }
}
```

**应用场景：**

- **任务处理类**：如需要独立处理的任务，确保任务之间互不影响。
- **有状态对象**：如需要为每个请求创建单独的状态对象。

**优势：**

- 独立性强：每个实例互不影响。
- 灵活性高：适合需要频繁创建和销毁的对象。

### (三)  **Request (请求作用域)**

#### 1. 场景：Web应用中的请求级别的Bean

在Web应用中，某些对象仅需要在每个HTTP请求期间生效。例如，一个控制器中的Bean实例应该在每个HTTP请求中生成一次，并且请求结束后销毁。

**应用场景：**

- **请求级别的处理逻辑**：如在请求期间临时存储数据。
- **Web层对象**：如特定请求的配置或处理数据。

**优势：**

- 生命周期与请求同步：对象在请求结束时销毁，节省内存。
- 数据隔离：每个请求的数据互不影响。

### (四) **Session (会话作用域)**

#### 1. 场景：需要跨请求共享数据的Web应用

在Web应用中，如果你需要在整个用户会话期间保持数据，例如一个购物车对象，需要在用户登录后跨多个请求保持购物车的状态，那么Session作用域是最佳选择。

**示例代码：**

```plain
java
复制代码
@Component
@Scope("session")
public class ShoppingCart {
    private List<String> items = new ArrayList<>();

    public void addItem(String item) {
        items.add(item);
    }

    public List<String> getItems() {
        return items;
    }
}
```

**应用场景：**

- **购物车**：在整个用户会话期间保持购物车状态。
- **用户登录信息**：如在会话期间保存用户信息。

**优势：**

- 数据持久性：在用户会话期间保持数据。
- 用户隔离：每个用户有独立的会话数据。

### (五) **Application (应用作用域)**

#### 1. 场景：整个应用程序共享的Bean

Application作用域通常用于需要在整个Web应用程序范围内共享的数据或配置，例如应用程序启动时初始化的配置类，这些配置在应用程序范围内都是共享的。

**示例代码：**

```plain
java
复制代码
@Component
@Scope("application")
public class ApplicationConfig {
    private Map<String, String> settings;

    @PostConstruct
    public void init() {
        settings = new HashMap<>();
        settings.put("appVersion", "1.0.0");
    }

    public String getSetting(String key) {
        return settings.get(key);
    }
}
```

**应用场景：**

- **全局配置**：如应用程序启动时的配置信息。
- **全局统计数据**：如访问次数、用户在线数等全局状态。

**优势：**

- 全局共享：在整个应用范围内可用。
- 数据持久：在应用生命周期内保持数据。

### (六)  **WebSocket (WebSocket作用域)**

#### 1. 场景：基于WebSocket的应用

对于使用WebSocket通信的应用，需要每个WebSocket会话期间保持数据时，可以使用WebSocket作用域。每个WebSocket连接都会生成一个独立的Bean实例，连接结束时销毁。

**示例代码：**

```plain
java
复制代码
@Component
@Scope("websocket")
public class WebSocketSessionBean {
    private String sessionId;

    public WebSocketSessionBean() {
        this.sessionId = UUID.randomUUID().toString();
    }

    public String getSessionId() {
        return sessionId;
    }
}
```

**应用场景：**

- **实时通信**：如聊天应用中的用户会话。
- **WebSocket连接管理**：如处理连接状态和会话数据。

**优势：**

- 实时管理：每个WebSocket会话独立处理。
- 生命周期控制：自动在连接结束时销毁Bean。
