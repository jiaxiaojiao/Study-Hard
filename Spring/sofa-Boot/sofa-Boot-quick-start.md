## 快速开始

> 在 SOFABoot 环境中创建一个简单的 Web 工程，并实现本地运行、云端运行。
>
> 参考： 官方文档

### 目录
* 创建工程
* 将工程导入 IDE 工具
* 本地编译运行

### 创建工程

两种方式：

* 使用 SOFA 应用中心 在线配置并下载工程包

* 通过 Maven 本地创建工程

    ```text
    mvn archetype:generate -DarchetypeRepository=http://mvn.cloud.alipay.com/nexus/content/repositories/snapshots/ -DarchetypeGroupId=com.alipay.sofa -DarchetypeArtifactId=sofaboot-web-archetype -DarchetypeVersion=1.0-SNAPSHOT -DarchetypeCatalog=internal
    ```

### 将工程导入 IDE 工具

SOFABoot 工程是标准的 Maven 工程。

IntelliJ IDEA 正常导入项目就行，修改Maven配置。

### 本地编译运行

IntelliJ IDEA 运行Main方法： SOFABootWebSpringApplication

成功运行后，浏览器打开： http://localhost:8080/index.html 
