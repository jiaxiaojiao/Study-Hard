## Apollo

GitHub： https://github.com/ctripcorp/apollo

https://gitee.com/lepdou/apollo

> 统一配置中心。 宋顺
>
> 开源，学习下源码，优点
> 参考： 官网。网络。

### 目录
* [是什么？](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [支持的注册中心](#支持的注册中心)
* [兼容性](#兼容性)
* [优缺点](#优缺点/特点)
* [其他替代组件](#其他替代组件)
* [配置中心对比](#配置中心对比)

### 是什么？

Apollo（阿波罗）是携程框架部门研发的分布式配置中心，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性，适用于微服务配置管理场景。

### 是否开源

开源

### 主要功能

服务端基于Spring Boot和Spring Cloud开发，打包后可以直接运行，不需要额外安装Tomcat等应用容器。

Java客户端不依赖任何框架，能够运行于所有Java运行时环境，同时对Spring/Spring Boot环境也有较好的支持。

.Net客户端不依赖任何框架，能够运行于所有.Net运行时环境。

### 支持的注册中心

* Eureka

### 兼容性

目前Apollo团队由于人力所限，只提供了Java和.Net的客户端，对于其它语言的应用，可以通过本文的介绍来直接通过Http接口获取配置。

另外，如果有团队/个人有兴趣的话，也欢迎帮助我们来实现其它语言的客户端，具体细节可以联系@nobodyiam和@lepdou。

注：目前已有热心用户贡献了Go、Python、NodeJS、PHP、C++的客户端，更多信息可以参考Go、Python、NodeJS、PHP等客户端使用指南

### 优缺点/特点

* 统一管理不同环境、不同集群的配置
    * Apollo提供了一个统一界面集中式管理不同环境（environment）、不同集群（cluster）、不同命名空间（namespace）的配置。
    * 同一份代码部署在不同的集群，可以有不同的配置，比如zk的地址等
    * 通过命名空间（namespace）可以很方便的支持多个不同应用共享同一份配置，同时还允许应用对共享的配置进行覆盖
    * 配置界面支持多语言（中文，English）
* 配置修改实时生效（热发布）
    * 用户在Apollo修改完配置并发布后，客户端能实时（1秒）接收到最新的配置，并通知到应用程序。
* 版本发布管理
    * 所有的配置发布都有版本概念，从而可以方便的支持配置的回滚。
* 灰度发布
    * 支持配置的灰度发布，比如点了发布后，只对部分应用实例生效，等观察一段时间没问题后再推给所有应用实例。
* 权限管理、发布审核、操作审计
    * 应用和配置的管理都有完善的权限管理机制，对配置的管理还分为了编辑和发布两个环节，从而减少人为的错误。
    * 所有的操作都有审计日志，可以方便的追踪问题。
* 客户端配置信息监控
    * 可以方便的看到配置在被哪些实例使用
* 提供Java和.Net原生客户端
    * 提供了Java和.Net的原生客户端，方便应用集成
    * 支持Spring Placeholder，Annotation和Spring Boot的ConfigurationProperties，方便应用使用（需要Spring 3.1.1+）
    * 同时提供了Http接口，非Java和.Net应用也可以方便的使用
* 提供开放平台API
    * Apollo自身提供了比较完善的统一配置管理界面，支持多环境、多数据中心配置管理、权限、流程治理等特性。
    * 不过Apollo出于通用性考虑，对配置的修改不会做过多限制，只要符合基本的格式就能够保存。
    * 在我们的调研中发现，对于有些使用方，它们的配置可能会有比较复杂的格式，如xml, json，需要对格式做校验。
    * 还有一些使用方如DAL，不仅有特定的格式，而且对输入的值也需要进行校验后方可保存，如检查数据库、用户名和密码是否匹配。
    * 对于这类应用，Apollo支持应用方通过开放接口在Apollo进行配置的修改和发布，并且具备完善的授权和权限控制
* 部署简单
    * 配置中心作为基础服务，可用性要求非常高，这就要求Apollo对外部依赖尽可能地少
    * 目前唯一的外部依赖是MySQL，所以部署非常简单，只要安装好Java和MySQL就可以让Apollo跑起来
    * Apollo还提供了打包脚本，一键就可以生成所有需要的安装包，并且支持自定义运行时参数

### 其他替代组件

* Spring Cloud/Spring Cloud Config
    ```text
    GitHub地址： https://github.com/spring-cloud/spring-cloud-config
    2014年9月开源，Spring Cloud 生态组件，为分布式系统中的外部配置提供服务器和客户端支持，可以和Spring Cloud体系无缝整合。
    ```

* 阿里 Nacos
    ```text
    GitHub地址：https://github.com/alibaba/nacos
    一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。
    2018年6月，阿里开源的配置中心，也可以做DNS和RPC的服务发现。
    ```

### 配置中心对比

* 功能对比（Nacos具有Apollo大部分功能）

<table>
  <tr><th>功能点</th><th>Spring Cloud Config</th><th>Apollo</th><th>阿里Nacos</th><th>备注</th></tr>
  <tr><td>静态配置管理</td><td>基于file</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>动态配置管理</td><td>支持</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>统一管理</td><td>无，需要github</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>多环境多集群</td><td>无，需要github</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>本地配置缓存</td><td>无</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>高可用</td><td>客户端本地无文件缓存，配置中心宕机，服务无法重启</td><td>客户端本地缓存，配置中心宕机，服务重启无影响</td><td>不影响</td><td>--</td></tr>
  <tr><td>配置锁</td><td>支持</td><td>不支持</td><td>不支持</td><td>不允许动态及远程更新</td></tr>
  <tr><td>配置校验</td><td>无</td><td>支持</td><td>支持</td><td>如：ip地址校验，配置</td></tr>
  <tr><td>配置生效时间</td><td>重启生效，或手动refresh生效</td><td>实时</td><td>实时</td><td>需要结合热加载管理， springcloudconfig需要 git webhook+rabbitmq 实时生效</td></tr>
  <tr><td>配置更新推送</td><td>需要手工触发</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>配置定时拉取</td><td>无</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>用户权限管理</td><td>无，需要github</td><td>支持</td><td>暂不支持</td><td>现阶段可以人工处理</td></tr>
  <tr><td>授权、审核、审计</td><td>无，需要github</td><td>支持</td><td>暂不支持</td><td>现阶段可以人工处理</td></tr>
  <tr><td>配置版本管理</td><td>Git做版本管理</td><td>界面上直接提供发布历史和回滚按钮</td><td>支持</td><td>--</td></tr>
  <tr><td>配置合规检测</td><td>不支持</td><td>支持（但还需完善）</td><td>支持</td><td>--</td></tr>
  <tr><td>实例配置监控</td><td>需要结合springadmin</td><td>支持</td><td>支持</td><td>--</td></tr>
  <tr><td>灰度发布</td><td>不支持</td><td>支持</td><td>暂不支持</td><td>现阶段可以人工处理</td></tr>
  <tr><td>告警通知</td><td>不支持</td><td>支持，邮件方式告警</td><td>支持，grafana支持多种告警方式，常用的有邮件，钉钉和webhook方式</td><td>--</td></tr>
</table>

总结： Apollo和Nacos相对于Spring Cloud Config的生态支持更广，在配置管理流程上做的更好。Apollo相对于Nacos在配置管理做的更加全面，不过使用起来也要麻烦一些。Nacos使用起来相对比较简洁，在对性能要求比较高的大规模场景更适合。
此外，Nacos除了提供配置中心的功能，还提供了动态服务发现、服务共享与管理的功能，降低了服务化改造过程中的难度。

* 技术路线兼容性

引入配置中心，需要考虑和现有项目的兼容性，以及是否引入额外的第三方组件。我们的java项目以SpringBoot为主，需要重点关注springboot支持性。

<table>
  <tr><th>功能点</th><th>Spring Cloud Config</th><th>Apollo</th><th>阿里Nacos</th></tr>
  <tr><td>SpringBoot支持</td><td>原生支持</td><td>支持</td><td>支持</td></tr>
  <tr><td>SpringCloud支持</td><td>原生支持</td><td>支持</td><td>支持</td></tr>
  <tr><td>客户端支持</td><td>Java</td><td>Java/.Net/Go/C++/Python/PHP/OpenApi</td><td>Python/Java/OpenApi/Nodejs</td></tr>
  <tr><td>依赖组件</td><td>Eureka</td><td>Eureka</td><td>不依赖其他组件</td></tr>
</table>

* 可用性和易用性

引入配置中心后，所有的应用都需要依赖配置中心，因此可用性需要重点关注，另外管理的易用性也需要关注。

<table>
  <tr><th>功能点</th><th>Spring Cloud Config</th><th>Apollo</th><th>阿里Nacos</th></tr>
  <tr><td>单点故障（SPOF）</td><td>支持HA部署</td><td>支持HA部署</td><td>--</td></tr>
  <tr><td>多数据中心部署</td><td>支持</td><td>支持</td><td>支持</td></tr>
  <tr><td>单机部署</td><td>Config-Server+Git+Spring Cloud Bus(支持配置实时推送)</td><td>Apollo-quickstart+MySQL</td><td>Nacos单节点</td></tr>
  <tr><td>分布式部署</td><td>部署复杂 Config-Server(2)+Git+MQ</td><td>部署复杂Config(2)+Admin(2)+Portal(2)+MySQL</td><td>部署简单 Nacos(3)+MySQL</td></tr>
  <tr><td>配置获取性能</td><td>较慢，通过git</td><td>快，数据库访问+缓存支持</td><td>快，性能最好</td></tr>
  <tr><td>配置界面</td><td>无，需要通过git操作</td><td>统一界面（ng编写）</td><td>--</td></tr>
</table>

总结： Nacos的部署结构比较简单，运维成本较低。Apollo部署组件较多，运维成本比Nacos高。Spring Cloud Config生产高可用的成本最高。