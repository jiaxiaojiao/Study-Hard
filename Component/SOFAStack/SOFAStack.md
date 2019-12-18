## SOFAStack

网站： https://www.sofastack.tech/

> 金融级分布式架构
>
> SOFAStack™（Scalable Open Financial Architecture Stack）
> 是一套用于快速构建金融级分布式架构的中间件，也是在金融场景里锤炼出来的最佳实践。
>
> 参考： 官网， https://help.aliyun.com/document_detail/131841.html

### 目录
* [是什么？](#是什么？)
* [特点](#特点)
* 项目
    * [主要项目](#主要项目)
    * [孵化项目](#孵化项目)
    * [工具项目](#工具项目)
    * [生态项目](#生态项目)

### 是什么？
SOFAStack™（Scalable Open Financial Architecture Stack）包含构建金融级云原生架构所需的各个组件，也是在金融场景里锤炼出来的最佳实践。提供项目管理、微服务应用开发、部署发布、监控运维、容灾高可用等全栈式解决方案，并兼容 Dubbo、Spring Cloud 等微服务运行环境，助力客户各类应用轻松转型分布式架构。

金融分布式架构SOFAStack（Scalable Open Financial Architecture Stack）的名称来自蚂蚁内部发展十多年的金融级分布式中间件SOFA（Service Oriented Fabric Architecture），代表着从支付宝创立之初就开始在关键金融交易系统锤炼出来的分布式架构实践。

SOFAStack所有的产品技术都经过蚂蚁金服自身严苛金融场景验证，为金融交易技术在保证风险安全的同时，帮助业务需求敏捷迭代，同时满足异地容灾、低成本快速扩容的需求，解决传统集中式架构转型的困难，打造大规模高可用分布式系统架构，支撑金融业务创新。为满足金融业务发展和严苛场景考验，让云计算更懂金融，SOFAStack有三大核心价值主张：开放、金融级、云原生。

* **全栈开放、开源共建** —- 源自蚂蚁金服实践演进沉淀，金融交易技术完整领域开放。技术向下兼容，实现与经典架构的融合，开放技术标准，拥抱开源生态。技术栈全面开源共建、保存社区中立、兼容社区和开源生态，组件可插拔，与其它开源组件可相互集成或替换。
* **满足资金安全、无损容灾的金融级要求** —- 包含构建金融级云原生架构所需的各个组件，让用户更加专注于业务开发，满足用户场景的现状和未来需求，经历过大规模场景的锤炼，特别是严苛的金融场景，保证在分布式架构下承受高并发交易，在系统扩展、容灾恢复、更新发布时确保数据无损，服务可用。
* **以异地多活、无限扩展为目标构建云原生架构** —- 基于SOFAStack可快速搭建云原生微服务体系，快速开发更具可靠性和扩展性、更加易于维护的云原生应用。在宏观架构层面，提供单机房向同城双活、两地三中心、异地多活架构演进路线，使系统容量能在多个数据中心内任意扩展和调度，充分利用服务器资源，提供机房级容灾能力，保证业务连续性。

### 特点

* 开放

    技术栈全面开源共建、 保持社区中立、兼容社区 兼容开源生态，组件可插拔， SOFAStack 组件与其它开源组件可相互集成或替换

* 金融级

    包含构建金融级云原生架构所需的各个组件，让用户更加专注于业务开发，满足用户场景的现状和未来需求，经历过大规模场景的锤炼，特别是严苛的金融场景

* 云原生

    基于 SOFAStack 可快速搭建云原生微服务体系，快速开发更具可靠性和扩展性、更加易于维护的云原生应用

### 主要项目
* [SOFABoot](SOFABoot/sofa-Boot.md)

    SOFABoot 基于 Spring Boot 的研发框架，在其基础上提供了诸如 Readiness Check，类隔离，日志空间隔离，Bean 异步初始化等能力。

* SOFARPC

    SOFARPC 是一个高可扩展性、高性能、生产级的 Java RPC 框架。

* [SOFAMosn](SOFAMosn.md)

    SOFAMosn 是一款采用 Go 开发的 Service Mesh 数据平面代理。

* SOFATracer

    SOFATracer 是蚂蚁金服开发的基于 OpenTracing 规范 的分布式链路跟踪系统。

* SOFALookout

    SOFALookout 是一个利用多维度的 metrics 对目标系统进行度量和监控的项目。

* SOFARegistry

    SOFARegistry 是一个生产级、高时效、高可用的服务注册中心。

### 孵化项目
* [SOFAMesh](SOFAMesh.md)

    SOFAMesh 是基于 Istio 改进和扩展而来的 Service Mesh 大规模落地实践方案。

* SOFADashboard

    SOFADashboard 是 SOFAStack 生态的管控端，提供应用信息查看，服务治理，动态模块管控等功能。

### 工具项目
* SOFABolt

    SOFABolt 是一套基于 Netty 实现的网络通信框架。

* SOFAJRaft

    SOFAJRaft 是一个基于 RAFT 一致性算法的生产级高性能 Java 实现，支持 MULTI-RAFT-GROUP，适用于高负载低延迟的场景。

* SOFAActs

    ACTS（AntCoreTest）是一款白盒测试框架，旨在为企业提供高效、精细化的接口自动化测试。

* SOFAArk

    SOFAArk是一款基于 Java 实现的轻量级类隔离容器。

### 生态项目
* [Seata](Seata.md)

    Seata 是一款分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务。



