## 在Docker中运行hello world


### 在Docker中运行Hello World 命令
* 显示本地已有镜像 `docker images`

sudo是linux系统管理指令，是允许系统管理员让普通用户执行一些或者全部的root命令的一个工具，如halt，reboot，su等等。

```text
[root@bogon ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ouruser/sinatra     v2                  bac43673a2c9        2 days ago          453 MB
docker.io/centos    latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu    12.04               5b117edd0b76        2 years ago         104 MB
```

* 运行容器，执行/bin/echo命令 输出Hello World
```text
[root@bogon ~]# docker run ubuntu:12.04 /bin/echo 'Hello World!'
Hello World!
```

* 后台运行Hello World并查看。

```text
# 创建一个容器，让它以守护进程的模式运行
[root@bogon ~]# docker run -d ubuntu:12.04 /bin/sh -c "while true; do echo hello world; sleep 2; done" 
334c430e2a57e03dc7ed88979a5a1b6d9a31b9b2de84ae1b3968480aaf54f233

# 返回容器ID，根据容器ID查看hello world进程
# 查询Docker进程的所有容器 docker ps
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
334c430e2a57        ubuntu:12.04        "/bin/sh -c 'while..."   3 minutes ago       Up 3 minutes                            romantic_bohr

# CONTAINER ID与容器ID前12位一样
# 查看输出的内容
[root@bogon ~]# docker logs romantic_bohr
hello world
...

# 停止这个后台进程容器 docker stop
[root@bogon ~]# docker stop romantic_bohr
romantic_bohr
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@bogon ~]# 

# 查询Docker进程的所有容器，已经停止了
```