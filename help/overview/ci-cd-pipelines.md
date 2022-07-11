---
title: CI/CD管线
description: 了解CI/CD管道以及它们如何在Cloud Manager中部署到暂存环境和生产环境。
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# CI/CD管线 {#ci-cd-pipeline}

了解CI/CD管道以及它们如何在Cloud Manager中部署到暂存环境和生产环境。

## 概述 {#overview}

[!UICONTROL Cloud Manager] 包括连续集成/连续交付(CI/CD)框架，该框架允许实施团队快速测试和交付新的或更新的代码。 例如，实施团队可以设置、配置和启动自动化的CI/CD管线，以利用Adobe编码最佳实践执行彻底的代码扫描并确保最高的代码质量。

CI/CD管道还可自动执行单元和性能测试流程，以提高部署效率，并主动确定在部署后需要解决的关键问题。 实施团队可以访问全面的代码性能报表，以深入了解在将代码部署到生产环境时，对KPI和关键安全验证的潜在影响。

## 管道过程 {#pipeline-process}

此图表说明在中触发某个版本后会发生的情况 [!UICONTROL Cloud Manager] 使用管道。

![管道过程](/help/assets/screen_shot_2018-05-30at82457pm.png)

| 管道步骤 | 描述 |
|---|---|
| 1.开始发行 | 部署管理器可以手动、通过git提交或根据定期计划触发发行版。 |
| 2.创建发行标记 | [!UICONTROL Cloud Manager] 创建一个git标记，以使用自动生成的版本号(例如， `2018.531.245527.0000001222`. |
| 3.以自动生成版本的形式构建 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4.评估代码质量 | [!UICONTROL Cloud Manager] 在将代码部署到暂存环境之前，会扫描源代码并提供摘要。 |
| 5.存储的版本化项目 | 将存储发行工件，以供稍后在部署步骤中使用。 |
| 6.自动将对象部署到AMS AEM暂存 | 释放对象将部署到暂存环境。 |
| 7.触发自动测试 | [!UICONTROL Cloud Manager] 对对象运行性能和安全测试。 |
| 8.生产触发器部署 | 自动测试完成后， [!UICONTROL Cloud Manager] 开始将部署到生产环境。 |
| 9. [!UICONTROL Cloud Manager] 获取要部署的工件 | [!UICONTROL Cloud Manager] 提取存储的释放工件。 |
| 10.将工件部署到生产环境 | 发布工件将部署到生产环境。 |

### 如何设置CI/CD管线 {#how-to-setup-a-ci-cd-pipeline}

要了解有关管道配置的更多信息，请参阅文档 [配置生产管道](/help/using/production-pipelines.md) 和 [配置非生产管道。](/help/using/non-production-pipelines.md)

## 质量门 {#quality-gates}

CI/CD管道提供质量门或接受标准，在将代码从暂存环境移动到部署环境之前，必须满足这些标准。 管道中有三扇门：

* 代码质量
* 性能测试
* 安全测试

对于每个门，可以识别三个级别的问题：

* **关键**  — 由闸门确定的关键问题导致管道立即失败。
* **重要信息**  — 由门标识的重要问题导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下管道会继续），也可以接受问题（在这种情况下，管道会因故障而停止）。
* **信息**  — 闸门所识别的信息问题仅供参考，对管道执行没有影响。

这是一个代码扫描示例，其中显示了已识别的问题。

![代码扫描示例](/help/assets/quality-gate-failed.png)

### 如何设置门 {#how-to-setup-gates}

查看文档 [配置生产管道](/help/using/production-pipelines.md) 有关设置代码、质量和性能门的详细信息。
