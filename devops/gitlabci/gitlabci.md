---
title: Gitlab CI
icon: gitlab
author: jangrui
category: 自动化
tags:
  - GitlabCI
copyrightText: >-
  本教程采用<a href="https://creativecommons.org/licenses/by-sa/3.0/deed.zh">知识共享
  署名-相同方式共享 3.0协议</a>
---

# Gitlab CI实践

## 简介

**GitLabCI** 轻量级，不需要复杂的安装手段。配置简单，与`gitlab`可直接适配。实时构建日志十分清晰，`UI`交互体验很好。使用 `YAML` 进行配置，任何人都可以很方便的使用。GitLabCI 有助于DevOps人员，例如敏捷开发中，开发与运维是同一个人，最便捷的开发方式。

## 为什么要学习这门课程?

### 您的团队需要CI / CD工作流程

* **持续集成**：尽快发现错误、减少集成问题、避免复杂的问题。
* **持续交付**：确保每个更改都是可发布的、降低每次发布的风险、更加频繁地交付价值、紧密的客户反馈循环。

![images](../../.gitbook/assets/01%20%281%29.png)

### GitLab CI / CD有独特优势

GitLab CI / CD是GitLab的一部分，支持从计划到部署具有出色的用户体验。CI / CD是开源GitLab社区版和专有GitLab企业版的一部分。测试可以在单独的计算机上分布式运行，您可以根据需要添加任意数量的计算节点，每个构建可以拆分为多个作业，这些作业可以在多台计算机上并行运行。

**集成、开源、无缝、可扩展、更快的结果、针对交付进行了优化**

![images](../../.gitbook/assets/02.png)

### GitLabCI/CD架构组成

**GitLab CI / CD** 是GitLab的一部分，GitLab是一个Web应用程序，具有将其状态存储在数据库中的API。除了GitLab的所有功能之外，它还管理项目/构建并提供一个不错的用户界面。

**GitLab Runner** 是一个处理构建的应用程序。它可以单独部署，并通过API与GitLab CI / CD一起使用。

