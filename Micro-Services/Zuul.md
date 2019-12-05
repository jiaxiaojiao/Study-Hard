## Zuul

GitHub: https://github.com/Netflix/zuul

> Zuul is an L7 application gateway that provides capabilities for dynamic routing, monitoring, resiliency, security, and more. 
> 
> 参考： GitHub-zuul-wiki
<br> 参考： https://www.jianshu.com/p/ca76a4f396d1

### 目录
* [zuul是什么](#Zuul是什么？)

### Zuul是什么？

Zuul包含了对请求的**路由**和**过滤**两个最主要的功能:

其中路由功能负责将外部请求转发到具体的微服务实例上,是实现外部访问统一入口的基础而过滤器功能则负责对请求的处理过程进行干预,是实现请求校验、服务聚合等功能的基础.

Zuul和Eureka进行整合,将Zuul自身注册为Eureka服务治理下的应用,同时从Eureka中获得其他微服务的消息,也即以后的访问微服务都是通过Zuul跳转后获得.

注意:Zuul服务最终还是会注册进Eureka

提供=代理+路由+过滤三大功能

