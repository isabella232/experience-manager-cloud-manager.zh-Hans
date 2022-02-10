---
title: Cloud Manager 简介
seo-title: Introduction to Cloud Manager
description: '本页作为了解 Cloud Manager 的起始点。 '
seo-description: This page serves as a starting point for learning about Adobe AEM Cloud Manager and highlights the benefits and key features.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
level: Beginner
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 66%

---

# [!UICONTROL Cloud Manager] 简介{#introduction-to-cloud-manager}

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Cloud Manager 简介"
>abstract="允许组织在云中自行管理Experience Manager。 它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="创建程序"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="创建环境"

## Communications API {#introduction}

[!UICONTROL Cloud Manager] 对于Adobe Experience Manager，开发人员能够通过基于Adobe Experience Manager最佳实践的简化工作流创建具有影响力的客户体验。 针对Adobe Experience Manager优化的CI/CD管道允许您通过检入代码并一直移动到生产就绪状态，轻松合并开发工作流。 在构建阶段，我们会使用经过尝试和学习的最佳实践对您的自定义代码更新进行彻底测试，以便为客户提供有影响的数字体验。 Cloud Manager使用开放API方法，使您能够与系统集成，而不会中断现有流程和工具。

本文档网站专门介绍了适用于Adobe Managed Services(AMS)客户的Cloud Manager的特性和功能。 AEMas a Cloud Service客户的对等文档可在 [为AEMas a Cloud Service实施应用程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html?lang=en).

借助Cloud Manager，您的开发团队可以利用以下功能：

* 持续集成和持续交付代码，将上市时间从几个月/几周缩短到几天/几小时。

* 在投入生产之前，根据最佳实践执行代码检查、性能测试和安全性验证以将生产中断降至最低。

* API连接，以补充现有DevOps流程。

* 自动缩放功能可智能地检测增加容量需求，并自动使更多的调度程序/发布区段联机。

下图说明了 [!UICONTROL Cloud Manager] 中使用的 CI/CD 流程：

![](assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL Cloud Manager] 的主要功能  {#key-features-in-cloud-manager}

组织可以利用 [!UICONTROL Cloud Manager] 的以下功能：

### 自助式界面 {#self-service-interface}

通过 [!UICONTROL Cloud Manager] 的用户界面 (UI)，客户可以轻松访问和管理其 Experience Manager 应用程序的云环境和 CI/CD 管线。

客户可以定义特定于应用程序的关键绩效指标 (KPI)（如每分钟的页面查看峰值和页面加载的预期响应时间），这些指标最终构成衡量部署是否成功的基础。可以轻松定义不同团队成员的角色和权限。新的自助式界面在将控制权重新交还给用户的同时，还提供了到最佳实践的链接，并且能够在需要时联系 Adobe 内可提供必要指导的专家。

探索并开始使用 [!UICONTROL Cloud Manager]的UI，请参阅 [首次登录](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD 管线 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的其中一项重要功能，是能够实施优化的 CI/CD 管线来加速自定义代码或更新的交付，例如，在网站上添加新的组件。

通过 [!UICONTROL Cloud Manager] UI，客户能够配置并启动他们的 CI/CD 管线。在执行此管线期间，会执行彻底的代码扫描，以确保只有高质量的应用程序才能投入到生产环境。

要详细了解如何从 [!UICONTROL Cloud Manager]的用户界面，查看文档 [配置生产管道](configuring-production-pipelines.md) 和 [配置非生产管道。](configuring-non-production-pipelines.md)

### 灵活的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 为客户提供了灵活的可配置部署模式，从而他们可以根据不断变化的业务需求提供不同体验。

在自动触发器模式下，系统会根据特定事件（例如，代码提交）将代码自动部署到环境。您还可以计划在指定的时间范围内，甚至在工作时间以外执行代码部署。

质量检查不依赖于部署触发器，每次触发部署时，都会在 CI/CD 管线执行期间执行质量检查。质量检查包括开箱即提供的代码审查、安全性测试和性能测试，无需客户或其合作伙伴进行任何操作。

要了解有关部署代码和质量检查的更多信息，请参阅[部署代码](deploying-code.md)

### 自动缩放 {#autoscaling}

[!UICONTROL Cloud Manager] 检测当生产环境遇到异常高的负载时对额外容量的需要，然后通过自动缩放功能使额外容量自动联机。

在自动缩放事件过程中，[!UICONTROL Cloud Manager] 自动触发自动缩放设置过程，发送自动缩放事件通知，并在几分钟内使额外容量联机。额外容量将在生产环境中与运行调度程序/发布节点相同的区域内进行配置，并遵守相同的系统规范。

自动缩放功能将仅应用于调度程序/发布层，并且始终使用水平缩放方法执行，一个调度程序/发布对至少一个额外区段，最多十个区段。所配置的任何额外容量都将在 CSE（客户成功工程师）确定的十个工作日内手动缩放。

>[!NOTE]
>有兴趣探索自动缩放是否适合其应用程序的客户必须联系其CSE或Adobe代表。
