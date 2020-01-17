## Docker安装软件



### 目录
* [2个Demo项目-两个多模块Spring Boot项目，已经提交到 `Study-SpringBoot`](../Spring/Spring-Boot/Spring-Boot-New.md#多模块项目创建)
* [注册中心，配置中心使用Nacos](../Nacos/Nacos-Install-Docker.md)
* [Prometheus监控Nacos](../Nacos/Nacos-Prometheus.md)
* [2个Demo项目通过Dubbo调用接口](#操作步骤)
* Demo项目和Nacos依赖的数据库使用物理机本机的MySQL数据库。
* [操作步骤](#操作步骤)
* [接下来做什么呢？](#接下来做什么呢？)


### 操作步骤

### 接下来做什么呢？
* ~~feign远程调用接口， 熔断、降级、负载均衡。~~ （使用Feign自带的fallback和loadbalance）
* ~~dubbo重试机制、超时配置~~。 

* Grafana面板主要展示： 
    * ~~机器硬件~~
    * 应用接口
    * HTTP接口 = 调用时间，一分钟最大时间，平均时间。。。。
    * RPC调用 = 调用时间，一分钟最大时间，平均时间。。。。 接入方式不能太复杂。或者从收集日志的角度。
    * ~~JVM、堆、栈、垃圾回收(每个代的gc数等)、线程~~。 找一下这些面板展示的模板。
Grafana告警，邮箱    
* 提醒，发送邮件，**企业微信推送**： alertmanger **  企业微信推送
* 异常捕获平台，日志监控 和日志提醒：Sentry ** （应用日志）统一日志收集，统一日志过滤，告警（自定义level）。
* feign链路监控Zipkin。 RPC链路监控， 找开源组件，包括类似Zipkin的一些功能。每一步的调用信息可见，组件间的依赖图。
既能监控http 又能监控RPC，链路。完整调用的详细信息，每一步调用信息，依赖关系。
* Zipkin和Grafana整合，看板。
灰度发布

* 限流，降级，熔断：Sentinel
* Docker容器间通信。 目前使用容器的IP和端口访问的。希望修改为外部IP和端口。 （后续）
* 配置管理： Apollo。
* 分布式事务解决方案。 seata。 （最后。。。）



