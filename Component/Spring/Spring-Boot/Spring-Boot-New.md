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
* 创建父节点项目，用于管理子节点项目和jar 包版本。 根据[使用IDEA创建Spring Boot项目](#使用IDEA创建Spring-Boot项目) 创建就可以，不用添加依赖
* 清除`src` 文件夹
* 修改 `pom` 文件，添加`packaging pom` , `dependencyManagement`
* 创建子节点项目， `New –> Module -> Maven`   `user-interface、user-service、user-web`
* 修改子节点 `pom` 文件子节点间，相互依赖。  `user-web` 添加依赖web启动器和 `user-service`, `user-service` 添加依赖 `user-interface`。
* `user-web` 添加配置文件和启动类。
```text
两个项目
demo1:
usercenter
	user-interface
	user-service （user-service依赖user-interface）
	user-web (user-web依赖user-service)

demo2:
ordercenter
	order-interface
	order-service （order-service依赖order-interface）
	order-web （order-web依赖order-service）

groupId: com.jxj.demo
artifactId: usercenter
artifactId: ordercenter
```
