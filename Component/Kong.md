## Kong

网站： https://konghq.com/kong/

源码： https://github.com/Kong/kong

### 目录
* [Kong 是什么？](#Kong-是什么？)
* [Kong 的组件](#Kong-的组件)
* [Kong 有哪些特性？](#Kong-有哪些特性？)
* [Kong 有哪些插件？](#Kong-有哪些插件？)
* [参考](#参考)

### Kong 是什么？
Kong 是 Mashape 开源的高性能高可用 API 网关和 API 管理服务层。

它基于 OpenResty 进行 API 管理，并提供了插件实现 API 的 AOP。

Kong是一款基于OpenResty（Nginx + Lua模块）编写的高可用、易扩展的，由Mashape公司开源的API Gateway项目。Kong是基于NGINX和Apache Cassandra或PostgreSQL构建的，能提供易于使用的RESTful API来操作和配置API管理系统，所以它可以水平扩展多个Kong服务器，通过前置的负载均衡配置把请求均匀地分发到各个Server，来应对大批量的网络请求。

### Kong 的组件
* Kong Server ：基于nginx的服务器，用来接收API请求。
* Apache Cassandra/PostgreSQL ：用来存储操作数据。
* Kong dashboard：官方推荐UI管理工具，当然，也可以使用 restfull 方式 管理admin api。

Kong采用插件机制进行功能定制，插件集（可以是0或N个）在API请求响应循环的生命周期中被执行。插件使用Lua编写，目前已有几个基础功能：HTTP基本认证、密钥认证、CORS（Cross-Origin Resource Sharing，跨域资源共享）、TCP、UDP、文件日志、API请求限流、请求转发以及Nginx监控。

### Kong 有哪些特性？
* 可扩展性: 通过简单地添加更多的服务器，可以轻松地进行横向扩展，这意味着您的平台可以在一个较低负载的情况下处理任何请求；
* 模块化: 可以通过添加新的插件进行扩展，这些插件可以通过RESTful Admin API轻松配置；
* 在任何基础架构上运行: Kong网关可以在任何地方都能运行。您可以在云或内部网络环境中部署Kong，包括单个或多个数据中心设置，以及public，private 或invite-only APIs。

### Kong 有哪些插件？
* 身份认证插件：Kong提供了Basic Authentication、Key authentication、OAuth2.0 authentication、HMAC authentication、JWT、LDAP authentication认证实现。
* 安全控制插件：ACL（访问控制）、CORS（跨域资源共享）、动态SSL、IP限制、爬虫检测实现。
* 流量控制插件：请求限流（基于请求计数限流）、上游响应限流（根据upstream响应计数限流）、请求大小限制。限流支持本地、Redis和集群限流模式。
* 分析监控插件：Galileo（记录请求和响应数据，实现API分析）、Datadog（记录API Metric如请求次数、请求大小、响应状态和延迟，可视化API Metric）、Runscope（记录请求和响应数据，实现API性能测试和监控）。
* 协议转换插件：请求转换（在转发到upstream之前修改请求）、响应转换（在upstream响应返回给客户端之前修改响应）。
* 日志应用插件：TCP、UDP、HTTP、File、Syslog、StatsD、Loggly等。

### Kong 架构
![Kong架构](images/kong-architecture.png)

1. Kong核心基于OpenResty构建，实现了请求/响应的Lua处理化；
2. Kong插件拦截请求/响应，如果接触过Java Servlet，等价于拦截器，实现请求/响应的AOP处理；
3. Kong Restful 管理API提供了API/API消费者/插件的管理；
4. 数据中心用于存储Kong集群节点信息、API、消费者、插件等信息，目前提供了PostgreSQL和Cassandra支持，如果需要高可用建议使用Cassandra；
5. Kong集群中的节点通过gossip协议自动发现其他节点，当通过一个Kong节点的管理API进行一些变更时也会通知其他节点。每个Kong节点的配置信息是会缓存的，如插件，那么当在某一个Kong节点修改了插件配置时，需要通知其他节点配置的变更。

Kong作为API网关提供了API管理功能，及围绕API管理实现了一些默认的插件，另外还具备集群水平扩展能力，从而提升整体吞吐量。Kong本身是基于OpenResty，可以在现有Kong的基础上进行一些扩展，从而实现更复杂的特性。

虽然有一些特性Kong默认是缺失的，如API级别的超时、重试、fallback策略、缓存、API聚合、AB测试等，这些功能插件需要企业开发人员通过Lua语言进行定制和扩展。

综上所述，Kong API网关默认提供的插件比较丰富， 适应针对企业级的API网关定位。

### 参考
* `https://www.jianshu.com/p/4dd5ed88468c`

