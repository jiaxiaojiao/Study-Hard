## ELK

网站： https://www.elastic.co/cn/

> 描述
>
> 参考： 官网， https://blog.csdn.net/u012562943/article/details/99946609

### 目录
* [是什么？](#是什么？)
* [是否开源](#是否开源)
* [主要功能](#主要功能)
* [兼容性](#兼容性)
* [支持的语言](#支持的语言)
* [优缺点](#优缺点)
* [其他替代组件](#其他替代组件)

### 是什么？

ELK 是elastic公司提供的一套完整的日志收集以及展示的解决方案，是三个产品的首字母缩写，分别是ElasticSearch、Logstash 和 Kibana。

* ElasticSearch简称ES，它是一个实时的分布式搜索和分析引擎，它可以用于全文搜索，结构化搜索以及分析。它是一个建立在全文搜索引擎 Apache Lucene 基础上的搜索引擎，使用 Java 语言编写。
* Logstash是一个具有实时传输能力的数据收集引擎，用来进行数据收集（如：读取文本文件）、解析，并将数据发送给ES。
* Kibana为 Elasticsearch 提供了分析和可视化的 Web 平台。它可以在 Elasticsearch 的索引中查找，交互数据，并生成各种维度表格、图形。

### 是否开源

开源, 用户可以基于 Apache 2 许可证免费使用 Elasticsearch 的开源功能。

### 主要功能

日志分析，基于日志的分析，能够在其上产生非常多的解决方案，譬如：
     
1. 问题排查。我们常说，运维和开发这一辈子无非就是和问题在战斗，所以这个说起来很朴实的四个字，其实是沉甸甸的。很多公司其实不缺钱，就要稳定，而要稳定，就要运维和开发能够快速的定位问题，甚至防微杜渐，把问题杀死在摇篮里。日志分析技术显然问题排查的基石。基于日志做问题排查，还有一个很帅的技术，叫全链路追踪，比如阿里的eagleeye 或者Google的dapper，也算是日志分析技术里的一种。
2. 监控和预警。 日志，监控，预警是相辅相成的。基于日志的监控，预警使得运维有自己的机械战队，大大节省人力以及延长运维的寿命。
3. 关联事件。多个数据源产生的日志进行联动分析，通过某种分析算法，就能够解决生活中各个问题。比如金融里的风险欺诈等。这个可以可以应用到无数领域了，取决于你的想象力。
4. 数据分析。 这个对于数据分析师，还有算法工程师都是有所裨益的。

* 什么是 Elasticsearch？

    Elasticsearch 是一个分布式的开源搜索和分析引擎，适用于所有类型的数据，包括文本、数字、地理空间、结构化和非结构化数据。Elasticsearch 在 Apache Lucene 的基础上开发而成，由 Elasticsearch N.V.（即现在的 Elastic）于 2010 年首次发布。Elasticsearch 以其简单的 REST 风格 API、分布式特性、速度和可扩展性而闻名，是 Elastic Stack 的核心组件；Elastic Stack 是适用于数据采集、充实、存储、分析和可视化的一组开源工具。人们通常将 Elastic Stack 称为 ELK Stack（代指 Elasticsearch、Logstash 和 Kibana），目前 Elastic Stack 包括一系列丰富的轻量型数据采集代理，这些代理统称为 Beats，可用来向 Elasticsearch 发送数据。

* Logstash 的用途是什么？

    Logstash 是 Elastic Stack 的核心产品之一，可用来对数据进行聚合和处理，并将数据发送到 Elasticsearch。Logstash 是一个开源的服务器端数据处理管道，允许您在将数据索引到 Elasticsearch 之前同时从多个来源采集数据，并对数据进行充实和转换。

* Kibana 的用途是什么？
    
    Kibana 是一款适用于 Elasticsearch 的数据可视化和管理工具，可以提供实时的直方图、线形图、饼状图和地图。Kibana 同时还包括诸如 Canvas 和 Elastic Maps 等高级应用程序；Canvas 允许用户基于自身数据创建定制的动态信息图表，而 Elastic Maps 则可用来对地理空间数据进行可视化。

### 兼容性

ELK各自版本最好都是一致的,否则可能会有兼容性问题。

### 支持的语言

Elasticsearch 支持多种编程语言，目前提供针对下列编程语言的官方客户端：
* Java
* JavaScript (Node.js)
* Go
* .NET (C#)
* PHP
* Perl
* Python
* Ruby

### 优缺点

Elasticsearch的优点：
* Elasticsearch 很快。 由于 Elasticsearch 是在 Lucene 基础上构建而成的，所以在全文本搜索方面表现十分出色。Elasticsearch 同时还是一个近实时的搜索平台，这意味着从文档索引操作到文档变为可搜索状态之间的延时很短，一般只有一秒。因此，Elasticsearch 非常适用于对时间有严苛要求的用例，例如安全分析和基础设施监测。
* Elasticsearch 具有分布式的本质特征。 Elasticsearch 中存储的文档分布在不同的容器中，这些容器称为分片，可以进行复制以提供数据冗余副本，以防发生硬件故障。Elasticsearch 的分布式特性使得它可以扩展至数百台（甚至数千台）服务器，并处理 PB 量级的数据。
* Elasticsearch 包含一系列广泛的功能。 除了速度、可扩展性和弹性等优势以外，Elasticsearch 还有大量强大的内置功能（例如数据汇总和索引生命周期管理），可以方便用户更加高效地存储和搜索数据。
* Elastic Stack 简化了数据采集、可视化和报告过程。 通过与 Beats 和 Logstash 进行集成，用户能够在向 Elasticsearch 中索引数据之前轻松地处理数据。同时，Kibana 不仅可针对 Elasticsearch 数据提供实时可视化，同时还提供 UI 以便用户快速访问应用程序性能监测 (APM)、日志和基础设施指标等数据。
* Elasticsearch 提供强大且全面的 REST API 集合，这些 API 可用来执行各种任务，例如检查集群的运行状况、针对索引执行 CRUD（创建、读取、更新、删除）和搜索操作，以及执行诸如筛选和聚合等高级搜索操作。

### 其他替代组件

ELK是作为替代Splunk的一个开源解决方案。