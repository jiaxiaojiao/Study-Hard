### 写数据

> 前提条件：
> 1. Organization
> 2. Bucket
> 3. 认证token ([查看Token](View-tokens.md))

* 行数据格式 line protocol

    > Use line protocol format to write data into InfluxDB. Each line represents a data point. Each point requires a measurement and field set and may also include a tag set and a timestamp.
    >
    > 每行表示一个point。
    > 每个point都需要一个 measurement 和 field set， 还可能包括tag set 和 timestamp。
    > 
    > 更多[行数据格式](Line-protocol.md)和[最佳实践](Best-practices.md)


* 时间戳精度 Timestamp precision

    > 时间戳是 InfluxDB 中最基本的，如果数据库接收到的数据 point 不含时间戳，InfluxDB就会使用系统当前时间。
    >
    > 默认时间戳精度是纳秒。

    <table>
      <tr><td> ns </td><td>纳秒</td></tr>
      <tr><td> us </td><td>微秒</td></tr>
      <tr><td> ms </td><td>毫秒</td></tr>
      <tr><td> s </td><td>秒</td></tr>
    </table>

#### 数据写入 InfluxDB 的方法

* 用户界面
* 命令行
* API接口

命令行 例：
```text
[root@bogon bin]# influx write -b test -o jxj -p s 'myMeasurement,host=myHost testField="testData" 1556896326'
```

