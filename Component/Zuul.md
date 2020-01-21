## Zuul

源码: https://github.com/Netflix/zuul

> Zuul is an L7 application gateway that provides capabilities for dynamic routing, monitoring, resiliency, security, and more. 
> 

### 目录
* [Zuul 是什么](#Zuul-是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [参考](#参考)

### Zuul 是什么？
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

### 参考
* GitHub-zuul-wiki
* https://www.jianshu.com/p/ca76a4f396d1
* https://www.zhihu.com/question/280850489