## Kubernetes
**_学习_**

网站： https://kubernetes.io/

源码： https://github.com/kubernetes/kubernetes

中文社区： https://www.kubernetes.org.cn/

> Kubernetes /koo-ber-nay'-tace/ 生产级别的容器编排系统 - 自动化的容器部署、扩展和管理

### 目录
* [Kubernetes是什么？](#Kubernetes是什么？)
    * [为什么简称K8s](#为什么简称K8s)
* [Kubernetes的发展经历](#Kubernetes的发展经历)
    * [为什么要有Kubernetes](#Google为什么开源Kubernetes)
    * [Kubernetes的特点](#Kubernetes的特点)
    * [如何成为当前唯一被业界广泛认可和看好的Docker分布式集群解决方案](#如何成为当前唯一被业界广泛认可和看好的Docker分布式集群解决方案)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [Kubernetes的优点](#Kubernetes的优点)
* [容器化的优点](#容器化的优点)
* Kubernetes的架构和使用
    * [K8S组件说明](Kubernetes-组件.md)
    * [K8S基础概念](Kubernetes-基础概念.md)
    * [Kubernetes安装](Kubernetes-安装.md)
    * [资源清单](资源清单.md)
    * [Pod控制器](Pod控制器.md)
    * [服务发现](服务发现.md)
    * [存储](存储.md)
    * [调度器](调度器.md)
    * [集群安全机制](集群安全机制.md)
    * [HELM](HELM.md)
    * [运维](运维.md)
* 与其他组件搭配
    * [监控K8S-Prometheus和Grafana](Kubernetes-monitor.md)

### Kubernetes是什么？
> Kubernetes (K8s) is an open-source system for automating deployment, scaling, and management of containerized applications.

Kubernetes (K8s) 是一个开源系统，用于容器化应用的自动部署、扩缩和管理。

Kubernetes 将构成应用的容器按逻辑单位进行分组以便于管理和发现。 

灵活！

云原生应用(Cloud Native Application)技术

#### 为什么简称K8s
Kubernetes 这个单词来自于希腊语，含义是舵手或领航员。K8S是它的缩写，用“8”字替代了“ubernete”这8个字符。

### Kubernetes的发展经历
1. 容器化趋势： Docker成为[PaaS](../../Architecture/Service-Model.md)下一代的标准。Docker这个新兴的容器化技术当前已经被很多公司所采用，其从单机走向集群已经成为必然，而云计算的蓬勃发展正在加速这一进程。 

2. 集群管理的需求： Docker分布式容器集群的管理起来比较复杂，需要资源管理平台来进行集群管理。

3. 资源管理平台使用历程： Apache MESOS -> Docker SWARM -> Kubernetes

4. Kubernetes地位确定： Kubernetes 作为当前唯一被业界广泛认可和看好的Docker分布式集群解决方案，可以预见，在未来几年内，会有大量的新系统选择它。

#### 资源管理平台
* Apache MESOS。 Apache License 2.0 开源协议。分布式的资源管理框架。2019.05 Twitter宣布放弃使用MESOS，转向Kubernetes。逐渐走下历史舞台……

* Docker SWARM。 Docker的集群化方案，已经成为Docker的一个组件。 2019.07 阿里云宣布Docker SWARM从选择列表中剔除。 优点： 轻量，在大型集群管理也不错。 缺点： 功能少，缺少更新回滚功能。 现在用的比较少。

* Kubernetes。  优点：功能稳定全面，是Google 10多年的积累。

#### Google为什么开源Kubernetes
Docker的大规模运行，很多公司都在研究资源管理平台，比如： Apache MESOS，Docker SWARM。 Google 为了巩固自己的在资源管理平台的领导地位，迂回争夺云计算市场，使用Go语言基于Borg开发出了Kubernetes 并且开源了出来。

谷歌惯于通过开源操作系统统治世界，进而实现更大的商业价值。比如： Android，TensorFlow。

#### Kubernetes的特点
我们的目标是促进完善组件和工具的生态系统，以减轻应用程序在公有云或私有云中运行的负担。

Kubernetes 特点
* 可移植: 支持公有云，私有云，混合云，多重云（multi-cloud）
* 可扩展: 模块化, 插件化, 可挂载, 可组合
* 自动化: 自动部署，自动重启，自动复制，自动伸缩/扩展

#### 如何成为当前唯一被业界广泛认可和看好的Docker分布式集群解决方案
1. 靠山硬： Kubernetes 是Google 2014年宣布开源的，是Google 10多年大规模容器管理技术Borg的开源版本，集结了Borg的精华。
2. 15+的经验实践技术成熟 + 社区最佳建议与实践： Kubernetes 基于谷歌公司在运行生产负载上的10年经验打造，并融合了来自社区的最佳建议与实践。
3. Kubernetes的特点： 轻量级(Go语言，消耗资源少)，开源，可扩展(弹性伸缩)，负载均衡(IPVS)

### 各个组件的作用

### 是否开源
Kubernetes (K8s) 是一个开源系统

民主化架构，从API到容器运行的每一层，Kubernetes项目都为开发者暴露出可以拓展的插件机制，鼓励用户通过代码的方式接入到Kubernetes项目的每个阶段。

这个变革，立即在容器社区催生出了到大量的基于Kubernetes API和拓展API的二次创新
* 微服务治理项目Istio
* 有状态应用部署架构Operator
* Rook: 通过Kubernetes的扩展接口，把Ceph这样的重量级产品封装成了简单易用的容器存储插件。

### 主要功能
* 快速部署应用
* 快速扩展应用
* 无缝对接新的应用功能
* 节省资源，优化硬件资源的使用

通过现代的 Web 服务，用户希望应用程序能够 24/7 全天候使用，开发人员希望每天可以多次发布部署新版本的应用程序。 容器化可以帮助软件包达成这些目标，使应用程序能够以简单快速的方式发布和更新，而无需停机。Kubernetes 帮助您确保这些容器化的应用程序在您想要的时间和地点运行，并帮助应用程序找到它们需要的资源和工具。 Kubernetes 是一个可用于生产的开源平台，根据 Google 容器集群方面积累的经验，以及来自社区的最佳实践而设计。

Kubernetes 基础模块：
1. 创建一个Kubernetes集群
2. 部署应用程序
3. 应用程序探索
4. 应用外部课件
5. 应用可扩展
6. 应用更新

### 兼容性
容器与语言无关

### Kubernetes的优点
K8s是一个开源的容器集群管理系统，可以实现容器集群的自动化部署、自动扩缩容、维护等功能。
1. 易学： 轻量级，简单，容易理解
2. 便携： 支持公有云，私有云，混合云，以及多种云平台
3. 可扩展： 模块化，可插拔，支持狗子，可任意组合
4. 自修复： 自动重调度，自动重启，自动复制

### 容器化的优点
**传统的应用部署方式**是通过插件或脚本来安装应用。这样做的缺点是应用的运行、配置、管理、所有生存周期将**与当前操作系统绑定**，这样做并不利于应用的升级更新/回滚等操作，当然也可以通过创建虚机的方式来实现某些功能，但是虚拟机非常重，并不利于可移植性。

**新的方式**是通过部署容器方式实现，每个容器之间**互相隔离**，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。相对于虚拟机，容器能**快速部署**，由于容器与底层设施、机器文件系统**解耦**的，所以它能在不同云、不同版本操作系统间进行迁移。

容器占用资源少、部署快，每个应用可以被打包成一个容器镜像，每个应用与容器间成一对一关系也使容器有更大优势，使用容器可以在build或release 的阶段，为应用创建容器镜像，因为每个应用不需要与其余的应用堆栈组合，也不依赖于生产环境基础结构，这使得从研发到测试、生产能提供一致环境。类似地，容器比虚机轻量、更“透明”，这更便于监控和管理。最后，

容器优势总结：

* 快速创建/部署应用：与VM虚拟机相比，容器镜像的创建更加容易。
* 持续开发、集成和部署：提供可靠且频繁的容器镜像构建/部署，并使用快速和简单的回滚(由于镜像不可变性)。
* 开发和运行相分离：在build或者release阶段创建容器镜像，使得应用和基础设施解耦。
* 开发，测试和生产环境一致性：在本地或外网（生产环境）运行的一致性。
* 云平台或其他操作系统：可以在 Ubuntu、RHEL、 CoreOS、on-prem、Google Container Engine或其它任何环境中运行。
* Loosely coupled，分布式，弹性，微服务化：应用程序分为更小的、独立的部件，可以动态部署和管理。
* 资源隔离
* 资源利用：更高效

### 参考
* `官网`
* `GitHub`
* `中文社区`
* `https://www.jianshu.com/p/94e551534035`
* `https://blog.csdn.net/wzq756984/article/details/88977439`
* `哔哩哔哩-尚硅谷 Kubernetes`

