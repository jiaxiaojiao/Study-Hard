## 搭建监控系统

> Prometheus + Alertmanager + Grafana
>
> 目标： 
> 1. 创建Demo项目
> 2. 集成监控系统（Prometheus + Alertmanager + Grafana）
> 3. Docker容器镜像启动监控系统（Prometheus + Alertmanager + Grafana）
> 4. Kubernetes管理容器（Prometheus + Alertmanager + Grafana）

### 目录
* [Demo项目](#Demo项目)
* [Docker部署Demo项目](../Docker/Docker安装部署-Java应用.md)
* [Docker安装Prometheus](Prometheus-install.md#2.-Docker-安装部署Prometheus) 之前已经安装过了
* [Prometheus配置监控Demo项目](#Prometheus配置监控Demo项目)
* [Prometheus集成Alertmanager](#Prometheus集成Alertmanager)
* [Docker安装Alertmanager](#Docker安装Alertmanager)
* [Docker安装Grafana](#Docker安装Grafana)
* 至此根据以上的步骤，已经搭建好了监控系统，但是还需要一些配置和验证，比如报警的邮件等等。 TODO
* [参考](#参考)


### Demo项目
* [使用IDEA创建Spring Boot项目](../Spring/Spring-Boot/Spring-Boot-New.md#使用IDEA创建Spring-Boot项目)
* 添加功能： 添加用户，用户列表。
* 集成Prometheus监控。
* Spring Boot 项目添加依赖
```text
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<!-- https://mvnrepository.com/artifact/io.micrometer/micrometer-registry-prometheus -->
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
    <version>1.3.2</version>
</dependency>
```
* 修改配置文件
```text
spring.application.name=DEMO
# 监控端点配置
management.endpoints.web.exposure.include=*
management.metrics.tags.application=${spring.application.name}
```
* 修改启动类，实例化MeterRegistryCustomizer：
```text
@SpringBootApplication
public class DemoApplication {
    @Value("${spring.application.name}")
    private String applicationName;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Bean
    MeterRegistryCustomizer<MeterRegistry> configurer(){
        return (registry) -> registry.config().commonTags("application", applicationName);
    }
}
```
* 集成Prometheus监控-检验。DEMO 项目（8080），启动后浏览器访问 `http://127.0.0.1:8080/actuator/prometheus`
```text
# HELP jvm_buffer_count_buffers An estimate of the number of buffers in the pool
# TYPE jvm_buffer_count_buffers gauge
jvm_buffer_count_buffers{application="DEMO",id="direct",} 6.0
jvm_buffer_count_buffers{application="DEMO",id="mapped",} 0.0
...
jvm_gc_memory_promoted_bytes_total{application="DEMO",} 7764208.0
```

### Prometheus配置监控Demo项目
* 编辑 `prometheus.yml` 配置文件。
```text
[root@bogon ~]# cd /etc/prometheus/
[root@bogon prometheus]# vim prometheus.yml 

global:
  scrape_interval:     15s

  external_labels:
    monitor: 'codelab-monitor'

scrape_configs:
  - job_name: 'prometheus'

    scrape_interval: 5s

    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'demo'
    metrics_path: '/demo/actuator/prometheus'
    scrape_interval: 5s

    static_configs:
      - targets: ['192.168.229.128:8080']
        labels:
          group: 'production'
```
* 重新启动Prometheus
```text
[root@bogon prometheus]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                            NAMES
e9141e53f3b3        tomcat:latest       "catalina.sh run"        3 hours ago         Up 58 minutes       0.0.0.0:8080->8080/tcp           mytomcat
78ec3d7edc23        prom/prometheus     "/bin/prometheus -..."   19 hours ago        Up 19 hours         192.168.229.128:9090->9090/tcp   prometheus
[root@bogon prometheus]# docker stop prometheus
prometheus
[root@bogon prometheus]# docker rm prometheus
prometheus
[root@bogon prometheus]# docker run -d -p 9090:9090 --name=prometheus -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
e8a045ed0340e4094e7b3918d017841a19f68f0ea7d38c68175a8241769cb55c
```
启动参数说明：
```text
-d 选项启动独立模式下的prometheus容器，这意味着容器将在后台启动，这种情况下只有stop docker才可以关闭prometheus，而不能执行ctrl+c
-p 选择指定端口号映射，通过访问本机的9090端口，即可访问prometheus容器的9090端口
--name 指定容器的名称
-v 选项建立本机文件和docker内文件的映射
--config.file 指定运行docker内prometheus的配置文件
```
* 检验
    * 物理机浏览器访问， `http://192.168.229.128:9090/targets` 查看监控对象
    * 查看应用的配置文件， `http://192.168.229.128:9090/config`
    * 查看项目CPU使用， `http://192.168.229.128:9090/graph?g0.range_input=1h&g0.expr=system_cpu_usage&g0.tab=0`
    * 等，检验没有问题。

### Prometheus集成Alertmanager
* 修改Prometheus的配置文件 `prometheus.yml`
```text
# Alertmanager配置
alerting:
  alertmanagers:
    - static_configs:
    - targets: ["localhost:9093"] # 设定alertmanager和prometheus交互的接口，即alertmanager监听的ip地址和端口
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      - alertmanager1:9093
```

### Docker安装Alertmanager
Alertmanager 下载和安装有很多种方式，这里使用Docker安装Alertmanager。

根据`https://github.com/prometheus/alertmanager`， 拉取镜像使用的镜像地址： `https://quay.io/repository/prometheus/alertmanager`

```text
$ docker pull quay.io/prometheus/alertmanager
```

具体操作的命令：
```text
# 本机虚拟机 VM-1 192.168.229.128
# Prometheus配置文件地址： /etc/prometheus/prometheus.yml
[root@bogon local]# docker pull quay.io/prometheus/alertmanager
Using default tag: latest
Trying to pull repository quay.io/prometheus/alertmanager ... 
latest: Pulling from quay.io/prometheus/alertmanager
0f8c40e1270f: Pull complete 
626a2a3fee8c: Pull complete 
05ec5ff61d82: Pull complete 
3e4eb9050294: Pull complete 
c920019f84ec: Pull complete 
59ee938b06a9: Pull complete 
Digest: sha256:7e4e9f7a0954b45736d149c40e9620a6664036bb05f0dce447bef5042b139f5d
Status: Downloaded newer image for quay.io/prometheus/alertmanager:latest

# 查看镜像 
[root@bogon local]# docker images
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
mytomcat                          v1                  e71e6a54722e        23 hours ago        561 MB
docker.io/tomcat                  latest              6fa48e047721        11 days ago         507 MB
quay.io/prometheus/alertmanager   latest              0881eb8f169f        13 days ago         52.1 MB
ouruser/sinatra                   v2                  bac43673a2c9        2 weeks ago         453 MB
docker.io/prom/prometheus         latest              7317640d555e        6 weeks ago         130 MB
docker.io/centos                  latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu                  12.04               5b117edd0b76        2 years ago         104 MB
[root@bogon local]# 

# 添加alertmanager配置文件（我放到了Prometheus配置文件相同的路径）
global:
  smtp_smarthost: 'smtp.163.com:25'　　#163服务器
  smtp_from: 'XX@163.com'　　　　　　　　#发邮件的邮箱
  smtp_auth_username: 'XX@163.com'　　#发邮件的邮箱用户名，也就是你的邮箱
  smtp_auth_password: 'XXXX'　　　　　　　　#发邮件的邮箱密码
  smtp_require_tls: false　　　　　　　　#不进行tls验证

route:
  group_by: ['alertname']
  group_wait: 10s
  group_interval: 10s
  repeat_interval: 10m
  receiver: live-monitoring

receivers:
- name: 'live-monitoring'
  email_configs:
  - to: '543240627@qq.com'　　　　　　　　#收邮件的邮箱


# 添加报警规则（相同的目录） node_down.yml
groups:
- name: node_down
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 1m
    labels:
      user: test
    annotations:
      summary: "Instance {{ $labels.instance }} down"
      description: "{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 1 minutes."

# 启动Alertmanager容器
[root@bogon prometheus]# docker run -d -p 9093:9093 -v /etc/prometheus/alertmanager.yml:/etc/alertmanager/config.yml --name alertmanager quay.io/prometheus/alertmanager
42fbc0df0f14be4bc998c3bf30bd5b759f3ce1efb9d99b7f046da084bff59508
[root@bogon prometheus]# 

# 物理机浏览器访问 http://192.168.229.128:9093

```

### Docker安装Grafana

```text
$ docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

```text
# 本机虚拟机 VM-1 192.168.229.128
[root@bogon local]# docker run -d --name=grafana -p 3000:3000 grafana/grafana
Unable to find image 'grafana/grafana:latest' locally
Trying to pull repository docker.io/grafana/grafana ... 
latest: Pulling from docker.io/grafana/grafana
89d9c30c1d48: Pull complete 
92c128799d27: Pull complete 
fa1904dc426e: Pull complete 
0bc30826133d: Pull complete 
a086b998918c: Pull complete 
3e65953c80f4: Pull complete 
c8acf10409a4: Pull complete 
deff1c4eb3ee: Pull complete 
Digest: sha256:5c2fc6c625d8d5aa44926a9bc7d02ce91ff85d1769ed2378006caed378e9fb4a
Status: Downloaded newer image for docker.io/grafana/grafana:latest
e31e47800596ee709eee30b2405ba71ffc91c268b7d0e541ee7f0e00eb70556f
[root@bogon local]# docker images
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
mytomcat                          v1                  e71e6a54722e        25 hours ago        561 MB
docker.io/tomcat                  latest              6fa48e047721        11 days ago         507 MB
quay.io/prometheus/alertmanager   latest              0881eb8f169f        13 days ago         52.1 MB
docker.io/grafana/grafana         latest              7a40c3c56100        13 days ago         228 MB
ouruser/sinatra                   v2                  bac43673a2c9        2 weeks ago         453 MB
docker.io/prom/prometheus         latest              7317640d555e        6 weeks ago         130 MB
docker.io/centos                  latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu                  12.04               5b117edd0b76        2 years ago         104 MB
[root@bogon local]# 
```

```text
账号： admin
密码： admin
新密码： jiaxiaojiao
```

* 物理机浏览器访问： `http://192.168.229.128:3000` , 管理员账号登录
* 创建一个prometheus的数据源。`Add data source -> Prometheus -> Prometheus地址 http://192.168.229.128:9090  -> save and test` 
* 配置一个`Dashboards`   可以用自带模板，也可以去https://grafana.com/dashboards，下载对应的模板。 我选择了自带的`Prometheus 2.0 Stats`
* 添加用户 `Add Users`  （随意）
* 查看Prometheus的dashboard。 



### 参考
* `后续才想到写参考，不全`
* `https://github.com/prometheus/alertmanager`
* `https://yq.aliyun.com/articles/664698`
* `https://grafana.com/grafana/download?platform=docker`
* `https://blog.51cto.com/msiyuetian/2369130`