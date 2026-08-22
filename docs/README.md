---
title: 不高山上 · Bugaoshan
editLink: false
---

# 不高山上 · Bugaoshan

**不高山上**（Bugaoshan）是由 **The-Brotherhood-of-SCU** 团队开发的四川大学校园助手 App，聚合课表、成绩、通知、校园服务和个性化工具，帮助川大学生处理日常学习与校园事务。

“不高山”是江安校区的一处标志性地标。App 以此命名，寓意扎根校园、服务同学。

## 从这里开始

- [用户手册](./manual/)：按使用场景查阅完整操作说明
- [快速入门](./manual/getting-started.md)：下载安装、首次启动、登录和导入第一份课表
- [更新日志](./changelog/)：查看各版本的功能更新与问题修复
- [开发文档](./develop/)：了解项目结构、架构和参与贡献的方法

## 功能概览

### 办事大厅与校园事务

- 在线提交离校请假申请，并查看请假、报备等申请记录
- 办理返校报备、暑假离校和留校登记
- 查询第二课堂活动、体测记录、空闲教室、校园网设备、校园卡和各类生活余额
- 查看校历、志愿四川、办事大厅和校园通知
- 浏览教务处、党委学工部、青春川大通知，并下载和管理附件

### 学习相关

- 从教务处等多来源导入和管理多份课表，并支持课程编辑、周次设置和课表小组件
- 将课表和考表导出为 ICS 日历文件或复制到剪切板
- 查询成绩、方案修读情况、培养方案、考试安排和班级课表

### 个性化体验

- 自定义主题颜色、课程表样式、字体、应用图标、动画时长和底部 Dock
- 支持 Android、iOS、macOS 的课表小组件；macOS 还支持将课表导入系统日历

## 下载与安装

请前往 [GitHub Releases](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/releases/latest) 下载最新版本。

当前主仓库的正式发布流程自动构建以下平台：

- Android
- Windows
- Linux

主仓库代码同时提供 iOS 和 macOS 支持，但这两个平台的安装渠道以项目公告和 Release 页面实际提供的制品为准。

::: tip 邀测
**iOS 与鸿蒙版本正在邀测中**，欢迎加入官方 QQ 群（1102483776）参与测试。
:::

## 获取帮助

遇到问题时，请先确认正在使用最新版本，再根据[故障排查](./manual/troubleshooting.md)页面检查登录、网络、导入和附件等常见问题。

如需提交问题，请准备以下信息：

- 在“不高山上 → 我的 → 关于 → 开发者页面 → 认证日志”中导出的认证日志
- 在同一页面的“环境信息”中复制的设备与应用环境信息
- 可复现问题的操作步骤、使用的平台和应用版本

问题可以通过官方 QQ 群或 GitHub Issue 反馈；提交 Issue 前请参阅[贡献指南中的 Issue 规范](./develop/guide/contribution-guide.md#issue-%E8%A7%84%E8%8C%83)。

## 当前版本

以下是最近一次发布的功能更新与修复。完整历史请查看[更新日志](./changelog/)。

::: details 最近更新
<!-- @include: ./changelog/_latest.md -->

:::

## 自行构建与贡献

各平台的构建和运行要求请参阅[开发指南](./develop/guide/getting-started.md)。欢迎通过 Issue、Pull Request 或文档改进参与项目建设。

## 开源许可

不高山上基于 [AGPL-3.0](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/blob/main/LICENSE) 协议开源。使用软件前请阅读 [EULA](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/blob/main/assets/eula.md)。

本应用为非官方第三方应用，与四川大学不存在隶属、授权或认可关系。

感谢所有贡献者以及 Flutter 等开源项目。完整依赖列表和对应协议请参阅主仓库的 [pubspec.yaml](https://github.com/The-Brotherhood-of-SCU/Bugaoshan/blob/main/pubspec.yaml)。
