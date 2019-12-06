## Eureka

GitHub： https://github.com/Netflix/eureka

> 服务注册与发现的组件
>
> 参考： https://github.com/Netflix/eureka/wiki，https://www.cnblogs.com/knowledgesea/p/11208000.html

### 目录
* [是什么？](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [优缺点](#优缺点)
* [其他替代组件](#其他替代组件)

### 是什么？

Eureka 是 Netflix 开发的，一个基于 REST 服务的，服务注册与发现的组件

它主要包括两个组件：Eureka Server 和 Eureka Client

* Eureka Client：一个Java客户端，用于简化与 Eureka Server 的交互（通常就是微服务中的客户端和服务端）
* Eureka Server：提供服务注册和发现的能力（通常就是微服务中的注册中心）

各个微服务启动时，会通过 Eureka Client 向 Eureka Server 注册自己，Eureka Server 会存储该服务的信息

也就是说，每个微服务的客户端和服务端，都会注册到 Eureka Server，这就衍生出了微服务相互识别的话题

* 同步：每个 Eureka Server 同时也是 Eureka Client（逻辑上的）

    多个 Eureka Server 之间通过复制的方式完成服务注册表的同步，形成 Eureka 的高可用
    
* 识别：Eureka Client 会缓存 Eureka Server 中的信息

    即使所有 Eureka Server 节点都宕掉，服务消费者仍可使用缓存中的信息找到服务提供者
    
* 续约：微服务会周期性（默认30s）地向 Eureka Server 发送心跳以Renew（续约）信息（类似于heartbeat）

* 续期：Eureka Server 会定期（默认60s）执行一次失效服务检测功能

    它会检查超过一定时间（默认90s）没有Renew的微服务，发现则会注销该微服务节点

Spring Cloud 已经把 Eureka 集成在其子项目 Spring Cloud Netflix 里面

关于 Eureka 配置的最佳实践，可参考：`https://github.com/spring-cloud/spring-cloud-netflix/issues/203`

### 是否开源
Eureka 1.x 开源。Eureka 2.0 闭源，停止更新。Spring Cloud集成的是1.x版本

The existing open source work on eureka 2.0 is discontinued. 

Eureka 1.x is a core part of Netflix's service discovery system and is still an active project.

### 主要功能

服务注册与发现

### 兼容性

Spring Cloud 将Eureka集成在子项目Spring-Cloud-Netflix中，以实现Spring Cloud的服务发现功能。

### 优缺点

对比ZooKeeper

* Eureka 优点： 基于AP高可用，主从复制 都是主节点，三级（多级）缓存机制，基于内存速度快，不会出现半数挂掉的不可用 只有一个节点也可用，天然支持Spring Boot。
* Eureka 缺点： 基于内存缺陷注册点有局限（有上限）， 缓存刷新需要时间 同步会有延迟。页面管控不全或者没有。服务升降级只提供了接口。

### 其他替代组件

ZooKeeper

