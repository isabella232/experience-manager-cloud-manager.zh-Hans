---
title: CI/CD管线
seo-title: CI/CD管线
description: 'null'
seo-description: 按照本节了解CI/CD管线，它负责处理Cloud Manager中的舞台和生产部署。
uuid: 763ddb24-05cd-463f-8d72-a2 e69 bbe6 b7 e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579.0fa9fcc0592
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# CI/CD管线 {#ci-cd-pipeline}

## 管道概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包括连续集成(CI)和连续交付(CD)框架，它允许实施团队快速测试和提供新的或更新的代码。例如，实施团队可以设置、配置和启动自动化CI/CD管线，它利用Adobe编码最佳实践执行全面的代码扫描，并确保最高代码质量。

CI/CD管线还可自动执行单元和性能测试流程以提高部署效率，并主动识别部署后修复成本高昂的关键问题。实施团队可以访问一份全面的代码性能报告，了解在将代码部署到生产中时KPI和关键安全验证对KPI的潜在影响。

## 管道流程 {#pipeline-process}

以下示意图说明了在中触发版本后发生 [!UICONTROL Cloud Manager]的情况。下表介绍了工作流中的每个步骤。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表详细说明了过程的每个步骤中发生的情况：

| 管道流程步骤 | 发生了什么？ |
|---|---|
| 1. 启动版本 | 部署管理器通过Git提交或基于定期计划触发发布。 |
| 2. 创建版本标签 | [!UICONTROL Cloud Manager] 创建一个Git标签，以使用自动生成的版本号标记发行版。例如：2018.531.245527.2001222 |
| 3. 以自动生成版本的形式构建 | [!UICONTROL Cloud Manager] 使用新分配的版本号构建应用程序。 |
| 4. 评估代码质量 | [!UICONTROL Cloud Manager] 扫描源代码并提供一个摘要，先将代码部署到舞台环境 |
| 5. 专业的伪像存储 | 在部署步骤中存储释放伪像以供以后使用。 |
| 6. 自动将伪像部署到AMS AEM Stage | 将伪像部署到舞台环境。 |
| 7. 触发自动测试 | [!UICONTROL Cloud Manager] 在伪像上运行性能和安全测试。 |
| 8. 生产触发部署 | 完成自动化测试后， [!UICONTROL Cloud Manager] 将开始部署到生产。 |
| 9. [!UICONTROL Cloud Manager] 获取要部署的伪像 | [!UICONTROL Cloud Manager] 提取存储的释放伪像。 |
| 10. 将伪像消除为生产 | 发布伪像被部署到生产环境中。 |

### 如何设置CI/CD管线 {#how-to-setup-a-ci-cd-pipeline}

要了解有关管道配置的更多信息，请参阅 [配置管道](configuring-pipeline.md)。

## Quality Gates {#quality-gates}

CI/CD管线提供高质量门或接受条件，在代码从舞台环境移动到部署环境之前必须满足这些标准。管道中有三个入口：

* 代码质量
* 性能测试
* 安全测试

对于每个门，发现三个等级的问题：

* **关键** -门户确定的问题，导致管道立即失败。
* **重要** -由门户确定的问题，该问题导致渠道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，渠道会继续发展，也可以接受问题，在这种情况下，管道会停止失败。
* **信息** -由门户确定的问题，其仅用于信息性目的且不影响管道执行。

下面是代码扫描的示例，其中包含代码所标识的问题：

![](assets/quality-gate-failed.png)

### 如何设置门 {#how-to-setup-gates}

有关设置代码、质量和性能门的详细信息，请参阅 **[配置网关](configuring-pipeline.md)** 。
