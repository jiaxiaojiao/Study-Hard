## Zuul

GitHub: https://github.com/Netflix/zuul

> Zuul is an L7 application gateway that provides capabilities for dynamic routing, monitoring, resiliency, security, and more. 
> 
> 参考： GitHub-zuul-wiki，https://www.jianshu.com/p/ca76a4f396d1，https://www.zhihu.com/question/280850489

### 目录
* [是什么](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [优缺点](#优缺点)
* [其他替代组件](#其他替代组件)

### 是什么？

Zuul是Spring Cloud全家桶中的微服务API网关。

### 是否开源

开源。

在4月29日OpenInfra2019年丹佛峰会上，OpenStack基金会董事会正式宣布，Kata Containers和Zuul正式确立为OpenStack基金会顶级开源基础设施项目。

### 主要功能

Zuul包含了对请求的**路由**和**过滤**两个最主要的功能:

其中路由功能负责将外部请求转发到具体的微服务实例上,是实现外部访问统一入口的基础而过滤器功能则负责对请求的处理过程进行干预,是实现请求校验、服务聚合等功能的基础.

Zuul和Eureka进行整合,将Zuul自身注册为Eureka服务治理下的应用,同时从Eureka中获得其他微服务的消息,也即以后的访问微服务都是通过Zuul跳转后获得.

注意:Zuul服务最终还是会注册进Eureka

提供=代理+路由+过滤三大功能

### 兼容性

兼容Spring。

Zuul 目前有两个大的版本，1.x和2.x

这两个版本差别很大：
* Zuul 1.x 基于同步IO，也是Spring Cloud全家桶的一部分，可以方便的配合Spring Boot、Spring Cloud配置和使用。 filter最主要的就是pre、routing、post这三种过滤器，分别作用于调用业务服务API直接的请求处理、直接响应、调用业务服务API之后的响应处理。
* Zuul 2.x最大的改进就是基于Netty Server实现了异步IO来接入请求，同时基于Netty Client实现了到后端业务服务API的请求。这样就可以实现更高的性能和更低的延迟。Zuul 2.x调整了filter过滤器的类型，将原来的三个核心的过滤器命名为： Inbound Filter、Endpoint Filter、Outbound Filter。

Spring Cloud Gateway网关介绍：
* Spring Cloud Gateway 基于Java8、Spring 5.0、Spring Boot 2.0、Project Reactor，发展的比Zuul 2.x要早，也是Spring Cloud全家桶的一部分。 
* Spring Cloud Gateway 可以看做是Zuul 1.x的升级版和替代品，比Zuul 2.x更早的使用Netty实现异步IO，从而实现了一个简单、比Zuul 1.x更高效的、与Spring Cloud紧密配合的API网关。  
* Spring Cloud Gateway明确区分了Router和Filter，内置了很多开箱即用的功能，并且都可以通过Spring Boot配置或手工编码链式调用来使用。


### 优缺点
开源网关的对比分析

<table>
  <tr><th>网关</th><th>限流</th><th>鉴权</th><th>监控</th><th>易用性</th><th>可维护性</th><th>成熟度</th><th>GitHub star(20191206)</th></tr>
  <tr><td>Spring Cloud Gateway</td><td>可以通过IP、用户、集群限流，提供了相应的接口进口扩展</td><td>普通鉴权、auth2.0</td><td>Gateway Metrics Filter</td><td>简单易用</td><td>Spring Cloud全家桶，可维护性好</td><td>成熟</td><td>star: 2k</td></tr>
  <tr><td>Zuul 2.x</td><td>配置集群限流和单服务器限流，通过filter扩展限流</td><td>Filter</td><td>Filter</td><td>易用性较差，资料较少</td><td>可维护性较差</td><td>不太成熟</td><td>star: 8.6</td></tr>
  <tr><td>OpenResty</td><td>需要开发</td><td>需要开发</td><td>需要开发</td><td>简单易用，但是需要lua开发的很多</td><td>可维护性较差，需要维护lua脚本</td><td>成熟</td><td>star: 7.8k</td></tr>
  <tr><td>Kong</td><td>根据秒、分、时、天、月、年，根据用户进行限流。可以在源码基础上进行开发</td><td>普通鉴权，Key Auth鉴权，HMAC，Auth2.0</td><td>可上报datadog，记录请求数量，请求数据量，应答数据量，接受与发送的时间间隔，状态码数量，kong内运行时间</td><td>简单易用，api转发通过管理员接口配置，开发需要lua脚本</td><td>可维护性较差，需要维护lua库</td><td>相对成熟，用户问题汇总，社区，插件开源</td><td>star: 24.2k</td></tr>
</table>

### 其他替代组件

开源网关
* OpenResty
* Kong
* Zuul2
* SpringCloudGateway 