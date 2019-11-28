## Vue.js

> 学习Vue.js之前需要有扎实的JavaScript/HTML/CSS基础。
>
> 来源： https://zhuanlan.zhihu.com/p/23134551

### 目录
* 基础
* 学习步骤
* 进阶

### 基础
* JavaScript 规范
    * ECMAScript 的历史和目前的规范制定方式
    * ES2015/16 的新特性
    * ES2015 modules
* 命令行的使用。（建议使用Mac）
* Node.js基础。
    * 使用 nvm 这样的工具来管理机器上的 Node 版本，并且将 npm 的 registry 注册表配置为淘宝的镜像源。
    * npm 的常用命令
    * npm scripts
    * 语义化版本号规则
    * CommonJS 模块规范，与ES2015 Modules 的异同。
    * Node 包的解析规则
    *  Node 的常用 API
    * 写一些基本的命令行程序
* 了解如何使用 / 配置 Babel 来将 ES2015 编译到 ES5 用于浏览器环境
* 学习 Webpack。

### 学习步骤

1. 官网教程基础篇。

2. 官网示例，自己想类似的例子。

3. 官网教程进阶版： Vue的响应式机制和组件生命周期。

4. 官网教程进阶版： 路由和状态管理，vue-router 和 vuex

### 进阶 

1. 通过 vue-cli 来搭建基于 Webpack ，并且支持单文件组件的项目

2. 根据 例子 尝试在 Webpack 模板基础上整合 vue-router 和 vuex

3. Virtual DOM 和『渲染函数 (Render Functions)』

4. （可选）根据需求，了解服务端渲染的使用（需要配合 Node 服务器开发的知识）。其实更重要的是理解它所解决的问题并搞清楚你是否需要它。

5. 阅读开源的 Vue 应用、组件、插件源码，自己尝试编写开源的 Vue 组件、插件。

6. 参考 贡献指南 阅读 Vue 的源码，理解内部实现细节。（需要了解 Flow）

