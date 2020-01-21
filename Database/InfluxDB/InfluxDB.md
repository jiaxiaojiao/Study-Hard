## InfluxDB

> influx [ˈɪnflʌks] 
>
> InfluxDB is an open source time series platform. This includes APIs for storing and querying data, processing it in the background for ETL or monitoring and alerting purposes, user dashboards, and visualizing and exploring the data and more. 
>
> InfluxDB是一个由InfluxData开发的开源时序型数据。它由Go写成，着力于高性能地查询与存储时序型数据。InfluxDB被广泛应用于存储系统的监控数据，IoT行业的实时数据等场景。 


### 目录
* [介绍](#介绍)
* [基础概念](#基础概念)
* [开始使用InfluxDB v2.0](Get-started.md)
    * [写数据 Write data](Write-data.md)
    * [查询数据 Query data](Query-data.md)
    * [数据进程 Process data](Process-data.md)
    * [数据可视化 Visualize data](Visualize-data.md)
    * [数据监控和警报 Monitor & alert](Monitor-alert.md)
    * [组织管理 Manage organizations](Manage-organizations.md)
    * [用户管理 Manage users](Manage-users.md)
    * [权限和安全管理 Security & authorization](Security-authorization.md)
    * [常用InfluxQL](InfluxQL.md)

### 介绍

* 使用TSM(Time Structured Merge)存储引擎，允许高摄取速度和数据压缩

### 基础概念

* 数据库

    database

* 表

    measurement

* 行
    
    points

* 列

    tag：带索引的，非必须，只能为字符串类型
    
    field：不带索引，类型没有限制
    
    timestamp：唯一主键

* 集合

    tag set：的每组tag key和tag value的集合
    
    field set：每组field key和field value的集合
    
    series：共同retention policy，measurement和tag set的集合

### 参考
* 网站： https://www.influxdata.com/
* 源码： https://github.com/influxdata/influxdb

