## Service Mesh

> 服务网格
> 
> 解决微服务之间通信愈发复杂的问题。
>
> 参考： 官网和 https://blog.51cto.com/12462495/2437636

### 目录
* Service Mesh的定义
* Service Mesh的作用和功能
* Service Mesh领域的项目

### Service Mesh的定义

关于Service mesh的定义，最为广泛接受的观点是：它是一种控制应用程序不同部分彼此共享数据的方式。

服务网格是一个基础设施层，功能在于处理服务间通信，职责是负责实现请求的可靠传递。在实践中，服务网格通常实现为轻量级网络代理，通常与应用程序部署在一起，但是对应用程序透明。

* 治理能力独立（Sidecar）
* 应用程序无感知
* 服务通信的基础设备层

术语服务网格用来描述组成这些应用程序的微服务网络以及它们之间的交互。随着服务网格的规模和复杂性不断的增长，它将会变得越来越难以理解和管理。它的需求可以包括服务发现、负载均衡、故障恢复、度量和监控。一个服务网格通常还有更复杂的操作需求，比如 A/B 测试、金丝雀发布、速率限制、访问控制和端到端认证。

### Service Mesh的作用和功能

Service mesh可以在短时间内自动处理发现和连接服务，而无需开发人员以及各个微服务自行匹配。

功能： 
1. 负载均衡

### Service Mesh领域的项目

* Linkerd ： Service mesh领域的第一个项目是Linkerd，它一开始是Twitter内部项目的一个分支。
```text
https://github.com/linkerd/linkerd
    
https://github.com/linkerd/linkerd2
```

* Istio ： Istio是另一个十分流行的service mesh项目，它起源于Lyft。 
```text
https://istio.io/

https://github.com/istio/istio

Connect, secure, control, and observe services.
连接、安全加固、控制和观察服务的开放平台
```

* SOFAMesh ： SOFAMesh 是基于 Istio 改进和扩展而来的 Service Mesh 大规模落地实践方案。在继承 Istio 强大功能和丰富特性的基础上，为满足大规模部署下的性能要求以及应对落地实践中的实际情况。
```text
https://github.com/sofastack/sofa-mesh
```

* Apache SkyWalking ： 分布式系统的应用程序性能监视工具，专为微服务、云原生架构和基于容器（Docker、K8s、Mesos）架构而设计。
```text
http://skywalking.apache.org/zh/

https://github.com/apache/skywalking
```
