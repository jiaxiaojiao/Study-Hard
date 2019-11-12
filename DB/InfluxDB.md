## InfluxDB

> influx [ˈɪnflʌks] 
>
> InfluxDB is an open source time series platform. This includes APIs for storing and querying data, processing it in the background for ETL or monitoring and alerting purposes, user dashboards, and visualizing and exploring the data and more. 
>
> InfluxDB是一个由InfluxData开发的开源时序型数据。它由Go写成，着力于高性能地查询与存储时序型数据。InfluxDB被广泛应用于存储系统的监控数据，IoT行业的实时数据等场景。 

GitHub https://github.com/influxdata/influxdb

网站 https://www.influxdata.com/

### 目录
* [介绍](#介绍)
* [基础概念](#基础概念)
* [常用InfluxQL](#InfluxQL)

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

### InfluxQL

```text
创建数据库：
create database mydb

创建用户：
create user "bigdata" with password 'bigdata' with all privileges

查看数据库：
show databases;

数据插入：
insert bigdata,host=server001,regin=HC load=88

使用特定的数据库：
use database_name;

查看所有的measurement：
show measurements;

查询10条数据：
select * from measurement_name limit 10;

数据中的时间字段默认显示的是一个纳秒时间戳，改成可读格式：
precision rfc3339; -- 之后再查询，时间就是rfc3339标准格式

或可以在连接数据库的时候，直接带该参数：
influx -precision rfc3339

查看一个measurement中所有的tag key：
show tag keys

查看一个measurement中所有的field key ：
show field keys

查看一个measurement中所有的保存策略(可以有多个，一个标识为default)：
show retention policies;
```

