## Zipkin

网站： https://zipkin.io/

GitHub： https://github.com/openzipkin/zipkin

> 参考： https://www.jianshu.com/p/4fa81b661f55

### 目录
* [是什么？](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [优缺点](#优缺点)
* [其他替代组件](#其他替代组件)

### 是什么？
Zipkin 是一个开放源代码分布式的跟踪系统，每个服务向zipkin报告计时数据，zipkin会根据调用关系通过Zipkin UI生成依赖关系图。

Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in service architectures. Features include both the collection and lookup of this data.

### 是否开源

开源

### 主要功能

Zipkin主要涉及四个组件： collector storage search web UI
* Collector接收各service传输的数据
* Cassandra作为Storage的一种，也可以是mysql等，默认存储在内存中，配置cassandra可以参考这里
* Query负责查询Storage中存储的数据,提供简单的JSON API获取数据，主要提供给web UI使用
* Web 提供简单的web界面

### 兼容性

Zipkin提供了可插拔数据存储方式：In-Memory、MySql、Cassandra以及Elasticsearch

### 优缺点

* 通过zipkin官网提供的服务来搭建，对老版本kafka的支持有缺陷。新版已经集成了对kafka的支持。

### 其他替代组件

* Pinpoint
* skywalking
