## Docker 安装软件

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

* 修改Prometheus配置文件： 添加监控Demo项目
```text
# 配置文件我放的目录： /etc/prometheus/prometheus.yml
docker run -d -p 9090:9090 --name=prometheus -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
# 带参数启动有异常，找一下什么原因？？？ TODO 
[root@bogon etc]# sudo docker run -p 9090:9090 -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
container_linux.go:235: starting container process caused "container init exited prematurely"
/usr/bin/docker-current: Error response from daemon: oci runtime error: container_linux.go:235: starting container process caused "container init exited prematurely".
```