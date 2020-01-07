## Dubbo 使用注解配置

> Dubbo 的配置方式：
> 1. XML （Spring XML配置）
> 2. 注解 （Spring 外部驱动dubbo配置）

### 目录
* 需要 2.6.3 及以上版本支持
* [服务提供方](#服务提供方)
* [服务消费方](#服务消费方)
* [参考](#参考)

### 服务提供方
Service注解暴露服务
```text
@Service
public class AnnotationServiceImpl implements AnnotationService {
    @Override
    public String sayHello(String name) {
        return "annotation: hello, " + name;
    }
}
```

增加应用共享配置
```text
# dubbo-provider.properties
dubbo.application.name=annotation-provider
dubbo.registry.address=zookeeper://127.0.0.1:2181
dubbo.protocol.name=dubbo
dubbo.protocol.port=20880
```

指定Spring扫描路径
```text
@Configuration
@EnableDubbo(scanBasePackages = "org.apache.dubbo.samples.simple.annotation.impl")
@PropertySource("classpath:/spring/dubbo-provider.properties")
static public class ProviderConfiguration {
       
}
```

### 服务消费方
Reference注解引用服务
```text
@Component("annotationAction")
public class AnnotationAction {

    @Reference
    private AnnotationService annotationService;
    
    public String doSayHello(String name) {
        return annotationService.sayHello(name);
    }
}
```

增加应用共享配置
```text
# dubbo-consumer.properties
dubbo.application.name=annotation-consumer
dubbo.registry.address=zookeeper://127.0.0.1:2181
dubbo.consumer.timeout=3000
```

指定Spring扫描路径
```text
@Configuration
@EnableDubbo(scanBasePackages = "org.apache.dubbo.samples.simple.annotation.action")
@PropertySource("classpath:/spring/dubbo-consumer.properties")
@ComponentScan(value = {"org.apache.dubbo.samples.simple.annotation.action"})
static public class ConsumerConfiguration {

}
```

调用服务
```text
public static void main(String[] args) throws Exception {
    AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(ConsumerConfiguration.class);
    context.start();
    final AnnotationAction annotationAction = (AnnotationAction) context.getBean("annotationAction");
    String hello = annotationAction.doSayHello("world");
}
```

### 参考
* `http://dubbo.apache.org/zh-cn/docs/user/configuration/annotation.html`