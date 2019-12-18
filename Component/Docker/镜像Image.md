## Image镜像

> 在 Docker 的术语里，一个只读层被称为镜像，一个镜像是永久不会变的。
>
> 参考： http://www.dockerinfo.net/image%e9%95%9c%e5%83%8f
>
> 本页中的命令是在本机虚拟机VM-1中执行的。（之前已经安装完成）

### 目录
* [1. 介绍](#1.-介绍)
    * [1.1 父镜像](#1.1-父镜像)
    * [1.2 基础镜像](#1.2-基础镜像)
    * [1.3 镜像ID](#1.3-镜像ID)
* [2. 获取镜像](#2.-获取镜像)
* [3. 列出本地镜像](#3.-列出本地镜像)
* [4. 创建镜像](#4.-创建镜像)
    * [4.1 修改已有镜像](#4.1-修改已有镜像)
    * [4.2 利用 Dockerfile 来创建镜像](#4.2-利用-Dockerfile-来创建镜像)
    * [4.3 从本地文件系统导入](#4.3-从本地文件系统导入)
    * [4.4 上传镜像](#4.4-上传镜像)
* [5 存出和载入镜像](#5-存出和载入镜像)
    * [5.1 存出镜像](#5.1-存出镜像)
    * [5.2 载入镜像](#5.2-载入镜像)
* [6. 移除本地镜像](#6.-移除本地镜像)
* [7. 镜像的实现原理](#7.-镜像的实现原理)
* [8. 镜像管理](#8.-镜像管理)

### 1. 介绍
在 Docker 的术语里，一个只读层被称为镜像，一个镜像是永久不会变的。

由于 Docker 使用一个统一文件系统，Docker 进程认为整个文件系统是以读写方式挂载的。 但是所有的变更都发生顶层的可写层，而下层的原始的只读镜像文件并未变化。由于镜像不 可写，所以镜像是无状态的。

#### 1.1 父镜像
每一个镜像都可能依赖于由一个或多个下层的组成的另一个镜像。我们有时说，下层那个 镜像是上层镜像的父镜像。

#### 1.2 基础镜像
一个没有任何父镜像的镜像，谓之基础镜像。

#### 1.3 镜像ID
所有镜像都是通过一个 64 位十六进制字符串 （内部是一个 256 bit 的值）来标识的。 为简化使用，前 12 个字符可以组成一个短ID，可以在命令行中使用。短ID还是有一定的 碰撞机率，所以服务器总是返回长ID。

### 2. 获取镜像
可以使用 `docker pull` 命令来从仓库获取所需要的镜像。

```text
# 例：从 Docker Hub 仓库下载一个 Ubuntu 12.04 操作系统的镜像
[root@bogon ~]# sudo docker pull ubuntu:12.04
Trying to pull repository docker.io/library/ubuntu ... 
12.04: Pulling from docker.io/library/ubuntu
d8868e50ac4c: Pull complete 
83251ac64627: Pull complete 
589bba2f1b36: Pull complete 
d62ecaceda39: Pull complete 
6d93b41cfc6b: Pull complete 
Digest: sha256:18305429afa14ea462f810146ba44d4363ae76e4c8dfc38288cf73aa07485005
Status: Downloaded newer image for docker.io/ubuntu:12.04
[root@bogon ~]#

# 该命令实际上相当于 $ sudo docker pull registry.hub.docker.com/ubuntu:12.04 命令，即从注册服务器registry.hub.docker.com 中的 ubuntu 仓库来下载标记为 12.04 的镜像。 
```

有时候官方仓库注册服务器下载较慢，可以从其他仓库下载。 从其它仓库下载时需要指定完整的仓库注册服务器地址。

完成后，即可随时使用该镜像了，例如创建一个容器，让其中运行 bash 应用。
```text
[root@bogon ~]# sudo docker run -t -i ubuntu:12.04 /bin/bash
root@d3c6a171906c:/# exit
exit
[root@bogon ~]# 
```

### 3. 列出本地镜像
使用 `docker images` 显示本地已有的镜像。
```text
[root@bogon ~]# sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/centos    latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu    12.04               5b117edd0b76        2 years ago         104 MB
[root@bogon ~]# 
```
在列出的信息中，可以看到几个字段信息：
* REPOSITORY 来自哪个仓库
* TAG 镜像标记
* IMAGE ID 镜像唯一ID
* CREATED 创建时间
* SIZE 镜像大小

如果不指定具体的标记，则默认使用 latest 标记信息。

### 4. 创建镜像

创建镜像有很多方法，用户可以从 Docker Hub 获取已有镜像并更新，也可以利用本地文件系统创建一个。

#### 4.1 修改已有镜像

* 先使用下载的镜像启动容器。
```text
# 之前不存在training/sinatra镜像，启动不了，先下载了镜像以后再启动。
[root@bogon ~]# sudo docker run -t -i training/sinatra /bin/bash
Unable to find image 'training/sinatra:latest' locally
Trying to pull repository docker.io/training/sinatra ... 
latest: Pulling from docker.io/training/sinatra
a3ed95caeb02: Pull complete 
6e71c809542e: Pull complete 
d196a7609355: Pull complete 
08f6dff5acea: Pull complete 
ce65532003d0: Pull complete 
54bcaa4d1a10: Pull complete 
8572ad96f6e1: Pull complete 
Digest: sha256:03fc0cd265cbc28723e4efd446f9f2f37b4790cf9cc12f1b9203c79fb86b6772
Status: Downloaded newer image for docker.io/training/sinatra:latest
root@c1074804f1a4:/# 
```

* 修改（在容器中添加应用）
```text
# 在容器中添加应用 json
root@c1074804f1a4:/# gem install json
Fetching: json-2.2.0.gem (100%)
Building native extensions.  This could take a while...
Successfully installed json-2.2.0
1 gem installed
Installing ri documentation for json-2.2.0...
Installing RDoc documentation for json-2.2.0...

# 使用 `exit`命令退出
root@c1074804f1a4:/# exit
exit
```

* 使用 `docker commit` 命令提交更新过的副本
```text
[root@bogon ~]# sudo docker commit -m "Added json gem" -a "Docker Newbee" c1074804f1a4 ouruser/sinatra:v2
sha256:bac43673a2c91a2b947e41c90b22ee4cff0d8a67da413f2b9f1148ec71cd06d2
```

其中，-m 来指定提交的说明信息，跟我们使用的版本控制工具一样；-a 可以指定更新的用户信息；之后是用来创建镜像的容器的 ID；最后指定目标镜像的仓库名和 tag 信息。创建成功后会返回这个镜像的 ID 信息。

* 使用 `docker images` 来查看新创建的镜像
```text
[root@bogon ~]# sudo docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
ouruser/sinatra              v2                  bac43673a2c9        41 seconds ago      453 MB
docker.io/centos             latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu             12.04               5b117edd0b76        2 years ago         104 MB
docker.io/training/sinatra   latest              49d952a36c58        5 years ago         447 MB
```

* 之后，可以使用新的镜像来启动容器
```text
[root@bogon ~]# sudo docker run -t -i ouruser/sinatra:v2 /bin/bash
root@3dba611c72b1:/# exit
exit
[root@bogon ~]# 
```

#### 4.2 利用 Dockerfile 来创建镜像

使用 docker commit 来扩展一个镜像比较简单，但是不方便在一个团队中分享。我们可以使用 docker build来创建一个新的镜像。为此，首先需要创建一个 Dockerfile，包含一些如何创建镜像的指令。

#### 4.3 从本地文件系统导入

要从本地文件系统导入一个镜像，可以使用 openvz（容器虚拟化的先锋技术）的模板来创建： openvz 的模板下载地址为 templates 。

#### 4.4 上传镜像

用户可以通过 docker push 命令，把自己创建的镜像上传到仓库中来共享。例如，用户在 Docker Hub 上完成注册后，可以推送自己的镜像到仓库中。

### 5 存出和载入镜像

#### 5.1 存出镜像
如果要导出镜像到本地文件，可以使用 `docker save` 命令。

#### 5.2 载入镜像
可以使用 `docker load` 从导出的本地文件中再导入到本地镜像库

```text
[root@bogon ~]# sudo docker images
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
ouruser/sinatra              v2                  bac43673a2c9        41 minutes ago      453 MB
docker.io/centos             latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu             12.04               5b117edd0b76        2 years ago         104 MB
docker.io/training/sinatra   latest              49d952a36c58        5 years ago         447 MB

# 存出镜像
[root@bogon ~]# sudo docker save -o ubuntu_12.04.tar docker.io/ubuntu:12.04
[root@bogon ~]# ls
anaconda-ks.cfg  logs  mysql57-community-release-el7-8.noarch.rpm  ubuntu_12.04.tar

# 载入镜像
[root@bogon ~]# sudo docker load --input ubuntu_12.04.tar 
Loaded image: docker.io/ubuntu:12.04
[root@bogon ~]# 

```

### 6. 移除本地镜像
如果要移除本地的镜像，可以使用 `docker rmi` 命令。注意 `docker rm` 命令是移除容器。

```text
[root@bogon ~]# sudo docker rm c1074804f1a4
Error response from daemon: No such container: c1074804f1a4
[root@bogon ~]# docker rmi training/sinatra
Untagged: training/sinatra:latest
Untagged: docker.io/training/sinatra@sha256:03fc0cd265cbc28723e4efd446f9f2f37b4790cf9cc12f1b9203c79fb86b6772
[root@bogon ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ouruser/sinatra     v2                  bac43673a2c9        About an hour ago   453 MB
docker.io/centos    latest              0f3e07c0138f        2 months ago        220 MB
docker.io/ubuntu    12.04               5b117edd0b76        2 years ago         104 MB
[root@bogon ~]# 
```

*注意：在删除镜像之前要先用 docker rm 删掉依赖于这个镜像的所有容器。

### 7. 镜像的实现原理
Docker 镜像是怎么实现增量的修改和维护的？ 每个镜像都由很多层次构成，Docker 使用 Union FS 将这些不同的层结合到一个镜像中去。

通常 Union FS 有两个用途, 一方面可以实现不借助 LVM、RAID 将多个 disk 挂到同一个目录下,另一个更常用的就是将一个只读的分支和一个可写的分支联合在一起，Live CD 正是基于此方法可以允许在镜像不变的基础上允许用户在其上进行一些写操作。 Docker 在 AUFS 上构建的容器也是利用了类似的原理。

### 8. 镜像管理

Docker Registry服务： 类似仓库管理员，负责对Docker镜像进行管理。Docker Registry服务对镜像的管理是非常严格的。

最常使用的Registry公开服务，是官方的Docker Hub，这也是默认的 Registry，并拥有大量的高质量的官方镜像。





