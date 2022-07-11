---
title: Cloud Manager for AMS简介
description: 从此处开始，了解Adobe Managed Services(AMS)的Cloud Manager，以及它如何让组织在云中自行管理Adobe Experience Manager。
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 14%

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
>AEMas a Cloud Service的对等文档可在 [AEMas a Cloud Service文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html)

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

### 自动缩放 {#autoscaling}

当生产环境承受异常高的负载时， [!UICONTROL Cloud Manager] 检测对额外容量的需求，并使用其自动缩放功能自动使额外容量联机。

在这种情况下， [!UICONTROL Cloud Manager] 自动触发自动缩放设置过程，发送自动缩放事件通知，并在几分钟内使额外容量联机。 额外容量是在生产环境中与运行的调度程序/发布节点相同的区域内进行配置的，并与相同的系统规范相匹配。

自动缩放功能仅适用于调度程序/发布层，并且使用水平缩放方法执行，调度程序/发布对的至少一个额外区段最多十个区段。 所配置的任何额外容量都将在 CSE（客户成功工程师）确定的十个工作日内手动缩放。

>[!NOTE]
>
>有兴趣探索自动缩放是否适合其应用程序的客户应联系其CSE或Adobe代表。
