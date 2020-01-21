## Dubbo 注册 - Nacos

> Dubbo 融合 Nacos 成为注册中心
>

### 目录
* 步骤
    * [1. 增加 Maven 依赖](#增加-Maven-依赖)
    * [2. 配置注册中心](#配置注册中心)
* [参考](#参考)

### 增加 Maven 依赖
* 添加Maven依赖 `dubbo-registry-nacos` 到 `pom.xml`。 版本：Dubbo 2.6.5+
```text
<!-- RPC - dubbo -->
<dependency>
    <groupId>com.alibaba.spring</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>1.0.5</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>2.6.7</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo-registry-nacos</artifactId>
    <version>2.6.7</version>
</dependency>
<dependency>
    <groupId>com.alibaba.nacos</groupId>
    <artifactId>nacos-client</artifactId>
    <version>1.1.4</version>
</dependency>
```
### 配置注册中心
如： Spring Boot `application.properties`
```text
# Dubbo
dubbo.application.name=user-provider
dubbo.registry.address=nacos://192.168.229.129:8848
```


### 参考
* https://github.com/apache/dubbo/tree/master/dubbo-registry/dubbo-registry-nacos
* http://dubbo.apache.org/zh-cn/docs/user/references/registry/nacos.html
* https://nacos.io/zh-cn/docs/use-nacos-with-dubbo.html
* https://github.com/ly641921791/knowledge-examples/tree/master/dubbo-example
* https://www.cnblogs.com/lanqie/p/10552500.html
* https://www.cnblogs.com/zjfjava/p/9696086.html
