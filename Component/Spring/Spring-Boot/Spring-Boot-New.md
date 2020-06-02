## 创建Spring Boot项目

### 目录
* [使用IDEA创建Spring Boot项目](#使用IDEA创建Spring-Boot项目)
* [多模块项目创建](#多模块项目创建)


### 使用IDEA创建Spring Boot项目
> 我使用的版本是： IntelliJ IDEA 2019.3 (Ultimate Edition)

创建步骤： 
* `File -> New -> Project... `  选择左侧 `Spring Initializr`  Project SDK 选择1.8版本，Choose Initializr Service URL 选择默认`http://start.spring.io`
* Next `Project Metadata` 默认demo
* Next `Dependencies` 自定义选择依赖，我选了：Spring Boot版本2.2.2，Lombok，Spring Web，MyBatis Framework， MySQL Driver
* Next  `Project name` 默认demo， `D:\IdeaProjects\demo`
* 完成，新窗口打开项目
* 初始化

### 多模块项目创建
> 父工程，多个子模块。

#### 构建思路
先创建一个 Spring Initializr工程父工程， 然后在父工程创建普通的Spring Initializr工程作为子模块 Module

#### 构建步骤
1. 创建父节点，一个`Spring Initializr`工程。（例：`usercenter`）
2. 删除父节点工程内（除`.idea` `pom.xml` `*.iml` 外）文件和文件夹。
3. 创建子节点，一个`Spring Initializr`工程。（例：`user-entity` 实体类 依赖了`lombok`； `user-dao` 与数据库交互 依赖了`MyBatis`和`MySQL`；`user-interface` 向外暴露接口 没有添加默认依赖； `user-service` 业务逻辑 没有添加默认依赖；`user-web` 页面交互 启动类，依赖了`spring web`）
4. 修改父节点工程 `pom.xml`。 打包方式 `<packaging>pom</packaging>`， 包含的子模块Module
    ```text
    <modules>
        <module>user-entity</module>
        <module>user-dao</module>
        <module>user-interface</module> => <module>user-openapi</module>
        <module>user-service</module>
        <module>user-web</module>
    </modules>
    ```
5. 修改子节点工程 `pom.xml`。父节点工程。
    ```text
    <parent>
        <groupId>com.jxj</groupId>
        <artifactId>usercenter</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <!-- <relativePath/> --> <!-- lookup parent from repository -->
    </parent>
    ```
6. 修改子节点项目。删除（除user-web）启动类和配置文件，因为整个只能保留一个启动类。 （例： 删除`XXApplication`，`application.properties/yml`）
7. 修改子节点项目 `pom.xml`， 添加模块间的依赖。
8. 修改子节点项目 `pom.xml`， 删除（除`user-web`）**测试**`spring-boot-starter-test`依赖和`spring-boot-maven-plugin`依赖，`test`文件夹。 
9. 修改子节点项目。 删除不需要的`resources`文件夹
10. 父节点项目管理Maven依赖的版本。`<dependencyManagement></dependencyManagement>`
```text
两个项目
usercenter
	user-entity    实体类（谁都不依赖）
	user-dao      用于持久化数据跟数据库交互(依赖entity)
	user-interface 向外暴露接口类
	user-service   处理业务逻辑 （依赖dao,entity,interface实现接口）
	user-web 	页面交互接收、传递数据，唯一有启动类的模块（依赖service，entity）

ordercenter
	order-entity
	order-dao
	order-interface => order-openapi
	order-service
	order-web

groupId: com.jxj
artifactId: usercenter
artifactId: ordercenter
```

#### 可能遇到的问题
* 异常
    ```text
    Failed to execute goal org.springframework.boot:spring-boot-maven-plugin:2.2.2.RELEASE:repackage (repackage) on project user-entity: Execution repackage of goal org.springframework.boot:spring-boot-maven-plugin:2.2.2.RELEASE:repackage failed: Unable to find main class
    ```
    问题原因： `spring-boot-maven-plugin` 依赖写在有main方法的`pom.xml`文件，或者指定main方法。
    解决： 父节点和其他子节点（除user-web存在main方法）删除依赖 `spring-boot-maven-plugin`。
* 异常。
    ```text
    Some problems were encountered while building the effective model for com.jxj:user-dao:jar:0.0.1-SNAPSHOT
    'dependencies.dependency.(groupId:artifactId:type:classifier)' must be unique: org.mybatis.spring.boot:mybatis-spring-boot-starter:jar -> duplicate declaration of version 2.1.1 @ line 37, column 21
    It is highly recommended to fix these problems because they threaten the stability of your build.
    For this reason, future Maven versions might no longer support building such malformed projects.
    ```
    问题原因： 手欠，`mybatis`依赖写了两遍。
* 异常。 controller找不到service，原因 XXApplication的目录需要在所有子节点的上一级。
* 疑问。`mysql-connector-java` 依赖到底放到user-web 还是user-dao？。 我放在user-web，没有问题。
* 疑问。 `spring-boot-starter` 依赖什么用，到底放哪儿呢，需要子节点项目都放吗？  我放在 user-service 、 user-interface、 父节点，目测没有问题。有问题再说吧。


### 参考
* https://www.jianshu.com/p/cac4759b2684
* https://blog.csdn.net/hu_zhiting/article/details/84577702
* https://blog.csdn.net/horacehe16/article/details/79811763