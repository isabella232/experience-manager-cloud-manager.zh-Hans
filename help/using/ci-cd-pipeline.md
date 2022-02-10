---
title: CI/CD 管线
seo-title: CI/CD Pipeline
description: CI/CD管道概述，该管道可在Cloud Manager中处理暂存和生产部署
seo-description: Follow this section to learn about the CI/CD pipeline, which handles deployments to stage and production in Cloud Manager
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
feature: CI-CD Pipeline
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 1%

---

# CI/CD 管线 {#ci-cd-pipeline}

## 管道概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包括连续集成(CI)和连续交付(CD)框架，该框架允许实施团队快速测试和交付新的或更新的代码。 例如，实施团队可以设置、配置和启动自动化的CI/CD管线，以利用Adobe编码最佳实践执行彻底的代码扫描并确保最高的代码质量。

CI/CD管道还可自动执行单元和性能测试流程，以提高部署效率，并主动确定在部署后需要解决的关键问题。 实施团队可以访问全面的代码性能报表，以深入了解在将代码部署到生产环境时，对KPI和关键安全验证的潜在影响。

## 管道过程 {#pipeline-process}

下图说明了在中触发某个版本后会发生什么情况 [!UICONTROL Cloud Manager]. 随附的表说明了工作流中的每个步骤。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表详细列出了流程每个步骤中所发生的情况：

| 管道处理步骤 | 这是怎么回事？ |
|---|---|
| 1.开始发行 | 部署管理器可以手动、通过Git提交或根据定期计划触发发行版。 |
| 2.创建发行标记 | [!UICONTROL Cloud Manager] 创建一个Git标记，以使用自动生成的版本号标记发行版。 例如：2018.531.245527.0000001222 |
| 3.以自动生成版本构建为版本 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4.评估代码质量 | [!UICONTROL Cloud Manager] 扫描源代码并提供摘要，然后代码才能部署到暂存环境 |
| 5.存储的版本化项目 | 将存储发行工件，以供稍后在部署步骤中使用。 |
| 6.自动将对象部署到AMS AEM Stage | 释放对象将部署到暂存环境。 |
| 7.触发自动测试 | [!UICONTROL Cloud Manager] 对对象运行性能和安全测试。 |
| 8.生产触发器部署 | 自动测试完成后 [!UICONTROL Cloud Manager] 开始将部署到生产环境。 |
| 9. [!UICONTROL Cloud Manager] 获取要部署的工件 | [!UICONTROL Cloud Manager] 提取存储的释放工件。 |
| 10.将工件放入生产 | 发布工件将部署到生产环境。 |

### 如何设置CI/CD管线 {#how-to-setup-a-ci-cd-pipeline}

要了解有关管道配置的更多信息，请参阅文档 [配置生产管道](configuring-production-pipelines.md) 和 [配置非生产管道。](configuring-non-production-pipelines.md)

## 质量门 {#quality-gates}

CI/CD管线提供质量门或验收标准，在将代码从暂存环境移动到部署环境之前，必须满足这些标准。 管道中有三扇门：

* 代码质量
* 性能测试
* 安全测试

对于每个门，都会发现三个级别的问题：

* **关键**  — 由闸门确定的导致管道立即失败的问题。
* **重要信息**  — 由门标识的导致管道进入暂停状态的问题。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下管道会继续），也可以接受问题（在这种情况下，管道会因故障而停止）。
* **信息**  — 闸门所识别的仅供参考且对管道执行没有影响的问题。

以下是代码扫描示例，其中包含针对代码发现的问题：

![](assets/quality-gate-failed.png)

### 如何设置门 {#how-to-setup-gates}

查看文档 [配置生产管道](configuring-production-pipelines.md) 有关设置代码、质量和性能门的详细信息。
