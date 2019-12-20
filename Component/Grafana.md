## Grafana

网站： https://grafana.com/

文档： https://grafana.com/docs/grafana/latest/

源码： https://github.com/grafana/grafana

美观、强大的可视化监控指标展示工具

### 目录
* [Grafana 是什么？](#Grafana-是什么？)
* [Grafana 的特点？](#Grafana-的特点？)
* [Grafana 有哪些组件？](#Grafana-有哪些组件？)
* [参考](#参考)

### Grafana 是什么？
Grafana 是一款可视化面板，有着非常漂亮的图表和布局展示，功能齐全的度量仪表盘和图形编辑器，支持 Graphite、zabbix、InfluxDB、Prometheus、OpenTSDB、Elasticsearch 等作为数据源

grafana 是一款采用 go 语言编写的开源应用，主要用于大规模指标数据的可视化展现，是网络架构和应用分析中最流行的时序数据展示工具，目前已经支持绝大部分常用的时序数据库。

Grafana支持许多不同的数据源。每个数据源都有一个特定的查询编辑器,该编辑器定制的特性和功能是公开的特定数据来源。 官方支持以下数据源:Graphite，Elasticsearch，InfluxDB，Prometheus，Cloudwatch，MySQL和OpenTSDB等。

每个数据源的查询语言和能力都是不同的。你可以把来自多个数据源的数据组合到一个仪表板，但每一个面板被绑定到一个特定的数据源,它就属于一个特定的组织。

### Grafana 的特点？
Grafana是一个跨平台的开源的度量分析和可视化工具，可以通过将采集的数据查询然后可视化的展示，并及时通知。它主要有以下六大特点：
1. 展示方式：快速灵活的客户端图表，面板插件有许多不同方式的可视化指标和日志，官方库中具有丰富的仪表盘插件，比如热图、折线图、图表等多种展示方式；
2. 数据源：Graphite，InfluxDB，OpenTSDB，Prometheus，Elasticsearch，CloudWatch和KairosDB等；
3. 通知提醒：以可视方式定义最重要指标的警报规则，Grafana将不断计算并发送通知，在数据达到阈值时通过Slack、PagerDuty等获得通知；
4. 混合展示：在同一图表中混合使用不同的数据源，可以基于每个查询指定数据源，甚至自定义数据源；
5. 注释：使用来自不同数据源的丰富事件注释图表，将鼠标悬停在事件上会显示完整的事件元数据和标记；
6. 过滤器：Ad-hoc过滤器允许动态创建新的键/值过滤器，这些过滤器会自动应用于使用该数据源的所有查询。

### Grafana 有哪些组件？
* DashBoard：仪表盘，就像汽车仪表盘一样可以展示很多信息，包括车速，水箱温度等。Grafana的DashBoard就是以各种图形的方式来展示从Datasource拿到的数据。
* Row：行，DashBoard的基本组成单元，一个DashBoard可以包含很多个row。一个row可以展示一种信息或者多种信息的组合，比如系统内存使用率，CPU五分钟及十分钟平均负载等。所以在一个DashBoard上可以集中展示很多内容。
* Panel：面板，实际上就是row展示信息的方式，支持表格（table），列表（alert list），热图（Heatmap）等多种方式，具体可以去官网上查阅。
* Query Editor：查询编辑器，用来指定获取哪一部分数据。类似于sql查询语句，比如你要在某个row里面展示test这张表的数据，那么Query Editor里面就可以写成select *from test。这只是一种比方，实际上每个DataSource获取数据的方式都不一样，所以写法也不一样（http://docs.grafana.org/features/datasources/），比如像zabbix，数据是以指定某个监控项的方式来获取的。
* Organization：组织，org是一个很大的概念，每个用户可以拥有多个org，grafana有一个默认的main org。用户登录后可以在不同的org之间切换，前提是该用户拥有多个org。不同的org之间完全不一样，包括datasource，dashboard等都不一样。创建一个org就相当于开了一个全新的视图，所有的datasource，dashboard等都要再重新开始创建。
* User：用户，这个概念应该很简单，不用多说。Grafana里面用户有三种角色admin,editor,viewer。admin权限最高，可以执行任何操作，包括创建用户，新增Datasource，创建DashBoard。editor角色不可以创建用户，不可以新增Datasource，可以创建DashBoard。viewer角色仅可以查看DashBoard。在2.1版本及之后新增了一种角色read only editor（只读编辑模式），这种模式允许用户修改DashBoard，但是不允许保存。每个user可以拥有多个organization。

### 参考
* `https://www.jianshu.com/p/7e7e0d06709b`
* `https://www.cnblogs.com/imyalost/p/9873641.html`