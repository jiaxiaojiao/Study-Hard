### Docker安装部署Nacos

> Docker Compose安装Nacos。 位置【本地虚拟机-VM4】，目前三个example： 单机模式 Derby、单机模式 Mysql、集群模式。
> 都可以启动，访问。但是可能是由于虚拟机性能和配置的原因集群模式下，经常连不上nacos或nacos重启。

### 目录
* [操作步骤](#操作步骤)
* [常见的配置属性Common property configuration](#常见的配置属性Common-property-configuration)
* [Docker安装部署遇到的问题](#Docker安装部署遇到的问题)
* [参考](#参考)

### 操作步骤
* Clone 项目
```text
git clone https://github.com/nacos-group/nacos-docker.git
cd nacos-docker

#地址：【本地虚拟机-VM4】  
```

* 单机模式 Derby
```text
docker-compose -f example/standalone-derby.yaml up

【本地虚拟机-VM4】
执行这一步一直有问题，已经修改了standalone-derby.yaml，也把所有的容器stop和rm了。
启动报错： nacos-standalone | bin/docker-startup.sh: line 99: /home/nacos/logs/start.out: Permission denied
临时关闭安全权限后可以启动。
```

* 单机模式 Mysql
```text
docker-compose -f example/standalone-mysql.yaml up

【本地虚拟机-VM4】
执行异常，临时关闭安全权限后可以启动。
```

* 集群模式
```text
docker-compose -f example/cluster-hostname.yaml up

【本地虚拟机-VM4】
可以启动。
【异常情况】
1. 但是nacos集群： nacos1，nacos2，nacos3经常重启restarting。原因： nacos1 exited with code 1
2. 物理机通过经常访问不到nacos(ip:8848)，有时能访问。不能访问的多。
``` 

* 服务注册
```text
curl -X POST 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080'

【本地虚拟机-VM4】
集群模式启动后，无法进行服务注册，无法打开。。。
```

* 服务发现
```text
curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instances?serviceName=nacos.naming.serviceName'
```

* 发布配置
```text
curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=helloWorld"
```

* 获取配置
```text
curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"
```

* Nacos 控制台
```text
link：http://127.0.0.1:8848/nacos/
```

### 常见的配置属性Common property configuration
<table>
  <tr><th>name名称</th><th>description描述</th><th>option选项</th></tr>
  <tr><td>MODE</td><td>cluster模式/standalone模式</td><td>cluster/standalone default cluster</td></tr>
  <tr><td>NACOS_SERVERS</td><td>nacos cluster地址</td><td>eg. ip1,ip2,ip3</td></tr>
  <tr><td>PREFER_HOST_MODE</td><td>是否支持hostname</td><td>hostname/ip default ip</td></tr>
  <tr><td>NACOS_SERVER_PORT</td><td>nacos服务器端口</td><td>default 8848</td></tr>
  <tr><td>NACOS_SERVER_IP</td><td>多网卡下的自定义nacos服务器IP</td><td></td></tr>
  <tr><td>SPRING_DATASOURCE_PLATFORM</td><td>standalone 支持 mysql</td><td>mysql / empty default empty</td></tr>
  <tr><td>MYSQL_MASTER_SERVICE_HOST</td><td>mysql 主节点host</td><td></td></tr>
  <tr><td>MYSQL_MASTER_SERVICE_PORT</td><td>mysql 主节点端口</td><td>default : 3306</td></tr>
  <tr><td>MYSQL_MASTER_SERVICE_DB_NAME</td><td>mysql 主节点数据库</td><td></td></tr>
  <tr><td>MYSQL_MASTER_SERVICE_USER</td><td>数据库用户名</td><td></td></tr>
  <tr><td>MYSQL_MASTER_SERVICE_PASSWORD</td><td>数据库密码</td><td></td></tr>
  <tr><td>MYSQL_SLAVE_SERVICE_HOST</td><td>mysql从节点host</td><td></td></tr>
  <tr><td>MYSQL_SLAVE_SERVICE_PORT</td><td>mysql从节点端口</td><td>default :3306</td></tr>
  <tr><td>MYSQL_DATABASE_NUM</td><td>数据库数量</td><td>default :2</td></tr>
  <tr><td>JVM_XMS</td><td>-Xms</td><td>default :2g</td></tr>
  <tr><td>JVM_XMX</td><td>-Xmx</td><td>default :2g</td></tr>
  <tr><td>JVM_XMN</td><td>-Xmn</td><td>default :1g</td></tr>
  <tr><td>JVM_MS</td><td>-XX:MetaspaceSize</td><td>default :128m</td></tr>
  <tr><td>JVM_MMS</td><td>-XX:MaxMetaspaceSize</td><td>default :320m</td></tr>
  <tr><td>NACOS_DEBUG</td><td>开启远程调试</td><td>y/n default :n</td></tr>
  <tr><td>TOMCAT_ACCESSLOG_ENABLED</td><td>server.tomcat.accesslog.enabled</td><td>default :false</td></tr>
</table>

### Docker安装部署遇到的问题
* 启动时异常，导致启动失败，查看日志。 
```text
nacos-standalone | bin/docker-startup.sh: line 99: /home/nacos/logs/start.out: Permission denied

chown: changing ownership of '/var/lib/mysql/': Permission denied
```
Centos7安全Selinux禁止了一些安全权限，导致mysql和mariadb在进行挂载/var/lib/mysql的时候会提示上面的信息。
解决方法：
1. 在docker run中加入 `--privileged=true`  给容器加上特定权限
2. 关闭selinux csdn
3. 在selinux添加规则，修改挂载目录。


### 参考
* `https://nacos.io/zh-cn/docs/quick-start-docker.html`
* `https://github.com/nacos-group/nacos-docker`
* `https://www.jianshu.com/p/bccda875e7a5`
* `https://blog.csdn.net/xinluke/article/details/51925293`
* `https://www.cnblogs.com/hellxz/p/nacos-cluster-docker.html`
* `https://www.jianshu.com/p/c410845f0dca`
* `https://cloud.tencent.com/developer/article/1453550`
* `http://www.itmuch.com/spring-cloud-alibaba/nacos-ha/`