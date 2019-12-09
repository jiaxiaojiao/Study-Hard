## ZooKeeper

网站： https://zookeeper.apache.org/

GitHub： https://github.com/apache/zookeeper

> 服务注册中心
>
> Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.
>
> 参考： 官网，百度百科， https://www.w3cschool.cn/zookeeper/zookeeper_overview.html， https://www.jianshu.com/p/e68c06a5d002

### 目录
* [是什么？](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [优缺点](#优缺点)
* [其他替代组件](#其他替代组件)

### 是什么？

ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these kinds of services are used in some form or another by distributed applications. Each time they are implemented there is a lot of work that goes into fixing the bugs and race conditions that are inevitable. Because of the difficulty of implementing these kinds of services, applications initially usually skimp on them, which make them brittle in the presence of change and difficult to manage. Even when done correctly, different implementations of these services lead to management complexity when the applications are deployed.

ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务，是Google的Chubby一个开源的实现，是Hadoop和Hbase的重要组件。它是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。

### 是否开源

开源

### 主要功能

ZooKeeper的目标就是封装好复杂易出错的关键服务，将简单易用的接口和性能高效、功能稳定的系统提供给用户。

Apache ZooKeeper是由集群（节点组）使用的一种服务，用于在自身之间协调，并通过稳健的同步技术维护共享数据。ZooKeeper本身是一个分布式应用程序，为写入分布式应用程序提供服务。

ZooKeeper提供的常见服务如下 :

* 命名服务 - 按名称标识集群中的节点。它类似于DNS，但仅对于节点。

* 配置管理 - 加入节点的最近的和最新的系统配置信息。

* 集群管理 - 实时地在集群和节点状态中加入/离开节点。

* 选举算法 - 选举一个节点作为协调目的的leader。

* 锁定和同步服务 - 在修改数据的同时锁定数据。此机制可帮助你在连接其他分布式应用程序（如Apache HBase）时进行自动故障恢复。

* 高度可靠的数据注册表 - 即使在一个或几个节点关闭时也可以获得数据。

分布式应用程序提供了很多好处，但它们也抛出了一些复杂和难以解决的挑战。ZooKeeper框架提供了一个完整的机制来克服所有的挑战。竞争条件和死锁使用故障安全同步方法进行处理。另一个主要缺点是数据的不一致性，ZooKeeper使用原子性解析。

### 兼容性

Zookeeper作为Hadoop和Hbase的重要组件，可以为分布式应用程序协调服务，同时还能使用Java和C的接口。

ZooKeeper是一种分布式协调服务，用于管理大型主机。在分布式环境中协调和管理服务是一个复杂的过程。ZooKeeper通过其简单的架构和API解决了这个问题。ZooKeeper允许开发人员专注于核心应用程序逻辑，而不必担心应用程序的分布式特性。

### 优缺点

优点：
* 最终一致性 为客户端展示同一个视图，这是zookeeper里面一 个非常重要的功能
* 可靠性 如果消息被到一台服务器接受，那么它将被所有的 服务器接受。
* 实时性 Zookeeper不能保证两个客户端能同时得到刚更新 的数据，如果需要最新数据，应该 在读数据之前调 用sync()接口。
* 独立性 各个Client之间互不干预 原子性 更新只能成功或者失败，没有中间状态。
* 顺序性 所 有Server，同一消息发布顺序一致。

### 其他替代组件

* Eureka

