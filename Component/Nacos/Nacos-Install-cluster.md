## Nacos 安装部署 - 集群模式

> Nacos支持三种部署模式
> * 单机模式 - 用于测试和单机试用。
> * 集群模式 - 用于生产环境，确保高可用。
> * 多集群模式 - 用于多数据中心场景。

### 目录
* [集群部署架构图](#集群部署架构图)
* [环境要求](#环境要求)
* [下载源码或安装包](#下载源码或安装包)
* [配置集群配置文件](#配置集群配置文件)
* [配置 MySQL 数据库](#配置-MySQL-数据库)
* [启动服务器](#启动服务器)
* [服务注册&发现和配置管理](#服务注册&发现和配置管理)
* [关闭服务器](#关闭服务器)
* [参考](#参考)

### 集群部署架构图
推荐用户把所有服务列表放到一个vip下面，然后挂到一个域名下面。
* `http://ip1:port/openAPI` 直连ip模式，机器挂则需要修改ip才可以使用。
* `http://VIP:port/openAPI` 挂载VIP模式，直连vip即可，下面挂server真实ip，可读性不好。
* `http://nacos.com:port/openAPI` 域名 + VIP模式，可读性好，而且换ip方便，推荐模式

![集群部署架构图](../images/nacos-cluster-mode.jpeg)

### 环境要求
* 64 bit OS Linux/Unix/Mac，推荐使用Linux系统。
* 64 bit JDK 1.8+
* Maven 3.2.x+
* 3个或3个以上Nacos节点才能构成集群

本次Demo安装在本地虚拟机VM-4上：
* ~~操作系统CentOS 7 64位。~~
* ~~JDK 1.8.0.231~~
* ~~Maven 3.6.3~~
```text
[root@bogon ~]# java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) m64-Bit Server VM (build 25.231-b11, mixed mode)
[root@bogon ~]# mvn -v
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /usr/local/apache-maven-3.6.3
Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: /usr/java/jdk1.8.0_231-amd64/jre
Default locale: zh_CN, platform encoding: UTF-8
OS name: "linux", version: "3.10.0-1062.el7.x86_64", arch: "amd64", family: "unix"
```

### 下载源码或安装包
两种方式：
1. 从 Github 上下载源码方式
    ```text
    unzip nacos-source.zip
    cd nacos/
    mvn -Prelease-nacos clean install -U  
    cd nacos/distribution/target/nacos-server-0.8.0/nacos/bin
    ```
2. 下载编译后压缩包方式
    ```text
    下载地址： 
    https://github.com/alibaba/nacos/releases/download/0.8.0/nacos-server-0.8.0.zip
    https://github.com/alibaba/nacos/releases/download/0.8.0/nacos-server-0.8.0.tar.gz
    解压缩：
    $ unzip nacos-server-0.8.0.zip 或者 tar -xvf nacos-server-0.8.0.tar.gz
    $ cd nacos/bin
    ```

### 配置集群配置文件
在nacos的解压目录nacos/的conf目录下，有配置文件cluster.conf，请每行配置成ip:port。（请配置3个或3个以上节点）
```text
# ip:port
200.8.9.16:8848
200.8.9.17:8848
200.8.9.18:8848
```
### 配置 MySQL 数据库
生产使用建议至少主备模式，或者采用高可用数据库。
1. 初始化 MySQL 数据库。 `https://github.com/alibaba/nacos/blob/master/distribution/conf/nacos-mysql.sql`
2. application.properties 配置。 `https://github.com/alibaba/nacos/blob/master/distribution/conf/application.properties`

### 启动服务器
Linux/Unix/Mac

启动命令(在没有参数模式，是集群模式): `sh startup.sh`

### 服务注册&发现和配置管理
* 服务注册

    `curl -X PUT 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080'`

* 服务发现

    `curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instances?serviceName=nacos.naming.serviceName'`

* 发布配置
    
    `curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=helloWorld"`

* 获取配置

    `curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"`

### 关闭服务器
Linux/Unix/Mac `sh shutdown.sh`

### 参考
* `https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html`
* `https://yq.aliyun.com/zt/492606`