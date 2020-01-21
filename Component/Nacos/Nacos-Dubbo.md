## Dubbo使用Nacos作为配置中心

### 目录
* [预备工作](#预备工作)
* [Dubbo使用Nacos](#Dubbo使用Nacos)
    * [增加 Maven 依赖](#增加-Maven-依赖)
    * [配置注册中心](#配置注册中心)
    * [接口与实现](#接口与实现)
* [参考](#参考)

### 预备工作
后台已经启动 Nacos 服务

### Dubbo使用Nacos
Dubbo 融合 Nacos 成为注册中心的操作步骤非常简单，大致步骤可分为“增加 Maven 依赖”以及“配置注册中心“。

#### 增加 Maven 依赖
Dubbo

```text
<!-- Dubbo dependency -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>[latest version]</version>
</dependency>

<!-- 使用Spring装配方式时可选: -->
<dependency>
    <groupId>com.alibaba.spring</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>[latest version]</version>
</dependency>
```

#### 配置注册中心
配置注册中心有两种方式：
* Dubbo Spring 外部化配置
* Spring XML 配置文件

##### Dubbo Spring 外部化配置
Dubbo Spring 外部化配置是由 Dubbo 2.5.8 引入的新特性，可通过 Spring `Environment` 属性自动地生成并绑定 Dubbo 配置 Bean，实现配置简化，并且降低微服务开发门槛。

```text
## application
dubbo.application.name = your-dubbo-application

## 注册中心 ZooKeeper or Nacos 配置如下
## Zookeeper registry address
dubbo.registry.address = zookeeper://10.20.153.10:2181
## Nacos registry address
dubbo.registry.address = nacos://10.20.153.10:8848
```
 
##### Spring XML 配置文件
```text
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
    xsi:schemaLocation="http://www.springframework.org/schema/beans        http://www.springframework.org/schema/beans/spring-beans-4.3.xsd        http://dubbo.apache.org/schema/dubbo        http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
 
    <!-- 提供方应用信息，用于计算依赖关系 -->
    <dubbo:application name="dubbo-provider-xml-demo"  />
 
    <!-- 配置中心 ZooKeeper or Nacos 配置如下：  -->
    <!-- 使用 Zookeeper 注册中心 -->
    <dubbo:registry address="zookeeper://10.20.153.10:2181" />
    <!-- 使用 Nacos 注册中心 -->
    <dubbo:registry address="nacos://10.20.153.10:8848" />
 	...
</beans>
```

### 接口与实现
接口实现方式有两种注解驱动和XML配置驱动。（个人习惯注解驱动，不用写XML配置文件）
* Dubbo Spring 注解驱动
* Dubbo Spring XML 配置驱动

##### Spring 注解驱动
Dubbo 2.5.7 重构了 Spring 注解驱动的编程模型。
* 服务提供方
* 服务消费方

##### 服务提供方
* 定义 Dubbo 提供方外部化配置属性源 - `provider-config.properties`
```text
## application
dubbo.application.name = dubbo-provider-demo

## Nacos registry address
dubbo.registry.address = nacos://127.0.0.1:8848

## Dubbo Protocol
dubbo.protocol.name = dubbo
dubbo.protocol.port = -1

# Provider @Service version
demo.service.version=1.0.0
demo.service.name = demoService
```

* 实现服务提供方引导类 - `DemoServiceProviderBootstrap`
```text
package com.alibaba.dubbo.demo.provider;

import com.alibaba.dubbo.config.spring.context.annotation.EnableDubbo;
import com.alibaba.dubbo.demo.service.DemoService;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.PropertySource;

import java.io.IOException;

/**
 * {@link DemoService} provider demo
 */
@EnableDubbo(scanBasePackages = "com.alibaba.dubbo.demo.service")
@PropertySource(value = "classpath:/provider-config.properties")
public class DemoServiceProviderBootstrap {

    public static void main(String[] args) throws IOException {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(DemoServiceProviderBootstrap.class);
        context.refresh();
        System.out.println("DemoService provider is starting...");
        System.in.read();
    }
}
```

其中注解 `@EnableDubbo` 激活 Dubbo 注解驱动以及外部化配置，其 `scanBasePackages` 属性扫描指定 Java 包，将所有标注 `@Service` 的服务接口实现类暴露为 Spring Bean，随即被导出 Dubbo 服务。

`@PropertySource` 是 Spring Framework 3.1 引入的标准导入属性配置资源注解，它将为 Dubbo 提供外部化配置。

##### 服务消费方
* 定义 Dubbo 消费方外部化配置属性源 - `consumer-config.properties`
```text
## Dubbo Application info
dubbo.application.name = dubbo-consumer-demo

## Nacos registry address
dubbo.registry.address = nacos://127.0.0.1:8848

# @Reference version
demo.service.version= 1.0.0
```

同样地，dubbo.registry.address 属性指向 Nacos 注册中心，其他 Dubbo 服务相关的元信息通过 Nacos 注册中心获取。

* 实现服务消费方引导类 - `DemoServiceConsumerBootstrap`
```text
package com.alibaba.dubbo.demo.consumer;

import com.alibaba.dubbo.config.annotation.Reference;
import com.alibaba.dubbo.config.spring.context.annotation.EnableDubbo;
import com.alibaba.dubbo.demo.service.DemoService;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.PropertySource;

import javax.annotation.PostConstruct;
import java.io.IOException;

/**
 * {@link DemoService} consumer demo
 */
@EnableDubbo
@PropertySource(value = "classpath:/consumer-config.properties")
public class DemoServiceConsumerBootstrap {

    @Reference(version = "${demo.service.version}")
    private DemoService demoService;

    @PostConstruct
    public void init() {
        for (int i = 0; i < 10; i++) {
            System.out.println(demoService.sayName("小马哥（mercyblitz）"));
        }
    }

    public static void main(String[] args) throws IOException {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(DemoServiceConsumerBootstrap.class);
        context.refresh();
        context.close();
    }
}
```

同样地，`@EnableDubbo` 注解激活 Dubbo 注解驱动和外部化配置，不过当前属于服务消费者，无需指定 Java 包名扫描标注 `@Service` 的服务实现。

`@Reference `是 Dubbo 远程服务的依赖注入注解，需要服务提供方和消费端约定接口（interface）、版本（version）以及分组（group）信息。在当前服务消费示例中，`DemoService` 的服务版本来源于属性配置文件 `consumer-config.properties。`

`@PostConstruct` 部分代码则说明当 `DemoServiceConsumerBootstrap` Bean 初始化时，执行十次 Dubbo 远程方法调用。

### 参考
* https://nacos.io/zh-cn/docs/use-nacos-with-dubbo.html