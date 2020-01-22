## DUBBO Spring Cloud
Spring Cloud 使用Dubbo。

### 目录
* [服务提供方](#服务提供方)
    * [定义 Dubbo 服务接口](#定义-Dubbo-服务接口)
    * [实现 Dubbo 服务提供方](#实现-Dubbo-服务提供方)
    * [配置 Dubbo 服务提供方](#配置-Dubbo-服务提供方)
    * [引导 Dubbo Spring Cloud 服务提供方应用](#引导-Dubbo-Spring-Cloud-服务提供方应用)
* [服务消费方](#服务消费方)
    * [消费 Dubbo 接口](#消费-Dubbo-接口)
    * [配置 Dubbo 服务消费方](#配置-Dubbo-服务消费方)
    * [引导 Dubbo Spring Cloud 服务消费方应用](#引导-Dubbo-Spring-Cloud-服务消费方应用)
* [参考](#参考)

### 服务提供方

#### 定义 Dubbo 服务接口
定义 Dubbo 服务接口。服务接口 `interface` 打包jar包中。 Dubbo 服务接口是服务提供方与消费方的远程通讯契约，通常由普通的 Java 接口（interface）来声明。

#### 实现 Dubbo 服务提供方
实现 Dubbo 服务提供方。 
* 依赖 定义好的服务接口。
* 依赖 `Dubbo Spring Cloud Starter`
```text
<!-- Dubbo Spring Cloud Starter -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-dubbo</artifactId>
</dependency>
```
* 依赖 Spring Boot dependencies
```text
<!-- Spring Boot dependencies -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-actuator</artifactId>
</dependency>

或者starter，我测试没有问题。
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
* 依赖 注册中心（注册服务） Spring Cloud Nacos Service Discovery
```text
<!-- Spring Cloud Nacos Service Discovery -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```
* 指定 依赖的版本
```text
<properties>
    <spring.cloud.alibaba.version>2.1.0.RELEASE</spring.cloud.alibaba.version>
</properties>
<dependencyManagement>
    <dependencies>
        <!-- Spring Cloud Alibaba dependencies -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-alibaba-dependencies</artifactId>
            <version>${spring.cloud.alibaba.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```
* 实现 `implements` 服务接口。`@org.apache.dubbo.config.annotation.Service` 是 Dubbo 服务注解，声明该 Java 服务（本地）实现为 Dubbo 服务。
```text
@org.apache.dubbo.config.annotation.Service
class EchoServiceImpl implements EchoService {

    @Override
    public String echo(String message) {
        return "[echo] Hello, " + message;
    }
}
```

#### 配置 Dubbo 服务提供方
暴露 Dubbo 服务配置方式有两种： xml 和 外部化配置。 推荐外部化配置的方式，即指定 Java 服务实现类的扫描基准包。

> Dubbo Spring Cloud 继承了 Dubbo Spring Boot 的外部化配置特性，也可以通过标注 @DubboComponentScan 来实现基准包扫描。

Dubbo 远程服务需要暴露网络端口，并设定通讯协议，完整的 YAML 配置如下所示：
```yaml
dubbo:
  scan:
    # dubbo 服务扫描基准包。 指定 Dubbo 服务实现类的扫描基准包
    base-packages: com.alibaba.cloud.dubbo.bootstrap
  protocol:
    # dubbo 协议。 Dubbo 服务暴露的协议配置，其中子属性 name 为协议名称，port 为协议端口（ -1 表示自增端口，从 20880 开始）
    name: dubbo
    # dubbo 协议端口（ -1 表示自增端口，从 20880 开始）
    port: -1
  registry:
    # 挂载到 Spring Cloud 注册中心。 Dubbo 服务注册中心配置，其中子属性 address 的值 "spring-cloud://localhost"，说明挂载到 Spring Cloud 注册中心
    address: spring-cloud://localhost
    
#  Spring Cloud 相关配置
spring:
  application:
    # 应用名称。 Spring 应用名称，用于 Spring Cloud 服务注册和发现。
    name: spring-cloud-alibaba-dubbo-server
  main:
    # Spring Boot 2.1 需要设定。  在 Spring Boot 2.1 以及更高的版本增加该设定， 因为 Spring Boot 默认调整了 Bean 定义覆盖行为。
    allow-bean-definition-overriding: true
  cloud:
    nacos:
      # Nacos 服务发现与注册配置。 Nacos 服务发现与注册配置，其中子属性 server-addr 指定 Nacos 服务器主机和端口
      discovery:
        server-addr: 127.0.0.1:8848
```

#### 引导 Dubbo Spring Cloud 服务提供方应用
```text
@EnableDiscoveryClient
@EnableAutoConfiguration
public class DubboSpringCloudServerBootstrap {

    public static void main(String[] args) {
        SpringApplication.run(DubboSpringCloudServerBootstrap.class);
    }
}
```

### 服务消费方

#### 消费 Dubbo 接口
* 依赖 定义好的服务接口。
* 依赖 `Dubbo Spring Cloud Starter`
```text
<!-- Dubbo Spring Cloud Starter -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-dubbo</artifactId>
</dependency>
```
* 依赖 Spring Boot dependencies
```text
<!-- Spring Boot dependencies -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-actuator</artifactId>
</dependency>

或者starter，我测试没有问题。
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
* 依赖 注册中心（注册服务） Spring Cloud Nacos Service Discovery
```text
<!-- Spring Cloud Nacos Service Discovery -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```
* 指定 依赖的版本
```text
<properties>
    <spring.cloud.alibaba.version>2.1.0.RELEASE</spring.cloud.alibaba.version>
</properties>
<dependencyManagement>
    <dependencies>
        <!-- Spring Cloud Alibaba dependencies -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-alibaba-dependencies</artifactId>
            <version>${spring.cloud.alibaba.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

#### 配置 Dubbo 服务消费方
```yaml
dubbo:
  registry:
    # 挂载到 Spring Cloud 注册中心
    address: spring-cloud://localhost
  cloud:
    subscribed-services: spring-cloud-alibaba-dubbo-server
    
spring:
  application:
    # Dubbo 应用名称
    name: spring-cloud-alibaba-dubbo-client
  main:
    # Spring Boot 2.1 需要设定
    allow-bean-definition-overriding: true
  cloud:
    nacos:
      # Nacos 服务发现与注册配置
      discovery:
        server-addr: 127.0.0.1:8848
```

#### 引导 Dubbo Spring Cloud 服务消费方应用
为了减少实现步骤，以下引导类将 Dubbo 服务消费以及引导功能合二为一：

```text
@EnableDiscoveryClient
@EnableAutoConfiguration
@RestController
public class DubboSpringCloudClientBootstrap {

    @Reference
    private EchoService echoService;

    @GetMapping("/echo")
    public String echo(String message) {
        return echoService.echo(message);
    }

    public static void main(String[] args) {
        SpringApplication.run(DubboSpringCloudClientBootstrap.class);
    }
}
```


### 参考
* Dubbo Spring Cloud 示例工程： https://github.com/alibaba/spring-cloud-alibaba/blob/master/spring-cloud-alibaba-examples/spring-cloud-alibaba-dubbo-examples/README_CN.md