### SOFABoot 安装和使用

文档： https://tech.antfin.com/docs/2/66011

> 参考： 官方文档
>

SOFABoot 基于 Spring Boot 框架开发，并依赖 Apache Maven 进行构建。SOFABoot 和 Spring Boot 版本对应关系，以及 JDK 版本要求如下：

<table>
  <tr><th>SOFABoot 版本</th><th>Spring Boot 版本</th><th>JDK 版本</th></tr>
  <tr><td>3.x</td><td>2.0.3.RELEASE</td><td>JDK 8+</td></tr>
  <tr><td>2.5.x - 2.6.x</td><td>1.5.16.RELEASE</td><td>JDK 7+</td></tr>
  <tr><td>2.3.x - 2.4.x</td><td>1.4.2.RELEASE</td><td>JDK 7+</td></tr>
</table>

### 目录
* 系统要求
* 获取SOFABoot框架
* 升级到最新版本 SOFABoot
* 将 Spring Boot 工程迁移至 SOFABoot 工程

### 系统要求

* 安装 JDK

* 安装 Apache Maven 3.2.5 或更高版本

* 配置金融科技 Maven 仓库地址

### 获取SOFABoot框架

SOFABoot 支持创建 Web 和 Core 两种类型的工程：

* Web 工程：当使用 SOFABoot 开发一个 Web 程序时，相当于“基于 Spring Boot 的 Web 应用 + 蚂蚁金服中间件” 进行开发。

* Core 工程：当使用 SOFABoot 开发一个 J2SE 程序（无 Web 页面访问），相当于“基于 Spring Boot 的非 Web 应用（无 servlet 依赖）+ 蚂蚁金服中间件” 进行开发。

按照不同的工程类型，您可根据需要运行以下命令行获取相应的 SOFABoot 工程原型。

* Web工程： 

    ```text
    mvn archetype:generate -DarchetypeRepository=http://mvn.cloud.alipay.com/nexus/content/repositories/snapshots/ -DarchetypeGroupId=com.alipay.sofa -DarchetypeArtifactId=sofaboot-web-archetype -DarchetypeVersion=1.0-SNAPSHOT -DarchetypeCatalog=internal
    ```
  
    ```text
    Define value for property 'groupId': com.alipay.sofa
    Define value for property 'artifactId': web-app
    Define value for property 'version' 1.0-SNAPSHOT: :
    ```
  
* Core 工程：

    ```text
    mvn archetype:generate -DarchetypeRepository=http://mvn.cloud.alipay.com/nexus/content/repositories/snapshots/ -DarchetypeGroupId=com.alipay.sofa -DarchetypeArtifactId=sofaboot-core-archetype -DarchetypeVersion=1.0-SNAPSHOT -DarchetypeCatalog=internal
    ```

### 升级到最新版本 SOFABoot

SOFABoot 版本包括 2.x 及 3.x 两个系列。如需从 SOFABoot 2.x 版本升级至 3.x 版本，您必须首先检查系统兼容性说明，并完成基础依赖框架 Spring Boot 版本的迁移。

### 将 Spring Boot 工程迁移至 SOFABoot 工程

SOFABoot 是基于 Spring Boot 框架构建的，所以可以轻松地从 Spring Boot 迁移至 SOFABoot。


