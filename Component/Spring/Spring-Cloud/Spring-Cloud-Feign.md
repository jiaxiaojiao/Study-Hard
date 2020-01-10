## Feign

网站： `https://projects.spring.io/spring-cloud/spring-cloud.html#spring-cloud-feign`

源码： `https://github.com/OpenFeign/feign`

文档： `https://cloud.spring.io/spring-cloud-openfeign/reference/html/`

自己写的使用feign代码： `https://github.com/jiaxiaojiao/Study-SpringBoot/tree/master/ordercenter`

### 目录
* [# 什么是 Feign？](##-什么是-Feign？)
* [# Feign 使用](##-Feign的使用)
* [# Feign 工作原理](##-Feign-工作原理)
* [# 配置](##-Feign-配置)
    * [Feign的日志级别](#Feign的日志级别)
* 注解
    * [@FeignClient](#@FeignClient)
* [参考](#参考)

### # 什么是 Feign？
Feign是Netflix开发的声明式、模板化的HTTP客户端， Feign可以帮助我们更快捷、优雅地调用HTTP API。

在Spring Cloud中，使用Feign非常简单——创建一个接口，并在接口上添加一些注解，代码就完成了。Feign支持多种注解，例如Feign自带的注解或者JAX-RS注解等。

Spring Cloud对Feign进行了增强，使Feign支持了Spring MVC注解，并整合了Ribbon和Eureka，从而让Feign的使用更加方便。

Spring Cloud Feign是基于Netflix feign实现，整合了Spring Cloud Ribbon和Spring Cloud Hystrix，除了提供这两者的强大功能外，还提供了一种声明式的Web服务客户端定义的方式。

Spring Cloud Feign帮助我们定义和实现依赖服务接口的定义。在Spring Cloud feign的实现下，只需要创建一个接口并用注解方式配置它，即可完成服务提供方的接口绑定，简化了在使用Spring Cloud Ribbon时自行封装服务调用客户端的开发量。

Spring Cloud Feign具备可插拔的注解支持，支持Feign注解、JAX-RS注解和Spring MVC的注解。

### # Feign的使用
1. 添加依赖
```text
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
    <version>1.4.7.RELEASE</version>
</dependency>

# SpringBoot2.X版本后，引入Feign依赖是：
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
    <version>2.2.1.RELEASE</version>
</dependency>
```
2. 启动类添加 @EnableFeignClients 注解支持
```text
@SpringBootApplication
@EnableFeignClients
public class XxxApplication {
    public static void main(String[] args) {
        ...
    }
}
```
3. 建立Client接口，并在接口中定义需调用的服务方法
```text
@FeignClient(name = "feign-user-provider")
public interface UserService {
    /**
     * 查询用户（通过主键用户ID）
     * @param id
     * @return
     */
    @RequestMapping(value = "/usr/{id}", method = RequestMethod.GET)
    UserVO findUser(Long id);
}
```
4. 使用Client接口。


### # Feign 工作原理
* 在开发微服务应用时，我们会在主程序入口添加 `@EnableFeignClients` 注解开启对 Feign Client 扫描加载处理。根据 Feign Client 的开发规范，定义接口并加 `@FeignClients` 注解。
* 当程序启动时，会进行包扫描，扫描所有 `@FeignClients` 的注解的类，并将这些信息注入 Spring IOC 容器中。当定义的 Feign 接口中的方法被调用时，通过JDK的代理的方式，来生成具体的 `RequestTemplate`。当生成代理时，Feign 会为每个接口方法创建一个 `RequetTemplate` 对象，该对象封装了 HTTP 请求需要的全部信息，如请求参数名、请求方法等信息都是在这个过程中确定的。
* 然后由 `RequestTemplate` 生成 `Request`，然后把 `Request` 交给 `Client` 去处理，这里指的 `Client` 可以是 JDK 原生的 `URLConnection`、Apache 的 Http Client 也可以是 Okhttp。最后 Client 被封装到 `LoadBalanceclient` 类，这个类结合 Ribbon 负载均衡发起服务之间的调用。

### # Feign 配置
Feign配置范围： 
* 全局配置。
* 局部配置。

Feign配置方式：
* 代码配置。使用Java文件进行配置（configuration）
```text
# 代码配置方式支持的配置项
Feign.Builder	# Feign的入口
Client	# Feign底层用什么http客户端去请求
Contract	# 契约，注解支持
Encoder	# 编码器，用于将对象转换成Http请求消息体
Decoder # 将响应消息体转换成对象
Logger	# 日志管理器
Logger.Level	# 指定日志级别
Retryer	# 指定重试策略
ErrorDecoder	# 指定异常×××
Request.Options	# 超时时间
Collection<RequestInterceptor>	# 请求拦截器
SetterFactory	# 用于设置Hystrix的配置属性，Feign整合Hystrix才会用
```
* 配置文件配置。使用Spring Boot的配置文件进行配置（application.properties/yml）
```text
# 配置文件方式支持的配置项
feign.client.config:
    <feignName>:
      connectTimeoout: 5000 # 连接超时时间
      readTimeout: 5000 # 读取超时时间
      loggerLevel: full # 日志级别
      errorDecoder: com.example.SimpleErrorDecoder # 错误解码器
      retryer: com.example.SimpleRetryer # 重试策略
      requestInterceptors:
        - com.example.FooRequestInterceptor # 拦截器
      # 是否对404错误码 解码
      # 处理逻辑详见 feign.SynchronousMethodHandler#executeAndDecode
      decode404: false
      encoder: com.example.SimpleEncoder # 编码器
      decoder: com.example.SimpleDecoder # 解码器
      contract: com.example.SimpleContract # 契约
      
```

两种配置方式的优缺点：
* 代码配置。
    * 优点： 基于代码，更灵活
    * 缺点： 代码侵入性高，线上需要重新打包、发布，如果Feign的配置类添加了注解 `@Configuration` 需要注意父子上下文。
* 配置文件配置。
    * 优点： 易上手，直观，无需重新打包、发布，优先级更高。
    * 缺点： 极端场景下没有代码配置灵活。

关于优先级： `细粒度 配置文件配置 > 细粒度 代码配置 > 全局配置文件配置 > 全局代码配置`

尽量使用配置文件配置。


```text
## [feign] 配置 - 是否开启断路器
feign.hystrix.enabled=true
feign.okhttp.enabled=false
feign.httpclient.enabled=false
## [feign] 配置 - 对请求和响应内容压缩
feign.compression.request.enabled=true
feign.compression.request.mime-types=text/xml,application/xml,application/json
feign.compression.request.min-request-size=2048
feign.compression.response.enabled=true
## [feign] 配置 - 全局配置 日志级别
feign.client.config.default.logger-level=basic
## [feign] 配置 - 特定服务提供者配置 日志级别
feign.client.config.user-provider.logger-level=full
## [feign] 配置 - 特定服务提供者配置 连接超时时间
feign.client.config.user-provider.connect-timeout=500
## [feign] 配置 - 特定服务提供者配置 读取超时时间
feign.client.config.user-provider.read-timeout=500
## [feign] 配置 - 404是否被解码
feign.client.config.user-provider.decode404=false
## 编码器
#feign.client.config.user-provider.encoder=
## 解码器
#feign.client.config.user-provider.decoder=
#feign.client.config.user-provider.error-decoder=
## 重试
#feign.client.config.user-provider.retryer=
## 拦截器
#feign.client.config.user-provider.request-interceptors[0]=
#feign.client.config.user-provider.request-interceptors[1]=
#feign.client.config.user-provider.request-interceptors[2]=
## 契约
#feign.client.config.user-provider.contract=
```

#### Feign的日志级别
Feign的日志级别与Spring Boot不一样，所以不能直接配置Spring Boot的日志级开启。

Feign的日志级别：
<table>
  <tr><th>级别</th><th>打印内容</th></tr>
  <tr><td>NONE</td><td>默认值，不记录任何信息</td></tr>
  <tr><td>BASIC</td><td>仅记录请求方法、URL、响应状态代码、执行时间</td></tr>
  <tr><td>HEADERS</td><td>记录BASIC级别的基础之上，记录请求和响应的header</td></tr>
  <tr><td>FULL</td><td>记录BASIC级别的基础之上，记录请求和响应的header、body和元数据</td></tr>
</table>

##### 局部配置 - 代码配置
步骤：
* 在代码定义相应的配置类。
```text
package com.jxj.order.service.config;

import feign.Logger;
import org.springframework.context.annotation.Bean;

/**
 * 配置类
 * 注： 如果是全局配置，类添加注解 @Configuration
 * 如果不是全局配置，类上不要添加注解 @Configuration
 */
public class UserClientConfig {

    @Bean
    public Logger.Level level(){
        return Logger.Level.FULL;
    }
}
```
* 再到feign文件中配置FeignClient接口的配置类 `configuration`。
```text
@FeignClient(name = "user-provider", configuration = UserClientConfig.class)
public interface UserClientService {
    // ... 省略
}
```
* 设置feign目录的日志级别debug。Spring Boot的配置文件进行配置（application.properties/yml）。 
```text
# 设置日志级别为debug，否则feign的日志级别配置不会生效
logging.level.com.jxj.order.service=debug
```

##### 局部配置 - 配置文件配置
步骤：
* Spring Boot的配置文件进行配置（application.properties/yml）： 设置feign目录的日志级别debug， 设置feign的微服务日志级别
```text
# 设置日志级别为debug，否则feign的日志级别配置不会生效
logging.level.com.jxj.order.service=debug
## [feign] 配置 - 特定服务提供者配置 日志级别
feign.client.config.user-provider.logger-level=full
```

##### 全局配置 - 代码配置
步骤：
* 在代码定义相应的配置类。 (同 局部配置 - 代码配置)
* 然后在启动类上的注解 `@EnableFeignClients` 配置 `defaultConfiguration` 属性
```text
@EnableFeignClients(basePackages = "com.jxj.order.service", defaultConfiguration = UserClientConfig.class)
```
* 设置feign目录的日志级别debug。Spring Boot的配置文件进行配置（application.properties/yml） （同 局部配置 - 代码配置 / 局部配置 - 配置文件配置）

##### 全局配置 - 配置文件配置
步骤：
* 设置feign目录的日志级别debug。Spring Boot的配置文件进行配置（application.properties/yml） （同 局部配置 - 代码配置 / 局部配置 - 配置文件配置）
* 设置feign的全局日志级别
```text
# 设置日志级别为debug，否则feign的日志级别配置不会生效
logging.level.com.jxj.order.service=debug
## [feign] 配置 - 全局配置 日志级别
feign.client.config.default.logger-level=basic
```

### @FeignClient
* name：指定 Feign Client 的名称，如果项目使用了 Ribbon，name 属性会作为微服务的名称，用于服务发现。
* url：url 一般用于调试，可以手动指定 @FeignClient 调用的地址。
* decode404：当发生404错误时，如果该字段为 true，会调用 decoder 进行解码，否则抛出 FeignException。
* configuration：Feign 配置类，可以自定义 Feign 的 Encoder、Decoder、LogLevel、Contract。
* fallback：定义容错的处理类，当调用远程接口失败或超时时，会调用对应接口的容错逻辑，fallback 指定的类必须实现 @FeignClient 标记的接口。
* fallbackFactory：工厂类，用于生成 fallback 类示例，通过这个属性我们可以实现每个接口通用的容错逻辑，减少重复的代码。
* path：定义当前 FeignClient 的统一前缀。

### 参考
* `https://spring.io/projects/spring-cloud-openfeign`
* `https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-feign.html`
* 配置 `https://blog.51cto.com/zero01/2424667`

* `https://blog.csdn.net/chengqiuming/article/details/80713471`
* `https://blog.csdn.net/antma/article/details/81317707`
* `https://blog.csdn.net/wo18237095579/article/details/83343915`
* `https://blog.csdn.net/qq_33363618/article/details/83048411`
* `https://blog.csdn.net/wo18237095579/article/details/83343915` 演示OK
* `https://www.jianshu.com/p/e3323e8131df`
* `https://www.jianshu.com/p/b6a47b06d3dc`
* `https://www.jianshu.com/p/5fae81b3624f`
* `https://www.jianshu.com/p/8abafab12243`
* `https://www.jianshu.com/p/59295c91dde7`
* `https://www.jianshu.com/p/8c7b92b4396c`
* `https://www.jianshu.com/p/e3f31133db85`
* `https://www.kancloud.cn/fymod/springcloud/536931`
