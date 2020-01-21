## Feign 使用 Nacos 作为注册中心

> 使用feign 进行远程调用、熔断、负载均衡

### 目录
* [# 前提条件](##-前提条件)
* [# 服务提供者](##-服务提供者)
* [# 服务消费者](##-服务消费者)
* [# 负载均衡](##-负载均衡)
* [遇到的问题](#遇到的问题)
* [参考](#参考)

### # 前提条件
启动注册中心 Nacos
```text
位置：【本地虚拟机VM-4】
已启动，路径： http://192.168.229.129:8848/nacos
```

### # 服务提供者
需要做： 将应用注册到Nacos，Controller 暴露接口。

步骤：
1. `pom.xml` 文件添加 `...nacos-discovery` 依赖
    ```text
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        <version>0.9.0.RELEASE</version>
    </dependency>
    ```
2. 启动类 开启服务注册发现功能 `@EnableDiscoveryClient` 
3. 配置文件 `application.properties/yml` 添加应用名称和Nacos注册地址
    ```text
    # 应用名称 - [feign]通过应用名称调用
    spring.application.name=user-provider
    # [feign] 注册到Nacos
    spring.cloud.nacos.discovery.server-addr=192.168.229.129:8848
    ```
4. `Controller` 暴露入口。（正常Controller的写法）

### # 服务消费者
需要做： 将应用注册到Nacos，通过feign远程调用 `user-provider` 应用的接口，feign远程调用的熔断和降级处理。等等

步骤： 
1. pom.xml 文件添加依赖 `...nacos-discovery` 、 `spring-cloud-starter-openfeign`
    ```text
    <!-- feign -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    </dependency>
    ```
2. 启动类 开启服务注册发现功能 `@EnableDiscoveryClient` 、开启OpenFeign `@EnableFeignClients`
3. 配置文件 `application.properties/yml` 添加应用名称和Nacos注册地址、
    ```text
    # 应用名称
    spring.application.name=user-consumer
    # feign
    ## [feign] 注册中心 - nacos
    spring.cloud.nacos.discovery.server-addr=192.168.229.129:8848
    ## [feign] 配置 - 是否开启断路器
    feign.hystrix.enabled=true
    feign.okhttp.enabled=false
    feign.httpclient.enabled=false
    ```
4. 通过feign远程调用 `user-provider`应用的接口，`fallback` 指定 `UserClientFallback` 类来进行远程调用的熔断和降级处理。
    ```text
    package com.jxj.order.service;
    
    import com.jxj.order.service.fallback.UserClientFallback;
    import org.springframework.cloud.openfeign.FeignClient;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @FeignClient(name = "user-provider", fallback = UserClientFallback.class)
    public interface UserClientService {
        @GetMapping(value = "/user/list")
        String list();
    }
    ```
5. 熔断和降级处理
    ```text
    package com.jxj.order.service.fallback;
    
    import com.jxj.order.service.UserClientService;
    import org.springframework.stereotype.Component;
    
    @Component
    public class UserClientFallback implements UserClientService {
        @Override
        public String list() {
            return "我出错了！";
        }
    }
    ```
6. Controller 验证， 通过feign远程调用、熔断、降级。
    ```text
    @RestController
    public class Consumer2Controller {
    
        @Autowired
        private UserClientService userClientService;
    
        @GetMapping("/consumer2")
        public String consumer2(){
            return userClientService.list();
        }
    }
    ```

### # 负载均衡
负载均衡： 负载均衡可以将工作任务分摊到多个处理单元，从而提高并发处理能力。 [更多关于负载均衡的描述](../../../Architecture/Load-Balance.md)

需要做： 启动多个服务提供者 `user-provider`， 测试负载均衡效果（服务提供者的接口中可以标记本服务的端口等）

效果： 启动了两个服务提供者，调用超时显示 "我出错了！"， 调用成功交替form两个应用。

### 遇到的问题

### 参考
* Nacos作为配置中心 https://www.bbsmax.com/A/x9J2P1rgd6/
* https://www.larscheng.com/namingservice/
* https://www.larscheng.com/nacos-openfeign/
* https://www.cnblogs.com/wuxun1997/p/11392772.html
* https://www.jianshu.com/p/98e916e825bc
* https://www.jianshu.com/p/cde9447fa21d

偶然发现不错的博客：
* https://removeif.github.io/
* https://www.larscheng.com/
