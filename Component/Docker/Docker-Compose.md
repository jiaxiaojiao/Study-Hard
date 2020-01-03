## Docker Compose

源码： `https://github.com/docker/compose`

### 目录
* [Docker Compose 是什么？](#Docker-Compose-是什么？)
* [使用Docker Compose](#使用Docker-Compose)
* [Docker Compose 下载安装](#Docker-Compose-下载安装)
* [Docker Compose 怎么使用？](#Docker-Compose-怎么使用？)
* [参考](#参考)

### Docker Compose 是什么？
Compose 是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务。

### 使用Docker Compose
Compose 使用的三个步骤：
1. 使用 Dockerfile 定义应用程序的环境。
2. 使用 docker-compose.yml 定义构成应用程序的服务，这样它们可以在隔离环境中一起运行。
3. 最后，执行 docker-compose up 命令来启动并运行整个应用程序。
 
### Docker Compose 下载安装
Linux环境下： 可以从 Github 上下载它的二进制包来使用，最新发行的版本地址：`https://github.com/docker/compose/releases`

```text
# 下载Docker Compose稳定版本（路径源码Releases里有）
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
或
$ curl -L https://github.com/docker/compose/releases/download/1.25.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

# 赋权。将可执行权限应用于二进制文件
chmod +x /usr/local/bin/docker-compose

# 创建软链接
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

操作日志：
```text
【本地虚拟机-VM4】
# 下载
[root@bogon docker]# curl -L https://github.com/docker/compose/releases/download/1.25.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/docker/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617    0   617    0     0    509      0 --:--:--  0:00:01 --:--:--   509
100 16.2M  100 16.2M    0     0   365k      0  0:00:45  0:00:45 --:--:--  934k
# 赋权
[root@bogon docker]# chmod +x /usr/local/docker/docker-compose
# 创建软链接
[root@bogon docker]# sudo ln -s /usr/local/docker/docker-compose /usr/bin/docker-compose
# 验证
[root@bogon docker]# docker-compose --version
docker-compose version 1.25.0, build 0a186604
```

### Docker Compose 怎么使用？


### 参考
* `https://www.runoob.com/docker/docker-compose.html`
* `https://github.com/docker/compose/releases`