---
title: 架构设计
icon: mdi:sitemap
index: true
collapsed: false
dir:
  order: 4
---

# 架构设计

本栏目描述 Bugaoshan 当前代码如何工作，是"当前实现"的权威说明，必须随实现变更同步更新。设计取舍与长期约束见[架构决策](../decisions/)。

| 文档 | 对应 ADR | 范围 | 状态 |
| --- | --- | --- | --- |
| [通知 WebView 架构](./notice-webview.md) | [ADR-0001](../decisions/0001-use-webview-and-js-injection-for-notices.md) | 三类通知来源、JS bridge、附件下载和平台边界 | 当前实现 |
| [认证架构](./authentication.md) | [ADR-0002](../decisions/0002-separate-subsystem-authentication.md) | SCU 根认证、子系统认证、重试、会话隔离和 DI | 当前实现 |
| [Linux 分发架构](./linux-distribution.md) | [ADR-0004](../decisions/0004-use-distribution-wpe-on-linux.md) | GitHub tar.gz、WPE 边界、Flatpak、AUR 和 Debian 状态 | 当前实现 |
| [发布流水线](./release-pipeline.md) | — | 两级分支流、预览/正式双通道、版本号模型与边界情况 | 当前实现 |
| [iOS 液态玻璃适配](./ios-liquid-glass.md) | — | UIKit 系统标签栏、原生按钮/开关、Flutter 内容延伸与平台回退 | 当前实现 |
| [iOS TestFlight 分发](./ios-distribution.md) | — | 本地归档、签名、上传、测试分发和加密问卷 | 当前实现 |

::: tip 维护规则
- 架构文档与代码冲突时以代码为准，并在同一变更中修正文档。
- 本栏目镜像自应用仓库的 [`docs/architecture/`](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/blob/main/docs/architecture)，新增或修改架构文档时两处同步。
- 文档使用仓库相对链接，不写本机绝对路径或易失效的代码行号。
:::
