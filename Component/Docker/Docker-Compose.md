## Docker Compose


### 目录
* [Docker Compose 是什么？](#Docker-Compose-是什么？)
* [使用Docker Compose](#使用Docker-Compose)
* [Docker Compose 下载安装](#Docker-Compose-下载安装)
* [异常 报错](#异常-报错)
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

### 异常 报错
* 启动单机版报错
    * 尝试重启虚拟机。 再次启动不报错，但是Nacos服务没有启动。 NO
    * 再次尝试重新启动后，依然报错。 NO
    * 把容器都rm，把docker 服务重启后，启动。没有报错，但是
```text
Starting grafana ... 
Starting alertmanager ... 
Starting node-exporter ... 
Starting nacos-standalone ... 

ERROR: for grafana  a bytes-like object is required, not 'str'

ERROR: for node-exporter  a bytes-like object is required, not 'str'

ERROR: for nacos-standalone  a bytes-like object is required, not 'str'

ERROR: for alertmanager  a bytes-like object is required, not 'str'

ERROR: for grafana  a bytes-like object is required, not 'str'

ERROR: for node-exporter  a bytes-like object is required, not 'str'

ERROR: for nacos  a bytes-like object is required, not 'str'

ERROR: for alertmanager  a bytes-like object is required, not 'str'
Traceback (most recent call last):
  File "site-packages/docker/api/client.py", line 261, in _raise_for_status
  File "site-packages/requests/models.py", line 940, in raise_for_status
requests.exceptions.HTTPError: 500 Server Error: Internal Server Error for url: http+docker://localhost/v1.22/containers/e98818aaedc46654a5ea11908222ca63988661c6856042480a5e0658cc444f3b/start

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "compose/service.py", line 625, in start_container
  File "compose/container.py", line 241, in start
  File "site-packages/docker/utils/decorators.py", line 19, in wrapped
  File "site-packages/docker/api/container.py", line 1095, in start
  File "site-packages/docker/api/client.py", line 263, in _raise_for_status
  File "site-packages/docker/errors.py", line 31, in create_api_error_from_http_exception
docker.errors.APIError: 500 Server Error: Internal Server Error ("b'driver failed programming external connectivity on endpoint alertmanager (663987fd1bdf89c25867221d045879096afb6814160bde84507e5903cdf432b5):  (iptables failed: iptables --wait -t nat -A DOCKER -p tcp -d 192.168.229.129 --dport 9093 -j DNAT --to-destination 172.18.0.3:9093 ! -i br-de9ac5b1d13a: iptables: No chain/target/match by that name.\n (exit status 1))'")

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "bin/docker-compose", line 6, in <module>
  File "compose/cli/main.py", line 72, in main
  File "compose/cli/main.py", line 128, in perform_command
  File "compose/cli/main.py", line 1107, in up
  File "compose/cli/main.py", line 1103, in up
  File "compose/project.py", line 570, in up
  File "compose/parallel.py", line 112, in parallel_execute
  File "compose/parallel.py", line 210, in producer
  File "compose/project.py", line 556, in do
  File "compose/service.py", line 568, in execute_convergence_plan
  File "compose/service.py", line 510, in _execute_convergence_start
  File "compose/parallel.py", line 112, in parallel_execute
  File "compose/parallel.py", line 210, in producer
  File "compose/service.py", line 508, in <lambda>
  File "compose/service.py", line 620, in start_container_if_stopped
  File "compose/service.py", line 627, in start_container
TypeError: a bytes-like object is required, not 'str'
[93775] Failed to execute script docker-compose
```


### 参考
* 源码： https://github.com/docker/compose
* https://www.runoob.com/docker/docker-compose.html
* https://github.com/docker/compose/releases
* https://blog.51cto.com/msiyuetian/2369130