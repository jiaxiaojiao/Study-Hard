## Istio

官网： https://istio.io/

GitHub： https://github.com/istio/istio

> Istio是一个十分流行的service mesh项目，它起源于Lyft。 
>


### Istio的功能

Connect, secure, control, and observe services.

* 连接 Connect： （流量管理） 负载均衡，动态路由，灰度发布，故障注入
* 安全加固 Secure： （服务身份和安全） 认证，鉴权
* 控制 Control： （策略执行） 限流，ACL访问规则的配置
* 观察 Observe： 调用链，访问日志，监控

支持的扩展平台： 
* Kubernetes (K8s)  应用容器化管理
* Cloud Foundry
* Eureka
* Consul

还可以集成和定制一些功能：
* ACL 安全规则
* 日志
* 配额

### Istio的应用

* Istio + Kubernetes ： 云原生应用治理+云原生应用设施

    Istio可以完美的补齐Kubernetes缺乏服务治理的缺陷。
    
    Kubernetes提供了很强的部署运维能力（部署、运维、扩缩容、服务发现、负载均衡），但是在服务发现和负载均衡比较简单。
    
    Istio的服务治理（调用链追踪、动态路由、熔断限流...）跟Kubernetes完美结合。

### Istio的架构

![Istio架构](../images/istio-architecture.svg)

1. Service A , Service B  用户的服务。
2. Proxy 在Istio中默认是envoy， 主要做服务之间的转发
3. Service A + Proxy， Service B + Proxy 构成了Istio的数据面，用户的服务之间的互访的数据面。
4. Istio的控制面： Pilot、Galley、Citadel、Mixer
5. Pilot： 配置规则到Istio-Proxy(envoy)里面，如跟Kubernetes对接，会配置一些获取Kubernetes的源信息，或者是用户定义的规则，路由规则等实现服务之间的服务治理。
6. Mixer： 主要包括两部分，Policy checks(策略管理，服务通信时能不能访问、多频繁的访问)，telemetry(监控，调用链分析)
7. Citadel： 用来配置服务之间访问的安全，证书生成和下发，在Citadel里统一管理。
8. Galley： 验证用户配置的规则有没有效果。











