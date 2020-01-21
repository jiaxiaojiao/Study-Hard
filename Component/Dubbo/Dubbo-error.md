## Dubbo 遇到的异常

### 目录
* [java.net.BindException: Address already in use: bind](#BindException)
* [参考](#参考)


### BindException
consumer 工程启动时报异常： 
* `[DUBBO] qos-server can not bind localhost:22222`
* `java.net.BindException: Address already in use: bind`
* `[DUBBO] Fail to start qos server`

```text
"C:\Program Files\Java\jdk1.8.0_221\bin\java.exe" -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:62882,suspend=y,server=n -XX:TieredStopAtLevel=1 -noverify -Dspring.output.ansi.enabled=always -Dcom.sun.management.jmxremote -Dspring.jmx.enabled=true -Dspring.liveBeansView.mbeanDomain -Dspring.application.admin.enabled=true -javaagent:C:\Users\Administrator.JRA1W1PF0YQU5F\.IntelliJIdea2019.3\system\captureAgent\debugger-agent.jar -Dfile.encoding=UTF-8 -classpath "C:\Program Files\Java\jdk1.8.0_221\jre\lib\charsets.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\deploy.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\access-bridge-64.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\cldrdata.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\dnsns.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\jaccess.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\jfxrt.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\localedata.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\nashorn.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\sunec.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\sunjce_provider.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\sunmscapi.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\sunpkcs11.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\ext\zipfs.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\javaws.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\jce.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\jfr.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\jfxswt.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\jsse.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\management-agent.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\plugin.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\resources.jar;C:\Program Files\Java\jdk1.8.0_221\jre\lib\rt.jar;D:\IdeaProjects\Study-SpringBoot\ordercenter\order-web\target\classes;D:\IdeaProjects\Study-SpringBoot\ordercenter\order-entity\target\classes;D:\IdeaProjects\Study-SpringBoot\ordercenter\order-service\target\classes;D:\IdeaProjects\Study-SpringBoot\ordercenter\order-dao\target\classes;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\mybatis\spring\boot\mybatis-spring-boot-starter\2.1.1\mybatis-spring-boot-starter-2.1.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-jdbc\2.2.2.RELEASE\spring-boot-starter-jdbc-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\zaxxer\HikariCP\3.4.1\HikariCP-3.4.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-jdbc\5.2.2.RELEASE\spring-jdbc-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-tx\5.2.2.RELEASE\spring-tx-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\mybatis\spring\boot\mybatis-spring-boot-autoconfigure\2.1.1\mybatis-spring-boot-autoconfigure-2.1.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\mybatis\mybatis\3.5.3\mybatis-3.5.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\mybatis\mybatis-spring\2.0.3\mybatis-spring-2.0.3.jar;D:\IdeaProjects\Study-SpringBoot\ordercenter\order-openapi\target\classes;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\fastjson\1.2.60\fastjson-1.2.60.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\jxj\user-openapi\0.0.1-SNAPSHOT\user-openapi-0.0.1-SNAPSHOT.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-web\2.2.2.RELEASE\spring-boot-starter-web-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter\2.2.2.RELEASE\spring-boot-starter-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot\2.2.2.RELEASE\spring-boot-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-autoconfigure\2.2.2.RELEASE\spring-boot-autoconfigure-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-logging\2.2.2.RELEASE\spring-boot-starter-logging-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\ch\qos\logback\logback-classic\1.2.3\logback-classic-1.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\ch\qos\logback\logback-core\1.2.3\logback-core-1.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\logging\log4j\log4j-to-slf4j\2.12.1\log4j-to-slf4j-2.12.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\logging\log4j\log4j-api\2.12.1\log4j-api-2.12.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\slf4j\jul-to-slf4j\1.7.29\jul-to-slf4j-1.7.29.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\jakarta\annotation\jakarta.annotation-api\1.3.5\jakarta.annotation-api-1.3.5.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-core\5.2.2.RELEASE\spring-core-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-jcl\5.2.2.RELEASE\spring-jcl-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\yaml\snakeyaml\1.25\snakeyaml-1.25.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-json\2.2.2.RELEASE\spring-boot-starter-json-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\datatype\jackson-datatype-jdk8\2.10.1\jackson-datatype-jdk8-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\datatype\jackson-datatype-jsr310\2.10.1\jackson-datatype-jsr310-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\module\jackson-module-parameter-names\2.10.1\jackson-module-parameter-names-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-tomcat\2.2.2.RELEASE\spring-boot-starter-tomcat-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\tomcat\embed\tomcat-embed-core\9.0.29\tomcat-embed-core-9.0.29.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\tomcat\embed\tomcat-embed-el\9.0.29\tomcat-embed-el-9.0.29.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\tomcat\embed\tomcat-embed-websocket\9.0.29\tomcat-embed-websocket-9.0.29.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\boot\spring-boot-starter-validation\2.2.2.RELEASE\spring-boot-starter-validation-2.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\jakarta\validation\jakarta.validation-api\2.0.1\jakarta.validation-api-2.0.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\hibernate\validator\hibernate-validator\6.0.18.Final\hibernate-validator-6.0.18.Final.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\jboss\logging\jboss-logging\3.4.1.Final\jboss-logging-3.4.1.Final.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\classmate\1.5.1\classmate-1.5.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-web\5.2.2.RELEASE\spring-web-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-beans\5.2.2.RELEASE\spring-beans-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-webmvc\5.2.2.RELEASE\spring-webmvc-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-aop\5.2.2.RELEASE\spring-aop-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-expression\5.2.2.RELEASE\spring-expression-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\mysql\mysql-connector-java\8.0.18\mysql-connector-java-8.0.18.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\boot\nacos-config-spring-boot-starter\0.2.3\nacos-config-spring-boot-starter-0.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\nacos\nacos-spring-context\0.3.3\nacos-spring-context-0.3.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\javax\annotation\javax.annotation-api\1.3.2\javax.annotation-api-1.3.2.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\boot\nacos-config-spring-boot-autoconfigure\0.2.3\nacos-config-spring-boot-autoconfigure-0.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\boot\nacos-spring-boot-base\0.2.3\nacos-spring-boot-base-0.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\boot\nacos-discovery-spring-boot-starter\0.2.3\nacos-discovery-spring-boot-starter-0.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\boot\nacos-discovery-spring-boot-autoconfigure\0.2.3\nacos-discovery-spring-boot-autoconfigure-0.2.3.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\spring\spring-context-support\1.0.5\spring-context-support-1.0.5.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\dubbo\2.6.7\dubbo-2.6.7.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\springframework\spring-context\5.2.2.RELEASE\spring-context-5.2.2.RELEASE.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\javassist\javassist\3.20.0-GA\javassist-3.20.0-GA.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\jboss\netty\netty\3.2.5.Final\netty-3.2.5.Final.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\dubbo-registry-nacos\2.6.7\dubbo-registry-nacos-2.6.7.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\nacos\nacos-client\1.1.4\nacos-client-1.1.4.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\nacos\nacos-common\1.1.4\nacos-common-1.1.4.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\slf4j\slf4j-api\1.7.29\slf4j-api-1.7.29.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\commons-io\commons-io\2.2\commons-io-2.2.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\apache\commons\commons-lang3\3.9\commons-lang3-3.9.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\alibaba\nacos\nacos-api\1.1.4\nacos-api-1.1.4.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\google\guava\guava\22.0\guava-22.0.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\google\code\findbugs\jsr305\1.3.9\jsr305-1.3.9.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\google\errorprone\error_prone_annotations\2.0.18\error_prone_annotations-2.0.18.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\google\j2objc\j2objc-annotations\1.1\j2objc-annotations-1.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\org\codehaus\mojo\animal-sniffer-annotations\1.14\animal-sniffer-annotations-1.14.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\commons-codec\commons-codec\1.13\commons-codec-1.13.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\core\jackson-core\2.10.1\jackson-core-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\core\jackson-databind\2.10.1\jackson-databind-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\com\fasterxml\jackson\core\jackson-annotations\2.10.1\jackson-annotations-2.10.1.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\io\prometheus\simpleclient\0.5.0\simpleclient-0.5.0.jar;C:\Users\Administrator.JRA1W1PF0YQU5F\.m2\repository\io\netty\netty-all\4.1.44.Final\netty-all-4.1.44.Final.jar;D:\Program Files\JetBrains\IntelliJ IDEA 2019.2\lib\idea_rt.jar" com.jxj.order.OrderWebApplication
Connected to the target VM, address: '127.0.0.1:0', transport: 'socket'

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.2.RELEASE)

2020-01-07 10:17:14.387  INFO 21432 --- [           main] NacosConfigApplicationContextInitializer : [Nacos Config Boot] : The preload configuration is not enabled
2020-01-07 10:17:14.401  INFO 21432 --- [           main] com.jxj.order.OrderWebApplication        : Starting OrderWebApplication on JRA1W1PF0YQU5F with PID 21432 (D:\IdeaProjects\Study-SpringBoot\ordercenter\order-web\target\classes started by 贾晓娇 in D:\IdeaProjects\Study-SpringBoot\ordercenter)
2020-01-07 10:17:14.402  INFO 21432 --- [           main] com.jxj.order.OrderWebApplication        : No active profile set, falling back to default profiles: default
2020-01-07 10:17:15.686  INFO 21432 --- [           main] .a.d.c.s.c.a.DubboConfigBindingRegistrar : The dubbo config bean definition [name : com.alibaba.dubbo.config.ApplicationConfig#0, class : com.alibaba.dubbo.config.ApplicationConfig] has been registered.
2020-01-07 10:17:15.687  INFO 21432 --- [           main] .a.d.c.s.c.a.DubboConfigBindingRegistrar : The BeanPostProcessor bean definition [com.alibaba.dubbo.config.spring.beans.factory.annotation.DubboConfigBindingBeanPostProcessor] for dubbo config bean [name : com.alibaba.dubbo.config.ApplicationConfig#0] has been registered.
2020-01-07 10:17:15.688  INFO 21432 --- [           main] .a.d.c.s.c.a.DubboConfigBindingRegistrar : The dubbo config bean definition [name : com.alibaba.dubbo.config.RegistryConfig#0, class : com.alibaba.dubbo.config.RegistryConfig] has been registered.
2020-01-07 10:17:15.688  INFO 21432 --- [           main] .a.d.c.s.c.a.DubboConfigBindingRegistrar : The BeanPostProcessor bean definition [com.alibaba.dubbo.config.spring.beans.factory.annotation.DubboConfigBindingBeanPostProcessor] for dubbo config bean [name : com.alibaba.dubbo.config.RegistryConfig#0] has been registered.
2020-01-07 10:17:15.710  INFO 21432 --- [           main] c.a.dubbo.common.logger.LoggerFactory    : using logger: com.alibaba.dubbo.common.logger.slf4j.Slf4jLoggerAdapter
2020-01-07 10:17:15.720  INFO 21432 --- [           main] b.f.a.ServiceAnnotationBeanPostProcessor :  [DUBBO] BeanNameGenerator bean can't be found in BeanFactory with name [org.springframework.context.annotation.internalConfigurationBeanNameGenerator], dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:15.720  INFO 21432 --- [           main] b.f.a.ServiceAnnotationBeanPostProcessor :  [DUBBO] BeanNameGenerator will be a instance of org.springframework.context.annotation.AnnotationBeanNameGenerator , it maybe a potential problem on bean name generation., dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:15.733  WARN 21432 --- [           main] b.f.a.ServiceAnnotationBeanPostProcessor :  [DUBBO] No Spring Bean annotating Dubbo's @Service was found under package[com.jxj.order], dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:16.119  INFO 21432 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.transaction.annotation.ProxyTransactionManagementConfiguration' of type [org.springframework.transaction.annotation.ProxyTransactionManagementConfiguration] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2020-01-07 10:17:16.702  INFO 21432 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8081 (http)
2020-01-07 10:17:16.715  INFO 21432 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2020-01-07 10:17:16.715  INFO 21432 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.29]
2020-01-07 10:17:16.920  INFO 21432 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2020-01-07 10:17:16.921  INFO 21432 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 2363 ms
2020-01-07 10:17:17.680  WARN 21432 --- [           main] c.a.d.c.s.e.SpringExtensionFactory       :  [DUBBO] No spring extension (bean) named:defaultCompiler, try to find an extension (bean) of type java.lang.String, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:17.680  WARN 21432 --- [           main] c.a.d.c.s.e.SpringExtensionFactory       :  [DUBBO] No spring extension (bean) named:defaultCompiler, type:java.lang.String found, stop get bean., dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:17.975  INFO 21432 --- [           main] .f.a.DubboConfigBindingBeanPostProcessor : The properties of bean [name : com.alibaba.dubbo.config.ApplicationConfig#0] have been binding by prefix of configuration properties : dubbo.application
2020-01-07 10:17:17.980  INFO 21432 --- [           main] .f.a.DubboConfigBindingBeanPostProcessor : The properties of bean [name : com.alibaba.dubbo.config.RegistryConfig#0] have been binding by prefix of configuration properties : dubbo.registry
2020-01-07 10:17:17.981  INFO 21432 --- [           main] c.a.d.c.s.b.f.a.ReferenceBeanBuilder     : The bean[type:ReferenceBean] has been built.
2020-01-07 10:17:18.789 ERROR 21432 --- [           main] com.alibaba.dubbo.qos.server.Server      :  [DUBBO] qos-server can not bind localhost:22222, dubbo version: 2.6.7, current host: 192.168.229.1

java.net.BindException: Address already in use: bind
	at sun.nio.ch.Net.bind0(Native Method) ~[na:1.8.0_221]
	at sun.nio.ch.Net.bind(Net.java:433) ~[na:1.8.0_221]
	at sun.nio.ch.Net.bind(Net.java:425) ~[na:1.8.0_221]
	at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223) ~[na:1.8.0_221]
	at io.netty.channel.socket.nio.NioServerSocketChannel.doBind(NioServerSocketChannel.java:134) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannel$AbstractUnsafe.bind(AbstractChannel.java:550) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.DefaultChannelPipeline$HeadContext.bind(DefaultChannelPipeline.java:1334) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannelHandlerContext.invokeBind(AbstractChannelHandlerContext.java:504) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannelHandlerContext.bind(AbstractChannelHandlerContext.java:489) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.DefaultChannelPipeline.bind(DefaultChannelPipeline.java:973) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannel.bind(AbstractChannel.java:248) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.bootstrap.AbstractBootstrap$2.run(AbstractBootstrap.java:348) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.AbstractEventExecutor.safeExecute$$$capture(AbstractEventExecutor.java:164) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.AbstractEventExecutor.safeExecute(AbstractEventExecutor.java) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.SingleThreadEventExecutor.runAllTasks(SingleThreadEventExecutor.java:472) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.nio.NioEventLoop.run(NioEventLoop.java:500) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.SingleThreadEventExecutor$4.run(SingleThreadEventExecutor.java:989) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.internal.ThreadExecutorMap$2.run(ThreadExecutorMap.java:74) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at java.lang.Thread.run(Thread.java:748) ~[na:1.8.0_221]

2020-01-07 10:17:18.790  WARN 21432 --- [           main] c.a.d.qos.protocol.QosProtocolWrapper    :  [DUBBO] Fail to start qos server: , dubbo version: 2.6.7, current host: 192.168.229.1

java.net.BindException: Address already in use: bind
	at sun.nio.ch.Net.bind0(Native Method) ~[na:1.8.0_221]
	at sun.nio.ch.Net.bind(Net.java:433) ~[na:1.8.0_221]
	at sun.nio.ch.Net.bind(Net.java:425) ~[na:1.8.0_221]
	at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223) ~[na:1.8.0_221]
	at io.netty.channel.socket.nio.NioServerSocketChannel.doBind(NioServerSocketChannel.java:134) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannel$AbstractUnsafe.bind(AbstractChannel.java:550) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.DefaultChannelPipeline$HeadContext.bind(DefaultChannelPipeline.java:1334) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannelHandlerContext.invokeBind(AbstractChannelHandlerContext.java:504) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannelHandlerContext.bind(AbstractChannelHandlerContext.java:489) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.DefaultChannelPipeline.bind(DefaultChannelPipeline.java:973) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.AbstractChannel.bind(AbstractChannel.java:248) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.bootstrap.AbstractBootstrap$2.run(AbstractBootstrap.java:348) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.AbstractEventExecutor.safeExecute$$$capture(AbstractEventExecutor.java:164) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.AbstractEventExecutor.safeExecute(AbstractEventExecutor.java) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.SingleThreadEventExecutor.runAllTasks(SingleThreadEventExecutor.java:472) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.channel.nio.NioEventLoop.run(NioEventLoop.java:500) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.SingleThreadEventExecutor$4.run(SingleThreadEventExecutor.java:989) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.internal.ThreadExecutorMap$2.run(ThreadExecutorMap.java:74) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30) ~[netty-all-4.1.44.Final.jar:4.1.44.Final]
	at java.lang.Thread.run(Thread.java:748) ~[na:1.8.0_221]

2020-01-07 10:17:18.933  INFO 21432 --- [           main] c.a.dubbo.registry.nacos.NacosRegistry   :  [DUBBO] Load registry store file C:\Users\Administrator.JRA1W1PF0YQU5F\.dubbo\dubbo-registry-consumer-usercenter-192.168.229.129:8848.cache, data: {com.jxj.user.openapi.OpenUserService:1.0.0=dubbo://192.168.229.1:20880?anyhost=true&application=provider-usercenter&bean.name=ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0&category=providers&dubbo=2.0.2&generic=false&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=37404&protocol=dubbo&revision=1.0.0&side=provider&timestamp=1578302663300&version=1.0.0}, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:18.963  INFO 21432 --- [           main] c.a.dubbo.registry.nacos.NacosRegistry   :  [DUBBO] Register: consumer://192.168.229.1/com.jxj.user.openapi.OpenUserService?application=consumer-usercenter&category=consumers&check=false&dubbo=2.0.2&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=21432&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1578363437987&version=1.0.0, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.265  INFO 21432 --- [           main] c.a.dubbo.registry.nacos.NacosRegistry   :  [DUBBO] Subscribe: consumer://192.168.229.1/com.jxj.user.openapi.OpenUserService?application=consumer-usercenter&category=providers,configurators,routers&dubbo=2.0.2&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=21432&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1578363437987&version=1.0.0, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.295  INFO 21432 --- [           main] c.a.dubbo.registry.nacos.NacosRegistry   : The URLs[size : 1] are about to be notified from instances : [{"clusterName":"DEFAULT","enabled":true,"ephemeral":true,"healthy":true,"instanceHeartBeatInterval":5000,"instanceHeartBeatTimeOut":15000,"instanceId":"192.168.229.1#20880#DEFAULT#DEFAULT_GROUP@@providers:com.jxj.user.openapi.OpenUserService:1.0.0","ip":"192.168.229.1","ipDeleteTimeout":30000,"metadata":{"side":"provider","methods":"getUser","dubbo":"2.0.2","pid":"37404","interface":"com.jxj.user.openapi.OpenUserService","version":"1.0.0","generic":"false","revision":"1.0.0","protocol":"dubbo","application":"provider-usercenter","category":"providers","anyhost":"true","bean.name":"ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0","timestamp":"1578302663300"},"port":20880,"serviceName":"DEFAULT_GROUP@@providers:com.jxj.user.openapi.OpenUserService:1.0.0","weight":1.0}]
2020-01-07 10:17:19.296  INFO 21432 --- [           main] c.a.dubbo.registry.nacos.NacosRegistry   :  [DUBBO] Notify urls for subscribe url consumer://192.168.229.1/com.jxj.user.openapi.OpenUserService?application=consumer-usercenter&category=providers,configurators,routers&dubbo=2.0.2&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=21432&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1578363437987&version=1.0.0, urls: [dubbo://192.168.229.1:20880?anyhost=true&application=provider-usercenter&bean.name=ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0&category=providers&dubbo=2.0.2&generic=false&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=37404&protocol=dubbo&revision=1.0.0&side=provider&timestamp=1578302663300&version=1.0.0], dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.447  INFO 21432 --- [           main] c.a.d.remoting.transport.AbstractClient  :  [DUBBO] Successed connect to server /192.168.229.1:20880 from NettyClient 192.168.229.1 using dubbo version 2.6.7, channel is NettyChannel [channel=[id: 0xdd0a8916, L:/192.168.229.1:62947 - R:/192.168.229.1:20880]], dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.447  INFO 21432 --- [           main] c.a.d.remoting.transport.AbstractClient  :  [DUBBO] Start NettyClient JRA1W1PF0YQU5F/192.168.229.1 connect to the server /192.168.229.1:20880, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.525  INFO 21432 --- [client.listener] c.a.dubbo.registry.nacos.NacosRegistry   : The URLs[size : 1] are about to be notified from instances : [{"clusterName":"DEFAULT","enabled":true,"ephemeral":true,"healthy":true,"instanceHeartBeatInterval":5000,"instanceHeartBeatTimeOut":15000,"instanceId":"192.168.229.1#20880#DEFAULT#DEFAULT_GROUP@@providers:com.jxj.user.openapi.OpenUserService:1.0.0","ip":"192.168.229.1","ipDeleteTimeout":30000,"metadata":{"side":"provider","methods":"getUser","dubbo":"2.0.2","pid":"37404","interface":"com.jxj.user.openapi.OpenUserService","version":"1.0.0","generic":"false","revision":"1.0.0","protocol":"dubbo","application":"provider-usercenter","category":"providers","anyhost":"true","bean.name":"ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0","timestamp":"1578302663300"},"port":20880,"serviceName":"DEFAULT_GROUP@@providers:com.jxj.user.openapi.OpenUserService:1.0.0","weight":1.0}]
2020-01-07 10:17:19.525  INFO 21432 --- [client.listener] c.a.dubbo.registry.nacos.NacosRegistry   :  [DUBBO] Notify urls for subscribe url consumer://192.168.229.1/com.jxj.user.openapi.OpenUserService?application=consumer-usercenter&category=providers,configurators,routers&dubbo=2.0.2&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=21432&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1578363437987&version=1.0.0, urls: [dubbo://192.168.229.1:20880?anyhost=true&application=provider-usercenter&bean.name=ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0&category=providers&dubbo=2.0.2&generic=false&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=37404&protocol=dubbo&revision=1.0.0&side=provider&timestamp=1578302663300&version=1.0.0], dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.530  INFO 21432 --- [           main] com.alibaba.dubbo.config.AbstractConfig  :  [DUBBO] Refer dubbo service com.jxj.user.openapi.OpenUserService from url nacos://192.168.229.129:8848/com.alibaba.dubbo.registry.RegistryService?anyhost=true&application=consumer-usercenter&bean.name=ServiceBean:com.jxj.user.openapi.OpenUserService:1.0.0&category=providers&check=false&dubbo=2.0.2&generic=false&interface=com.jxj.user.openapi.OpenUserService&methods=getUser&pid=21432&protocol=dubbo&register.ip=192.168.229.1&remote.timestamp=1578302663300&revision=0.0.1-SNAPSHOT&side=consumer&timestamp=1578363437987&version=1.0.0, dubbo version: 2.6.7, current host: 192.168.229.1
2020-01-07 10:17:19.927  INFO 21432 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2020-01-07 10:17:20.766  INFO 21432 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path ''
2020-01-07 10:17:20.771  INFO 21432 --- [           main] com.jxj.order.OrderWebApplication        : Started OrderWebApplication in 7.556 seconds (JVM running for 9.403)
```

什么是QoS：
* Quality of Service
* qos是Dubbo的在线运维命令，可以对服务进行动态的配置、控制及查询
* Dubboo2.5.8新版本重构了telnet（telnet是从Dubbo2.0.5开始支持的）模块，提供了新的telnet命令支持，新版本的telnet端口与dubbo协议的端口是不同的端口，默认为22222，可以通过配置文件dubbo.properties修改。

QoS参数可以通过如下方式进行配置：优先顺序为JVM系统属性 > dubbo.properties > XML/Spring-boot自动装配方式。
* JVM系统属性
    ```text
    -Ddubbo.application.qos.enable=true
    -Ddubbo.application.qos.port=33333
    -Ddubbo.application.qos.accept.foreign.ip=false
    ```
* dubbo.properties
    ```text
    # 在项目的src/main/resources目录下添加dubbo.properties文件
    dubbo.application.qos.enable=true
    dubbo.application.qos.port=33333
    dubbo.application.qos.accept.foreign.ip=false
    ```
* XML方式
    ```text
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd">
      <dubbo:application name="demo-provider">
        <dubbo:parameter key="qos.enable" value="true"/>
        <dubbo:parameter key="qos.accept.foreign.ip" value="false"/>
        <dubbo:parameter key="qos.port" value="33333"/>
      </dubbo:application>
      <dubbo:registry address="multicast://224.5.6.7:1234"/>
      <dubbo:protocol name="dubbo" port="20880"/>
      <dubbo:service interface="org.apache.dubbo.demo.provider.DemoService" ref="demoService"/>
      <bean id="demoService" class="org.apache.dubbo.demo.provider.DemoServiceImpl"/>
    </beans>
    ```
* Spring-boot自动装配方式
    ```text
    # application.properties或者application.yml
    dubbo.application.qosEnable=true
    dubbo.application.qosPort=33333
    dubbo.application.qosAcceptForeignIp=false
    ```

问题原因分析： consumer启动时qos-server也是使用的默认的22222端口，但是这时候端口已经被provider给占用了，所以才会报错的。



### 参考
* https://blog.csdn.net/u012988901/article/details/84503672
