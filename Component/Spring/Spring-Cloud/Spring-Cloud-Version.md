## Spring Cloud 版本对应关系

### 目录
* [推荐使用的版本依赖关系](#推荐使用的版本依赖关系)
* [Spring Cloud Greenwich](#Spring-Cloud-Greenwich)
* [Spring Cloud Alibaba 组件版本关系](#Spring-Cloud-Alibaba-组件版本关系)
* [参考](#参考)

### 推荐使用的版本依赖关系
<table>
  <tr><th>Spring Cloud Version</th><th>Spring Cloud Alibaba Version</th><th>Spring Boot Version</th></tr>
  <tr><td>Spring Cloud Greenwich</td><td>2.1.1.RELEASE</td><td>2.1.X.RELEASE</td></tr>
  <tr><td>Spring Cloud Finchley</td><td>2.0.1.RELEASE</td><td>2.0.X.RELEASE</td></tr>
  <tr><td>Spring Cloud Edgware</td><td>1.5.1.RELEASE</td><td>1.5.X.RELEASE</td></tr>
</table>

### Spring Cloud Greenwich
dependencyManagement 中 `Spring Cloud Alibaba` 依赖：
```text
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.1.1.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

### Spring Cloud Finchley
dependencyManagement 中 `Spring Cloud Alibaba` 依赖：
```text
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.0.1.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

### Spring Cloud Alibaba 组件版本关系
<table>
  <tr><th>Spring Cloud Alibaba Version</th><th>Sentinel Version</th><th>Nacos Version</th><th>RocketMQ Version</th><th>Dubbo Version</th><th>Seata Version</th></tr>
  <tr><td>(毕业版本) 2.1.1.RELEASE or 2.0.1.RELEASE or 1.5.1.RELEASE</td><td>1.7.0</td><td>1.1.4</td><td>4.4.0</td><td>2.7.3</td><td>0.9.0</td></tr>
  <tr><td>(毕业版本) 2.1.0.RELEASE or 2.0.0.RELEASE or 1.5.0.RELEASE</td><td>1.6.3</td><td>1.1.1</td><td>4.4.0</td><td>2.7.3</td><td>0.7.1</td></tr>
  <tr><td>(孵化器版本) 0.9.0.RELEASE or 0.2.2.RELEASE or 0.1.2.RELEASE</td><td>1.5.2</td><td>1.0.0</td><td>4.4.0</td><td>2.7.1</td><td>0.4.2</td></tr>
  <tr><td>(孵化器版本) 0.2.1.RELEASE or 0.1.1.RELEASE</td><td>1.4.0</td><td>0.6.2</td><td>4.3.1</td><td>❌</td><td>❌</td></tr>
  <tr><td>(孵化器版本) 0.2.0.RELEASE or 0.1.0.RELEASE</td><td>1.3.0-GA</td><td>0.3.0</td><td>❌</td><td>❌</td><td>❌</td></tr>
</table>

### 参考
* Spring Cloud Alibaba 版本说明 `https://github.com/alibaba/spring-cloud-alibaba/wiki/%E7%89%88%E6%9C%AC%E8%AF%B4%E6%98%8E`
