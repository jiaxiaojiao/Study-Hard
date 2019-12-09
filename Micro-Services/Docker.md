## Docker

网站： https://www.docker.com/

GitHub: https://github.com/docker

中文社区： http://www.docker.org.cn/

中文文档： http://www.dockerinfo.net/document

> Debug your app, not your environment 
>
> Securely build, share and run any application, anywhere
>
> 参考： 官网，GitHub，中文社区
<br> 参考： https://www.cnblogs.com/micrari/p/6748072.html
<br> 参考： https://www.gitdig.com/k8s-my-definition/

### 目录
* [描述](#描述)
* [Docker和Moby](#Docker和Moby)
* [开源](#关于开源)
* [功能](#功能)
* [Docker和K8s](#Docker和K8s)

### 描述

Docker 是一个开源项目，诞生于 2013 年初，最初是 dotCloud 公司内部的一个业余项目。它基于 Google 公司推出的 Go 语言实现。 项目后来加入了 Linux 基金会，遵从了 Apache 2.0 协议，项目代码在 GitHub 上进行维护。

Docker 自开源后受到广泛的关注和讨论，以至于 dotCloud 公司后来都改名为 Docker Inc。Redhat 已经在其 RHEL6.5 中集中支持 Docker；Google 也在其 PaaS 产品中广泛应用。

Docker 项目的目标是实现轻量级的操作系统虚拟化解决方案。 Docker 的基础是 Linux 容器（LXC）等技术。

在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。


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

### 关于开源

* moby是继承了原先的docker的项目，是社区维护的的开源项目
* docker-ce是docker公司维护的开源项目，是一个基于moby项目的免费的容器产品
* docker-ee是docker公司维护的闭源产品，是docker公司的商业产品。

### 功能

Docker 是一个软件部署的解决方案，轻量级的应用容器框架，可以打包、发布、运行任何的应用。

### Docker和K8s

Docker容器技术是Kubernetes平台的基础。容器技术主要作用是隔离，通过对系统的关键资源的隔离，实现了主机抽象。Kubernetes平台则是在抽象主机的基础上，实现了集群抽象。

容器，提供应用级的主机抽象；Kubernetes，提供应用级的集群抽象。


