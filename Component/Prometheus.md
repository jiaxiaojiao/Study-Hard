## Prometheus

网站： https://prometheus.io/

源码： https://github.com/prometheus/prometheus

> 普罗米修斯
>
> (入门门槛有点高)

### 目录
* [Prometheus 是什么？](#Prometheus-是什么？)
* [Prometheus 有哪些特点？](#Prometheus-有哪些特点？)
* [有哪些使用场景/案例？](#有哪些使用场景/案例？)
* [参考](#参考)

### Prometheus 是什么？
> Prometheus, a Cloud Native Computing Foundation project, is a systems and service monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts if some condition is observed to be true.

Prometheus是一个云计算基础项目，是一个系统和服务监控系统。它以给定的时间间隔从配置的目标收集指标，计算规则表达式，显示结果，并且可以在观察到某些条件为真时触发警报。

Prometheus 是监测系统和时间序列数据库。

Prometheus 是由 SoundCloud 开源监控告警解决方案。

### Prometheus 有哪些特点？
> a multi-dimensional data model (timeseries defined by metric name and set of key/value dimensions)
>
> a flexible query language to leverage this dimensionality
>
> no dependency on distributed storage; single server nodes are autonomous
>
> timeseries collection happens via a pull model over HTTP
>
> pushing timeseries is supported via an intermediary gateway
>
> targets are discovered via service discovery or static configuration
>
> multiple modes of graphing and dashboarding support
>
> support for hierarchical and horizontal federation

与其他监控系统相比，Prometheus有哪些的特点：
* 多维数据模型(由度量名称和键/值维集定义的timeseries)
* 一种灵活的查询语言来利用这种维度
* 不依赖分布式存储;单个服务器节点是自治的
* timeseries时序数据的收集通过HTTP的pull方式进行
* 通过中间网关进行timeseries时序数据的推送
* 通过服务发现或静态配置发现目标
* 支持多种模式的图表和界面展示
* 支持层次和水平联合

### 有哪些使用场景/案例？
* Kubernetes添加Prometheus插件提供K8S集群的监控能力
* Prometheus + grafana 系统和容器信息一起监控

### 参考
* 官网