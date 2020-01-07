## Feign

网站： `https://projects.spring.io/spring-cloud/spring-cloud.html#spring-cloud-feign`

源码： `https://github.com/OpenFeign/feign`

### 目录
* [什么是 Feign？](#什么是-Feign？)
* [Feign的使用](#Feign的使用)
* [参考](#参考)

### 什么是 Feign？
Feign是Netflix开发的声明式、模板化的HTTP客户端， Feign可以帮助我们更快捷、优雅地调用HTTP API。

在Spring Cloud中，使用Feign非常简单——创建一个接口，并在接口上添加一些注解，代码就完成了。Feign支持多种注解，例如Feign自带的注解或者JAX-RS注解等。

Spring Cloud对Feign进行了增强，使Feign支持了Spring MVC注解，并整合了Ribbon和Eureka，从而让Feign的使用更加方便。

Spring Cloud Feign是基于Netflix feign实现，整合了Spring Cloud Ribbon和Spring Cloud Hystrix，除了提供这两者的强大功能外，还提供了一种声明式的Web服务客户端定义的方式。

Spring Cloud Feign帮助我们定义和实现依赖服务接口的定义。在Spring Cloud feign的实现下，只需要创建一个接口并用注解方式配置它，即可完成服务提供方的接口绑定，简化了在使用Spring Cloud Ribbon时自行封装服务调用客户端的开发量。

Spring Cloud Feign具备可插拔的注解支持，支持Feign注解、JAX-RS注解和Spring MVC的注解。

### Feign的使用
1. 添加依赖
```text
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
    <version>1.4.7.RELEASE</version>
</dependency>
# SpringBoot2.X版本后，引入Feign依赖是：
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
2. 启动类添加 @EnableFeignClients 注解支持
```text
@SpringBootApplication
@EnableFeignClients
public class XxxApplication {
    public static void main(String[] args) {
        ...
    }
}
```
3. 建立Client接口，并在接口中定义需调用的服务方法
```text
@FeignClient(name = "feign-user-provider")
public interface UserService {
    /**
     * 查询用户（通过主键用户ID）
     * @param id
     * @return
     */
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    UserVO findUser(Long id);
}
```
4. 使用Client接口。

### 参考
* `https://blog.csdn.net/chengqiuming/article/details/80713471`
* `https://blog.csdn.net/antma/article/details/81317707`
* `https://blog.csdn.net/wo18237095579/article/details/83343915`
* `https://spring.io/projects/spring-cloud-openfeign`