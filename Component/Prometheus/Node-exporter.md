## Node exporter 

源码： `https://github.com/prometheus/node_exporter`


### 目录
* [Node exporter 是什么？](#Node-exporter-是什么？)
* [安装部署](#安装部署)
* 使用
    * [修改Prometheus配置](#修改Prometheus配置)
* [](#)
* [参考](#参考)

### Node exporter 是什么？
Node exporter 由prometheus官方提供、维护，不会捆绑安装，但基本上是必备的exporter。

Node exporter 的作用是收集机器的系统数据（采集服务器层面的运行指标）， 包括机器的loadavg、filesystem、meminfo等基础监控，类似于传统主机监控维度的zabbix-agent。

### 安装部署
安装方式包括：
* 二进制部署
* Docker 安装 Node exporter
* K8s 安装 Node exporter

### 修改Prometheus配置

### 
### 参考
* `https://www.jianshu.com/p/e3c9fc929d8a`
* `https://zhuanlan.zhihu.com/p/78290435`
* `https://songjiayang.gitbooks.io/prometheus/content/`
* `https://www.jianshu.com/p/7bec152d1a1f`