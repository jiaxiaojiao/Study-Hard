## gRPC


### 目录
* [gRPC 是什么？](#是什么？)
* [为什么要选择 gRPC？](#为什么要选择-gRPC？)
* [gRPC 有哪些特性？](#有哪些特性？)
* [参考](#参考)

### 是什么？
> A high performance, open-source universal RPC framework

gRPC 是高性能、开源的通用RPC框架。

### 为什么要选择 gRPC？
> gRPC is a modern open source high performance RPC framework that can run in any environment. It can efficiently connect services in and across data centers with pluggable support for load balancing, tracing, health checking and authentication. It is also applicable in last mile of distributed computing to connect devices, mobile applications and browsers to backend services.

gRPC是一个可以在任何环境中运行的现代开源高性能RPC框架。它可以有效地连接数据中心内和跨数据中心的服务，并支持可插拔的负载平衡、跟踪、健康检查和身份验证。它也适用于连接设备、移动应用程序和浏览器到后端服务的分布式计算的最后一英里。

### 有哪些特性？
> Simple service definition
>
> Define your service using Protocol Buffers, a powerful binary serialization toolset and language
>
> Start quickly and scale
>
> Install runtime and dev environments with a single line and also scale to millions of RPCs per second with the framework
>
> Works across languages and platforms
>
> Automatically generate idiomatic client and server stubs for your service in a variety of languages and platforms
>
> Bi-directional streaming and integrated auth
>
> Bi-directional streaming and fully integrated pluggable authentication with http/2 based transport

* 简单的服务定义
    * 使用协议缓冲区(一种强大的二进制序列化工具集和语言)定义服务
* 快速启动和扩展
    * 使用单行安装运行时和开发环境，并使用该框架扩展到每秒数百万个rpc
* 跨语言和平台工作
    * 在各种语言和平台中为您的服务自动生成惯用的客户机和服务器存根
* 双向流和集成验证
    * 基于http/2传输的双向流和完全集成的可插拔身份验证

### 参考
* 网站： https://grpc.io/
* 源码： https://github.com/grpc/grpc