## SOFABoot

GitHub: https://github.com/sofastack/sofa-boot


> SOFABoot 是蚂蚁金服开源的基于 Spring Boot 的研发框架，它在 Spring Boot 的基础上，提供了诸如 Readiness Check，类隔离，日志空间隔离等等能力。在增强了 Spring Boot 的同时，SOFABoot 提供了让用户可以在 Spring Boot 中非常方便地使用 SOFA 中间件的能力。
> 
> 参考： 官网和官方GitHub

### 目录
* 背景（Spring Boot的局限性）
* 什么是SOFABoot
* 功能特性
* 基础术语
* [安装和使用](sofa-Boot-install.md)
* [快速开始](sofa-Boot-quick-start.md)

### 背景

Spring Boot 是一个非常优秀的开源框架，可以非常方便地就构建出一个基于 Spring 的应用程序，但是在使用过程中，还是会遇到一些问题：

* Spring Boot 提供了一个基础的健康检查的能力，中间件和应用都可以扩展来实现自己的健康检查逻辑。但是 Spring Boot 的健康检查只有 Liveness Check 的能力，缺少 Readiness Check 的能力，这样会有比较致命的问题。当一个微服务应用启动的时候，必须要先保证启动后应用是健康的，才可以将上游的流量放进来（来自于 RPC，网关，定时任务等等流量），否则就可能会导致一定时间内大量的错误发生。

* Spring Boot 虽然通过依赖管理（Dependency Management）的方式最大程度的保证了 Spring Boot 管理的 JAR 包之间的兼容性，但是不可避免的，当引入一些其他的 JAR 包的时候，还是可能会遇到冲突，而且很多时候这种冲突解决起来并不是这么容易，一个例子是当冲突的包是序列化相关的类库时，比如说 Hessian，如果应用中的一个组件需要使用 Hessian 3，而另一个则必须要使用 Hessian 4，由于 Hessian 3 和 Hessian 4 之间的不兼容性，并且序列化还涉及到微服务中的上下游服务，要把 Hessian 统一到一个版本绝非易事。

* 在超大规模微服务运维的场景下，运维能力的平台化是一定要解决的问题，而监控又是其中非常主要的一个点，针对于日志监控这种情况，Spring Boot 并没有提供任何解决方案。大部分的开源组件，具体要打印哪些日志，打印到什么路径，什么文件下面，都是由应用的使用者来决定，这样会导致每一个应用的日志配置都各式各样，每一个应用都需要去监控系统中配置自己应用的日志监控，导致关键的监控的实施成本特别高。

* 在企业级应用场景，模块化开发是解决多团队沟通成本的有效解决方案，每个业务团队专注于开发自己的应用模块，每个模块自包含，便于开发及自测，减少团队间的沟通成本。但是 Spring Boot 默认不支持模块化开发，所有 Bean 共用一个 Spring 上下文，在多团队开发时，如果不同团队定义了相同 BeanId，运行时将出现 BeanId 冲突错误。

为了解决以上的问题，又因为 SOFA 中间件中的各个组件本身就需要集成 Spring Boot，所以蚂蚁金服基于 Spring Boot 开发并开源了 SOFABoot，来解决以上的问题，也方便使用者在 Spring Boot 中方便地去使用 SOFA 中间件。

### 什么是SOFABoot

SOFABoot 是基于 Spring Boot 的开发框架，用于快速、敏捷地开发 Spring 应用程序，特别适合构建微服务系统。SOFABoot 在 Spring Boot 的基础上提供了诸如 Readiness Check、类隔离、日志空间隔离等能力，以解决大规模团队开发云原生微服务系统中会遇到的问题。同时 SOFABoot 也提供了蚂蚁金服金融科技中间件的轻量级集成方案，仅需少量配置即可在 SOFABoot 中使用金融科技中间件。金融科技中间件也可通过相应的 starter 模块单独配置集成到 Spring Boot 工程中。普通 Spring 工程通过 Embedded-SOFA 模式可以方便地集成并使用金融科技中间件。

SOFABoot 基于 Spring Boot 1.4.2 版本开发，使用标准 Spring 接口实现。可将 SOFABoot 理解为 Spring 的一个扩展，构建在 Spring Boot 基础之上提供金融科技中间件解决方案，每一个中间件均是一个可插拔的组件，添加和移除非常方便，同时，利用“约定优先配置”（convention over configuration）的理念完成自动配置，开发者能够更加专注于业务逻辑。

> Spring Boot 是一个非常优秀的开源框架，可以快速、敏捷地开发新一代基于 Spring 框架的应用程序，它并不是用来替代 Spring 的解决方案，而是和 Spring 框架紧密结合，用于提升 Spring 开发者体验的工具。SOFABoot 在 Spring Boot 的基础上进行了能力的增强并提供了蚂蚁中间件的轻量集成，且可与 Spring Boot、Spring 工程无缝集成。

SOFABoot 支持创建 Web 和 Core 两种类型的工程。当使用 SOFABoot 开发一个 Web 程序时，相当于“基于 Spring Boot 的 Web 应用 + 蚂蚁金服中间件” 进行开发；当使用 SOFABoot 开发一个 J2SE 程序（无 Web 页面访问），相当于“基于 Spring Boot 的非 Web 应用（无 servlet 依赖）+ 蚂蚁金服中间件” 进行开发。

SOFABoot 作为开发框架，在整个微服务架构中起着至关重要的作用，其本身也在不断优化升级。

### 功能特性

SOFABoot 框架不仅能实现中间件的集成管理、自动配置以及调用链路监控及治理，支持 Embedded-SOFA 模式、多类型的部署模式，还具有应用日志和中间件日志的隔离能力，并拥有一套完整的技术栈。

* 集成管理和自动配置

    只需添加相应中间件的 starter 模块，SOFABoot 会自动导入所需的依赖并完成必要的配置。

* Embedded-SOFA 模式

    提供 Embedded-SOFA 模式，以便于在 Spring 编程环境下使用蚂蚁金服金融科技中间件。

* 调用链路监控及治理

    集成日志跟踪工具 Tracer，提供统一的中间件日志埋点和上下文 ID，将上下游系统的调用关系串联起来。

* 多类型的部署模式

    既支持直接运行可执行的 fat JAR 文件，也支持部署至各种 servlet 容器中（如 Tomcat、Jetty、Undertow 等）。

* 应用日志和中间件日志的隔离能力

    各中间件日志均面向 SLF4J 接口进行编程，日志实现依赖于具体的应用配置，且支持日志隔离。

* 完整的技术栈

    拥有一套完整的技术栈，能自动解决后续的依赖下载、应用部署、健康检查、运维监控等问题。开发人员集成框架后，只需专心编写业务代码。

### 基础术语

<table>
  <tr><th>术语</th><th>英文</th><th>说明</th></tr>
  <tr><td>Dubbo</td><td>Dubbo</td><td>Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，是阿里巴巴 SOA 服务化治理方案的核心框架，每天为 2,000+ 个服务提供 3,000,000,000+ 次访问量支持，并被广泛应用于阿里巴巴集团的各成员站点。</td></tr>
  <tr><td>Embedded-SOFA</td><td>Embedded-SOFA</td><td>支持在 Spring 编程环境下使用蚂蚁金服金融科技中间件。</td></tr>
  <tr><td>Fat JAR</td><td>Fat JAR</td><td>Fat JAR 是一种可执行的 JAR 包（Executable JAR），包含编译后的类及代码运行所需依赖 jar 的存档，可以使用 java-jar 命令运行该应用程序。Fat JAR 和普通的 JAR 不同在于它包含了依赖的 JAR 包。</td></tr>
  <tr><td>Gradle</td><td>Gradle</td><td>ApacheGradle 是一个基于 Apache Ant 和 Apache Maven 概念的项目自动化构建工具。它使用一种基于 Groovy 的特定领域语言（DSL）来声明项目设置，抛弃了基于 XML 的各种繁琐配置。</td></tr>
  <tr><td>Jetty</td><td>Jetty</td><td>Jetty 是一个开源的 Java servlet 容器，它为基于 Java 的 Web 容器，例如 JSP 和 servlet，提供运行环境。</td></tr>
  <tr><td>Log4j</td><td>Log4j</td><td>Apache Log4j，即 log for Java（Java 的日志)，是 Apache 的一个开源项目，可以控制日志信息输送的目的地，也可以控制每一条日志的输出格式，通过定义每一条日志信息的级别，能够更加细致地控制日志的生成过程。</td></tr>
  <tr><td>Log4j 2</td><td>Log4j 2</td><td>Log4j 2 是 Log4j 的升级版。</td></tr>
  <tr><td>Logback</td><td>Logback</td><td>Logback 是一个开源日志组件。SOFABoot 默认使用 SLF4J + Logback 日志框架。</td></tr>
  <tr><td>Maven</td><td>Maven</td><td>Apache Maven 是一个项目管理和构建自动化工具，为开发者提供了一套完整的构建生命周期框架，开发团队几乎不用花多少时间就能够自动完成工程的基础构建配置。</td></tr>
  <tr><td>RpcId</td><td>RpcId</td><td>RpcId 代表了本次请求在整个调用链路中的位置，比如 A 系统在处理一个请求的过程中依次调用了 B，C，D 三个系统，那么这三次调用的 RpcId 分别是：0.1，0.2，0.3。如果 B 系统继续调用了 E，F 两个系统，那么这两次调用的 RpcId 分别是：0.1.1，0.1.2。</td></tr>
  <tr><td>SOFA</td><td>SOFA</td><td>Scalable Open Financial Architecture，简称 SOFA，是蚂蚁金服自主研发的金融级分布式中间件框架。</td></tr>
  <tr><td>SOFABoot</td><td>SOFABoot</td><td>基于 Spring Boot 的中间件轻量集成方案，与标准的 Spring Boot 工程无缝集成，集成了蚂蚁金服全套金融级中间件。</td></tr>
  <tr><td>SOFALite</td><td>SOFALite</td><td>基于 Spring 的中间件集成框架，可与标准的 Spring 工程无缝集成。</td></tr>
  <tr><td>SOFAREST</td><td>SOFAREST</td><td>SOFAREST 是一种基于 JAX-RS（Java API for RESTful Web Services）标准的 SOA（Service-Oriented Architecture）解决方案。</td></tr>
  <tr><td>SOFARPC</td><td>SOFARPC</td><td>SOFARPC 提供应用之间的点对点服务调用功能。</td></tr>
  <tr><td>Spring Boot</td><td>Spring Boot</td><td>Spring Boot 是一种用于简化 Spring 应用的初始搭建以及开发过程的框架，该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板式的配置。</td></tr>
  <tr><td>Spring Cloud</td><td>Spring Cloud</td><td>Spring Cloud 是一系列框架的集合，利用 Spring Boot 简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用 Spring Boot 的开发风格做到一键启动和部署。</td></tr>
  <tr><td>Starter</td><td>Starter</td><td>Spring Boot/SOFABoot 的启动器，可快速接入内嵌的功能模块。</td></tr>
  <tr><td>Tengine</td><td>Tengine</td><td>由淘宝网发起的 Web 服务器项目。它在 Nginx 的基础上，针对大访问量网站的需求，添加了很多高级功能和特性。</td></tr>
  <tr><td>Tomcat</td><td>Tomcat</td><td>主要是作为 Java servlet/JSP 容器，也有许多传统 Web 服务器的性能。</td></tr>
  <tr><td>TraceId</td><td>TraceId</td><td>TraceId 指的是 Tracer 中代表唯一一次请求的 ID，此 ID 一般由集群中第一个处理请求的系统产生。</td></tr>
  <tr><td>Tracer</td><td>Tracer</td><td>标识整个请求链，即一些列 Span 的组合。其自身的 ID 将贯穿整个调用链，其中的每个 Span 都必须携带这个 traceId，因此 traceId 将在整个调用链中传递。</td></tr>
  <tr><td>定时任务</td><td>Scheduling Task</td><td>定时任务服务为业务系统提供统一通用的任务调度服务，提供定时任务的管理监控平台。</td></tr>
  <tr><td>动态配置</td><td>Dynamic Configuration</td><td>微服务的模块之一，是一个配置管理框架，可以在分布式环境下，动态管理应用集群配置参数。</td></tr>
  <tr><td>分布式链路跟踪</td><td>Distributed System Tracing</td><td>分布式链路跟踪是一款实时监控并管理企业应用性能和故障的云服务。</td></tr>
  <tr><td>分布式事务</td><td>Distributed Transaction-eXtended</td><td>蚂蚁金服自主研发的金融级分布式事务中间件，用来保障在大规模分布式环境下业务活动的最终一致性。</td></tr>
  <tr><td>数据访问代理</td><td>Database Proxy</td><td>蚂蚁金服自主研发的金融级分布式数据库中间件，用于解决海量请求下数据访问的瓶颈及数据库的容灾问题，提供水平拆分、平滑扩缩容、读写分离的在线分布式数据库服务。</td></tr>
  <tr><td>微服务</td><td>Microservices</td><td>主要提供分布式应用常用解决方案，包含 RPC 服务、定时任务调度服务、动态配置等。</td></tr>
  <tr><td>消息队列</td><td>Message Queue</td><td>消息代理组件，主要应用于分布式系统或组件之间的消息通讯。</td></tr>
</table>


