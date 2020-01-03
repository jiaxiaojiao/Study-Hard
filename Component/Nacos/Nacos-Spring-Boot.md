## Spring Boot 使用Nacos，来实现分布式环境下的配置管理和服务发现。


### 目录
* [前提条件](#前提条件)
* [Spring Boot 使用 Nacos](#Spring-Boot-使用-Nacos)
    * [配置管理](#配置管理)
    * [服务发现](#服务发现)
* [参考](#参考)

### 前提条件
* 已经下载并启动Nacos Server。 这里用的是[Docker安装单机Nacos](Nacos-Install-single.md#单机模式部署Nacos)

### Spring Boot 使用 Nacos

#### 配置管理
* `pom.xml` 添加依赖
    ```text
    <dependency>
        <groupId>com.alibaba.boot</groupId>
        <artifactId>nacos-config-spring-boot-starter</artifactId>
        <version>${latest.version}</version>
    </dependency>
    ```
    * 注意：版本 0.2.x.RELEASE 对应的是 Spring Boot 2.x 版本，版本 0.1.x.RELEASE 对应的是 Spring Boot 1.x 版本。
* 在 `application.properties` 中配置 Nacos server 的地址： `nacos.config.server-addr=127.0.0.1:8848`
* 修改启动项。使用 `@NacosPropertySource` 加载 `dataId` 为 `example` 的配置源，并开启自动更新。
    ```text
    @SpringBootApplication
    @NacosPropertySource(dataId = "example", autoRefreshed = true)
    public class NacosConfigApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(NacosConfigApplication.class, args);
        }
    }
    ```
* 通过 Nacos 的 `@NacosValue` 注解设置属性值。
    ```text
    @Controller
    @RequestMapping("config")
    public class ConfigController {
    
        @NacosValue(value = "${useLocalCache:false}", autoRefreshed = true)
        private boolean useLocalCache;
    
        @RequestMapping(value = "/get", method = GET)
        @ResponseBody
        public boolean get() {
            return useLocalCache;
        }
    }
    ```
* 启动 `NacosConfigApplication`，调用 `curl http://localhost:8080/config/get`，返回内容是 `false`。
* 通过调用 Nacos Open API 向 Nacos server 发布配置：dataId `为example`，内容为`useLocalCache=true`
`curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=example&group=DEFAULT_GROUP&content=useLocalCache=true"`
* 再次访问 `http://localhost:8080/config/get`，此时返回内容为`true`，说明程序中的`useLocalCache`值已经被动态更新了。

#### 服务发现
* 添加依赖
    ```text
    <dependency>
        <groupId>com.alibaba.boot</groupId>
        <artifactId>nacos-discovery-spring-boot-starter</artifactId>
        <version>${latest.version}</version>
    </dependency>
    ```
    * 注意：版本 0.2.x.RELEASE 对应的是 Spring Boot 2.x 版本，版本 0.1.x.RELEASE 对应的是 Spring Boot 1.x 版本。
* 在 application.properties 中配置 Nacos server 的地址： `nacos.discovery.server-addr=127.0.0.1:8848`
* 使用 `@NacosInjected` 注入 Nacos 的 `NamingService` 实例：
    ```text
    @Controller
    @RequestMapping("discovery")
    public class DiscoveryController {
    
        @NacosInjected
        private NamingService namingService;
    
        @RequestMapping(value = "/get", method = GET)
        @ResponseBody
        public List<Instance> get(@RequestParam String serviceName) throws NacosException {
            return namingService.getAllInstances(serviceName);
        }
    }
    ```
* 启动 `NacosDiscoveryApplication`，调用 `curl http://localhost:8080/discovery/get?serviceName=example`，此时返回为空 JSON 数组`[]`
* 通过调用 Nacos Open API 向 Nacos server 注册一个名称为 `example` 服务: `curl -X PUT 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=example&ip=127.0.0.1&port=8080'`
* 再次访问 curl http://localhost:8080/discovery/get?serviceName=example，此时返回内容为：
    ```text
    [
      {
        "instanceId": "127.0.0.1-8080-DEFAULT-example",
        "ip": "127.0.0.1",
        "port": 8080,
        "weight": 1.0,
        "healthy": true,
        "cluster": {
          "serviceName": null,
          "name": "",
          "healthChecker": {
            "type": "TCP"
          },
          "defaultPort": 80,
          "defaultCheckPort": 80,
          "useIPPort4Check": true,
          "metadata": {}
        },
        "service": null,
        "metadata": {}
      }
    ]
    ```



### 参考
* ``