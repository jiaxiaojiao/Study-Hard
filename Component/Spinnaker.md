## Spinnaker

### 目录
* [Spinnaker 是什么？](#Spinnaker-是什么？)
* [参考](#参考)

### Spinnaker 是什么？
> Spinnaker is an open source, multi-cloud continuous delivery platform for releasing software changes with high velocity and confidence.
>
> Spinnaker is a continuous delivery platform for releasing changes with high velocity and confidence.

Spinnaker是一个开源的、多云的连续交付平台，用于以高速度和信心发布软件更改。

Spinnaker是一个持续的交付平台，以高速度和信心释放变化。

Spinnaker 出自 Netflix，它更关注持续部署而非持续集成。它可以与其他工具整合，比如 Travis 和 Jenkins，来启动测试和部署流程。它也能与 Prometheus、Datadog 这样的监控工具集成，参考它们提供的指标来决定如何部署。例如，在 金丝雀发布(canary deployment)里，我们可以根据收集到的相关监控指标来做出判断：最近的这次发布是否导致了服务降级，应该立刻回滚；还是说看起来一切 OK，应该继续执行部署。

谈到持续部署，一些另类但却至关重要的问题往往被忽略掉了，说出来可能有点让人困惑：Spinnaker 可以帮助持续部署不那么“持续”。在整个应用部署流程期间，如果发生了重大问题，它可以让流程停止执行，以阻止可能发生的部署错误。但它也可以在最关键的时刻让人工审核强制通过，发布新版本上线，使整体收益最大化。实际上，CI/CD 的主要目的就是在商业模式需要调整时，能够让待更新的代码立即得到部署。

### 参考
* 网站： https://www.spinnaker.io/
* 源码： https://github.com/spinnaker/spinnaker