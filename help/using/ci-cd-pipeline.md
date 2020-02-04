---
title: CI/CD 管线
seo-title: CI/CD 管线
description: 'null'
seo-description: 请按照本节内容了解CI/CD管道，该管道在Cloud Manager中处理舞台和生产部署。
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
translation-type: tm+mt
source-git-commit: 2d7b18ea55e2bd5879cf8bd896cafed4d46c0011

---

SHANKARI_TEST_CHANGE
# CI/CD 管线 {#ci-cd-pipeline}

## 管道概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包括连续集成(CI)和连续交付(CD)框架，使实施团队能够快速测试和交付新的或更新的代码。 例如，实施团队可以设置、配置和启动自动的CI/CD管道，该管道利用Adobe编码最佳实践来执行彻底的代码扫描并确保最高的代码质量。

CI/CD管道还自动处理单元和性能测试流程，以提高部署效率并主动识别部署后需要解决的关键问题。 实施团队可以访问全面的代码性能报告，以便在将代码部署到生产时了解对KPI的潜在影响和关键安全验证。

## 管道处理 {#pipeline-process}

下图说明了在中触发发行版后会发生什么情况 [!UICONTROL Cloud Manager]。 随附的表格说明了工作流中的每个步骤。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表详细说明了在流程的每个步骤中所发生的情况：

| 管线处理步骤 | 怎么回事？ |
|---|---|
| 1.开始发布 | 部署管理器可以手动、通过Git提交或基于重复计划触发发布。 |
| 2.“创建发布”标签 | [!UICONTROL Cloud Manager] 创建一个Git标签，使用自动生成的版本号标记发行版。 例如：2018.531.245527.000001222 |
| 3.内置为发行版，自动生成版本 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4.评估代码质量 | [!UICONTROL Cloud Manager] 扫描源代码并提供摘要，然后代码才能部署到舞台环境 |
| 5.已存储的版本控制对象 | 发行版对象会存储起来，供以后在部署步骤中使用。 |
| 6.自动将对象部署到AMS AEM Stage | 释放对象将部署到舞台环境。 |
| 7.触发自动测试 | [!UICONTROL Cloud Manager] 对对象运行性能和安全性测试。 |
| 8.生产触发器部署 | 自动测试完成后， [!UICONTROL Cloud Manager] 开始部署到生产。 |
| 9.获 [!UICONTROL Cloud Manager] 取要部署的对象 | [!UICONTROL Cloud Manager] 提取存储的释放伪像。 |
| 10.将伪像部署到生产 | 发行版对象将部署到生产环境。 |

### 如何设置CI/CD管道 {#how-to-setup-a-ci-cd-pipeline}

要了解有关管道配置的更多信息，请参 [阅配置管道](configuring-pipeline.md)。

## 质量门 {#quality-gates}

CI/CD管道提供质量门或接受标准，在将代码从舞台环境移动到部署环境之前必须满足这些标准。 有三扇门在酝酿中：

* 代码质量
* 性能测试
* 安全性测试

对于每个门，已发现三个级别的问题：

* **关键** -由门确定的导致管道立即故障的问题。
* **重要** -由门确定的导致管道进入暂停状态的问题。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下，管道会继续），或者他们可以接受问题（在这种情况下，管道会因故障而停止）。
* **信息** -门所查明的问题，这些问题仅供参考，对管道执行没有影响。

以下是代码扫描的示例，其中包含为代码确定的问题：

![](assets/quality-gate-failed.png)

### 如何设置门 {#how-to-setup-gates}

有关 **[设置代码、质量和性能门的详细信息](configuring-pipeline.md)**，请参阅配置门。
