## Apache Dubbo

> Apache Dubbo™ is a high-performance, java based open source RPC framework.
>
> Apache Dubbo™ 是一款高性能Java RPC框架。
>
> 内容来源： http://dubbo.apache.org/en-us/
> http://dubbo.apache.org/zh-cn/

Apache Dubbo |ˈdʌbəʊ| 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。

### 目录
* Dubbo架构图
* Dubbo特性
* Dubbo的负载策略，容错机制
* Dubbo支持的协议


### Dubbo 架构图

![images](images/dubbo-architecture.png)

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
 
 
 