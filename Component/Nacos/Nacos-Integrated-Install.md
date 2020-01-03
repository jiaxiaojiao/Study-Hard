## Nacos 集成安装

> Spring Cloud Alibaba
> 1. 两个项目应用，服务调用（Demo1, Demo2）。通过RPC、Feign方式。
> 2. 注册中心： Nacos(nacos-config-servier, nacos-config, nacos-discovery)。 服务管理（服务列表，订阅者列表），集群管理（节点列表）。
>     3. 监控平台： Prometheus + AlertManager + Grafana 。 监控平台监控：1. 本身， 2. 应用， 3. 注册中心。
> 4. RPC : dubbo (spring-cloud-alibaba-dubbo)
> 5. 配置管理： Apollo
> 6. 限流，降级，熔断：sentinel
> 7. 分布式事务解决方案。 seata。 （最后。。。）

### 目录
* [1. 2个Demo应用](#2个Demo应用)
* [2. 注册中心Nacos](Nacos-Install-single.md)
* [3. 监控平台Prometheus+Alertmanager+Grafana](../Prometheus/Prometheus-install2.md)
* [3.2 监控平台Prometheus+Alertmanager+Grafana2](../Docker/Docker-demo20191230.md)
* [5. 配置管理Apollo](../Apollo/Apollo-install.md) 我觉得Apollo和Nacos都不错，可以先安装上，用哪个后续再选。
* [参考](#参考)

### 2个Demo应用
需求： 2个Demo应用通过RPC、Feign方式相互调用服务。
* Demo1： UserCenter
    * 添加用户。校验： 用户名不能重复。
	* 用户列表 状态是否有效用户，订单数>0为有效用户。 -> interface2-1
	* interface1-1根据用户ID查询用户信息。
* Demo2： OrderCenter
    * 添加订单。 会验证用户的真实有效性 -> interface1-1
    * 订单列表。 会根据用户ID展示用户名 -> interface1-1
    * interface2-1 根据用户ID查询订单数。

步骤：
* 创建Spring Boot项目：usercenter， ordercenter
* 配置MyBatis、MySQL。
* 根据需求开发功能。
* 

### 参考
* `https://github.com/alibaba/spring-cloud-alibaba`
