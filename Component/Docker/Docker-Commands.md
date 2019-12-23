## Docker 的常用命令

### 目录
* [Docker容器-创建](#Docker容器-创建)
* [Docker容器-启动](#Docker容器-启动)
* [Docker容器-停止](#Docker容器-停止)
* [查看容器IP地址：docker inspect 容器名称或 id](#docker-inspect)

### Docker容器 创建 
### Docker容器 启动 
` docker run`

### Docker容器 停止 
`docker stop $CONTAINER_ID`

* 查看启动的容器 `docker ps`
* 查看终止状态的容器 `docker ps -a`
* 启动终止状态的容器 `docker start $CONTAINER_ID`
* 重启容器 `docker restart $CONTAINER_ID`

### docker-inspect
docker查看容器IP地址：
`docker inspect 容器名称或 id`

以下测试命令基于[Docker安装部署Prometheus](../Prometheus/Prometheus-install.md)
```text
[root@bogon ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                            NAMES
78ec3d7edc23        prom/prometheus     "/bin/prometheus -..."   11 seconds ago      Up 10 seconds       192.168.229.128:9090->9090/tcp   prometheus
[root@bogon ~]# docker inspect 78ec3d7edc23
[
    {
        "Id": "78ec3d7edc23371355d9765ef31075241ffcbcb428ee191c45daade7f8a5255b",
        "Created": "2019-12-23T14:30:26.333766192Z",
        "Path": "/bin/prometheus",
        "Args": [
            "--config.file=/etc/prometheus/prometheus.yml",
            "--storage.tsdb.path=/prometheus",
            "--web.console.libraries=/usr/share/prometheus/console_libraries",
            "--web.console.templates=/usr/share/prometheus/consoles"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 13109,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2019-12-23T14:30:26.685770863Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:7317640d555e85d809d525dd7da42e703cfae67d0bcf5d6cceff699c76db9ea0",
        "ResolvConfPath": "/var/lib/docker/containers/78ec3d7edc23371355d9765ef31075241ffcbcb428ee191c45daade7f8a5255b/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/78ec3d7edc23371355d9765ef31075241ffcbcb428ee191c45daade7f8a5255b/hostname",
        "HostsPath": "/var/lib/docker/containers/78ec3d7edc23371355d9765ef31075241ffcbcb428ee191c45daade7f8a5255b/hosts",
        "LogPath": "",
        "Name": "/prometheus",
        "RestartCount": 0,
        "Driver": "overlay2",
        "MountLabel": "system_u:object_r:svirt_sandbox_file_t:s0:c287,c646",
        "ProcessLabel": "system_u:system_r:svirt_lxc_net_t:s0:c287,c646",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "journald",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "9090/tcp": [
                    {
                        "HostIp": "192.168.229.128",
                        "HostPort": "9090"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "docker-runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": -1,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0
        },
        "GraphDriver": {
            "Name": "overlay2",
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/dc6f8cf285d75bfe1f2d0e23acb14e0e3b54c55e66ab9f32882e916262a0eaa0-init/diff:/var/lib/docker/overlay2/a5e59acd372a3578056f5583a3b68b7d957397f26477d4a054ff0e6248269cf4/diff:/var/lib/docker/overlay2/631103703d3d1391c408dafa7d6e29b458c5f294eb1d22348f451c1b47c905dd/diff:/var/lib/docker/overlay2/487bb6960a3f54fe30e7825322ade70c045a47caa02ed1effeebd9bb43fc0629/diff:/var/lib/docker/overlay2/e94f5abc7e3714437e2cc2e74d9bd2cd99ae4918d4e0b43ae40f13e76bf9858f/diff:/var/lib/docker/overlay2/18880c39bb71cd33c9d3d0a0711d2ad592e5ccc2c2cc8546ab515daab2e793cb/diff:/var/lib/docker/overlay2/efece8a31e907ed6bacc5416ab3fd7905c807855b4212586f028937a2b4d71c4/diff:/var/lib/docker/overlay2/2134598a7f4ac420e168f785c761e34062a24e611efc33a7c1a91fd7ff449d27/diff:/var/lib/docker/overlay2/c040dce78739637651eb79e626d48aac672dd9bf9d19c407c95db8eb90f803a6/diff:/var/lib/docker/overlay2/1b9099352f2a950a1a6738f7f409c76950a3c261feb7eb7469f5b83d2384acec/diff:/var/lib/docker/overlay2/898721f1e60caf12b4563904563f797e977061b23408cae5ca8d6e5a45247d54/diff:/var/lib/docker/overlay2/8a865a7bc3c610238440a5545d67f41183dab636ea9b51e59b2621b03268ee4d/diff:/var/lib/docker/overlay2/7b7bf722136c9ea5d66092b595d98dc2de26f1a0cc27e6f0b4a2f1154104eb32/diff",
                "MergedDir": "/var/lib/docker/overlay2/dc6f8cf285d75bfe1f2d0e23acb14e0e3b54c55e66ab9f32882e916262a0eaa0/merged",
                "UpperDir": "/var/lib/docker/overlay2/dc6f8cf285d75bfe1f2d0e23acb14e0e3b54c55e66ab9f32882e916262a0eaa0/diff",
                "WorkDir": "/var/lib/docker/overlay2/dc6f8cf285d75bfe1f2d0e23acb14e0e3b54c55e66ab9f32882e916262a0eaa0/work"
            }
        },
        "Mounts": [
            {
                "Type": "volume",
                "Name": "373ad46ebe2fba3b3784adcd0aaae13f4898cd86c899c158247ab7e4dd21cc2b",
                "Source": "/var/lib/docker/volumes/373ad46ebe2fba3b3784adcd0aaae13f4898cd86c899c158247ab7e4dd21cc2b/_data",
                "Destination": "/prometheus",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],
        "Config": {
            "Hostname": "78ec3d7edc23",
            "Domainname": "",
            "User": "nobody",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "9090/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "--config.file=/etc/prometheus/prometheus.yml",
                "--storage.tsdb.path=/prometheus",
                "--web.console.libraries=/usr/share/prometheus/console_libraries",
                "--web.console.templates=/usr/share/prometheus/consoles"
            ],
            "ArgsEscaped": true,
            "Image": "prom/prometheus",
            "Volumes": {
                "/prometheus": {}
            },
            "WorkingDir": "/prometheus",
            "Entrypoint": [
                "/bin/prometheus"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "The Prometheus Authors <prometheus-developers@googlegroups.com>"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "6536b2d7c2b5fdeb4355196b1b6af12a6f630ce3a39d19d45b5ed5d27b2672a2",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "9090/tcp": [
                    {
                        "HostIp": "192.168.229.128",
                        "HostPort": "9090"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/6536b2d7c2b5",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "c69795b1404b45587ce263c0322c0916f76c409d23b4bc2ddea748eff6602539",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "94fa5adcca371294f7038ed98f6f0156885773534724bd596814dfa888ae15f6",
                    "EndpointID": "c69795b1404b45587ce263c0322c0916f76c409d23b4bc2ddea748eff6602539",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02"
                }
            }
        }
    }
]

```
