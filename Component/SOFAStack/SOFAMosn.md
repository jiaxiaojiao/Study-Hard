## SOFAMosn

> SOFAMosn 是一款使用 Go 语言开发的 Service Mesh 数据平面代理，
> 旨在为服务提供分布式、模块化、可观察和智能化的代理能力。
> SOFAMosn 是 SOFAStack 中的一个项目，
> 其中 MOSN 是 Modular Observable Smart Network 的简称。
> SOFAMosn 可以与任何支持 xDS API 的 Service Mesh 集成，亦可以作为独立的四、七层负载均衡使用。
> 未来 SOFAMosn 将支持更多云原生场景，并支持 Nginx 的核心转发功能。

### 目录
* [核心能力](#核心能力)
* [参考](#参考)

### 核心能力

* Istio集成
    * 集成 Istio 1.0 版本与 V4 API，可基于全动态资源配置运行
* 核心转发
    * 自包含的网络服务器
    * 支持 TCP 代理
    * 支持 TProxy 模式
* 多协议
    * 支持 HTTP/1.1，HTTP/2
    * 支持 SOFARPC
    * 支持 Dubbo 协议（开发中）
* 核心路由
    * 支持 Virtual Host 路由
    * 支持 Headers/URL/Prefix 路由
    * 支持基于 Host Metadata 的 Subset 路由
    * 支持重试
* 后端管理&负载均衡
    * 支持连接池
    * 支持熔断
    * 支持后端主动健康检查
    * 支持 Random/RR 等负载策略
    * 支持基于 Host Metadata 的 Subset 负载策略
* 可观察性
    * 观察网络数据
    * 观察协议数据
* TLS
    * 支持 HTTP/1.1 on TLS
    * 支持 HTTP/2.0 on TLS
    * 支持 SOFARPC on TLS
* 进程管理
    * 支持平滑 reload
    * 支持平滑升级
* 扩展能力
    * 支持自定义私有协议
    * 支持在 TCP IO 层，协议层面加入自定义扩展

### 参考
* 网站：https://www.sofastack.tech/projects/sofa-mosn/overview/

Envoy、Istio 体系