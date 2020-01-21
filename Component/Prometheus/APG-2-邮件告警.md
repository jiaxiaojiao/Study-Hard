## 告警，邮件告警

> 2020.1.17

### 目录
* [前提](#前提)
* [告警](#告警)
* [支持的告警方式](#支持的告警方式)
* [配置和使用](#配置和使用)
* [参考](#参考)

### 前提
* Grafana面板，账号密码：admin-admin 。 http://192.168.229.129:3000
* Prometheus，没有账号密码。 http://192.168.229.129:9090/targets
* Nacos， 账号密码： nacos-nacos 。 http://192.168.229.129:8848/nacos/
* Nacos暴露actuator 。 http://192.168.229.129:8848/nacos/actuator/prometheus

```text
# 操作步骤
# cd /usr/local/nacos-docker/
# docker-compose -f example/standalone-derby.yaml up

```



### 告警
### 支持的告警方式
### 配置和使用

### 参考
* Nacos监控手册-配置grafana告警 https://nacos.io/zh-cn/docs/monitor-guide.html
* Grafana https://grafana.com/
* https://baijiahao.baidu.com/s?id=1637241250614233036&wfr=spider&for=pc
* https://www.cnblogs.com/cjsblog/p/11288530.html
* https://baijiahao.baidu.com/s?id=1637241250614233036&wfr=spider&for=pc
* http://www.imooc.com/article/73338
* https://blog.csdn.net/jailman/article/details/78920166
* https://blog.csdn.net/Jailman/article/details/103294998