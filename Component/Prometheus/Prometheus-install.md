## Prometheus 安装， 搭建Prometheus 监控平台

> 安装基于本地的虚拟机
>
> 本机虚拟机 VM-1 192.168.229.128 （root-jiaxiaojiao）
<br> 本地虚拟机 VM-2 192.168.229.131 （root-jiaxiaojiao）
<br> 本地虚拟机 VM-3 192.168.229.132 （root-jiaxiaojiao）
<br> 本地虚拟机 VM-4 192.168.229.129 （root-jiaxiaojiao）


### 目录
* 安装方式
    * [1. 二进制包安装](#1.-二进制包安装)
        * [下载最新安装包](#下载最新安装包)
        * [配置Prometheus监控对象-自己](#配置Prometheus监控自已)
        * [启动Prometheus](#启动Prometheus)
    * [2. Docker 安装](#2.-Docker-安装部署Prometheus)
* [参考](#参考)
### 1. 二进制包安装

安装位置： 本地虚拟机 VM-4 192.168.229.129

##### 下载最新安装包
下载地址： `https://prometheus.io/download/`
* Prometheus 监控系统和时序数据库。主要是负责存储、抓取、聚合、查询方面。
* Alertmanager 主要用于接收 Prometheus 发送的告警信息，实现报警功能。
* Pushgateway 主要是实现接收由Client push过来的指标数据，在指定的时间间隔，由主程序来抓取。推动接受器完成临时和批处理作业。
```text
## 20191220下载：
prometheus-2.14.0.linux-amd64.tar.gz
alertmanager-0.20.0.linux-amd64.tar.gz
pushgateway-1.0.0.linux-amd64.tar.gz

## 上传到本地虚拟机 VM-4
[root@bogon ~]# cd /usr/local/
[root@bogon local]# ls
apollo  bin  data  etc  games  include  lib  lib64  libexec  mysql  sbin  share  src
[root@bogon local]# rz
[root@bogon local]# ls
alertmanager-0.20.0.linux-amd64.tar.gz  etc      lib64                                 pushgateway-1.0.0.linux-amd64.tar.gz
apollo                                  games    libexec                               sbin
bin                                     include  mysql                                 share
data                                    lib      prometheus-2.14.0.linux-amd64.tar.gz  src

## 解压
[root@bogon local]# tar xvfz prometheus-2.14.0.linux-amd64.tar.gz
prometheus-2.14.0.linux-amd64/
prometheus-2.14.0.linux-amd64/NOTICE
prometheus-2.14.0.linux-amd64/prometheus
prometheus-2.14.0.linux-amd64/LICENSE
prometheus-2.14.0.linux-amd64/prometheus.yml
prometheus-2.14.0.linux-amd64/console_libraries/
prometheus-2.14.0.linux-amd64/console_libraries/prom.lib
prometheus-2.14.0.linux-amd64/console_libraries/menu.lib
prometheus-2.14.0.linux-amd64/consoles/
prometheus-2.14.0.linux-amd64/consoles/prometheus.html
prometheus-2.14.0.linux-amd64/consoles/node-overview.html
prometheus-2.14.0.linux-amd64/consoles/node-cpu.html
prometheus-2.14.0.linux-amd64/consoles/prometheus-overview.html
prometheus-2.14.0.linux-amd64/consoles/node.html
prometheus-2.14.0.linux-amd64/consoles/index.html.example
prometheus-2.14.0.linux-amd64/consoles/node-disk.html
prometheus-2.14.0.linux-amd64/tsdb
prometheus-2.14.0.linux-amd64/promtool
[root@bogon local]# tar xvfz alertmanager-0.20.0.linux-amd64.tar.gz 
alertmanager-0.20.0.linux-amd64/
alertmanager-0.20.0.linux-amd64/LICENSE
alertmanager-0.20.0.linux-amd64/alertmanager
alertmanager-0.20.0.linux-amd64/amtool
alertmanager-0.20.0.linux-amd64/NOTICE
alertmanager-0.20.0.linux-amd64/alertmanager.yml
[root@bogon local]# tar xvfz pushgateway-1.0.0.linux-amd64.tar.gz 
pushgateway-1.0.0.linux-amd64/
pushgateway-1.0.0.linux-amd64/NOTICE
pushgateway-1.0.0.linux-amd64/pushgateway
pushgateway-1.0.0.linux-amd64/LICENSE
[root@bogon local]# ls
alertmanager-0.20.0.linux-amd64         data     lib      prometheus-2.14.0.linux-amd64         sbin
alertmanager-0.20.0.linux-amd64.tar.gz  etc      lib64    prometheus-2.14.0.linux-amd64.tar.gz  share
apollo                                  games    libexec  pushgateway-1.0.0.linux-amd64         src
bin                                     include  mysql    pushgateway-1.0.0.linux-amd64.tar.gz
[root@bogon local]# 

## 修改包名，删除tar.gz文件。（个人习惯）
[root@bogon local]# mv prometheus-2.14.0.linux-amd64 prometheus
[root@bogon local]# mv alertmanager-0.20.0.linux-amd64 alertmanager
[root@bogon local]# mv pushgateway-1.0.0.linux-amd64 pushgateway
[root@bogon local]# rm alertmanager-0.20.0.linux-amd64.tar.gz 
rm：是否删除普通文件 "alertmanager-0.20.0.linux-amd64.tar.gz"？y
[root@bogon local]# rm prometheus-2.14.0.linux-amd64.tar.gz 
rm：是否删除普通文件 "prometheus-2.14.0.linux-amd64.tar.gz"？y
[root@bogon local]# rm pushgateway-1.0.0.linux-amd64.tar.gz 
rm：是否删除普通文件 "pushgateway-1.0.0.linux-amd64.tar.gz"？y
[root@bogon local]# 
```

##### 配置Prometheus监控自已
Prometheus 通过默认 http://localhost:9090/metrics HTTP接口暴露了自己的性能指标数据，当然也就可以配置抓取目标 targets 为自己了。

Prometheus 采集自身性能数据就是一个十分好的例子了，打开解压目录下面的prometheus.yml文件。
```text
# 全局配置
global:
  scrape_interval:     15s # 默认 15秒到目标处抓取数据

  # 这个标签是在本机上每一条时间序列上都会默认产生的，主要可以用于 联合查询、远程存储、Alertmanger时使用。
  external_labels:
    monitor: 'codelab-monitor'

# 这里就表示抓取对象的配置
# 设置抓取自身数据
scrape_configs:
  #  job name 这个配置是表示在这个配置内的时间序例，每一条都会自动添加上这个{job_name:"prometheus"}的标签。
  - job_name: 'prometheus'

    # 重写了全局抓取间隔时间，由15秒重写成5秒。
    scrape_interval: 5s

    static_configs:
      - targets: ['localhost:9090']
```

本机虚拟机VM-4的配置信息
```text
[root@bogon prometheus]# vim prometheus.yml 

# Alertmanager configuration
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.
    static_configs:
    - targets: ['localhost:9090']
```

##### 启动Prometheus
* 使用刚才的配置文件启动Prometheus。
* 使用IP:9090访问
    * 如果不能访问，查看ping网络状态和telnet端口是否开启。
```text
./prometheus --config.file=prometheus.yml

或

./prometheus
```

Window-使用浏览器访问： `http://192.168.229.129:9090/`  无法访问，可以ping通。为什么呢？

原因是防火墙。

关闭防火墙
```text
# 查看防火墙状态
> systemctl status firewalld
# 暂时关闭防火墙
> systemctl stop firewalld
# 关闭开机启动防火墙
> systemctl disable firewalld
# 关闭安全策略
> vi /etc/sysconfig/selinux

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
# 这里修改为disabled
SELINUX=disabled
# SELINUXTYPE= can take one of three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

然后再访问就可以了。



### 2. Docker 安装部署Prometheus
本机虚拟机 VM-1 192.168.229.128

> 前提条件： 已经安装Docker

```text
Prometheus的Docker镜像地址：
https://hub.docker.com/u/prom
```

* 首先获取Prometheusdocker镜像
```text
docker pull prom/prometheus
```
* 然后编写配置文件 prometheus.yml
```text
global:
  scrape_interval: 10s
  scrape_timeout: 10s
  evaluation_interval: 10m
scrape_configs:
  - job_name: spring-boot
    scrape_interval: 5s
    scrape_timeout: 5s
    metrics_path: /admin/prometheus
    scheme: http
    basic_auth:
      # 对应application.yml security配置
      username: admin
      password: 123456
    static_configs:
      - targets:
        - 127.0.0.1:7778
```
* 启动容器
```text
docker run -d \
--name prometheus \
-p 10000:9090 \
-m 500M \
-v "$(pwd)/prometheus.yml":/etc/prometheus/prometheus.yml \
-v "$(pwd)/data":/data \
prom/prometheus \
--config.file=/etc/prometheus/prometheus.yml \
--log.level=info
```

安装路径和命令是在本机虚拟机 VM-1 192.168.229.128 上进行的。如下： 
```text
# 1. 获取Prometheus docker镜像
[root@bogon ~]# docker pull prom/prometheus
Using default tag: latest
Trying to pull repository docker.io/prom/prometheus ... 
latest: Pulling from docker.io/prom/prometheus
8e674ad76dce: Pull complete 
e77d2419d1c2: Pull complete 
8674123643f1: Pull complete 
21ee3b79b17a: Pull complete 
d9073bbe10c3: Pull complete 
585b5cbc27c1: Pull complete 
0b174c1d55cf: Pull complete 
a1b4e43b91a7: Pull complete 
31ccb7962a7c: Pull complete 
e247e238102a: Pull complete 
6798557a5ee4: Pull complete 
cbfcb065e0ae: Pull complete 
Digest: sha256:907e20b3b0f8b0a76a33c088fe9827e8edc180e874bd2173c27089eade63d8b8
Status: Downloaded newer image for docker.io/prom/prometheus:latest


# 2. 编辑配置文件prometheus.yml
[root@bogon ~]# cat << EOF >prometheus.yml
> global:
>   scrape_interval: 15s
>   external_labels:
>     monitor: 'codelab-monitor'
> scrape_configs:
>   - job_name: 'prometheus'
>     scrape_interval: 5s
>     target_groups:
>       - targets: ['localhost:9090']
> EOF
[root@bogon ~]# sudo mkdir /etc/prometheus
[root@bogon ~]# sudo mv prometheus.yml /etc/prometheus
# 以上配置暂时没有用到


# 3. 启动Prometheus
[root@bogon prometheus]# docker run --name prometheus -d -p 127.0.0.1:9090:9090 prom/prometheus
1ef4ed17ebeb024b0e08408d1832076ea9807cb11d703274ac0eeba8b0f71f61
[root@bogon prometheus]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                      NAMES
1ef4ed17ebeb        prom/prometheus     "/bin/prometheus -..."   5 seconds ago       Up 4 seconds        127.0.0.1:9090->9090/tcp   prometheus
# 以上这个本机用命令访问没有问题，但是物理机访问不了。 使用好几个方法都不管用。

# 4. 解决物理机无法访问虚拟机Docker中的应用
## 1. 重建Docker网络
### 停止docker服务
> systemctl stop docker
### 重建 docker 网络
> ifconfig docker0 down
> brctl delbr docker0
### 重启docker服务
> systemctl start docker
## 2. 也是网络的，不懂
> vi /etc/sysctl.conf
### 添加如下代码：
> net.ipv4.ip_forward=1
### 重启network服务
> systemctl restart network
### 查看是否修改成功
> sysctl net.ipv4.ip_forward
### 如果返回为“net.ipv4.ip_forward = 1”则表示成功了
### 我没有设置，只是验证了最后一步。没有问题。

[root@bogon prometheus]# docker run --name prometheus -d -p 192.168.229.128:9090:9090 prom/prometheus
78ec3d7edc23371355d9765ef31075241ffcbcb428ee191c45daade7f8a5255b
## 以上，本机访问和物理机访问都没有问题。 不知道是之前设置的网络好了，还是启动时应该指定IP
### 查看Docker启动镜像的IP地址
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                            NAMES
78ec3d7edc23        prom/prometheus     "/bin/prometheus -..."   11 seconds ago      Up 10 seconds       192.168.229.128:9090->9090/tcp   prometheus
[root@bogon ~]# docker inspect 78ec3d7edc23
... HostIP HostPort IPAddress 
[root@bogon ~]# curl http://172.17.0.2:9090/graph
[root@bogon ~]# curl http://192.168.229.128:9090/graph
```

### 参考
* https://www.cnblogs.com/vovlie/p/Prometheus_install.html
* https://www.jianshu.com/p/3284507b2f87
* http://qinghua.github.io/prometheus/
* https://www.cnblogs.com/suveng/p/11481399.html
* https://blog.csdn.net/qq_27520051/article/details/91478732
* https://blog.csdn.net/weixin_38860565/article/details/90047972