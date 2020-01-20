## Dubbo

> Apache Dubbo /ˈdʌbəʊ/

网站： http://dubbo.apache.org/zh-cn/

源码： https://github.com/apache/dubbo

### 目录
* [Dubbo 是什么？](#Dubbo-是什么？)
* [Dubbo 架构](#Dubbo-架构)
* [Dubbo 特性](#Dubbo-特性)
* Dubbo 设置
    * [注解配置](Dubbo-configuration-annotation.md)
* [Dubbo 的超时机制和重试机制](Dubbo-timeout-retries.md)
* [文档](http://dubbo.apache.org/zh-cn/docs/user/quick-start.html)
* [脚手架：快速生成基于 Spring Boot 的 Dubbo 项目](http://start.dubbo.io/)

### Dubbo 是什么？
Apache Dubbo™ 是一款高性能Java RPC框架。

Apache Dubbo `|ˈdʌbəʊ|` 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。

### Dubbo 架构
![dubbo](../images/dubbo-architecture.png)

### Dubbo 特性
* 面向接口代理的高性能RPC调用

    提供高性能的基于代理的远程调用能力，服务以接口为粒度，为开发者屏蔽远程调用底层细节。

* 智能负载均衡

    内置多种负载均衡策略，智能感知下游节点健康状况，显著减少调用延迟，提高系统吞吐量。

* 服务自动注册与发现

    支持多种注册中心服务，服务实例上下线实时感知。

* 高度可扩展能力

    遵循微内核+插件的设计原则，所有核心能力如Protocol、Transport、Serialization被设计为扩展点，平等对待内置实现和第三方实现。

* 运行期流量调度

    内置条件、脚本等路由策略，通过配置不同的路由规则，轻松实现灰度发布，同机房优先等功能。

* 可视化的服务治理与运维

    提供丰富服务治理、运维工具：随时查询服务元数据、服务健康状态及调用统计，实时下发路由策略、调整配置参数。
 

