## Docker 安装软件

### 目录
* CentOS安装Docker
* Docker安装Tomcat
* Tomcat部署Demo应用
* Docker安装Prometheus，监控Demo应用
* Docker安装Alertmanager
* Docker安装Grafana
* [安装步骤](#安装步骤)
* [接下来做什么呢？](#接下来做什么呢？)

### 安装步骤
* 安装Docker
```text
# 下载Docker（sudo 使用root账户操作，我一般用的都是root账户，所以就没有用sudo）
# yum install docker

# 启动Docker
# service docker start

# 开机启动
chkconfig docker on

# 获取镜像
# docker pull centos

# 查看CentOS镜像
# docker images

# 测试CentOS
[root@bogon ~]# docker run -i -t centos /bin/bash
[root@cc687ea63840 /]# date
Mon Dec 30 09:04:35 UTC 2019

# 时间还是不对，怎么回事啊？ 继续安装别的试试吧。
[root@cc687ea63840 /]# exit
exit

```

* 安装Tomcat
```text
# 安装Tomcat
# docker pull tomcat

# 生成容器，run
# 启动容器-1： 有问题，时间不对。
    # docker run -p 8080:8080 tomcat:latest
    日志时间不对。
    # 进入容器，查看容器时间
    # docker exec -it $CONTAINER_ID /bin/bash
    时间也不对。

# 时间不一致-解决-1： 创建容器时指定启动参数，自动挂载localtime文件到容器内。
# docker run -v /etc/localtime:/etc/localtime -p 8080:8080 tomcat:latest
# docker run -d -v /etc/localtime:/etc/localtime -p 8080:8080 tomcat:latest
日志时间不对。 进入容器，查看容器时间，时间对。

# 时间不一致-解决-2： 复制主机的localtime
# docker cp /etc/localtime【容器ID或者NAME】:/etc/localtime
# docker cp /etc/localtime 4d2c1004db41:/etc/localtime
报错：Error response from daemon: Error processing tar file(exit status 1): invalid symlink "/usr/share/zoneinfo/UCT" -> "../usr/share/zoneinfo/Asia/Shanghai"

# 时间不一致-解决-3： 把时区设置加入到Dockerfile中
# Dockerfile内容： 我放的地址： /usr/local/docker/
FROM tomcat 
RUN echo 'Asia/shanghai' > /etc/timezone;
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# docker build -t tomcat:v1 .

# 生成容器，启动tomcat:v1。 日志时间没有问题，进入容器时间没有问题。
```

* 上传Demo.war 放到webapps下，重启tomcat
```text
[root@bogon local]# docker cp demo.war [tomcat容器ID]:/usr/local/tomcat/webapps
[root@bogon local]# docker restart [tomcat容器ID]

```

* 安装监控软件 Prometheus
```text
# docker pull prom/prometheus

# 生成容器，启动。 日志中时序时间使用的是UTC世界标准时间，本机使用的是CST时间China Standard Time UT+8:00 中国标准时间。
# docker run -p 9090:9090 prom/prometheus 
# 不用解决，集成Grafana后看一下展示时间有没有问题。
```

* 修改Prometheus配置文件： 添加监控Demo项目。 启动后demo是不健康的，为什么呢？？！！
```text
# 配置文件我放的目录： /etc/prometheus/prometheus.yml
docker run -d -p 9090:9090 --name=prometheus -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
# 使用的配置信息

global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s
  external_labels:
    monitor: 'codelab-monitor'
alerting:
  alertmanagers:
  - static_configs:
    - targets: []
    scheme: http
    timeout: 10s
    api_version: v1
scrape_configs:
- job_name: prometheus
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - localhost:9090
- job_name: 'demo'
  metrics_path: '/demo/actuator/prometheus'
  scrape_interval: 5s
  static_configs:
  - targets: ['192.168.229.129:8080']

```

* 安装Alertmanager，配置到Prometheus
```text
# Alertmanager配置
# 1. 设定alertmanager和prometheus交互的接口，即alertmanager监听的ip地址和端口 （修改在/etc/prometheus/prometheus.yml）
alerting:
  alertmanagers:
    - static_configs:
    - targets: ["localhost:9093"] 

# 2. 添加alertmanager.yml
# 3. 添加node_down.yml

# 安装Alertmanager
# docker pull prom/alertmanager

# 启动
# docker run -p 9093:9093 -v /etc/prometheus/alertmanager.yml:/etc/alertmanager/config.yml prom/alertmanager
# docker run -d -p 9093:9093 -v /etc/prometheus/alertmanager.yml:/etc/alertmanager/config.yml --name alertmanager quay.io/prometheus/alertmanager
```

* 安装 grafana
```text
# docker pull grafana/grafana

# 运行
# docker run -p 3000:3000 grafana/grafana
# docker run -d --name=grafana -p 3000:3000 grafana/grafana

账号： admin
密码： admin
新密码： jiaxiaojiao
# 配置data source： Prometheus
* 物理机浏览器访问： `http://192.168.229.128:3000` , 管理员账号登录
* 创建一个prometheus的数据源。`Add data source -> Prometheus -> Prometheus地址 http://192.168.229.129:9090  -> save and test` 
* 配置一个`Dashboards`   可以用自带模板，也可以去https://grafana.com/dashboards，下载对应的模板。 我选择了自带的`Prometheus 2.0 Stats`
* 添加用户 `Add Users`  （随意）
* 查看Prometheus的dashboard。 
```

### 接下来做什么呢？
* Docker容器内通讯，使用的是内部的IP地址，需要通过 `docker inspect 容器名称或 id` 查看容器的IP地址，写到配置文件。
* 这个应该是可以配置修改的。待定。
* Grafana面板主要展示： 机器硬件、应用接口、JVM、堆、栈、垃圾回收、线程。 找一下这些面板展示的模板。
* 以上几个监控组件的启动方式，由命令行启动（也就是上面写的一条一条的启动） 修改为使用 Docker Compose 运行。
* 2个项目互相调用，通过RPC、Feign方式
* 注册中心 Nacos
* 配置管理： Apollo
* 限流，降级，熔断：sentinel
* 分布式事务解决方案。 seata。 （最后。。。）
