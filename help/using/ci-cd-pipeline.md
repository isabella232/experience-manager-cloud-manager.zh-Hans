---
title: CI/CD 管线
seo-title: CI/CD 管线
description: 'null'
seo-description: 可查看本节以了解CI/CD管道，该管道在Cloud Manager中处理舞台和生产部署。
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
translation-type: tm+mt
source-git-commit: 8580cec50ac5dafb4e2525371a39d58c82f1cbc9
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 1%

---


# CI/CD 管线 {#ci-cd-pipeline}

## 管道概述{#pipeline-overview}

[!UICONTROL Cloud Manager] 包括连续集成(CI)和连续投放(CD)框架，它允许实施团队快速测试和交付新的或更新的代码。例如，实施团队可以设置、配置和开始自动化CI/CD管道，该管道利用Adobe编码最佳实践执行彻底的代码扫描并确保最高的代码质量。

CI/CD管道还自动处理单元和性能测试流程，以提高部署效率并主动确定部署后需要解决的关键问题。 实施团队可以访问全面的代码性能报告，以便了解将代码部署到生产时对KPI的潜在影响和关键安全验证。

## 管道进程{#pipeline-process}

下图说明在[!UICONTROL Cloud Manager]中触发发行版后会发生什么情况。 随附的表说明了工作流中的每个步骤。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表详细说明了在流程的每个步骤中所发生的情况：

| 管线处理步骤 | 怎么回事？ |
|---|---|
| 1.开始版本 | 部署管理器可以手动、通过Git提交或基于循环计划触发发布。 |
| 2.创建发行标记 | [!UICONTROL Cloud Manager] 创建一个Git标签，使用自动生成的版本号来标记发行版。例如：2018.531.245527.0000001222 |
| 3.使用自动生成的版本构建为发行版 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4.评估代码质量 | [!UICONTROL Cloud Manager] 扫描源代码并提供摘要，然后将代码部署到阶段环境 |
| 5.已存储的版本化项目 | 发行版对象会存储起来供以后在部署步骤中使用。 |
| 6.自动将对象部署到AMS AEM Stage | 释放对象将部署到阶段环境。 |
| 7.触发自动测试 | [!UICONTROL Cloud Manager] 对对象运行性能和安全性测试。 |
| 8.生产触发器部署 | 完成自动测试后，[!UICONTROL Cloud Manager]将部署开始到生产。 |
| 9.[!UICONTROL Cloud Manager]获取要部署的工件 | [!UICONTROL Cloud Manager] 提取存储的释放伪像。 |
| 10.将伪像放置到生产 | 发布对象将部署到生产环境。 |

### 如何设置CI/CD管道{#how-to-setup-a-ci-cd-pipeline}

要了解有关管线配置的更多信息，请参阅[配置管线](configuring-pipeline.md)。

## 质量门{#quality-gates}

CI/CD管道提供质量门或接受标准，在将代码从阶段环境移动到部署环境之前，必须满足这些标准。 有三扇门在等待：

* 代码质量
* 性能测试
* 安全测试

对于每个门，已发现三个级别的问题：

* **关键** -由门确定的导致管道立即故障的严重问题。
* **重要** -由门标识的导致管道进入暂停状态的问题。部署经理、项目经理或业务所有者可以改写问题，在这种情况下，管道将继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。
* **信息** -由门确定的问题，这些问题仅用于信息目的，对管道执行没有影响。

以下是代码扫描的示例，其中包含为代码确定的问题：

![](assets/quality-gate-failed.png)

### 如何设置门{#how-to-setup-gates}

有关设置代码、质量和性能门的详细信息，请参阅&#x200B;**[配置门](configuring-pipeline.md)**。
