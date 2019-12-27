## Spring Boot 启动 - 内部Tomcat和外部Tomcat

### 目录
* [Spring Boot使用内置Tomcat启动](#使用内置Tomcat启动)
* [Spring Boot使用外部Tomcat启动](#使用外部Tomcat启动)

### 使用内置Tomcat启动

1. IDEA中main函数启动

```text
还有其他启动方式，我没有验证。
```

### 使用外部Tomcat启动

1. 需要在启动类中继承SpringBootServletInitializer并实现configure方法

    作用与在web.xml中配置负责初始化Spring应用上下文的监听器作用类似，不需要编写额外的XML文件了。

    ```text
    @SpringBootApplication
    @EnableScheduling
    public class XxxApplication extends SpringBootServletInitializer {
    
        @Override
        protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
            builder.sources(this.getClass());
            return super.configure(builder);
        }
        
        public static void main(String[] args) {
            SpringApplication.run(XxxApplication.class, args);
        }
    }
    ```

2. pom.xml 修改Tomcat相关配置

    1. 移除spring-boot-starter-web对Tomcat的依赖
    
        ```text
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>2.1.5.RELEASE</version>
            <exclusions>
                <exclusion>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-tomcat</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        ```
        
    2. tomcat-embed-jasper中scope必须是provided
        ```text
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
            <scope>provided</scope>
        </dependency>
        ```
    
    3. packaging war
        ```text
        <packaging>war</packaging>
        ```
