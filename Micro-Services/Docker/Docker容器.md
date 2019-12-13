## Docker容器

> 参考： http://www.dockerinfo.net/docker%e5%ae%b9%e5%99%a8-2
>
> 本页中的命令是在本机虚拟机VM-1中执行的命令，之前已经安装完成并操作了镜像Image

### 目录
* [1. 启动容器](#1.-启动容器)
    * [1.1 新建并启动](#1.1-新建并启动)
    * [1.2 启动已终止容器](#1.2-启动已终止容器)
* [2. 守护态运行](#2.-守护态运行)
* [3. 终止容器](#3.-终止容器)
* [4. 进入容器](#4.-进入容器)
    * [4.1 attach 命令](#4.1-attach-命令)
    * [4.2 nsenter 命令](#4.2-nsenter-命令)
        * [4.2.1 安装](#4.2.1-安装)
        * [4.2.2 使用](#4.2.2-使用)
* [5. 导出和导入容器](#5.-导出和导入容器)
    * [5.1 导出容器](#5.1-导出容器)
    * [5.2 导入容器快照](#5.2-导入容器快照)
* [6. 删除容器](#6.-删除容器)

### 1. 启动容器
启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

因为 Docker 的容器实在太轻量级了，很多时候用户都是随时删除和新创建容器。

#### 1.1 新建并启动
所需要的命令主要为 docker run。

```text
# 例：下面的命令输出一个 “Hello World”，之后终止容器。
# 这跟在本地直接执行 /bin/echo 'hello world' 几乎感觉不出任何区别。
[root@bogon ~]# docker run ubuntu:12.04 /bin/echo 'Hello World'
Hello World
[root@bogon ~]# 

# 启动一个 bash 终端，允许用户进行交互
[root@bogon ~]# docker run -t -i ubuntu:12.04 /bin/bash
root@fea18ee350f3:/# exit
exit
[root@bogon ~]#
```
其中，-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上， -i 则让容器的标准输入保持打开。

当利用 docker run 来创建容器时，Docker 在后台运行的标准操作包括：
* 检查本地是否存在指定的镜像，不存在就从公有仓库下载
* 利用镜像创建并启动一个容器
* 分配一个文件系统，并在只读的镜像层外面挂载一层可读写层
* 从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
* 从地址池配置一个 ip 地址给容器
* 执行用户指定的应用程序
* 执行完毕后容器被终止

#### 1.2 启动已终止容器
可以利用 docker start 命令，直接将一个已经终止的容器启动运行。

容器的核心为所执行的应用程序，所需要的资源都是应用程序运行所必需的。除此之外，并没有其它的资源。可以在伪终端中利用 ps 或 top 来查看进程信息。

```text
[root@bogon ~]# docker run -t -i ubuntu:12.04 /bin/bash
root@73286ef9ac71:/# ps
   PID TTY          TIME CMD
     1 ?        00:00:00 bash
    10 ?        00:00:00 ps
root@73286ef9ac71:/# 
```
可见，容器中仅运行了指定的 bash 应用。这种特点使得 Docker 对资源的利用率极高，是货真价实的轻量级虚拟化。

### 2. 守护态运行
更多的时候，需要让 Docker 容器在后台以守护态（Daemonized）形式运行。此时，可以通过添加 `-d` 参数来实现。

```text
# 例： 下面的命令会在后台运行容器。
[root@bogon ~]# sudo docker run -d ubuntu:12.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
444f3fbd6ef78f3ad669585936b5e370f8dfef7f00b0f0498627172b2f28a25a

# 容器启动后会返回一个唯一的 id，也可以通过 docker ps 命令来查看容器信息。
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
444f3fbd6ef7        ubuntu:12.04        "/bin/sh -c 'while..."   42 seconds ago      Up 42 seconds                           goofy_gates
4345110b2062        ubuntu:12.04        "/bin/bash"              25 minutes ago      Up 25 minutes                           wonderful_bardeen
4191e3970c3f        ubuntu:12.04        "/bin/bash"              25 minutes ago      Up 25 minutes                           pensive_yalow
[root@bogon ~]# 

# 要获取容器的输出信息，可以通过 docker logs 命令
[root@bogon ~]# docker logs goofy_gates

hello world
...
hello world
[root@bogon ~]# 

```
### 3. 终止容器
可以使用 `docker stop` 来终止一个运行中的容器。

此外，当Docker容器中指定的应用终结时，容器也自动终止。 例如对于上一章节中只启动了一个终端的容器，用户通过 `exit` 命令或 `Ctrl+d` 来退出终端时，所创建的容器立刻终止。

终止状态的容器可以用 `docker ps -a` 命令看到。
```text
[root@bogon ~]# docker ps -a
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS                       PORTS               NAMES
444f3fbd6ef7        ubuntu:12.04         "/bin/sh -c 'while..."   5 minutes ago       Up 5 minutes                                     goofy_gates
...
ddd700a6bb09        centos               "/bin/bash"              3 hours ago         Exited (0) 3 hours ago                           dazzling_pasteur
[root@bogon ~]# 
```
处于终止状态的容器，可以通过 `docker start` 命令来重新启动。

此外，`docker restart` 命令会将一个运行态的容器终止，然后再重新启动它。

### 4. 进入容器
在使用 `-d` 参数时，容器启动后会进入后台。 某些时候需要进入容器进行操作，有很多种方法，包括使用`docker attach` 命令或 `nsenter` 工具等。

#### 4.1 attach 命令
docker attach 是Docker自带的命令。

```text
[root@bogon ~]# docker attach goofy_gates
hello world
hello world
...
```

但是使用 attach 命令有时候并不方便。当多个窗口同时 attach 到同一个容器的时候，所有窗口都会同步显示。当某个窗口因命令阻塞时,其他窗口也无法执行操作了。

#### 4.2 nsenter 命令

##### 4.2.1 安装
nsenter 工具在 util-linux 包2.23版本后包含。 如果系统中 util-linux 包没有该命令

##### 4.2.2 使用
nsenter 可以访问另一个进程的名字空间。nsenter 要正常工作需要有 root 权限。 很不幸，Ubuntu 14.04 仍然使用的是 util-linux 2.20。

### 5. 导出和导入容器

#### 5.1 导出容器
如果要导出本地某个容器，可以使用 docker export 命令。

#### 5.2 导入容器快照
可以使用 docker import 从容器快照文件中再导入为镜像

*注：用户既可以使用 docker load 来导入镜像存储文件到本地镜像库，也可以使用 docker import 来导入一个容器快照到本地镜像库。这两者的区别在于容器快照文件将丢弃所有的历史记录和元数据信息（即仅保存容器当时的快照状态），而镜像存储文件将保存完整记录，体积也要大。此外，从容器快照文件导入时可以重新指定标签等元数据信息。

### 6. 删除容器
可以使用 docker rm 来删除一个处于终止状态的容器。

如果要删除一个运行中的容器，可以添加 -f 参数。Docker 会发送 SIGKILL 信号给容器。


