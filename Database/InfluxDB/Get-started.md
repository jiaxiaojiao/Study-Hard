### 开始使用InfluxDB

> 20191111开始的，目前使用的是v2.0版本。

1. 下载InfluxDB

    环境： macOS、Linux、Docker
    
    ```text
    环境： 虚拟机CentOS 7,
    下载： InfluxDB v2.0 alpha (amd64)
          influxdb_2.0.0-alpha.19_linux_amd64.tar.gz
    ```

2. 安装和配置
    ```text
    # 1. 上传到虚拟机指定目录
    [root@bogon ~]# cd /usr/local/
    [root@bogon local]# rz
    
    # 2. 解压缩
    [root@bogon local]# tar xvzf influxdb_2.0.0-alpha.19_linux_amd64.tar.gz
    influxdb_2.0.0-alpha.19_linux_amd64/LICENSE
    influxdb_2.0.0-alpha.19_linux_amd64/README.md
    influxdb_2.0.0-alpha.19_linux_amd64/influx
    influxdb_2.0.0-alpha.19_linux_amd64/influxd
    [root@bogon local]# ls
    apache-maven-3.6.2  data   include                                     lib      rocketmq  src
    apollo              etc    influxdb_2.0.0-alpha.19_linux_amd64         lib64    sbin
    bin                 games  influxdb_2.0.0-alpha.19_linux_amd64.tar.gz  libexec  share
    
    # 3. 修改文件夹名称（随意）
    [root@bogon local]# mv influxdb_2.0.0-alpha.19_linux_amd64 influxdb_2.0.0
    
    # 4. 复制文件influx 和 influxd，到$PATH 
    /usr/local/influxdb_2.0.0
    [root@bogon influxdb_2.0.0]# sudo cp {influx,influxd} /usr/local/bin/
    [root@bogon influxdb_2.0.0]# ls
    influx  influxd  LICENSE  README.md
    [root@bogon influxdb_2.0.0]# cd /usr/local/bin/
    [root@bogon bin]# ls
    influx  influxd
    
    # 5. 网络端口 默认client-server使用端口9999通信 
    ```

3. 启动
    ```text
    # 运行文件influxd 启动
    [root@bogon bin]# influxd
    2019-11-12T16:31:43.364362Z	info	Welcome to InfluxDB	{"log_id": "0J479710000", "version": "2.0.0-alpha.19", "commit": "ce3e2969a", "build_date": "2019-10-30T23:33:54Z"}
    2019-11-12T16:31:43.381861Z	info	Resources opened	{"log_id": "0J479710000", "service": "bolt", "path": "/root/.influxdbv2/influxd.bolt"}
    2019-11-12T16:31:43.392178Z	info	Opening Series File (start)	{"log_id": "0J479710000", "service": "storage-engine", "service": "series-file", "op_name": "series_file_open", "path": "/root/.influxdbv2/engine/_series", "op_event": "start"}
    2019-11-12T16:31:43.445242Z	info	Opening Series File (end)	{"log_id": "0J479710000", "service": "storage-engine", "service": "series-file", "op_name": "series_file_open", "path": "/root/.influxdbv2/engine/_series", "op_event": "end", "op_elapsed": "53.065ms"}
    2019-11-12T16:31:43.484789Z	info	Index opened	{"log_id": "0J479710000", "service": "storage-engine", "index": "tsi", "partitions": 8}
    2019-11-12T16:31:43.485531Z	info	Reloaded WAL	{"log_id": "0J479710000", "service": "storage-engine", "path": "/root/.influxdbv2/engine/wal", "duration": "0.026ms"}
    2019-11-12T16:31:43.485585Z	info	Starting	{"log_id": "0J479710000", "service": "storage-engine", "component": "retention_enforcer", "check_interval": "1h"}
    2019-11-12T16:31:43.485835Z	info	Starting query controller	{"log_id": "0J479710000", "service": "storage-reads", "concurrency_quota": 10, "initial_memory_bytes_quota_per_query": 9223372036854775807, "memory_bytes_quota_per_query": 9223372036854775807, "max_memory_bytes": 0, "queue_size": 10}
    2019-11-12T16:31:43.818478Z	info	Starting	{"log_id": "0J479710000", "service": "telemetry", "interval": "8h"}
    2019-11-12T16:31:43.819280Z	info	Listening	{"log_id": "0J479710000", "service": "http", "transport": "http", "addr": ":9999", "port": 9999}
    ```

4. 创建用户
    ```text
    # 设置influx setup 按照步骤创建用户
    [root@bogon ~]# cd /usr/local/bin/
    [root@bogon bin]# influx setup
    Welcome to InfluxDB 2.0!
    Please type your primary username: jiaxiaojiao
    
    Please type your password: 
    
    Please type your password again: 
    
    Please type your primary organization name: jxj
    
    Please type your primary bucket name: test
    
    Please type your retention period in hours.
    Or press ENTER for infinite.: 
    
    
    You have entered:
      Username:          jiaxiaojiao
      Organization:      jxj
      Bucket:            test
      Retention Period:  infinite
    Confirm? (y/n): y
    
    Your token has been stored in /root/.influxdbv2/credentials.
    User		Organization	Bucket
    jiaxiaojiao	jxj		test
    ```
