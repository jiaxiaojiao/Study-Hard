## Grafana

网站： `https://grafana.com/`

文档： `https://grafana.com/docs/grafana/latest/`

源码： `https://github.com/grafana/grafana`

美观、强大的可视化监控指标展示工具

### 目录
* [Grafana 是什么？](#Grafana-是什么？)
* [Grafana 的一些基本概念和组件](#Grafana-的一些基本概念)
* [Grafana 有哪些特点？](#Grafana-有哪些特点？)
* [Grafana与Kibana的相同点和差异](#Grafana与Kibana的相同点和差异)
* 安装使用
    * [Docker安装Grafana](Prometheus-install2.md#Docker安装Grafana)
    * [引入DashBoard模板](Grafana-DashBoard.md)
* [参考](#参考)

### Grafana 是什么？
开放的可观测平台，Grafana是每个数据库的开源分析和监控解决方案。

Grafana项目由Torkel Odegaard于2014年启动，在过去的几年里，它已经成为GitHub上最受欢迎的开源项目之一。它允许您对指标和日志进行查询、可视化和警报，无论它们存储在何处。

Grafana具有可插拔的数据源模型，并附带了对许多最流行的时间序列数据库(如Graphite, Prometheus, Elasticsearch, OpenTSDB, InfluxDB)的丰富支持。它还内置了对云监控供应商的支持，如谷歌Stackdriver、Amazon Cloudwatch、Microsoft Azure和SQL数据库(如MySQL和Postgres)。Grafana是唯一能够将如此多地方的数据合并到一个仪表板中的工具。

Grafana 是一款采用 go 语言编写的开源应用，主要用于大规模指标数据的可视化展现，是网络架构和应用分析中最流行的时序数据展示工具。

每个数据源的查询语言和能力都是不同的。你可以把来自多个数据源的数据组合到一个仪表板，但每一个面板被绑定到一个特定的数据源,它就属于一个特定的组织。

### Grafana 的一些基本概念
* 数据源。 Grafana支持许多不同的数据源。每个数据源都有一个特定的查询编辑器,该编辑器定制的特性和功能是公开的特定数据来源。
* DashBoard 仪表板。 Grafana的DashBoard就是以各种图形的方式来展示从Datasource拿到的数据。
* Row 行。DashBoard的基本组成单元，一个DashBoard可以包含很多个row。一个row可以展示一种信息或者多种信息的组合，比如系统内存使用率，CPU五分钟及十分钟平均负载等。所以在一个DashBoard上可以集中展示很多内容。
* Panel 面板。实际上就是row展示信息的方式，支持表格（table），列表（alert list），热图（Heatmap）等多种方式。面板（或整个仪表板）可以以多种方式轻松共享，既可以通过链接分享，也可以导出JSON等文本文件。
* Query Editor 查询编辑器。用来指定获取哪一部分数据。
* Organization 组织。org是一个很大的概念，每个用户可以拥有多个org，grafana有一个默认的main org。用户登录后可以在不同的org之间切换，前提是该用户拥有多个org。不同的org之间完全不一样，包括datasource，dashboard等都不一样。创建一个org就相当于开了一个全新的视图，所有的datasource，dashboard等都要再重新开始创建。
* User 用户。Grafana里面用户有三种角色admin,editor,viewer。admin权限最高，可以执行任何操作，包括创建用户，新增Datasource，创建DashBoard。editor角色不可以创建用户，不可以新增Datasource，可以创建DashBoard。viewer角色仅可以查看DashBoard。在2.1版本及之后新增了一种角色read only editor（只读编辑模式），这种模式允许用户修改DashBoard，但是不允许保存。每个user可以拥有多个organization。
* Alerting 警报。 以可视方式定义最重要指标的警报规则。Grafana将不断评估它们并发送通知。
* Notifications 通知。 当警报更改状态时，它会发送通知。接收电子邮件通知或从Slack，PagerDuty，VictorOps，OpsGenie或通过webhook获取。

### Grafana 有哪些特点？
* 可视化：快速和灵活的客户端图形具有多种选项。面板插件为许多不同的方式可视化指标和日志。
* 报警：可视化地为最重要的指标定义警报规则。Grafana将持续评估它们，并发送通知。
* 通知：警报更改状态时，它会发出通知。接收电子邮件通知。
* 动态仪表盘：使用模板变量创建动态和可重用的仪表板，这些模板变量作为下拉菜单出现在仪表板顶部。
* 混合数据源：在同一个图中混合不同的数据源!可以根据每个查询指定数据源。这甚至适用于自定义数据源。
* 注释：注释来自不同数据源图表。将鼠标悬停在事件上可以显示完整的事件元数据和标记。
* 过滤器：过滤器允许您动态创建新的键/值过滤器，这些过滤器将自动应用于使用该数据源的所有查询。

### Grafana与Kibana的相同点和差异
Grafana类似Kibana, 是对后端的数据进行实时展示。

不同点：
* 日常使用中Kibana是跟着Logstash、ElasticSearch等组件一起使用做日志展示、索引、分析的，Kibana专注于可视化ElasticSearch里面的数据，而且生态圈没有Grafana好。
* Grafana一般是和一些时间序列数据库进行配合来展示数据的，例如：Graphite、OpenTSDB、InfluxDB等。有着丰富的插件可以选择和进行定制。


### 参考
* `https://grafana.com/grafana/download?platform=docker`
* `https://grafana.com/docs/grafana/latest/features/datasources/prometheus/`
* `https://www.jianshu.com/p/7e7e0d06709b`
* `https://www.jianshu.com/p/0d82c7ccc85a`
* `https://www.jianshu.com/p/3527f48165d7`
