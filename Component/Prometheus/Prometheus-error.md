## Prometheus 问题排查 - 数据不展示

#### 现象描述
1. Prometheus 查询监控数据，不显示
2. Prometheus 数据在 Grafana 中进行展示，数据不显示。
3. 全都是 `No Data`

#### 问题排查
* 数据库 
* `web` 端。
访问http://192.168.229.128:9090/graph ，提示：
```text
Warning! Detected 28799.39 seconds time difference between your browser and the server. Prometheus relies on accurate time and time drift might cause unexpected query results.
```
数据不显示的原因是： 时间不同步。

#### 问题修复

浏览器时间 和 数据库时间 不同步会导致浏览器端无法正常显示数据，需要把数据库端和浏览器端时间同步。

*安装 Prometheus 之前需要先安装 ntp时间同步。

1. 安装 `ntpdate` 工具。 命令： ` yum -y install ntp ntpdate`
2. 设置系统时间与网络时间同步。 `ntpdate -d time.nist.gov` 或 `time.nist.gov、time.nuri.net、0.asia.pool.ntp.org、1.asia.pool.ntp.org、2.asia.pool.ntp.org、3.asia.pool.ntp.org` 没执行成功，直接修改的 `date -s 14:29:00` 强制修改的时间。
3. 系统实现写入硬件时间。 `hwclock --systohc`
4. 虚拟机与主机时间同步。 VM-虚拟机设置-将客户机时间与主机时间同步。 我用的是虚拟机，只设置这个就好了。
5. `docker` 容器时间和系统时间不一致。???
按照网上查询的 容器run 添加`-v /etc/timezone:/etc/timezone -v /etc/localtime:/etc/localtime`，在虚拟机中执行，还是有问题。。。。不知道哪儿。。。。所以，我决定： VM-1 暂时弃用，改为使用VM-4



