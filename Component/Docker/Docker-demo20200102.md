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

* Grafana面板主要展示： 机器硬件、应用接口、HTTP接口、RPC调用、JVM、堆、栈、垃圾回收、线程。 找一下这些面板展示的模板。

* 限流，降级，熔断：Sentinel
* Docker容器间通信。 目前使用容器的IP和端口访问的。希望修改为外部IP和端口。 （后续）
* 配置管理： Apollo。
* 提醒，发送邮件，微信推送： alertmanger 
* 异常捕获平台，日志监控 和日志提醒：Sentry
* 分布式事务解决方案。 seata。 （最后。。。）



