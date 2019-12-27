## IDEA 把Spring Boot项目打成war包

### 目录
* [Spring Boot项目打war包](#Spring-Boot项目打war包)
* [参考](#参考)

### Spring Boot项目打war包
* `pom.xml` 查看打包方式。
    ```text
    <packaging>war</packaging>
    ```
* `pom.xml` 添加 `spring-boot-starter-tomcat` 依赖，表示tomcat是外部提供的。
    ```text
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
        <scope>provided</scope>
    </dependency>
    ```
* 查看项目结构 `File -> Project Structure... -> 项目 -> Web `  查看webapp路径 `Web Resource Directory` ，一般是自动设置好的。
* `Deployment Descriptors` 添加 `web.xml`， 跟上一步同样的页面。 （web.xml路径在webapp里，如下：）
    ```text
    D:\IdeaProjects\demo\src\main\webapp\WEB-INF\web.xml
    D:\IdeaProjects\demo\src\main\webapp
    ```
* 修改项目启动类，继承 SpringBootServletInitializer ，并重写configure方法
    ```text
    @SpringBootApplication
    public class DemoApplication extends SpringBootServletInitializer {
        ...
    
        @Override
        protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
            builder.sources(this.getClass());
            return super.configure(builder);
        }
    
        public static void main(String[] args) {
            SpringApplication.run(DemoApplication.class, args);
        }
    
        ...
    }
    ```
* 项目打包，使用Maven方式。 `Maven -> 项目 -> Lifecycle -> package`
* 项目部署，把war包，放到Tomcat 的webapps文件下，启动Tomcat，war会启动解压。
* 访问已经启动的项目。
    ```text
    http://127.0.0.1:8080/demo/user/list
    功能可以正常访问没有问题。
    ```
### 参考
* `https://www.jianshu.com/p/baf624064540`