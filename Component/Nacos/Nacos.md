## Nacos
**_重点学习_**

注册中心，服务治理能力

### 目录
* [Nacos 是什么？](#Nacos-是什么？)
* [Nacos 的愿景](#Nacos-的愿景)
* [Nacos 有什么功能？](#Nacos-有什么功能？)
* [Nacos 有什么特性？](#Nacos-有什么特性？)
* [Nacos 基本架构](#Nacos-基本架构)
* [Nacos 概念，引入的基本概念](Nacos-概念.md)
* [Nacos 与 Apollo对比](../Apollo/Apollo.md#配置中心对比)
* 安装和使用
    * [Nacos部署-单机模式](Nacos-Install-single.md)
    * [Nacos部署-集群模式](Nacos-Install-cluster.md)
    * [Nacos部署-Docker（单机模式和集群模式）](Nacos-Install-Docker.md)
    * [Nacos集成监控](Nacos-Integrated-Install.md)
    * [Nacos Spring Cloud](Nacos-Spring-Cloud.md)
* [开源生态相关/与开源组件的集成](#开源生态相关/与开源组件的集成)
* [参考](#参考)

### Nacos 是什么？
Nacos 是一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。

2018年6月，阿里开源的配置中心，也可以做DNS和RPC的服务发现。

服务（Service）是 Nacos 世界的一等公民。Nacos 支持几乎所有主流类型的“服务”的发现、配置和管理：
* Kubernetes Service
* gRPC & Dubbo RPC Service
* Spring Cloud RESTful Service

### Nacos 的愿景
Nacos 通过提供简单易用的动态服务发现、服务配置、服务共享与管理等服务基础设施，帮助用户在云原生时代，在私有云、混合云或者公有云等所有云环境中，更好的构建、交付、管理自己的微服务平台，更快的复用和组合业务服务，更快的交付商业创新的价值，从而为用户赢得市场。

### Nacos 有什么功能？
* 服务发现和服务健康监测

    Nacos 支持基于 DNS 和基于 RPC 的服务发现。服务提供者使用 原生SDK、OpenAPI、或一个独立的Agent TODO注册 Service 后，服务消费者可以使用DNS TODO 或HTTP&API查找和发现服务。

    Nacos 提供对服务的实时的健康检查，阻止向不健康的主机或服务实例发送请求。Nacos 支持传输层 (PING 或 TCP)和应用层 (如 HTTP、MySQL、用户自定义）的健康检查。 对于复杂的云环境和网络拓扑环境中（如 VPC、边缘网络等）服务的健康检查，Nacos 提供了 agent 上报模式和服务端主动检测2种健康检查模式。Nacos 还提供了统一的健康检查仪表盘，帮助您根据健康状态管理服务的可用性及流量。

* 动态配置服务

    动态配置服务可以让您以中心化、外部化和动态化的方式管理所有环境的应用配置和服务配置。

    动态配置消除了配置变更时重新部署应用和服务的需要，让配置管理变得更加高效和敏捷。

    配置中心化管理让实现无状态服务变得更简单，让服务按需弹性扩展变得更容易。

    Nacos 提供了一个简洁易用的UI (控制台样例 Demo) 帮助您管理所有的服务和应用的配置。Nacos 还提供包括配置版本跟踪、金丝雀发布、一键回滚配置以及客户端配置更新状态跟踪在内的一系列开箱即用的配置管理特性，帮助您更安全地在生产环境中管理配置变更和降低配置变更带来的风险。

* 动态 DNS 服务

    动态 DNS 服务支持权重路由，让您更容易地实现中间层负载均衡、更灵活的路由策略、流量控制以及数据中心内网的简单DNS解析服务。动态DNS服务还能让您更容易地实现以 DNS 协议为基础的服务发现，以帮助您消除耦合到厂商私有服务发现 API 上的风险。

    Nacos 提供了一些简单的 DNS APIs TODO 帮助您管理服务的关联域名和可用的 IP:PORT 列表.

* 服务及其元数据管理

    Nacos 能让您从微服务平台建设的视角管理数据中心的所有服务及元数据，包括管理服务的描述、生命周期、服务的静态依赖分析、服务的健康状态、服务的流量管理、路由及安全策略、服务的 SLA 以及最首要的 metrics 统计数据。

等。

### Nacos 有什么特性？
1. 易于使用
    * 动态配置管理、服务发现和动态的一站式解决方案
    * 20多种开箱即用的以服务为中心的架构特性
    * 基本符合生产要求的轻量级易用控制台
2. 更适应云架构
    * 无缝支持Kubernetes和Spring Cloud
    * 在主流公共云上更容易部署和运行（例如阿里云和AWS）
    * 多租户和多环境支持
3. 生产等级
    * 脱胎于历经阿里巴巴10年生产验证的内部产品
    * 支持具有数百万服务的大规模场景
    * 具备企业级SLA的开源产品
4. 丰富的应用场景
    * 支持限流、大促销预案和异地多活
    * 直接支持或稍作扩展即可支持大量有用的互联网应用场景
    * 流量调度和服务治理

### Nacos 基本架构
![Nacos架构](../images/nacos.jpeg)

### 开源生态相关/与开源组件的集成
* Dubbo and Dubbo Mesh
    * Dubbo 及 Nacos是阿里巴巴大规模微服务生产实践中的经典组合，对比传统的如ZooKeeper等注册中心与配置中心解决方案，在使用云原生及Service Mesh范式构建微服务应用平台时，通过在Dubbo中使用Nacos，可以完全释放Dubbo在大规模微服务治理、流量管理、服务集成及共享上的所有威力。
* Kubernetes and CNCF
    * Nacos 支持Kubernetes 以及 CNCF所需要的服务发现及动态配置管理的需求，Nacos可以完全无缝的替代Kubernetes的原生的DNS-based Service Discovery 解决方案，Nacos 提供了更多的服务治理侧的特性，这包括服务的域名管理，服务健康及生命周期管理，流量管理及智能路由策略管理等，Nacos也增强了对ConfigMap的管理，这包括版本配置、灰度发布等。
* Spring Cloud
    * Nacos 完全兼容和无缝支持 Spring Cloud的相关API及主要相关功能，你可以将Nacos作为SpringCloud Config Server的配置服务或者Eureka/Consul/ZooKeeper等的服务发现产品的更好替代者，Nacos 在配置管理和服务管理上带来了很多面向生产及微服务治理所需要的特性增强。

### 参考
* 网站 https://nacos.io/zh-cn/
* 源码 https://github.com/alibaba/nacos