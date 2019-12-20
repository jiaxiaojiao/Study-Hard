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
    * [2. Docker 安装](#2.-Docker-安装)
### 1. 二进制包安装

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






### 2. Docker 安装
> 前提条件： 已经安装Docker

```text
Prometheus的Docker镜像地址：
https://hub.docker.com/u/prom
```


