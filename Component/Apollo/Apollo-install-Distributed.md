## Apollo 分布式部署

### 目录
* [一、准备工作](#一、准备工作)
* [二、部署步骤](#二、部署步骤)
* [三、登录](#三、登录)
* [参考](#参考)

### 一、准备工作
1.1 运行时环境
* OS 建议： Linux (CentOS7)
* Java 1.8+

1.2 MySQL 5.6.5+

1.3 环境。

1.4 网络策略

1.5 Docker 部署

1.6 Kubernetes支持

#### 环境
分布式部署需要事先确定部署的环境以及部署方式。

Apollo目前支持以下环境：
* DEV 开发环境
* FAT 测试环境，相当于alpha环境(功能测试)
* UAT 集成环境，相当于beta环境（回归测试）
* PRO 生产环境

```text
部署策略（例子）：
1. Portal部署在生产环境的机房，通过它来直接管理DEV、FAT、PRO环境的配置
2. Meta Server、Config Service和Admin Service在每个环境都单独部署，使用独立的数据库
3. Meta Server、Config Service和Admin Service在生产环境部署在两个机房，实现双活

本机Mac，安装虚拟机VMware Fusion
• centos 7-1  172.16.85.132
• centos 7-2  172.16.85.135
• centos 7-3  172.16.85.128
• centos 7-4  172.16.85.129

PRO生产环境 centos 7-1、centos 7-2
FAT测试环境 centos 7-3
DEV开发环境 centos 7-4
```

### 二、部署步骤

#### Docker 部署
1. 获取安装包
    * 从[GitHub Release](https://github.com/ctripcorp/apollo/releases)页面下载最新版本的apollo-configservice-x.x.x-github.zip、apollo-adminservice-x.x.x-github.zip和apollo-portal-x.x.x-github.zip
2. 配置数据库连接信息
    * 配置apollo-configservice的数据库连接信息。 config/application-github.properties
    ```text
    # DataSource
    spring.datasource.url = jdbc:mysql://localhost:3306/ApolloConfigDB?useSSL=false&characterEncoding=utf8
    spring.datasource.username = root
    spring.datasource.password = 123456
    
    
    #apollo.eureka.server.enabled=true
    #apollo.eureka.client.enabled=true
    ```
    * 配置apollo-adminservice的数据库连接信息。 config/application-github.properties
    ```text
    # DataSource
    spring.datasource.url = jdbc:mysql://localhost:3306/ApolloConfigDB?useSSL=false&characterEncoding=utf8
    spring.datasource.username = root
    spring.datasource.password = 123456
    ```    
    * 配置apollo-portal的数据库连接信息。 config/application-github.properties
    ```text
    # DataSource
    spring.datasource.url = jdbc:mysql://localhost:3306/ApolloPortalDB?useSSL=false&characterEncoding=utf8
    spring.datasource.username = root
    spring.datasource.password = 123456
    ```    
    * 配置apollo-portal的meta service信息。 config/apollo-env.properties。 `暂时没有负载均衡`
    ```text
    local.meta=http://localhost:8080
    dev.meta=http://172.16.85.129:8080
    fat.meta=http://172.16.85.128:8080
    # uat.meta=http://fill-in-uat-meta-server:8080
    # lpt.meta=${lpt_meta}
    pro.meta=http://172.16.85.132:8080,http://172.16.85.135:8080
    ```    
3. 部署Apollo服务端
```text
# 1. 将配置好的安装包 打包。 使用终端打包。Mac-终端（安装包目录下）
zip apollo-adminservice-1.5.1-github.zip apollo-adminservice-1.5.1-github
zip apollo-configservice-1.5.1-github.zip apollo-configservice-1.5.1-github
zip apollo-portal-1.5.1-github.zip apollo-portal-1.5.1-github

# 2. 将配置好的安装包 上传到4台虚拟机/usr/local。 使用Mac-终端scp命令。（安装包目录下） 密码123456
scp apollo-adminservice-1.5.1-github.zip root@172.16.85.129:/usr/local/
scp apollo-adminservice-1.5.1-github.zip root@172.16.85.128:/usr/local/
scp apollo-adminservice-1.5.1-github.zip root@172.16.85.135:/usr/local/
scp apollo-adminservice-1.5.1-github.zip root@172.16.85.132:/usr/local/

scp apollo-configservice-1.5.1-github.zip root@172.16.85.129:/usr/local/
scp apollo-configservice-1.5.1-github.zip root@172.16.85.128:/usr/local/
scp apollo-configservice-1.5.1-github.zip root@172.16.85.135:/usr/local/
scp apollo-configservice-1.5.1-github.zip root@172.16.85.132:/usr/local/

scp apollo-portal-1.5.1-github.zip root@172.16.85.129:/usr/local/
scp apollo-portal-1.5.1-github.zip root@172.16.85.128:/usr/local/
scp apollo-portal-1.5.1-github.zip root@172.16.85.135:/usr/local/
scp apollo-portal-1.5.1-github.zip root@172.16.85.132:/usr/local/

# 3. 将DockerFile文件 上传到4台虚拟机/usr/local。 使用Mac-终端scp命令。(指定Dockerfile目录下) 密码123456
## cd /Users/jiaxiaojiao/WebstormProjects/apollo/apollo-adminservice/src/main/docker/
scp Dockerfile root@172.16.85.129:/usr/local/apollo/apollo-adminservice/
scp Dockerfile root@172.16.85.128:/usr/local/apollo/apollo-adminservice/
scp Dockerfile root@172.16.85.135:/usr/local/apollo/apollo-adminservice/
scp Dockerfile root@172.16.85.132:/usr/local/apollo/apollo-adminservice/

## cd /Users/jiaxiaojiao/WebstormProjects/apollo/apollo-configservice/src/main/docker
scp Dockerfile root@172.16.85.129:/usr/local/apollo/apollo-configservice/
scp Dockerfile root@172.16.85.128:/usr/local/apollo/apollo-configservice/
scp Dockerfile root@172.16.85.135:/usr/local/apollo/apollo-configservice/
scp Dockerfile root@172.16.85.132:/usr/local/apollo/apollo-configservice/

## cd /Users/jiaxiaojiao/WebstormProjects/apollo/apollo-portal/src/main/docker/
scp Dockerfile root@172.16.85.129:/usr/local/apollo/apollo-portal/
scp Dockerfile root@172.16.85.128:/usr/local/apollo/apollo-portal/
scp Dockerfile root@172.16.85.135:/usr/local/apollo/apollo-portal/
scp Dockerfile root@172.16.85.132:/usr/local/apollo/apollo-portal/


# 4. 构建Docker镜像。 服务器（虚拟机）
目录：
apollo_portal
      - Dokerfile
      - apollo-portal-x.x.x-github.zip
apollo_config
      - Dokerfile
      - apollo-configservice-x.x.x-github.zip      
apollo_admin
      - Dokerfile
      - apollo-adminservice-x.x.x-github.zip

## cd /usr/local/apollo/apollo-adminservice-1.5.1
docker build -t apollo_adminservice
## cd /usr/local/apollo/apollo-configservice-1.5.1
docker build -t apollo_configservice
## cd /usr/local/apollo/apollo-portal-1.5.1
docker build -t apollo_portal
############################# 到这一步总是build失败，不知道为什么，，，呜呜

打Apollo镜像。
构建docker镜像：为apollo-configservice, apollo-adminservice, apollo-portal构建Docker镜像
部署Apollo服务端：构建镜像后通过docker compose就可以部署到公司的测试和生产环境了

# 4. 创建数据库。 地址： https://github.com/ctripcorp/apollo/tree/master/scripts/sql
## PRO生产环境 centos 7-1、centos 7-2  创建数据库configdb、portaldb
## FAT测试环境 centos 7-3 创建数据库configdb
## DEV开发环境 centos 7-4 创建数据库configdb
```

```text
# 部署服务器
# 使用镜像  https://hub.docker.com/r/idoop/docker-apollo/


```


### 三、登录

### 参考
* 文档 https://github.com/ctripcorp/apollo/wiki/%E5%88%86%E5%B8%83%E5%BC%8F%E9%83%A8%E7%BD%B2%E6%8C%87%E5%8D%97