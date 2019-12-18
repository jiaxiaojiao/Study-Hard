## Kubernetes 基础概念

### 目录
* [Kubernetes对象](#Kubernetes对象)
    * [对象规范和状态](#对象规范和状态)
    * [描述Kubernetes对象](#描述Kubernetes对象)
    * [Kubernetes对象的name](#Kubernetes对象的name)
* [Kubernetes的Pod](#Pod概念)
    * [自主式 Pod](#自主式-Pod)
    * [管理器管理的 Pod](#管理器管理的-Pod)
        * [RS、RC](#RS、RC)
        * [deployment](#deployment)
        * [HPA](#HPA)
        * [StatefullSet](#StatefullSet)
        * [DaemonSet](#DaemonSet)
        * [Job，Cronjob](#Job，Cronjob)
    * [服务发现](#服务发现)
    * [Pod协同](#Pod协同)
* [Kubernetes的Namespace命名空间](#Kubernetesd的Namespace)
* [Kubernetes的标签](#Kubernetes的标签)
* [Kubernetes的Volume卷](#Kubernetes的Volume卷)
    * [Volume的类型](#Volume的类型)
* [Kubernetes的Annotations注释](#Kubernetes的Annotations注释)
    * [标签和注释的区别](#标签和注释的区别)
* [Kubernetes的Nodes节点](#Kubernetes的Nodes)
* [Kubernetes组件间通信](#Kubernetes组件间通信)
    * [网络通讯模式](#网络通讯模式)
    * [网络通讯模式说明](#网络通讯模式说明)
    * [组件通讯模式说明](#组件通讯模式说明)
* [Kubernetes的ReplicaSet](#Kubernetes的ReplicaSet)
* [Kubernetes的Deployment](#Kubernetes的Deployment)
* [Kubernetes的Replication Controller](#Kubernetes的Replication-Controller)
* [Kubernetes的StatefulSets](#Kubernetes的StatefulSets)
* [Kubernetes的Ingress](#Kubernetes的Ingress)
* [Kubernetes的Service](#Kubernetes的Service)
* [Kubernetes的垃圾收集](#Kubernetes的垃圾收集)
* [Windows Server 容器](#Windows-Server-容器)


### Kubernetes对象
Kubernetes对象是Kubernetes系统中的持久实体。Kubernetes使用这些实体来表示集群的状态。

Kubernetes对象是“record of intent”，一旦创建了对象，Kubernetes系统会确保对象存在。通过创建对象，可以有效地告诉Kubernetes系统你希望集群的工作负载是什么样的。

要使用Kubernetes对象（无论是创建，修改还是删除），都需要使用Kubernetes API

#### 对象规范和状态
每个Kubernetes对象都包含两个嵌套对象字段，用于管理Object的配置：Object Spec和Object Status。
* Spec描述了对象所需的状态 - 希望Object具有的特性。
* Status描述了对象的实际状态，并由Kubernetes系统提供和更新。                                                                                                    

#### 描述Kubernetes对象
在Kubernetes中创建对象时，必须提供描述其所需Status的对象Spec，以及关于对象（如name）的一些基本信息。当使用Kubernetes API创建对象（直接或通过kubectl）时，该API请求必须将该信息作为JSON包含在请求body中。通常，可以将信息提供给kubectl .yaml文件，在进行API请求时，kubectl将信息转换为JSON。

##### Kubernetes对象的name
Kubernetes REST API中的所有对象都用Name和UID来明确地标识。
* Name 在一个对象中同一时间只能拥有单个Name。
* UID 是由Kubernetes生成的，在Kubernetes集群的整个生命周期中创建的每个对象都有不同的UID（即它们在空间和时间上是唯一的）。


### Pod概念
什么是Pod？
* Pod 是Kubernetes创建或部署的最小/最简单的基本单位，一个Pod代表集群上正在运行的一个进程。
* 一个Pod封装一个应用容器（也可以有多个容器），存储资源、一个独立的网络IP以及管理控制容器运行方式的策略选项。Pod代表部署的一个单位：Kubernetes中单个应用的实例，它可能由单个容器或多个容器共享组成的资源。
* Docker是Kubernetes Pod中最常见的runtime ，Pods也支持其他容器runtimes。

Pods提供两种共享资源：网络和存储。
* 网络  每个Pod被分配一个独立的IP地址，Pod中的每个容器共享网络命名空间，包括IP地址和网络端口。Pod内的容器可以使用localhost相互通信。当Pod中的容器与Pod 外部通信时，他们必须协调如何使用共享网络资源（如端口）。
* 存储  Pod可以指定一组共享存储volumes。Pod中的所有容器都可以访问共享volumes，允许这些容器共享数据。volumes 还用于Pod中的数据持久化，以防其中一个容器需要重新启动而丢失数据。

#### 自主式 Pod
#### 管理器管理的 Pod
控制器类型

##### RS、RC
##### deployment
##### HPA
##### StatefullSet
##### DaemonSet
##### Job，Cronjob
#### Pod协同

每个Pod之间是怎样沟通的？

### Kubernetesd的Namespace

Kubernetes可以使用Namespaces（命名空间）创建多个虚拟集群。

Namespace为名称提供了一个范围。资源的Names在Namespace中具有唯一性。

Namespace是一种将集群资源划分为多个用途的方法。

### Kubernetes的标签
Labels其实就一对 key/value ，被关联到对象上，标签的使用我们倾向于能够标示对象的特殊特点，并且对用户而言是有意义的，但是标签对内核系统是没有直接意义的。

### Kubernetes的Volume卷
默认情况下容器中的磁盘文件是非持久化的，对于运行在容器中的应用来说面临两个问题，第一：当容器挂掉kubelet将重启启动它时，文件将会丢失；第二：当Pod中同时运行多个容器，容器之间需要共享文件时。Kubernetes的Volume解决了这两个问题。

Kubernetes Volume具有明确的生命周期，Volume的生命周期比Pod中运行的任何容器要持久，在容器重新启动时能可以保留数据，当然，当Pod被删除不存在时，Volume也将消失。注意，Kubernetes支持许多类型的Volume，Pod可以同时使用任意类型/数量的Volume。

#### Volume的类型
Kubernetes支持Volume类型有：
* emptyDir
* hostPath
* gcePersistentDisk
* awsElasticBlockStore
* nfs
* iscsi
* fc (fibre channel)
* flocker
* glusterfs
* rbd
* cephfs
* gitRepo
* secret
* persistentVolumeClaim
* downwardAPI
* projected
* azureFileVolume
* azureDisk
* vsphereVolume
* Quobyte
* PortworxVolume
* ScaleIO
* StorageOS
* local

### Kubernetes的Annotations注释
可以使用Kubernetes Annotations将任何非标识metadata附加到对象。

#### 标签和注释的区别

使用Labels标签或Annotations注释都可以将元数据附加到Kubernetes对象。
* 标签 可用于选择对象并查找满足某些条件的对象集合。
* 注释 不用于标识和选择对象

### Kubernetes的Nodes
Node是Kubernetes中的工作节点，最开始被称为minion。一个Node可以是VM或物理机。每个Node（节点）具有运行pod的一些必要服务，并由Master组件进行管理，Node节点上的服务包括Docker、kubelet和kube-proxy。

Node是Kubernetes REST API中的最高级别资源

节点的状态信息：
* Addresses
* ~~Phase~~ (已弃用)
* Condition
* Capacity
* Info

### Kubernetes组件间通信
* Cluster -> Master  从集群到Master节点的所有通信路径都在apiserver中终止。
    
    Master组件通过非加密(未加密或认证)端口与集群apiserver通信。这个端口通常只在Master主机的localhost接口上暴露。

* Master -> Cluster  从Master (apiserver)到集群有两个主要的通信路径。

    1. apiserver - > kubelet  从apiserver到在集群中的每个节点上运行的kubelet进程。用于获取pod的日志，通过kubectl来运行pod，并使用kubelet的端口转发功能。这些连接在kubelet的HTTPS终端处终止。
    
    2. apiserver -> nodes、pods、services  通过apiserver的代理功能从apiserver到任何node、pod或service 。 从apiserver到Node、Pod或Service的连接默认为HTTP连接，因此不需进行认证加密。也可以通过HTTPS的安全连接，但是它们不会验证HTTPS 端口提供的证书，也不提供客户端凭据，因此连接将被加密但不会提供任何诚信的保证。这些连接不可以在不受信任/或公共网络上运行。
    
    SSH Tunnels 使用SSH tunnels来保护 Master -> 集群 通信路径，SSH tunnel能够使Node、Pod或Service发送的流量不会暴露在集群外部。

#### 网络通讯模式
Pod间是怎样通讯的？

#### 网络通讯模式说明
#### 组件通讯模式说明

### Kubernetes的ReplicaSet
ReplicaSet（RS）是Replication Controller（RC）的升级版本。

ReplicaSet 和  Replication Controller之间的唯一区别是对选择器的支持。
* ReplicaSet支持labels user guide中描述的set-based选择器要求
* Replication Controller仅支持equality-based的选择器要求。

如何使用ReplicaSet？
* 大多数kubectl 支持Replication Controller 命令的也支持ReplicaSets。

什么时候使用ReplicaSet？
* ReplicaSet能确保运行指定数量的pod。然而，Deployment 是一个更高层次的概念，它能管理ReplicaSets，并提供对pod的更新等功能。因此，我们建议你使用Deployment来管理ReplicaSets，除非你需要自定义更新编排。

### Kubernetes的Deployment
Deployment为Pod和Replica Set（升级版的 Replication Controller）提供声明式更新。

Deployment典型用例：
* 使用Deployment来创建ReplicaSet。ReplicaSet在后台创建pod。检查启动状态，看它是成功还是失败。
* 然后，通过更新Deployment的PodTemplateSpec字段来声明Pod的新状态。这会创建一个新的ReplicaSet，Deployment会按照控制的速率将pod从旧的ReplicaSet移动到新的ReplicaSet中。
* 如果当前状态不稳定，回滚到之前的Deployment revision。每次回滚都会更新Deployment的revision。
* 扩容Deployment以满足更高的负载。
* 暂停Deployment来应用PodTemplateSpec的多个修复，然后恢复上线。
* 根据Deployment 的状态判断上线是否hang住了。
* 清除旧的不必要的 ReplicaSet。

### Kubernetes的Replication Controller

注意：建议使用Deployment 配置 ReplicaSet （简称RS）方法来控制副本数。

ReplicationController（简称RC）是确保用户定义的Pod副本数保持不变。

#### ReplicationController 工作原理
在用户定义范围内，如果pod增多，则ReplicationController会终止额外的pod，如果减少，RC会创建新的pod，始终保持在定义范围。例如，RC会在Pod维护（例如内核升级）后在节点上重新创建新Pod。

注：
* ReplicationController会替换由于某些原因而被删除或终止的pod，例如在节点故障或中断节点维护（例如内核升级）的情况下。因此，即使应用只需要一个pod，我们也建议使用ReplicationController。
* RC跨多个Node节点监视多个pod。

### Kubernetes的StatefulSets
StatefulSets（有状态系统服务设计）在Kubernetes 1.7中还是beta特性，同时StatefulSets是1.4 版本中PetSets的替代品。

在具有以下特点时使用StatefulSets：
* 稳定性，唯一的网络标识符。
* 稳定性，持久化存储。
* 有序的部署和扩展。
* 有序的删除和终止。
* 有序的自动滚动更新。

StatefulSets的使用限制：
* StatefulSet还是beta特性，在Kubernetes 1.5版本之前任何版本都不可以使用。
* 与所有alpha / beta 特性的资源一样，可以通过apiserver配置-runtime-config来禁用StatefulSet。
* Pod的存储，必须基于请求storage class的PersistentVolume Provisioner或由管理员预先配置来提供。
* 基于数据安全性设计，删除或缩放StatefulSet将不会删除与StatefulSet关联的Volume。
* StatefulSets需要Headless Service负责Pods的网络的一致性（必须创建此服务）。

### Kubernetes的Ingress
service和pod仅可在集群内部网络中通过IP地址访问。所有到达边界路由器的流量或被丢弃或被转发到其他地方。Ingress是授权入站连接到达集群服务的规则集合。

* Ingress是beta版本的resource，在kubernetes1.1之前还没有。
* 你需要一个Ingress Controller来实现Ingress，单纯的创建一个Ingress没有任何意义。
* GCE/GKE会在master节点上部署一个ingress controller。

Ingress Controllers
* 为了使Ingress正常工作，集群中必须运行Ingress controller。 
* 这与其他类型的控制器不同，其他类型的控制器通常作为kube-controller-manager二进制文件的一部分运行，在集群启动时自动启动。 
* 你需要选择最适合自己集群的Ingress controller或者自己实现一个。

#### Ingress类型
* 单Service Ingress  Kubernetes中已经存在一些概念可以暴露单个service，但是你仍然可以通过Ingress来实现，通过指定一个没有rule的默认backend的方式。
* 简单展开
* 基于名称的虚拟主机
* TLS

#### 替代方案
可以通过很多种方式暴露service而不必直接使用ingress：
* 使用Service.Type=LoadBalancer
* 使用Service.Type=NodePort
* 使用Port Proxy
* 部署一个Service loadbalancer 这允许你在多个service之间共享单个IP，并通过Service Annotations实现更高级的负载平衡。

### Kubernetes的Service

#### 背景/Service解决什么问题
Kubernetes Pod 是有生命周期的，它们可以被创建，也可以被销毁，然而一旦被销毁生命就永远结束。 通过 ReplicationController 能够动态地创建和销毁 Pod（例如，需要进行扩缩容，或者执行 滚动升级）。 每个 Pod 都会获取它自己的 IP 地址，即使这些 IP 地址不总是稳定可依赖的。 这会导致一个问题：在 Kubernetes 集群中，如果一组 Pod（称为 backend）为其它 Pod （称为 frontend）提供服务，那么那些 frontend 该如何发现，并连接到这组 Pod 中的哪些 backend 呢？

#### 关于Service
Kubernetes Service 定义了这样一种抽象：一个 Pod 的逻辑分组，一种可以访问它们的策略 —— 通常称为微服务。这一组 Pod 能够被 Service 访问到，通常是通过 Label Selector实现的。

#### 定义 Service
一个 Service 在 Kubernetes 中是一个 REST 对象，和 Pod 类似。 像所有的 REST 对象一样， Service 定义可以基于 POST 方式，请求 apiserver 创建新的实例。

Kubernetes Service 能够支持 TCP 和 UDP 协议，默认 TCP 协议。

#### VIP 和 Service 代理
在 Kubernetes 集群中，每个 Node 运行一个 kube-proxy 进程。kube-proxy 负责为 Service 实现了一种 VIP（虚拟 IP）的形式，而不是 ExternalName 的形式。 在 Kubernetes v1.0 版本，代理完全在 userspace。在 Kubernetes v1.1 版本，新增了 iptables 代理，但并不是默认的运行模式。 从 Kubernetes v1.2 起，默认就是 iptables 代理。

在 Kubernetes v1.0 版本，Service 是 “4层”（TCP/UDP over IP）概念。 在 Kubernetes v1.1 版本，新增了 Ingress API（beta 版），用来表示 “7层”（HTTP）服务。

#### 服务发现
Kubernetes 支持2种基本的服务发现模式：
* 环境变量
* DNS

### Kubernetes的垃圾收集
Kubernetes 垃圾收集器的角色是删除指定的对象，这些对象曾经有但以后不再拥有 Owner 了。

注意：垃圾收集是 beta 特性，在 Kubernetes 1.4 及以上版本默认启用。

#### Owner 和 Dependent
一些 Kubernetes 对象是其它一些的 Owner。例如，一个 ReplicaSet 是一组 Pod 的 Owner。具有 Owner 的对象被称为是 Owner 的 Dependent。每个 Dependent 对象具有一个指向其所属对象的 metadata.ownerReferences 字段。

有时，Kubernetes 会自动设置 ownerReference 的值。例如，当创建一个 ReplicaSet 时，Kubernetes 自动设置 ReplicaSet 中每个 Pod 的 ownerReference 字段值。在 1.6 版本，Kubernetes 会自动为一些对象设置 ownerReference 的值，这些对象是由 ReplicationController、ReplicaSet、StatefulSet、DaemonSet 和 Deployment 所创建或管理。

也可以通过手动设置 ownerReference 的值，来指定 Owner 和 Dependent 之间的关系。

#### 控制垃圾收集器删除 Dependent
* 当删除对象时，可以指定是否该对象的 Dependent 也自动删除掉。自动删除 Dependent 也称为 级联删除。
    * background 模式。 Kubernetes 会立即删除 Owner 对象，然后垃圾收集器会在后台删除这些 Dependent。
    * foreground 模式。 根对象首先进入 “删除中” 状态，一旦被设置为 “删除中” 状态，垃圾收集器会删除对象的所有 Dependent。之后删除 Owner 对象。
* 如果删除对象时，不自动删除它的 Dependent，这些 Dependent 被称作是原对象的 孤儿。

### Windows Server 容器
Kubernetes v1.5引入了对Windows Server容器的支持。在版本1.5中，Kubernetes控制面板（API服务器，调度器，控制管理器等）仍然运行在Linux上，但是kubelet和kube-proxy可以运行在Windows Server上。

注意: 在Kubernetes 1.5中，Kubernetes中的Windows Server容器还属于Alpha功能。

