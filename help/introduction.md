---
title: Cloud Manager for AMS简介
description: 从此处开始，了解Adobe Managed Services(AMS)的Cloud Manager，以及它如何让组织在云中自行管理Adobe Experience Manager。
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 22d40a1f07f56ee7a7dddb4897e4079f1e346674
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 10%

---


# 简介 [!UICONTROL Cloud Manager] （对于AMS） {#introduction-to-cloud-manager}

从此处开始，了解Cloud Manager for Cloud Manager for Manage Services(AMS)，以及它如何让组织在云中自行管理Adobe Experience Manager。

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Cloud Manager for AMS简介"
>abstract="允许组织在云中自行管理Adobe Experience Manager。 它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="创建程序"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="创建环境"

## 简介 {#introduction}

[!UICONTROL Cloud Manager] 对于Adobe Experience Manager，开发人员能够通过基于Adobe Experience Manager最佳实践的简化工作流创建具有影响力的客户体验。 通过针对Adobe Experience Manager优化的CI/CD管道，您只需检入代码即可轻松合并开发工作流，然后代码可一直移动到生产就绪状态。 在构建阶段，将根据为客户提供可靠应用程序的最佳实践对您的自定义代码更新进行全面测试。 Cloud Manager使用开放API方法，使您能够与系统集成，而不会中断现有流程和工具。

>[!NOTE]
>
>本文档专门介绍适用于Adobe Managed Services(AMS)的Cloud Manager的特性和功能。
>
>AEMas a Cloud Service的对等文档可在 [AEMas a Cloud Service文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/home.html)

借助Cloud Manager，您的开发团队可以从以下功能中受益：

* 持续集成/持续交付(CI/CD)代码，将上市时间从几个月/几周缩短到几天/几小时

* 在投入生产之前，根据最佳实践进行代码检查、性能测试和安全验证，以最大限度地减少生产中断

* 用于补充现有DevOps流程的API连接

* 自动缩放功能可智能地检测增加容量的需求，并自动使更多的调度程序/发布区段联机

本图说明了 [!UICONTROL Cloud Manager]:

![CI/CD流量](/help/assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL Cloud Manager] 的主要功能  {#key-features-in-cloud-manager}

以下更深入地介绍了Cloud Manager的选定关键功能。

### 自助式界面 {#self-service-interface}

的用户界面(UI) [!UICONTROL Cloud Manager] 使您能够轻松访问和管理Adobe Experience Manager应用程序的云环境和CI/CD管线。

您可以定义特定于应用程序的关键绩效指标(KPI)（如每分钟的页面查看峰值和页面加载的预期响应时间），这些指标构成了衡量部署是否成功的基础。 可以轻松定义不同团队成员的角色和权限。自助服务界面将控制权交到您手中，但它也提供指向最佳实践资源的链接，以及联系Adobe内可根据需要提供必要指导的专家。

探索并开始使用 [!UICONTROL Cloud Manager]的UI，请参阅文档 [首次登录。](/help/getting-started/first-time-login.md)

### CI/CD 管线 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的其中一项重要功能，是能够实施优化的 CI/CD 管线来加速自定义代码或更新的交付，例如，在网站上添加新的组件。

通过 [!UICONTROL Cloud Manager] UI中，您可以配置并启动CI/CD管线。 作为此管道的一部分，将执行彻底的代码扫描，以确保只有高质量的应用程序才能通过到生产环境。

要详细了解如何从 [!UICONTROL Cloud Manager]的用户界面，查看文档 [配置生产管道](/help/using/production-pipelines.md) 和 [配置非生产管道。](/help/using/non-production-pipelines.md)

### 灵活的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 提供了灵活且可配置的部署模式，因此您可以根据不断变化的业务需求提供不同的体验。

在自动触发模式下，系统会根据特定事件（如代码提交）将代码自动部署到环境。 您还可以计划在指定的时间范围内，甚至在工作时间以外执行代码部署。

质量检查与部署触发器无关，每次触发部署时，质量检查始终作为CI/CD管线执行的一部分执行。 质量检查包括代码检查、安全测试和性能测试，所有这些都是开箱即用提供的，您或您的合作伙伴无需做任何工作。

要了解有关部署代码和质量检查的更多信息，请参阅此文档 [部署代码。](/help/using/code-deployment.md)

## Cloud Manager中的可选功能 {#optional-features-in-cloud-manager}

Cloud Manager提供了其他高级功能，根据您的特定环境设置和需求，该功能可能会对您的项目有益。 如果您对这些功能感兴趣，请联系您的客户成功工程师(CSE)或Adobe代表以进一步讨论。

### 自动缩放 {#autoscaling}

当生产环境承受异常高的负载时， [!UICONTROL Cloud Manager] 检测对额外容量的需求，并使用其自动缩放功能自动使额外容量联机。

在这种情况下， [!UICONTROL Cloud Manager] 自动触发自动缩放设置过程，发送自动缩放事件通知，并在几分钟内使额外容量联机。 额外容量是在生产环境中与运行的调度程序/发布节点相同的区域中进行配置的，并符合相同的系统规范。

自动缩放功能仅适用于调度程序/发布层，并且使用水平缩放方法执行，调度程序/发布对的至少一个额外区段最多十个区段。 所配置的任何额外容量都将在 CSE（客户成功工程师）确定的十个工作日内手动缩放。

>[!NOTE]
>
>如果您有兴趣探索自动缩放是否适合您的应用程序，请联系您的CSE或Adobe代表。

### 蓝色/绿色部署 {#blue-green}

蓝色/绿色部署是一种技术，通过运行两个称为蓝色和绿色的相同生产环境来减少停机时间和风险。

在任何时候，只有一个环境处于实时状态，且实时环境为所有生产流量提供服务。 通常，蓝色表示当前的实时环境，绿色表示空闲。

* 蓝色/绿色部署是Cloud Manager CI/CD管道的附加组件，其中创建了第二组发布和调度程序实例（绿色）并用于部署。 绿色实例随后会附加到生产负载平衡器，旧实例（蓝色）将被删除并终止。
* 蓝色/绿色实施将实例视为临时实例，蓝色/绿色管道的每次迭代都将创建一组新的发布和调度程序服务器。
* 将在设置中创建绿色的负载平衡器。 此负载平衡器将永远不会发生更改，您应将绿色或“测试”URL指向该负载平衡器。
* 在蓝色/绿色部署期间，将创建现有发布/调度程序层的确切副本（从TDL读取）。

#### 蓝色/绿色部署流程 {#flow}

启用蓝色/绿色部署后，部署流程与标准Cloud Service部署流程有所不同。

| 步骤 | 蓝色/绿色部署 | 标准部署 |
|---|---|---|
| 1 | 部署到创作 | 部署到创作 |
| 2 | 暂停测试 | - |
| 3 | 创建了绿色基础结构 | - |
| 4 | 部署到绿色发布层/调度程序层 | 部署到发布者 |
| 5 | 暂停测试（最长24小时） | - |
| 6 | 向生产负载平衡器中添加了绿色基础架构 | - |
| 7 | 从生产负载平衡器中删除了蓝色的基础架构 —  |
| 8 | 蓝色基础架构自动终止 | - |

#### 实施蓝色/绿色 {#implementing}

所有使用Cloud Manager进行生产部署的AMS用户都有资格使用蓝色/绿色部署。 但是，使用蓝色/绿色部署需要通过AdobeCSE对环境进行额外验证和设置。

如果您对蓝色/绿色部署感兴趣，请考虑以下要求和限制，并联系您的CSE。

#### 要求和限制 {#limitations}

* 蓝色/绿色仅适用于发布/调度程序对。
* 预览调度程序/发布对未包含在蓝色/绿色部署中。
* 每个Dispatcher/发布对都与每个其他Dispatcher/发布对相同。
* 蓝色/绿色仅在生产环境中可用。
* 蓝色/绿色在AWS和Azure中可用。
* 蓝色/绿色不仅适用于Assets客户。
