## Docker安装 CentOS


### 目录
* [支持Docker的CentOS版本](#支持Docker的CentOS版本)
* [1. CentOS7 安装Docker](#1.-CentOS7-安装Docker)
* [2. 开始运行 Docker daemon](#2.-开始运行-Docker-daemon)
* [自定义进程选项](#自定义进程选项)
* [Dockerfiles](#Dockerfiles)
* [具体命令和安装明细](#具体命令和安装明细)
* [参考](#参考)

### 支持Docker的CentOS版本

* CentOS 7 (64-bit)
* CentOS 6.5 (64-bit) or later

由于 Docker 的局限性，Docker 只能运行在64位的系统中，需要内核版本是 2.6.32-431 或者更高版本。

### 1. CentOS7 安装Docker

Docker 软件包已经包含在默认的 CentOS-Extras 软件源里，安装命令如下：

`# sudo yum install docker`

（前提条件： 安装sudo命令`# yum install sudo`）

#### FirewallD
CentOS-7 中介绍了 firewalld，firewall的底层是使用iptables进行数据过滤，建立在iptables之上，这可能会与 Docker 产生冲突。

当 firewalld 启动或者重启的时候，将会从 iptables 中移除 DOCKER 的规则，从而影响了 Docker 的正常工作。

当你使用的是 Systemd 的时候， firewalld 会在 Docker 之前启动，但是如果你在 Docker 启动之后再启动 或者重启 firewalld ，你就需要重启 Docker 进程了。

### 2. 开始运行 Docker daemon

当 Docker 安装完成之后，你需要启动 docker 进程。

`$ sudo service docker start`

如果我们希望 Docker 默认开机启动，如下操作：

`$ sudo chkconfig docker on`

现在，我们来验证 Docker 是否正常工作。第一步，我们需要下载最新的 centos 镜像。

`$ sudo docker pull centos`

下一步，我们运行下边的命令来查看镜像，确认镜像是否存在：

`$ sudo docker images centos`

这将会输出如下的信息：

```text
$ sudo docker images centos
REPOSITORY      TAG             IMAGE ID          CREATED             VIRTUAL SIZE
centos          latest          0b443ba03958      2 hours ago         297.6 MB
```

运行简单的脚本来测试镜像：

`$ sudo docker run -i -t centos /bin/bash`

如果正常运行，你将会获得一个简单的 bash 提示，输入 exit 来退出。


### 自定义进程选项

定制Docker进程

### Dockerfiles

CentOS 项目为开发者提供了大量的的示例镜像，作为开发模板或者学习 Docker 的实例。你可以在这里找到这些示例：

`https://github.com/CentOS/CentOS-Dockerfiles`

#### 具体命令和安装明细

* 安装位置

    本机虚拟机 VM-1 192.168.229.128 （root-jiaxiaojiao）
    本地虚拟机 VM-2 192.168.229.131 （root-jiaxiaojiao）
    本地虚拟机 VM-3 192.168.229.132 （root-jiaxiaojiao）
    

* 安装sudo命令
```text
[root@bogon ~]# yum install sudo
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.zju.edu.cn
 * extras: mirrors.huaweicloud.com
 * updates: mirrors.zju.edu.cn
正在解决依赖关系
--> 正在检查事务
---> 软件包 sudo.x86_64.0.1.8.23-4.el7 将被 升级
---> 软件包 sudo.x86_64.0.1.8.23-4.el7_7.1 将被 更新
--> 解决依赖关系完成

依赖关系解决

======================================================================================================================================
 Package                    架构                         版本                                     源                             大小
======================================================================================================================================
正在更新:
 sudo                       x86_64                       1.8.23-4.el7_7.1                         updates                       841 k

事务概要
======================================================================================================================================
升级  1 软件包

总下载量：841 k
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
sudo-1.8.23-4.el7_7.1.x86_64.rpm                                                                               | 841 kB  00:00:01     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在更新    : sudo-1.8.23-4.el7_7.1.x86_64                                                                                      1/2 
  清理        : sudo-1.8.23-4.el7.x86_64                                                                                          2/2 
  验证中      : sudo-1.8.23-4.el7_7.1.x86_64                                                                                      1/2 
  验证中      : sudo-1.8.23-4.el7.x86_64                                                                                          2/2 

更新完毕:
  sudo.x86_64 0:1.8.23-4.el7_7.1                                                                                                      

完毕！

```

* 安装Docker

```text
[root@bogon ~]# sudo yum install docker
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.zju.edu.cn
 * extras: mirrors.huaweicloud.com
 * updates: mirrors.zju.edu.cn
正在解决依赖关系
--> 正在检查事务
---> 软件包 docker.x86_64.2.1.13.1-103.git7f2769b.el7.centos 将被 安装
--> 正在处理依赖关系 docker-common = 2:1.13.1-103.git7f2769b.el7.centos，它被软件包 2:docker-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 docker-client = 2:1.13.1-103.git7f2769b.el7.centos，它被软件包 2:docker-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 subscription-manager-rhsm-certificates，它被软件包 2:docker-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在检查事务
---> 软件包 docker-client.x86_64.2.1.13.1-103.git7f2769b.el7.centos 将被 安装
---> 软件包 docker-common.x86_64.2.1.13.1-103.git7f2769b.el7.centos 将被 安装
--> 正在处理依赖关系 skopeo-containers >= 1:0.1.26-2，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 oci-umount >= 2:2.3.3-3，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 oci-systemd-hook >= 1:0.1.4-9，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 oci-register-machine >= 1:0-5.13，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 container-storage-setup >= 0.9.0-1，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 container-selinux >= 2:2.51-1，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
--> 正在处理依赖关系 atomic-registries，它被软件包 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64 需要
---> 软件包 subscription-manager-rhsm-certificates.x86_64.0.1.24.13-3.el7.centos 将被 安装
--> 正在检查事务
---> 软件包 atomic-registries.x86_64.1.1.22.1-29.gitb507039.el7 将被 安装
--> 正在处理依赖关系 python-yaml，它被软件包 1:atomic-registries-1.22.1-29.gitb507039.el7.x86_64 需要
--> 正在处理依赖关系 python-setuptools，它被软件包 1:atomic-registries-1.22.1-29.gitb507039.el7.x86_64 需要
--> 正在处理依赖关系 python-pytoml，它被软件包 1:atomic-registries-1.22.1-29.gitb507039.el7.x86_64 需要
---> 软件包 container-selinux.noarch.2.2.107-3.el7 将被 安装
--> 正在处理依赖关系 policycoreutils-python，它被软件包 2:container-selinux-2.107-3.el7.noarch 需要
---> 软件包 container-storage-setup.noarch.0.0.11.0-2.git5eaf76c.el7 将被 安装
---> 软件包 containers-common.x86_64.1.0.1.37-3.el7.centos 将被 安装
---> 软件包 oci-register-machine.x86_64.1.0-6.git2b44233.el7 将被 安装
---> 软件包 oci-systemd-hook.x86_64.1.0.2.0-1.git05e6923.el7_6 将被 安装
--> 正在处理依赖关系 libyajl.so.2()(64bit)，它被软件包 1:oci-systemd-hook-0.2.0-1.git05e6923.el7_6.x86_64 需要
---> 软件包 oci-umount.x86_64.2.2.5-3.el7 将被 安装
--> 正在检查事务
---> 软件包 PyYAML.x86_64.0.3.10-11.el7 将被 安装
--> 正在处理依赖关系 libyaml-0.so.2()(64bit)，它被软件包 PyYAML-3.10-11.el7.x86_64 需要
---> 软件包 policycoreutils-python.x86_64.0.2.5-33.el7 将被 安装
--> 正在处理依赖关系 setools-libs >= 3.3.8-4，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libsemanage-python >= 2.5-14，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 audit-libs-python >= 2.1.3-4，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 python-IPy，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1(VERS_1.4)(64bit)，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1(VERS_1.2)(64bit)，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libcgroup，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libapol.so.4(VERS_4.0)(64bit)，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 checkpolicy，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1()(64bit)，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
--> 正在处理依赖关系 libapol.so.4()(64bit)，它被软件包 policycoreutils-python-2.5-33.el7.x86_64 需要
---> 软件包 python-pytoml.noarch.0.0.1.14-1.git7dea353.el7 将被 安装
---> 软件包 python-setuptools.noarch.0.0.9.8-7.el7 将被 安装
--> 正在处理依赖关系 python-backports-ssl_match_hostname，它被软件包 python-setuptools-0.9.8-7.el7.noarch 需要
---> 软件包 yajl.x86_64.0.2.0.4-4.el7 将被 安装
--> 正在检查事务
---> 软件包 audit-libs-python.x86_64.0.2.8.5-4.el7 将被 安装
---> 软件包 checkpolicy.x86_64.0.2.5-8.el7 将被 安装
---> 软件包 libcgroup.x86_64.0.0.41-21.el7 将被 安装
---> 软件包 libsemanage-python.x86_64.0.2.5-14.el7 将被 安装
---> 软件包 libyaml.x86_64.0.0.1.4-11.el7_0 将被 安装
---> 软件包 python-IPy.noarch.0.0.75-6.el7 将被 安装
---> 软件包 python-backports-ssl_match_hostname.noarch.0.3.5.0.1-1.el7 将被 安装
--> 正在处理依赖关系 python-ipaddress，它被软件包 python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch 需要
--> 正在处理依赖关系 python-backports，它被软件包 python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch 需要
---> 软件包 setools-libs.x86_64.0.3.3.8-4.el7 将被 安装
--> 正在检查事务
---> 软件包 python-backports.x86_64.0.1.0-8.el7 将被 安装
---> 软件包 python-ipaddress.noarch.0.1.0.16-2.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

======================================================================================================================================
 Package                                         架构            版本                                          源                大小
======================================================================================================================================
正在安装:
 docker                                          x86_64          2:1.13.1-103.git7f2769b.el7.centos            extras            18 M
为依赖而安装:
 PyYAML                                          x86_64          3.10-11.el7                                   base             153 k
 atomic-registries                               x86_64          1:1.22.1-29.gitb507039.el7                    extras            35 k
 audit-libs-python                               x86_64          2.8.5-4.el7                                   base              76 k
 checkpolicy                                     x86_64          2.5-8.el7                                     base             295 k
 container-selinux                               noarch          2:2.107-3.el7                                 extras            39 k
 container-storage-setup                         noarch          0.11.0-2.git5eaf76c.el7                       extras            35 k
 containers-common                               x86_64          1:0.1.37-3.el7.centos                         extras            21 k
 docker-client                                   x86_64          2:1.13.1-103.git7f2769b.el7.centos            extras           3.9 M
 docker-common                                   x86_64          2:1.13.1-103.git7f2769b.el7.centos            extras            97 k
 libcgroup                                       x86_64          0.41-21.el7                                   base              66 k
 libsemanage-python                              x86_64          2.5-14.el7                                    base             113 k
 libyaml                                         x86_64          0.1.4-11.el7_0                                base              55 k
 oci-register-machine                            x86_64          1:0-6.git2b44233.el7                          extras           1.1 M
 oci-systemd-hook                                x86_64          1:0.2.0-1.git05e6923.el7_6                    extras            34 k
 oci-umount                                      x86_64          2:2.5-3.el7                                   extras            33 k
 policycoreutils-python                          x86_64          2.5-33.el7                                    base             457 k
 python-IPy                                      noarch          0.75-6.el7                                    base              32 k
 python-backports                                x86_64          1.0-8.el7                                     base             5.8 k
 python-backports-ssl_match_hostname             noarch          3.5.0.1-1.el7                                 base              13 k
 python-ipaddress                                noarch          1.0.16-2.el7                                  base              34 k
 python-pytoml                                   noarch          0.1.14-1.git7dea353.el7                       extras            18 k
 python-setuptools                               noarch          0.9.8-7.el7                                   base             397 k
 setools-libs                                    x86_64          3.3.8-4.el7                                   base             620 k
 subscription-manager-rhsm-certificates          x86_64          1.24.13-3.el7.centos                          updates          228 k
 yajl                                            x86_64          2.0.4-4.el7                                   base              39 k

事务概要
======================================================================================================================================
安装  1 软件包 (+25 依赖软件包)

总计：25 M
总下载量：23 M
安装大小：89 M
Is this ok [y/d/N]: y
Downloading packages:
(1/12): container-selinux-2.107-3.el7.noarch.rpm                                                               |  39 kB  00:00:00     
(2/12): atomic-registries-1.22.1-29.gitb507039.el7.x86_64.rpm                                                  |  35 kB  00:00:00     
(3/12): docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64.rpm                                              |  97 kB  00:00:00     
(4/12): container-storage-setup-0.11.0-2.git5eaf76c.el7.noarch.rpm                                             |  35 kB  00:00:00     
(5/12): containers-common-0.1.37-3.el7.centos.x86_64.rpm                                                       |  21 kB  00:00:00     
(6/12): oci-systemd-hook-0.2.0-1.git05e6923.el7_6.x86_64.rpm                                                   |  34 kB  00:00:00     
(7/12): oci-umount-2.5-3.el7.x86_64.rpm                                                                        |  33 kB  00:00:00     
(8/12): python-pytoml-0.1.14-1.git7dea353.el7.noarch.rpm                                                       |  18 kB  00:00:00     
(9/12): subscription-manager-rhsm-certificates-1.24.13-3.el7.centos.x86_64.rpm                                 | 228 kB  00:00:00     
(10/12): oci-register-machine-0-6.git2b44233.el7.x86_64.rpm                                                    | 1.1 MB  00:00:02     
(11/12): docker-client-1.13.1-103.git7f2769b.el7.centos.x86_64.rpm                                             | 3.9 MB  00:00:06     
(12/12): docker-1.13.1-103.git7f2769b.el7.centos.x86_64.rpm                                                    |  18 MB  00:03:51     
--------------------------------------------------------------------------------------------------------------------------------------
总计                                                                                                  102 kB/s |  23 MB  00:03:51     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : yajl-2.0.4-4.el7.x86_64                                                                                          1/26 
  正在安装    : 2:oci-umount-2.5-3.el7.x86_64                                                                                    2/26 
  正在安装    : 1:oci-systemd-hook-0.2.0-1.git05e6923.el7_6.x86_64                                                               3/26 
  正在安装    : libcgroup-0.41-21.el7.x86_64                                                                                     4/26 
  正在安装    : subscription-manager-rhsm-certificates-1.24.13-3.el7.centos.x86_64                                               5/26 
  正在安装    : python-ipaddress-1.0.16-2.el7.noarch                                                                             6/26 
  正在安装    : libyaml-0.1.4-11.el7_0.x86_64                                                                                    7/26 
  正在安装    : PyYAML-3.10-11.el7.x86_64                                                                                        8/26 
  正在安装    : audit-libs-python-2.8.5-4.el7.x86_64                                                                             9/26 
  正在安装    : python-backports-1.0-8.el7.x86_64                                                                               10/26 
  正在安装    : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                        11/26 
  正在安装    : python-setuptools-0.9.8-7.el7.noarch                                                                            12/26 
  正在安装    : 1:oci-register-machine-0-6.git2b44233.el7.x86_64                                                                13/26 
  正在安装    : libsemanage-python-2.5-14.el7.x86_64                                                                            14/26 
  正在安装    : setools-libs-3.3.8-4.el7.x86_64                                                                                 15/26 
  正在安装    : python-pytoml-0.1.14-1.git7dea353.el7.noarch                                                                    16/26 
  正在安装    : 1:atomic-registries-1.22.1-29.gitb507039.el7.x86_64                                                             17/26 
  正在安装    : python-IPy-0.75-6.el7.noarch                                                                                    18/26 
  正在安装    : 1:containers-common-0.1.37-3.el7.centos.x86_64                                                                  19/26 
  正在安装    : checkpolicy-2.5-8.el7.x86_64                                                                                    20/26 
  正在安装    : policycoreutils-python-2.5-33.el7.x86_64                                                                        21/26 
  正在安装    : 2:container-selinux-2.107-3.el7.noarch                                                                          22/26 
  正在安装    : container-storage-setup-0.11.0-2.git5eaf76c.el7.noarch                                                          23/26 
  正在安装    : 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64                                                         24/26 
  正在安装    : 2:docker-client-1.13.1-103.git7f2769b.el7.centos.x86_64                                                         25/26 
  正在安装    : 2:docker-1.13.1-103.git7f2769b.el7.centos.x86_64                                                                26/26 
  验证中      : 2:docker-common-1.13.1-103.git7f2769b.el7.centos.x86_64                                                          1/26 
  验证中      : 2:docker-1.13.1-103.git7f2769b.el7.centos.x86_64                                                                 2/26 
  验证中      : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                         3/26 
  验证中      : 2:container-selinux-2.107-3.el7.noarch                                                                           4/26 
  验证中      : container-storage-setup-0.11.0-2.git5eaf76c.el7.noarch                                                           5/26 
  验证中      : 1:atomic-registries-1.22.1-29.gitb507039.el7.x86_64                                                              6/26 
  验证中      : python-setuptools-0.9.8-7.el7.noarch                                                                             7/26 
  验证中      : checkpolicy-2.5-8.el7.x86_64                                                                                     8/26 
  验证中      : 2:oci-umount-2.5-3.el7.x86_64                                                                                    9/26 
  验证中      : 1:containers-common-0.1.37-3.el7.centos.x86_64                                                                  10/26 
  验证中      : python-IPy-0.75-6.el7.noarch                                                                                    11/26 
  验证中      : python-pytoml-0.1.14-1.git7dea353.el7.noarch                                                                    12/26 
  验证中      : setools-libs-3.3.8-4.el7.x86_64                                                                                 13/26 
  验证中      : policycoreutils-python-2.5-33.el7.x86_64                                                                        14/26 
  验证中      : libsemanage-python-2.5-14.el7.x86_64                                                                            15/26 
  验证中      : 1:oci-systemd-hook-0.2.0-1.git05e6923.el7_6.x86_64                                                              16/26 
  验证中      : 2:docker-client-1.13.1-103.git7f2769b.el7.centos.x86_64                                                         17/26 
  验证中      : 1:oci-register-machine-0-6.git2b44233.el7.x86_64                                                                18/26 
  验证中      : python-backports-1.0-8.el7.x86_64                                                                               19/26 
  验证中      : yajl-2.0.4-4.el7.x86_64                                                                                         20/26 
  验证中      : audit-libs-python-2.8.5-4.el7.x86_64                                                                            21/26 
  验证中      : libyaml-0.1.4-11.el7_0.x86_64                                                                                   22/26 
  验证中      : python-ipaddress-1.0.16-2.el7.noarch                                                                            23/26 
  验证中      : PyYAML-3.10-11.el7.x86_64                                                                                       24/26 
  验证中      : subscription-manager-rhsm-certificates-1.24.13-3.el7.centos.x86_64                                              25/26 
  验证中      : libcgroup-0.41-21.el7.x86_64                                                                                    26/26 

已安装:
  docker.x86_64 2:1.13.1-103.git7f2769b.el7.centos                                                                                    

作为依赖被安装:
  PyYAML.x86_64 0:3.10-11.el7                                  atomic-registries.x86_64 1:1.22.1-29.gitb507039.el7                   
  audit-libs-python.x86_64 0:2.8.5-4.el7                       checkpolicy.x86_64 0:2.5-8.el7                                        
  container-selinux.noarch 2:2.107-3.el7                       container-storage-setup.noarch 0:0.11.0-2.git5eaf76c.el7              
  containers-common.x86_64 1:0.1.37-3.el7.centos               docker-client.x86_64 2:1.13.1-103.git7f2769b.el7.centos               
  docker-common.x86_64 2:1.13.1-103.git7f2769b.el7.centos      libcgroup.x86_64 0:0.41-21.el7                                        
  libsemanage-python.x86_64 0:2.5-14.el7                       libyaml.x86_64 0:0.1.4-11.el7_0                                       
  oci-register-machine.x86_64 1:0-6.git2b44233.el7             oci-systemd-hook.x86_64 1:0.2.0-1.git05e6923.el7_6                    
  oci-umount.x86_64 2:2.5-3.el7                                policycoreutils-python.x86_64 0:2.5-33.el7                            
  python-IPy.noarch 0:0.75-6.el7                               python-backports.x86_64 0:1.0-8.el7                                   
  python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7   python-ipaddress.noarch 0:1.0.16-2.el7                                
  python-pytoml.noarch 0:0.1.14-1.git7dea353.el7               python-setuptools.noarch 0:0.9.8-7.el7                                
  setools-libs.x86_64 0:3.3.8-4.el7                            subscription-manager-rhsm-certificates.x86_64 0:1.24.13-3.el7.centos  
  yajl.x86_64 0:2.0.4-4.el7                                   

完毕！

```

* 开始运行 Docker daemon
```text
# 启动Docker进程
[root@bogon ~]# sudo service docker start
Redirecting to /bin/systemctl start docker.service

# Docker默认开机启动
[root@bogon ~]# sudo chkconfig docker on
注意：正在将请求转发到“systemctl enable docker.service”。
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.

# 验证Docker是否正常工作，下载最新CentOS镜像
[root@bogon ~]# sudo docker pull centos
Using default tag: latest
Trying to pull repository docker.io/library/centos ... 
latest: Pulling from docker.io/library/centos
729ec3a6ada3: Pull complete 
Digest: sha256:f94c1d992c193b3dc09e297ffd54d8a4f1dc946c37cbeceb26d35ce1647f88d9
Status: Downloaded newer image for docker.io/centos:latest

# 查看镜像
[root@bogon ~]# sudo docker images centos
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/centos    latest              0f3e07c0138f        2 months ago        220 MB

# 测试镜像
[root@bogon ~]# sudo docker run -i -t centos /bin/bash
[root@ddd700a6bb09 /]# exit
exit
[root@bogon ~]# 
```


### 参考
* http://www.dockerinfo.net/docker%e5%ae%89%e8%a3%85-centos
