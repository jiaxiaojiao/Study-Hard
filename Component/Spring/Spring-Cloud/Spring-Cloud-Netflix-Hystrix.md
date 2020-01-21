## Hystrix

Circuit Breaker

### 目录
* [Hystrix 是什么？](#Hystrix-是什么？)
* [Hystrix 的设计原则](#Hystrix-的设计原则)
* [参考](#参考)

### Hystrix 是什么？
在微服务的架构系统中，每个服务都可能会调用很多其他服务，被调用的那些服务就是依赖服务。有的时候某些依赖服务出现故障也是很正常的。Hystrix可以让我们在对服务间的调用进行控制，加入一些调用延迟或者依赖故障的容错机制。Hystrix通过将依赖服务进行资源隔离，进而组织某个依赖服务出现故障的时候，这种故障在整个系统所有的依赖服务调用中进行蔓延，同时Hystrix还提供故障时的fallback降级机制。总而言之，Hystrix通过这些方法帮助我们提升系统的可用性和稳定性。

### Hystrix 的设计原则
Hystrix为了实现高可用性的架构，有以下设计原则：
1. 对依赖服务调用时出现的调用延迟和调用失败进行控制和容错保护。
2. 阻止某一个依赖服务的故障在整个系统中蔓延，服务A->服务B->服务C，服务C故障了，服务B也故障了，服务A故障了，整个系统全部故障，整体宕机。
3. 提供fail-fast（快速失败）和快速恢复的支持。
4. 提供fallback优雅降级的支持。
5. 支持近实时的监控、报警以及运维操作。

### 参考
* 网站 https://spring.io/projects/spring-cloud-netflix
* 源码 https://github.com/Netflix/Hystrix
* https://blog.csdn.net/Anbang713/article/details/85591774