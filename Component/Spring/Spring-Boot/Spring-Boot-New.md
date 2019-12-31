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
        <module>user-interface</module>
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
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    ```
6. 修改子节点项目。删除（除user-web）启动类和配置文件，因为整个只能保留一个启动类。 （例： 删除`XXApplication`，`application.properties/yml`）
7. 修改子节点项目 `pom.xml`， 添加模块间的依赖。
8. 修改子节点项目 `pom.xml`， 删除（除`user-web`）测试依赖，`test`文件夹。 删不删都行~

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
	order-interface
	order-service
	order-web

groupId: com.jxj.user
artifactId: usercenter
artifactId: ordercenter
```
