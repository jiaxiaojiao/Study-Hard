## Node exporter 

源码： `https://github.com/prometheus/node_exporter`


### 目录
* [Node exporter 是什么？](#Node-exporter-是什么？)
* [Node exporter 有哪些功能？](#Node-exporter-有哪些功能？)
* [安装部署](#安装部署)
* 使用
    * [修改Prometheus配置](#修改Prometheus配置)
* [参考](#参考)

### Node exporter 是什么？
Exporter是Prometheus的一类数据采集组件的总称。它负责从目标处搜集数据，并将其转化为Prometheus支持的格式。与传统的数据采集组件不同的是，它并不向中央服务器发送数据，而是等待中央服务器主动前来抓取，默认的抓取地址为http://CURRENT_IP:9100/metrics

Node exporter 的作用是收集机器的系统数据（采集服务器层面的运行指标）， 包括机器的loadavg、filesystem、meminfo等基础监控，类似于传统主机监控维度的zabbix-agent。

Node exporter 由prometheus官方提供、维护，不会捆绑安装，但基本上是必备的exporter。

### Node exporter 有哪些功能？
* node-exporter用于提供*NIX内核的硬件以及系统指标。
* 根据不同的*NIX操作系统，node-exporter采集指标的支持也是不一样的。

### 安装部署
安装方式包括：
* 二进制部署
* Docker 安装 Node exporter
```text
docker run -d \
  --net="host" \
  --pid="host" \
  -v "/:/host:ro,rslave" \
  quay.io/prometheus/node-exporter \
  --path.rootfs /host

【位置本地虚拟机-VM4】
# 1. 拉取镜像 
docker pull prom/node-exporter
# 2. 修改docker compose配置。（修改了 /usr/local/nacos-docker/example/standalone-derby.yaml）
  node-exporter:
    container_name: node-exporter
    image: prom/node-exporter:latest
    ports:
      - "9100:9100"
    restart: on-failure
# 3. 修改Prometheus配置。 （/etc/prometheus/prometheus.yml）
- job_name: 'node-exporter'
  scrape_interval: 8s
  static_configs:
  - targets:
    - localhost:9100
```
* K8s 安装 Node exporter

### 修改Prometheus配置


```text
# http://192.168.229.129:9100/metrics
# HELP go_gc_duration_seconds A summary of the GC invocation durations.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
go_gc_duration_seconds{quantile="0.25"} 0
go_gc_duration_seconds{quantile="0.5"} 0
go_gc_duration_seconds{quantile="0.75"} 0
go_gc_duration_seconds{quantile="1"} 0
......
promhttp_metric_handler_requests_total{code="200"} 0
promhttp_metric_handler_requests_total{code="500"} 0
promhttp_metric_handler_requests_total{code="503"} 0
```

```text
修改docker compose配置。（修改了 /usr/local/nacos-docker/example/standalone-derby.yaml）
net: "host"
```

```text
# 删除docker 容器
docker rm prometheus
docker rm alertmanager
docker rm nacos-standalone
docker rm grafana
docker rm node-exporter
```
### 参考
* https://www.jianshu.com/p/e3c9fc929d8a
* https://zhuanlan.zhihu.com/p/78290435
* https://songjiayang.gitbooks.io/prometheus/content/
* https://www.jianshu.com/p/7bec152d1a1f