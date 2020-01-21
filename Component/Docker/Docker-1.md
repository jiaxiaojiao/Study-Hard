## Docker
**_学习_**

> Debug your app, not your environment  调试应用程序，而不是调试环境。
>
> Securely build, share and run any application, anywhere

### 目录
* [Docker是什么？](#是什么？)
* [历史](#历史)
* [功能](#功能)
* 核心概念
    * [镜像Image](镜像Image.md)
    * [容器Container](Docker容器.md)
    * [仓库Repository](Docker-Repository.md)
* Docker的使用
    * [在CentOS环境安装Docker](CentOS安装Docker.md)
    * [运行HelloWorld](实例-在Docker中运行helloworld.md)
    * [Docker的安全介绍](安全介绍.md)
    * [Docker的常用命令](Docker-Commands.md)
* [Docker的网络](Docker-1.md)
* [为什么选择Docker](#为什么选择Docker)
* [Docker和Moby](#Docker和Moby)
* [Docker的版本](#Docker的版本)
* [Docker和K8s](#Docker和K8s)
* [参考](#参考)

### 是什么？
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的Linux机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

Docker 项目的目标是实现轻量级的操作系统虚拟化解决方案。 Docker 的基础是 Linux 容器（LXC）等技术。在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

*Docker本身并不是容器，它是创建容器的工具，是应用容器引擎。

### 历史
* 2010年，几个搞IT的年轻人，在美国旧金山成立了一家名叫“dotCloud”的公司。主要提供基于PaaS的云计算技术服务。具体来说，是和**[LXC](#LXC是什么)**有关的容器技术。
* 后来，dotCloud公司将自己的容器技术进行了简化和标准化，并命名为——Docker。它基于 Google 公司推出的 Go 语言实现。
* 2013年3月，Docker项目开源。加入了 Linux 基金会，遵从了 Apache 2.0 协议，项目代码在 GitHub 上进行维护。
* Docker 自开源后受到广泛的关注和讨论，以至于 dotCloud 公司后来都改名为 Docker Inc。Redhat 已经在其 RHEL6.5 中集中支持 Docker；Google 也在其 PaaS 产品中广泛应用。

### 功能
Docker 是一个软件部署的解决方案，轻量级的应用容器框架，可以打包、发布、运行任何的应用。

在任何地方开发、部署和运行任何应用。 Docker是一款针对程序开发人员和系统管理员来开发、部署、运行应用的一款虚拟化平台。Docker 可以让你像使用集装箱一样快速的组合成应用，并且可以像运输标准集装箱一样，尽可能的屏蔽代码层面的差异。Docker 会尽可能的缩短从代码测试到产品部署的时间。

Docker组件：
* The Docker Engine。 Docker Engine 是一个基于虚拟化技术的轻量级并且功能强大的开源容器引擎管理工具。它可以将不同的 work flow 组合起来构建成你的应用。
* Docker Hub。 可以分享和管理你的images镜像的一个 Saas 服务。

### 为什么选择Docker
1. 快速交付应用程序
2. 快速构建 轻松管理

### Docker和Moby
**原来在Github上托管的docker也随着PR#32691的合入正式变为Moby，为什么呢？**

**官方说法**： 

Introducing Moby Project: a new open-source project to advance the software containerization movement（April 18 2017）
一个致力于推进软件容器化运动的开源项目

Docker改名为Moby了吗？答案已经很明确了，Docker仍然还在，仍然还叫Docker。只是Moby项目已经问世，它是Docker的上游项目，是Docker之母。正因如此，Docker这个名字也已经不适合作为原来源码库的名字了。而对于普通的容器个人使用者或者企业，影响并不是太大。对于一些容器系统厂商和组件提供方，Moby提供了一种新形式的协作平台，可以定制化、增强、适配容器系统等等。

Moby主要针对的人群是想要组装一个基于容器的系统的人，包括
* 想要定制化Docker构建的hacker
* 想要构建一个容器系统的系统工程师
* 想要将已经存在的容器系统适配到自己环境的 基础设施提供方
* 想要体验最新容器技术的容器爱好者
* 想要在不同系统中测试项目的开源开发者
* 任何对Docker内部原理与如何构建感兴趣的人

但对于如下人群，Moby并不适合：
* 寻求一种简单的在容器中运行应用程序的应用开发者。推荐使用Docker CE。
* 想要一个带有商业支持且开箱即用容器平台的企业IT与开发团队。推荐使用Docker EE。
* 任何对容器感兴趣并且寻求一种简单易学的方式的人。请访问docker.com吧。

**另一种社区讨论的说法**：

他在平衡社区的生态与各方开发者的情感以及自己商业化道路之间复杂微妙的关系。

### Docker的版本
* moby是继承了原先的docker的项目，是社区维护的的开源项目
* docker-ce是docker公司维护的开源项目，是一个基于moby项目的免费的容器产品
* docker-ee是docker公司维护的闭源产品，是docker公司的商业产品。

### Docker和K8s
Docker容器技术是Kubernetes平台的基础。容器技术主要作用是隔离，通过对系统的关键资源的隔离，实现了主机抽象。Kubernetes平台则是在抽象主机的基础上，实现了集群抽象。

容器，提供应用级的主机抽象；Kubernetes，提供应用级的集群抽象。

### LXC是什么
LXC为Linux Container的简写。

Linux 容器是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源。

### 参考
* 网站： https://www.docker.com/
* 源码： https://github.com/docker
* 中文社区： http://www.docker.org.cn/
* 中文文档： http://www.dockerinfo.net/document
* Docker 菜鸟教程： https://www.runoob.com/docker/docker-tutorial.html
* 使用 Docker Hub 仓库： https://www.jianshu.com/p/94eb79825372
* 上传 Docker Hub 仓库： https://www.hangge.com/blog/cache/detail_2409.html
* LXC是什么： https://linuxcontainers.org/lxc/introduction/
* Docker改名为Moby了吗？： https://www.cnblogs.com/micrari/p/6748072.html
* Docker和Kubernetes： https://www.gitdig.com/k8s-my-definition/
* Docker和Kubernetes： https://zhuanlan.zhihu.com/p/53260098
* 微服务框架（Spring Boot + Dubbo + Docker + Jenkins）： https://zhuanlan.zhihu.com/p/33296468