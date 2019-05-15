---
title: 云管理器简介
seo-title: 云管理器简介
description: '本页作为有关Cloud Manager的学习起点。 '
seo-description: '本页作为了解Adobe AEM Cloud Manager的起点，并突出显示优势和主要功能。 '
uuid: 62d68e79-c2 ba-4d8 b-ba7 d-33709014d5 b6
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9 e-4684-8146-d88 f4013 d4 d1
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 介绍 [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## 简介 {#introduction}

[!UICONTROL Cloud Manager]作为Adobe Managed Cloud Services的一部分，组织可以在云中自行管理Experience Manager。它包括持续集成和持续交付(CI/CD)框架，使IT团队和实施合作伙伴能够加快自定义或更新交付，而不会影响性能或安全性。

使用 [!UICONTROL Cloud Manager] 自助服务客户门户， **组织可以** 执行/利用以下各项：

* **持续集成/持续交付** 代码，将时间从数月/数周缩短到数天/数小时。
* **代码检查、性能测试和安全验证基于** 最佳实践，然后推送到生产以最大限度减少生产中断。
* **甚至在业务时间外自动、定时或手动部署** ，从而实现最大灵活性和控制。
* **自动缩放** 功能可智能检测需要增加容量并自动引入在线额外的调度程序/发布区段。

下图说明了在以下方面使用的CI/CD流程流程 [!UICONTROL Cloud Manager]：

![](assets/screen_shot_2018-05-12at73843pm.png)

## 主要功能 [!UICONTROL Cloud Manager]{#key-features-in-cloud-manager}

组织可以利用以下功能， [!UICONTROL Cloud Manager]包括：

### 自助服务界面 {#self-service-interface}

用户界面(UI)使客户 [!UICONTROL Cloud Manager] 能够轻松访问和管理云环境以及其Experience Manager应用程序的CI/CD管线。

客户定义特定于应用程序的关键绩效指标(KPI)-每分钟页面查看次数和页面加载预期响应时间，这最终构成评估成功部署的基础。可以轻松定义不同团队成员的角色和权限。新的自助服务界面将控制权放回手中，同时它还提供了最佳实践的链接和Adobe内专家的访问权限，他们可以根据需要提供必要的指导。

要探索和开始使用UI， [!UICONTROL Cloud Manager]请参阅 [首次登录](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html)。

### CI/CD管线 {#ci-cd-pipeline}

其主要功能之一是 [!UICONTROL Cloud Manager] 执行优化的CI/CD管线以加快自定义代码或更新的交付，如在网站上添加新组件。

通过 [!UICONTROL Cloud Manager] UI，客户可以配置并启动其CI/CD管线。在此管道中，执行整个代码扫描以确保只有高质量的应用程序传递到生产环境。

要了解有关从 [!UICONTROL Cloud Manager]UI配置管道的更多信息，请参阅 [配置CI/CD管线](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)。

### 灵活的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 为客户提供灵活、可配置的部署模式，以便根据不断变化的业务需求提供体验。

使用自动触发器模式，代码会根据特定事件(如代码提交)自动部署到环境。您还可以在指定的时间范围内计划代码部署，甚至在业务时间以外。

与部署触发器无关，质量检查始终在每次触发部署时执行CI/CD管线执行的一部分。质量检查包括客户或其合作伙伴所需的代码检查、安全测试、安全测试和性能测试。

要了解有关部署代码和质量检查的更多信息，请参阅 [部署代码](deploying-code.md)

### 自动缩放 {#autoscaling}

[!UICONTROL Cloud Manager] 检测生产环境受到异常高负载时需要额外容量，并通过自动缩放功能自动带来更多容量。

在自动缩放事件期间 [!UICONTROL Cloud Manager] ，自动触发自动缩放供应过程，发送自动缩放事件的通知，并在几分钟内将附加容量引入。额外的容量将在生产环境中进行供应，在同一区域中，与运行调度程序/发布节点的系统规范相同。

自动缩放功能只适用于调度程序/发布层，并且始终使用水平缩放方法执行，最少只需使用一个调度程序/发布对，最多可达十个区段。任何额外的容量将在CSE(客户成功工程师)确定的10个工作日内手动放大。
