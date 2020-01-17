## 自定义JVM Dashboard

> 2020.01.14

### 目录
* [前提条件](#前提条件)
    * [Prometheus监控的目标Targets](#Prometheus监控的目标Targets)
* [Grafana 的 Dashboard 市场](#Grafana-的-Dashboard-市场)
* [使用的Dashboard](#使用的Dashboard)
* [自定义Dashboard](#自定义Dashboard)
* [参考](#参考)

### 前提条件
* 目前Prometheus已经监控的目标Targets， State状态： UP

##### Prometheus监控的目标Targets
Endpoint(端点) 
* nacos(注册中心，配置中心) `http://192.168.229.129:8848/nacos/actuator/prometheus`
    * metric（指标）主要是：nacos, tomcat, http_server_requests, system_cpu, jvm_gc, jvm_memory, jvm_buffer, jvm_threads
* node-exporter（收集机器的系统数据） `http://192.168.229.129:9100/metrics`
    * metric（指标）主要是：node, go_gc, go_goroutines, go_memstats, process
* prometheus(监控自己) `http://192.168.229.129:9090/metrics`
    * metric（指标）主要是：prometheus, go_gc, go_goroutines, go_memstats, net_conntrack, process
* springboot-user-consumer
* springboot-user-provider

### Grafana 的 Dashboard 市场
Grafana 的 Dashboard 市场： `https://grafana.com/grafana/dashboards`

我的账户： `https://grafana.com/orgs/jiaxiaojiao`

### 使用的Dashboard
* JVM (Micrometer) `https://grafana.com/grafana/dashboards/4701`
* 硬件信息监控，包含：CPU 内存 磁盘 IO 网络 温度等监控指标。 `https://grafana.com/grafana/dashboards/8919`
* Prometheus 2.0 Stats， Grafana面板自带的Dashboard。
* 硬件监控2 `https://grafana.com/grafana/dashboards/9096`
* 硬件监控full `https://grafana.com/grafana/dashboards/1860`
* Nacos监控， `https://github.com/nacos-group/nacos-template/blob/master/nacos-grafana.json` 

注意： Nacos监控信息的数据源默认是 prometheus。 

### 自定义Dashboard
```text
# 需要的metric
http_server_requests_seconds_count    http请求次数，包括多种(url,方法,code)
http_server_requests_seconds_sum	http请求总耗时，包括多种(url,方法,code)
http_server_requests_seconds_max

```

### 参考
* 参考了Grafana创建Dashboard `https://segmentfault.com/a/1190000021430295`
