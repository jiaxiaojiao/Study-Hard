## Spring Cloud Gateway


### 目录
* [Spring Cloud Gateway 是什么？](#Spring-Cloud-Gateway-是什么？)
* [Spring Cloud Netflix Zuul和Spring Cloud Gateway的共同点和不同点](#共同点和不同点)
* [与其他API网关的对比](../../../Architecture/API-Gateway.md#API网关对比)
* [参考](#参考)

### Spring Cloud Gateway 是什么？
> This project provides a library for building an API Gateway on top of Spring MVC. Spring Cloud Gateway aims to provide a simple, yet effective way to route to APIs and provide cross cutting concerns to them such as: security, monitoring/metrics, and resiliency.

Spring Cloud Gateway可被视为Spring Cloud Netflix Zuul项目的后续产品 。

### 共同点和不同点
共同点： 这两个项目都负责为我们的微服务生态系统提供切入点，提供动态路由，安全和呼叫监控功能。

不同点：
1. Zuul基于servlet 2.5（与3.x一起使用），使用API阻止，例如websockets。
2. Spring Cloud Gateway基于Spring Framework 5，Project Reactor（允许与Spring WebFlux集成）和Spring Boot 2使用API而不会阻塞。这使它与长期连接（Websockets） 兼容，并且与Spring有更好的集成。
3. 随着Spring Boot 2和Spring Cloud 2的发布，与Zuul相比，Spring Cloud Gateway具有卓越的性能。

### 参考
* 网站： https://spring.io/projects/spring-cloud-gateway
* 源码： https://github.com/spring-cloud/spring-cloud-gateway
* https://baijiahao.baidu.com/s?id=1635961493324983528&wfr=spider&for=pc

