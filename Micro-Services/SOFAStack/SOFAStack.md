## SOFAStack

网站： https://www.sofastack.tech/

> 金融级分布式架构
>
> SOFAStack™（Scalable Open Financial Architecture Stack）
> 是一套用于快速构建金融级分布式架构的中间件，也是在金融场景里锤炼出来的最佳实践。
>
> 参考： 官网

### 目录
* 特点
* 项目


### 特点

* 开放

    技术栈全面开源共建、 保持社区中立、兼容社区 兼容开源生态，组件可插拔， SOFAStack 组件与其它开源组件可相互集成或替换

* 金融级

    包含构建金融级云原生架构所需的各个组件，让用户更加专注于业务开发，满足用户场景的现状和未来需求，经历过大规模场景的锤炼，特别是严苛的金融场景

* 云原生

    基于 SOFAStack 可快速搭建云原生微服务体系，快速开发更具可靠性和扩展性、更加易于维护的云原生应用

### 项目

主要项目
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

孵化项目
* [SOFAMesh](SOFAMesh.md)

    SOFAMesh 是基于 Istio 改进和扩展而来的 Service Mesh 大规模落地实践方案。

* SOFADashboard

    SOFADashboard 是 SOFAStack 生态的管控端，提供应用信息查看，服务治理，动态模块管控等功能。

工具项目
* SOFABolt

    SOFABolt 是一套基于 Netty 实现的网络通信框架。

* SOFAJRaft

    SOFAJRaft 是一个基于 RAFT 一致性算法的生产级高性能 Java 实现，支持 MULTI-RAFT-GROUP，适用于高负载低延迟的场景。

* SOFAActs

    ACTS（AntCoreTest）是一款白盒测试框架，旨在为企业提供高效、精细化的接口自动化测试。

* SOFAArk

    SOFAArk是一款基于 Java 实现的轻量级类隔离容器。

生态项目
* Seata

    Seata 是一款分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务。



