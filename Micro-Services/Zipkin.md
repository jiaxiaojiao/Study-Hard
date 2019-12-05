## Zipkin

网站： https://zipkin.io/

GitHub： https://github.com/openzipkin/zipkin

### 目录
* [Zipkin是什么](#Zipkin是什么)
* [Zipkin支持的数据存储方式](#Zipkin支持的数据存储方式)
* [Zipkin主要涉及四个组件](#Zipkin主要涉及四个组件)

### Zipkin是什么

Zipkin 是一个开放源代码分布式的跟踪系统，每个服务向zipkin报告计时数据，zipkin会根据调用关系通过Zipkin UI生成依赖关系图。

### Zipkin支持的数据存储方式

Zipkin提供了可插拔数据存储方式：In-Memory、MySql、Cassandra以及Elasticsearch

### Zipkin主要涉及四个组件
collector storage search web UI
* Collector接收各service传输的数据
* Cassandra作为Storage的一种，也可以是mysql等，默认存储在内存中，配置cassandra可以参考这里
* Query负责查询Storage中存储的数据,提供简单的JSON API获取数据，主要提供给web UI使用
* Web 提供简单的web界面


