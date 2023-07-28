---
title: Cloud Manager for AMS 简介
description: 从此处开始了解 Cloud Manager for Adobe Managed Services (AMS) 以及它如何使组织能够在云中自行管理 Adobe Experience Manager。
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: a2cea28061304d109a3c9a48650d01255579443c
workflow-type: ht
source-wordcount: '1322'
ht-degree: 100%

---


# [!UICONTROL Cloud Manager] for AMS 简介 {#introduction-to-cloud-manager}

从此处开始了解 Cloud Manager for Adobe Managed Services (AMS) 以及它如何使组织能够在云中自行管理 Adobe Experience Manager。

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Cloud Manager for AMS 简介"
>abstract="使组织能够在云中自行管理 Adobe Experience Manager。它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义项或更新。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=zh-Hans#cloud-manager" text="创建项目"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=zh-Hans#cloud-manager" text="创建环境"

## 简介 {#introduction}

[!UICONTROL Cloud Manager] for Adobe Experience Manager 使开发人员能够通过基于 Adobe Experience Manager 最佳实践构建的简化工作流来打造令人印象深刻的客户体验。利用为 Adobe Experience Manager 优化的 CI/CD 管道，您可以轻松地合并开发工作流。只需签入代码，代码随后会持续推进到生产就绪状态。在构建阶段，将根据最佳实践全面测试自定义代码更新，以便为客户提供可靠的应用程序。Cloud Manager 使用开放式 API 方法，使您能够在不中断现有流程和工具的情况下与系统集成。

>[!NOTE]
>
>本文档具体描述了 Cloud Manager for Adobe Managed Services (AMS) 的特性和功能。
>
>可以在 [AEM as a Cloud Service 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/home.html)中找到 AEM as a Cloud Service 的等效文档。

使用 Cloud Manager 时，您的开发团队将从以下功能受益：

* 持续集成/持续交付 (CI/CD) 代码，将上市时间从几个月/几周缩短到几天/几小时

* 在投入生产之前，根据最佳实践执行代码审查、性能测试和安全性验证以将生产中断降至最低

* API 连接，对现有 DevOps 过程进行补充

* 自动缩放功能可智能地检测增加容量需求，并自动使更多的 Dispatcher/发布区段联机

下图说明了 [!UICONTROL Cloud Manager] 中使用的 CI/CD 流程：

![CI/CD 流](/help/assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL  中的主要功能Cloud Manager] {#key-features-in-cloud-manager}

下面对精选的 Cloud Manager 主要功能进行了深入探讨。

### 自助式界面 {#self-service-interface}

利用 [!UICONTROL Cloud Manager] 的用户界面 (UI)，您可以轻松访问和管理 Adobe Experience Manager 应用程序的云环境和 CI/CD 管道。

您可以定义特定于应用程序的关键绩效指标 (KPI)（如每分钟的页面查看峰值和页面加载的预期响应时间），这些指标构成了衡量部署是否成功的基础。可以轻松定义不同团队成员的角色和权限。自助式界面在将控制权重新交还给您的同时，还提供了指向最佳实践资源的链接，并使您能够在需要时联系可提供必要指导的 Adobe 专家。

要探究并开始使用 [!UICONTROL Cloud Manager] 的 UI，请参阅[首次登录文档。](/help/getting-started/first-time-login.md)

### CI/CD 管道 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的一项重要功能是，能够实施优化的 CI/CD 管道来加速自定义代码或更新的交付，例如，在网站上添加新的组件。

通过 [!UICONTROL Cloud Manager] UI，您能够配置并启动您的 CI/CD 管道。在执行此管道期间，会执行彻底的代码扫描，以确保只有高质量的应用程序才能投入到生产环境。

要详细了解如何从 [!UICONTROL Cloud Manager] UI 配置管道，请参阅[配置生产管道](/help/using/production-pipelines.md)和[配置非生产管道文档。](/help/using/non-production-pipelines.md)

### 灵活的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 提供了灵活的可配置部署模式，使您能够根据不断变化的业务需求来交付体验。

在自动触发器模式下，系统会根据特定事件（例如，代码提交）将代码自动部署到环境。您还可以计划在指定的时间范围内，甚至在工作时间以外执行代码部署。

质量检查不依赖于部署触发器，每次触发部署时，都会在 CI/CD 管道执行期间执行质量检查。质量检查包括现成的代码审查、安全性测试和性能测试，无需您或您的合作伙伴进行任何操作。

要了解有关部署代码和质量检查的更多信息，请参阅[部署代码](/help/using/code-deployment.md)文档。

## Cloud Manager 中的可选功能 {#optional-features-in-cloud-manager}

Cloud Manager 提供了附加高级功能，这些功能可能有助于实施您的项目，具体取决于特定环境设置和需求。如果您对这些功能感兴趣，请联系您的客户成功工程师 (CSE) 或 Adobe 代表来进行深入讨论。

### 自动缩放 {#autoscaling}

当生产环境承受异常高的负载时，[!UICONTROL Cloud Manager] 将检测对额外容量的需求，并使用其自动缩放功能自动使额外容量联机。

在此类事件中，[!UICONTROL Cloud Manager] 自动触发自动缩放配置过程，发送自动缩放事件通知，并在几分钟内使额外容量联机。额外容量将在生产环境中与运行 Dispatcher/发布节点相同的区域内进行配置，并遵守相同的系统规范。

自动缩放功能将仅应用于 Dispatcher/发布层，并且始终使用水平缩放方法执行，一个 Dispatcher/发布对至少一个额外区段，最多十个区段。所配置的任何额外容量都将在 CSE（客户成功工程师）确定的十个工作日内手动缩放。

>[!NOTE]
>
>如果您想探索自动缩放功能是否适合您的应用程序，请联系您的 CSE 或 Adobe 代表。

### 蓝/绿部署 {#blue-green}

蓝/绿部署是一种方法，通过运行两个分别称作蓝色和绿色的相同生产环境来减少停机时间并降低风险。

在任何时候，只有一个环境是实时的，并且实时环境服务于所有生产流量。通常，蓝色表示当前的实时环境，绿色表示空闲环境。

* 蓝/绿部署是 Cloud Manager CI/CD 管道的附加组件，其中创建了第二组发布和 Dispatcher 实例（绿色）并将它们用于部署。随后，将绿色实例附加到生产负载平衡器，并移除和终止旧的实例（蓝色）。
* 此蓝/绿实施将实例视为瞬态实例，并且蓝/绿管道的每次迭代都会创建一组新的发布和 Dispatcher 服务器。
* 在设置过程中，将创建一个绿色负载平衡器。此负载平衡器永不会发生改变，并且您应将绿色或“测试”URL 指向它。
* 在蓝/绿部署期间，将创建现有发布/Dispatcher 层的精确副本。

#### 蓝/绿部署流 {#flow}

启用蓝/绿部署时，部署流与标准 Cloud Service 部署流不同。

| 步骤 | 蓝/绿部署 | 标准部署 |
|---|---|---|
| 1 | 部署到作者 | 部署到作者 |
| 2 | 暂停以进行测试 | - |
| 3 | 创建绿色基础架构 | - |
| 4 | 部署到绿色发布/Dispatcher 层 | 部署到发布者 |
| 5 | 暂停以进行测试（最多 24 小时） | - |
| 6 | 将绿色基础架构添加到生产负载平衡器 | - |
| 7 | 从生产负载平衡器中移除蓝色基础架构 |
| 8 | 暂停以进行最终签发（最长 24 小时） | - |
| 9 | 自动终止蓝色基础架构 | - |
| 10 | 管道完成 | - |

#### 实施蓝/绿部署 {#implementing}

所有使用 Cloud Manager 进行生产部署的 AMS 用户都有资格使用蓝/绿部署。不过，要使用蓝/绿部署，不仅需要对您的环境进行额外验证，还需要由 Adobe CSE 进行设置。

如果您想进行蓝/绿部署，请考虑以下要求和限制并联系您的 CSE。

#### 要求和限制 {#limitations}

* 蓝/绿部署仅适用于发布/Dispatcher 对。
* 在蓝/绿部署中，不会预览 Dispatcher/发布对。
* 每个 Dispatcher/发布对都与所有其他 Dispatcher/发布对相同。
* 蓝/绿部署仅适用于生产环境。
* 可以在 AWS 和 Azure 中进行蓝/绿部署。
* 蓝/绿部署不适用于仅使用 Assets 的客户。
