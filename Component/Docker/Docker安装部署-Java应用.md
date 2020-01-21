## Docker 安装部署Java应用

> 安装基于本地的虚拟机
>
> 本机虚拟机 VM-1 192.168.229.128 （root/jxj-jiaxiaojiao）
<br> 本地虚拟机 VM-2 192.168.229.131 （root/jxj-jiaxiaojiao）
<br> 本地虚拟机 VM-3 192.168.229.132 （root/jxj-jiaxiaojiao）
<br> 本地虚拟机 VM-4 192.168.229.129 （root/jxj-jiaxiaojiao）

### 目录
* [安装Tomcat](#安装Tomcat)
* [安装JDK](#安装JDK)
* [部署web应用](#部署web应用)
* [参考](#参考)

### 安装Tomcat
安装位置： 本机虚拟机 VM-1 192.168.229.128 

```text
# Docker命令安装Tomcat
docker pull tomcat
# 提取镜像，生成容器，并命名容器为：mytomcat
docker run -p 8080:8080 --name mytomcat tomcat:latest
```

以下是虚拟机执行命令：
```text
# 使用用户jxj，所以命令前添加了sudo
[jxj@bogon ~]$ sudo docker run -p 8080:8080 --name mytomcat tomcat:latest
Unable to find image 'tomcat:latest' locally
Trying to pull repository docker.io/library/tomcat ... 
latest: Pulling from docker.io/library/tomcat
844c33c7e6ea: Pull complete 
ada5d61ae65d: Pull complete 
f8427fdf4292: Pull complete 
f025bafc4ab8: Pull complete 
67b8714e1225: Pull complete 
64b12da521a3: Pull complete 
2e38df533772: Pull complete 
4144d55bbb47: Pull complete 
fc059d90e2b2: Pull complete 
9d8f80ed8620: Pull complete 
Digest: sha256:68355b27adee5fc76c23e3d3cb994bd2733f05aa8e2c070a61346e16eed308ac
Status: Downloaded newer image for docker.io/tomcat:latest
24-Dec-2019 06:48:10.220 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version name:   Apache Tomcat/8.5.50
24-Dec-2019 06:48:10.325 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server built:          Dec 7 2019 19:19:46 UTC
24-Dec-2019 06:48:10.325 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version number: 8.5.50.0
24-Dec-2019 06:48:10.325 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Name:               Linux
24-Dec-2019 06:48:10.325 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Version:            3.10.0-1062.el7.x86_64
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Architecture:          amd64
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Java Home:             /usr/local/openjdk-8/jre
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Version:           1.8.0_232-b09
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Vendor:            Oracle Corporation
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_BASE:         /usr/local/tomcat
24-Dec-2019 06:48:10.326 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_HOME:         /usr/local/tomcat
24-Dec-2019 06:48:10.327 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.config.file=/usr/local/tomcat/conf/logging.properties
24-Dec-2019 06:48:10.350 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
24-Dec-2019 06:48:10.351 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djdk.tls.ephemeralDHKeySize=2048
24-Dec-2019 06:48:10.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.protocol.handler.pkgs=org.apache.catalina.webresources
24-Dec-2019 06:48:10.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dorg.apache.catalina.security.SecurityListener.UMASK=0027
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dignore.endorsed.dirs=
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.base=/usr/local/tomcat
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.home=/usr/local/tomcat
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.io.tmpdir=/usr/local/tomcat/temp
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent Loaded APR based Apache Tomcat Native library [1.2.23] using APR version [1.5.2].
24-Dec-2019 06:48:10.364 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR capabilities: IPv6 [true], sendfile [true], accept filters [false], random [true].
24-Dec-2019 06:48:10.365 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR/OpenSSL configuration: useAprConnector [false], useOpenSSL [true]
24-Dec-2019 06:48:10.432 INFO [main] org.apache.catalina.core.AprLifecycleListener.initializeSSL OpenSSL successfully initialized [OpenSSL 1.1.0l  10 Sep 2019]
24-Dec-2019 06:48:11.019 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["http-nio-8080"]
24-Dec-2019 06:48:11.098 INFO [main] org.apache.tomcat.util.net.NioSelectorPool.getSharedSelector Using a shared selector for servlet write/read
24-Dec-2019 06:48:11.151 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["ajp-nio-8009"]
24-Dec-2019 06:48:11.179 INFO [main] org.apache.tomcat.util.net.NioSelectorPool.getSharedSelector Using a shared selector for servlet write/read
24-Dec-2019 06:48:11.183 INFO [main] org.apache.catalina.startup.Catalina.load Initialization processed in 2737 ms
24-Dec-2019 06:48:11.292 INFO [main] org.apache.catalina.core.StandardService.startInternal Starting service [Catalina]
24-Dec-2019 06:48:11.292 INFO [main] org.apache.catalina.core.StandardEngine.startInternal Starting Servlet Engine: Apache Tomcat/8.5.50
24-Dec-2019 06:48:11.444 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory [/usr/local/tomcat/webapps/ROOT]
24-Dec-2019 06:48:12.196 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory [/usr/local/tomcat/webapps/ROOT] has finished in [750] ms
24-Dec-2019 06:48:12.196 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory [/usr/local/tomcat/webapps/docs]
24-Dec-2019 06:48:12.235 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory [/usr/local/tomcat/webapps/docs] has finished in [39] ms
24-Dec-2019 06:48:12.244 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory [/usr/local/tomcat/webapps/examples]
24-Dec-2019 06:48:12.759 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory [/usr/local/tomcat/webapps/examples] has finished in [515] ms
24-Dec-2019 06:48:12.759 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory [/usr/local/tomcat/webapps/host-manager]
24-Dec-2019 06:48:12.822 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory [/usr/local/tomcat/webapps/host-manager] has finished in [63] ms
24-Dec-2019 06:48:12.822 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory [/usr/local/tomcat/webapps/manager]
24-Dec-2019 06:48:12.907 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory [/usr/local/tomcat/webapps/manager] has finished in [85] ms
24-Dec-2019 06:48:12.915 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["http-nio-8080"]
24-Dec-2019 06:48:13.042 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["ajp-nio-8009"]
24-Dec-2019 06:48:13.159 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in 1976 ms
```

物理机浏览器访问 `http://192.168.229.128:8080/`， 没有问题，显示Tomcat主页。

### 安装JDK
安装位置： 本机虚拟机 VM-1 192.168.229.128 

这个虚拟机，之前已经安装过JDK了。
```text
[jxj@bogon ~]$ java -version
java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)
[jxj@bogon ~]$ 
```

### 部署web应用
Web应用是DEMO项目， [Prometheus](../Prometheus/Prometheus-install2.md#Demo项目)也使用这个DEMO项目。
* 使用IDEA，把Spring Boot 项目[打成war包](../../Tools-Software/IDE/JetBrains/IDEA-war-SpringBoot.md)。
* 把war包上传到mytomcat容器。
    ```text
    # 切换到root账号
    [jxj@bogon local]$ sudo -i
    # 上传war包
    [root@bogon local]# rz
    [root@bogon local]# ls
    apache-maven-3.6.2  bin   demo-0.0.1-SNAPSHOT.war  games    influxdb_2.0.0  lib64    rocketmq  share
    apollo              data  etc                      include  lib             libexec  sbin      src
    # 修改war包名称（个人习惯）
    [root@bogon local]# mv demo-0.0.1-SNAPSHOT.war demo.war
    [root@bogon local]# ls
    apache-maven-3.6.2  apollo  bin  data  demo.war  etc  games  include  influxdb_2.0.0  lib  lib64  libexec  rocketmq  sbin  share  src
    # 查看Docker启动的容器
    [root@bogon local]# docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                            NAMES
    e9141e53f3b3        tomcat:latest       "catalina.sh run"        2 hours ago         Up 2 hours          0.0.0.0:8080->8080/tcp           mytomcat
    78ec3d7edc23        prom/prometheus     "/bin/prometheus -..."   18 hours ago        Up 18 hours         192.168.229.128:9090->9090/tcp   prometheus
    # 把war包传入Tomcat容器(NAMES:mytomcat)
    [root@bogon local]# docker cp demo.war e9141e53f3b3:/usr/local/tomcat/webapps
    # 重启Tomcat
    [root@bogon local]# docker restart mytomcat
    ```
* 测试部署的web应用，物理机浏览器访问
    1. `http://192.168.229.128:8080/`  Tomcat首页
    2. `http://192.168.229.128:8080/demo/user/list`  Web应用的用户列表功能
    3. `http://192.168.229.128:8080/demo/actuator/prometheus`  已[集成的Prometheus](../Prometheus/Prometheus-install2.md)测试。 
* 测试通过后，将此容器建立镜像
    ```text
    # docker  commit -m  “提交说明文字”  -a  “作者”   要提交的容器名  提交后的镜像名：提交后的镜像tag名
    docker commit -a 'jiaxiaojiao' -m 'this is the first Demo version' e9141e53f3b3 mytomcat:v1
    ```
    在虚拟机VM-1，把新容器建立镜像
    ```text
    [root@bogon local]# docker commit -a 'jiaxiaojiao' -m 'this is the first Demo version' e9141e53f3b3 mytomcat:v1
    sha256:e71e6a54722eba9d027950eee26731e1ac89288eb671129d391845f3ec051244
    [root@bogon local]# docker images
    REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
    mytomcat                    v1                  e71e6a54722e        13 seconds ago      561 MB
    docker.io/tomcat            latest              6fa48e047721        10 days ago         507 MB
    ouruser/sinatra             v2                  bac43673a2c9        13 days ago         453 MB
    docker.io/prom/prometheus   latest              7317640d555e        6 weeks ago         130 MB
    docker.io/centos            latest              0f3e07c0138f        2 months ago        220 MB
    docker.io/ubuntu            12.04               5b117edd0b76        2 years ago         104 MB
    [root@bogon local]# 
    ```
* 为容器打标签。 
* 推入私有库
* 客户端就可以从私有库拉取镜像，转为容器，运行了。

后面三步没有操作，暂时没有私有库。

### 参考
* https://www.cnblogs.com/jizhong/p/11058840.html