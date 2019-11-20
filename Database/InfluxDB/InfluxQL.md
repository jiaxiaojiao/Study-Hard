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
