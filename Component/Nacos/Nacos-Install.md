## Nacos 安装部署

> Nacos支持三种部署模式
> * 单机模式 - 用于测试和单机试用。
> * 集群模式 - 用于生产环境，确保高可用。
> * 多集群模式 - 用于多数据中心场景。

### 目录
* [单机模式部署Nacos](#单机模式部署Nacos)
* [常见的配置属性](#常见的配置属性)
* [参考](#参考)

### 单机模式部署Nacos
* 环境要求
    * 64位操作系统。 推荐选用 Linux/Unix/Mac
    * JDK 1.8+
    * Maven 3.2.x+
* 安装包
    * 可以通过源码或者发行包两种方式获取Nacos
    * Docker运行Nacos
* 数据库。（目前没有配置数据库）
    * MySQL 5.6.5+
    * 初始化MySQL数据库 nacos-mysql.sql
    * 修改数据源配置。 conf/application.properties
    ```text
    # 添加mysql数据源的url、用户名和密码
    spring.datasource.platform=mysql
    
    db.num=1
    db.url.0=jdbc:mysql://11.162.196.16:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
    db.user=nacos_devtest
    db.password=youdontknow
    ```

安装位置： 
> 本机虚拟机 VM-1 192.168.229.128 （root/jxj-jiaxiaojiao） 
```text
# 本机系统 CentOS7 64位

# JDK版本
[root@bogon ~]# java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)

# Maven版本
[root@bogon ~]# mvn -version
Apache Maven 3.6.2 (40f52333136460af0dc0d7232c0dc0bcf0d9e117; 2019-08-27T23:06:16+08:00)
Maven home: /usr/local/apache-maven-3.6.2
Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: /usr/java/jdk1.8.0_231-amd64/jre
Default locale: zh_CN, platform encoding: UTF-8
OS name: "linux", version: "3.10.0-1062.el7.x86_64", arch: "amd64", family: "unix"

# Docker拉取Nacos镜像
[root@bogon ~]# docker pull nacos/nacos-server
Using default tag: latest
Trying to pull repository docker.io/nacos/nacos-server ... 
latest: Pulling from docker.io/nacos/nacos-server
5ad559c5ae16: Pull complete 
da32a341d035: Pull complete 
019d4d5f3169: Pull complete 
1ce7fbd2c815: Pull complete 
1decf73a8a1e: Pull complete 
b326f098f5e6: Pull complete 
2d5f4eb12791: Pull complete 
d3a258cafbc2: Pull complete 
Digest: sha256:ed289ed534932f4990233eb3184d435e58b583d6cc38473b6c9444ba9a3dbc88
Status: Downloaded newer image for docker.io/nacos/nacos-server:latest

# 查看镜像文件
[root@bogon ~]# docker images
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
mytomcat                          v1                  e71e6a54722e        46 hours ago        561 MB
docker.io/tomcat                  latest              6fa48e047721        12 days ago         507 MB
quay.io/prometheus/alertmanager   latest              0881eb8f169f        2 weeks ago         52.1 MB
docker.io/grafana/grafana         latest              7a40c3c56100        2 weeks ago         228 MB
ouruser/sinatra                   v2                  bac43673a2c9        2 weeks ago         453 MB
docker.io/nacos/nacos-server      latest              44ce3286a406        4 weeks ago         718 MB
docker.io/prom/prometheus         latest              7317640d555e        6 weeks ago         130 MB
docker.io/centos                  latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu                  12.04               5b117edd0b76        2 years ago         104 MB

# 运行Nacos
[root@bogon ~]# docker run --env MODE=standalone --name nacos -d -p 8848:8848 nacos/nacos-server
d91d45372033c46e7b6c3ba501ca10083fc0eacc9b1aec431a6a07e5e9af4633
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS              PORTS                    NAMES
d91d45372033        nacos/nacos-server                "bin/docker-startu..."   34 seconds ago      Up 21 seconds       0.0.0.0:8848->8848/tcp   nacos
42fbc0df0f14        quay.io/prometheus/alertmanager   "/bin/alertmanager..."   20 hours ago        Up 20 hours         0.0.0.0:9093->9093/tcp   alertmanager
e31e47800596        grafana/grafana                   "/run.sh"                21 hours ago        Up 21 hours         0.0.0.0:3000->3000/tcp   grafana
e8a045ed0340        prom/prometheus                   "/bin/prometheus -..."   28 hours ago        Up 28 hours         0.0.0.0:9090->9090/tcp   prometheus
e9141e53f3b3        tomcat:latest                     "catalina.sh run"        2 days ago          Up 46 hours         0.0.0.0:8080->8080/tcp   mytomcat

# 物理机浏览器访问： http://192.168.229.128:8848/nacos/ 

# 虚拟机执行服务注册发现和配置管理命令，控制台和面板都能获取相应的数据。
# 服务注册
curl -X POST 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080'
# 服务发现
curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instance/list?serviceName=nacos.naming.serviceName'
# 发布配置
curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=HelloWorld"
# 获取配置
curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"

```
###  常见的配置属性
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

### 参考
* `https://nacos.io/zh-cn/docs/deployment.html`