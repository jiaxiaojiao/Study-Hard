## Nacos Spring Cloud

Spring Cloud 的使用者，如何使用 Nacos 来实现分布式环境下的配置管理和服务注册发现。

### 目录
* [前提条件](#前提条件)
* [配置管理](#配置管理)
* [服务注册发现](#服务注册发现)
* 答疑解惑
    * [为什么需要配置spring.application.name？](#为什么需要配置spring.application.name？)
* [参考](#参考)


### 前提条件
下载 Nacos 并启动 Nacos server。

### 配置管理
* 添加依赖。 （[版本对应关系](../Spring/Spring-Cloud/Spring-Cloud-Version.md)）
    ```text
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        <version>${latest.version}</version>
    </dependency>
    ```
* 修改配置文件。配置 Nacos server 的地址和应用名。`application.properties/yml`
```text
spring.cloud.nacos.config.server-addr=127.0.0.1:8848
spring.application.name=example
```
* 通过 Spring Cloud 原生注解 `@RefreshScope` 实现配置自动更新
```text
@RestController
@RequestMapping("/config")
@RefreshScope
public class ConfigController {

    @Value("${useLocalCache:false}")
    private boolean useLocalCache;

    @RequestMapping("/get")
    public boolean get() {
        return useLocalCache;
    }
}
```
* 示例代码： `https://github.com/nacos-group/nacos-examples/tree/master/nacos-spring-cloud-example/nacos-spring-cloud-config-example`

### 服务注册发现
* 添加依赖。
```text
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    <version>${latest.version}</version>
</dependency>
```
* 配置服务提供者。 
    * 在 `application.properties` 中配置 Nacos server 的地址
    ```text
    server.port=8070
    spring.application.name=service-provider
    
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    ```
  * 通过 Spring Cloud 原生注解 `@EnableDiscoveryClient` 开启服务注册发现功能。
    ```text
    @SpringBootApplication
    @EnableDiscoveryClient
    public class NacosProviderApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(NacosProviderApplication.class, args);
        }
    
        @RestController
        class EchoController {
            @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
            public String echo(@PathVariable String string) {
                return "Hello Nacos Discovery " + string;
            }
        }
    }
    ```
* 配置服务消费者。
    * 在 `application.properties` 中配置 Nacos server 的地址。
    ```text
    server.port=8080
    spring.application.name=service-consumer
    
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    ```
    * 通过 Spring Cloud 原生注解 @EnableDiscoveryClient 开启服务注册发现功能。
    ```text
    @SpringBootApplication
    @EnableDiscoveryClient
    public class NacosConsumerApplication {
    
        @LoadBalanced
        @Bean
        public RestTemplate restTemplate() {
            return new RestTemplate();
        }
    
        public static void main(String[] args) {
            SpringApplication.run(NacosConsumerApplication.class, args);
        }
    
        @RestController
        public class TestController {
    
            private final RestTemplate restTemplate;
    
            @Autowired
            public TestController(RestTemplate restTemplate) {this.restTemplate = restTemplate;}
    
            @RequestMapping(value = "/echo/{str}", method = RequestMethod.GET)
            public String echo(@PathVariable String str) {
                return restTemplate.getForObject("http://service-provider/echo/" + str, String.class);
            }
        }
    }
    ```
* 示例代码： `https://github.com/nacos-group/nacos-examples/tree/master/nacos-spring-cloud-example/nacos-spring-cloud-discovery-example`

### 为什么需要配置spring.application.name？
为什么配置文件里需要配置应用名 `spring.application.name`？

因为应用名是构成 Nacos 配置管理 `dataId`字段的一部分。

在 Nacos Spring Cloud 中，`dataId` 的完整格式如下：
```text
${prefix}-${spring.profile.active}.${file-extension}
``` 

* `prefix` 默认为 `spring.application.name` 的值，也可以通过配置项 `spring.cloud.nacos.config.prefix`来配置。
* `spring.profile.active` 即为当前环境对应的 profile，详情可以参考 [Spring Boot文档](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-profiles)。 注意：当 `spring.profile.active` 为空时，对应的连接符 `-` 也将不存在，dataId 的拼接格式变成 `${prefix}.${file-extension}`
* `file-exetension` 为配置内容的数据格式，可以通过配置项 `spring.cloud.nacos.config.file-extension` 来配置。目前只支持 `properties` 和 `yaml` 类型。

### 参考
* 官方文档 `https://nacos.io/zh-cn/docs/quick-start-spring-cloud.html`
* 配置管理 `https://github.com/alibaba/spring-cloud-alibaba/wiki/Nacos-config`
* 服务注册发现 `https://github.com/alibaba/spring-cloud-alibaba/wiki/Nacos-discovery`