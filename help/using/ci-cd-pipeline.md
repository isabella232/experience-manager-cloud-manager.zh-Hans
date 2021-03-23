---
title: CI/CD 管线
seo-title: CI/CD 管线
description: CI/CD Pipeline概述，它在Cloud Manager中处理舞台和生产部署
seo-description: 可查看本节以了解CI/CD管道，该管道在Cloud Manager中处理舞台和生产部署
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
feature: CI-CD管道
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---


# CI/CD 管线 {#ci-cd-pipeline}

## 管道概述{#pipeline-overview}

[!UICONTROL Cloud Manager] 包括连续集成(CI)和连续投放(CD)框架，使实施团队能够快速测试和交付新的或更新的代码。例如，实施团队可以设置、配置和开始自动化的CI/CD管道，该管道利用Adobe编码最佳做法执行彻底的代码扫描并确保最高的代码质量。

CI/CD管道还实现了单元和性能测试流程的自动化，以提高部署效率并主动确定在部署后修复成本高昂的关键问题。 实施团队可以访问全面的代码性能报告，以便了解在将代码部署到生产时对KPI的潜在影响和关键安全验证。

## 管道进程{#pipeline-process}

下图说明了在[!UICONTROL Cloud Manager]中触发发行版后会发生什么情况。 随附的表格说明了工作流中的每个步骤。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表详细说明了在流程的每个步骤中正在进行的操作：

| 管线处理步骤 | 怎么了？ |
|---|---|
| 1.开始发行版 | 部署管理器可以手动、通过Git提交或基于循环计划触发发行版。 |
| 2.创建发行标签 | [!UICONTROL Cloud Manager] 创建一个Git标记，以使用自动生成的版本号标记发行版。例如：2018.531.245527.0000001222 |
| 3.使用自动生成的版本构建为发行版 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4.评估代码质量 | [!UICONTROL Cloud Manager] 扫描源代码并提供摘要，然后将代码部署到舞台环境 |
| 5.已存储的版本化项目 | 将存储释放对象，以供以后在部署步骤中使用。 |
| 6.自动将对象部署到AMS AEM Stage | 释放对象将部署到舞台环境。 |
| 7.触发自动测试 | [!UICONTROL Cloud Manager] 对对象运行性能和安全性测试。 |
| 8.生产触发器部署 | 完成自动测试后，[!UICONTROL Cloud Manager]将部署开始到生产。 |
| 9.[!UICONTROL Cloud Manager]获取要部署的工件 | [!UICONTROL Cloud Manager] 提取存储的释放伪像。 |
| 10.将伪品放入生产 | 释放对象将部署到生产环境。 |

### 如何设置CI/CD管线{#how-to-setup-a-ci-cd-pipeline}

要了解有关管线配置的更多信息，请参阅[配置管线](configuring-pipeline.md)。

## 质量门{#quality-gates}

CI/CD管道提供质量门或接受标准，在将代码从阶段环境移动到部署环境之前必须满足这些标准。 有三扇大门正在酝酿之中：

* 代码质量
* 性能测试
* 安全测试

对于每一道门，已发现三个级别的问题：

* **关键**  — 由门确定的导致管道立即故障的问题。
* **重要**  — 由门确定的导致管线进入暂停状态的问题。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，管道继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。
* **信息**  — 由门确定的问题，这些问题仅用于信息目的，对管道执行没有影响。

以下是代码扫描的示例，其中包含为代码确定的问题：

![](assets/quality-gate-failed.png)

### 如何设置{#how-to-setup-gates}门

有关设置代码、质量和性能门的详细信息，请参阅&#x200B;**[配置门](configuring-pipeline.md)**。
