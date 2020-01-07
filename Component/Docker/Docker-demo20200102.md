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
从上一个demo copy的。
* Docker容器内通讯，使用的是内部的IP地址，需要通过 `docker inspect 容器名称或 id` 查看容器的IP地址，写到配置文件。
* 这个应该是可以配置修改的。待定。
* Grafana面板主要展示： 机器硬件、应用接口、HTTP接口、RPC调用、JVM、堆、栈、垃圾回收、线程。 找一下这些面板展示的模板。
* ~~以上几个监控组件的启动方式，由命令行启动（也就是上面写的一条一条的启动） 修改为使用 Docker Compose 运行~~。


* 2个项目互相调用，通过RPC、Feign方式
* ~~注册中心 Nacos~~
* 配置管理： Apollo
* 限流，降级，熔断：Sentinel
* 提醒，发送邮件，微信推送： alertmanger 
* 异常捕获平台，日志监控 和日志提醒：Sentry
* 分布式事务解决方案。 Seata。 （最后。。。）
* ~~dubbo重试机制、超时配置~~。 



