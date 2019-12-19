## OpenResty

网站： http://openresty.org/cn/

源码： https://github.com/openresty/openresty

### 目录
* [OpenResty 是什么？](#OpenResty-是什么？)
* [OpenResty 有哪些组件？](#OpenResty-有哪些组件？)
* [参考](#参考)

### OpenResty 是什么？
OpenResty® 是一款基于 NGINX 和 LuaJIT 的 Web 平台。

OpenResty® 是通过 Lua 扩展 NGINX 实现的可伸缩的 Web 平台。

OpenResty® 是一个基于 Nginx 与 Lua 的高性能 Web 平台，其内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。

OpenResty® 通过汇聚各种设计精良的 Nginx 模块（主要由 OpenResty 团队自主开发），从而将 Nginx 有效地变成一个强大的通用 Web 应用平台。这样，Web 开发人员和系统工程师可以使用 Lua 脚本语言调动 Nginx 支持的各种 C 以及 Lua 模块，快速构造出足以胜任 10K 乃至 1000K 以上单机并发连接的高性能 Web 应用系统。

OpenResty® 的目标是让你的Web服务直接跑在 Nginx 服务内部，充分利用 Nginx 的非阻塞 I/O 模型，不仅仅对 HTTP 客户端请求,甚至于对远程后端诸如 MySQL、PostgreSQL、Memcached 以及 Redis 等都进行一致的高性能响应。

### OpenResty 有哪些组件？
所有组件均可以方便的被激活或禁止。
Drizzle Nginx 模块、 Postgres Nginx 模块 以及 Iconv Nginx 模块 默认并未启用。 

```text
LuaJIT
ArrayVarNginxModule
AuthRequestNginxModule
CoolkitNginxModule
DrizzleNginxModule
EchoNginxModule
EncryptedSessionNginxModule
FormInputNginxModule
HeadersMoreNginxModule
IconvNginxModule
StandardLuaInterpreter
MemcNginxModule
Nginx
NginxDevelKit
LuaCjsonLibrary
LuaNginxModule
LuaRdsParserLibrary
LuaRedisParserLibrary
LuaRestyCoreLibrary
LuaRestyDNSLibrary
LuaRestyLockLibrary
LuaRestyLrucacheLibrary
LuaRestyMemcachedLibrary
LuaRestyMySQLLibrary
LuaRestyRedisLibrary
LuaRestyStringLibrary
LuaRestyUploadLibrary
LuaRestyUpstreamHealthcheckLibrary
LuaRestyWebSocketLibrary
LuaRestyLimitTrafficLibrary
LuaRestyShellLibrary
LuaRestySignalLibrary
LuaTablePoolLibrary
LuaUpstreamNginxModule
OPM
PostgresNginxModule
RdsCsvNginxModule
RdsJsonNginxModule
RedisNginxModule
Redis2NginxModule
RestyCLI
SetMiscNginxModule
SrcacheNginxModule
StreamLuaNginxModule
XssNginxModule
```

### 参考
* `官网`
* ``
