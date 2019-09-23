---
title: Cloud manager简介
seo-title: Cloud manager简介
description: '本页面是了解Cloud manager的起点。 '
seo-description: '本页是了解Adobe AEM Cloud manager的起点，并重点介绍优势和主要功能。 '
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 简介
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: d7c9ab3795fb3df02ab7dffd1328760ccd914a18

---


# 简介 [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## 简介 {#introduction}

[!UICONTROL Cloud Manager]作为Adobe Managed Cloud services的一部分，组织可以在云中自行管理Experience Manager。 它包含一个连续集成和连续交付(CI/CD)框架，使IT团队和实施合作伙伴能够在不影响性能或安全性的情况下加快定制或更新的交付。

使用自 [!UICONTROL Cloud Manager] 助客户门户，组织 **可以执行** /利用以下各项：

* **持续集成／持续交付代码** ，将上市时间从数月／周缩短到数天／小时。
* **代码检查、性能测试和基于最佳实践的安全性验证** ，然后再推向生产，以最大限度地减少生产中断。
* **自动、计划或手动部署** ，甚至在工作时间以外也可实现最大的灵活性和控制。
* **自动缩放** 功能可以智能地检测对增加容量的需求，并自动带来额外的在线调度程序／发布区段。

下图说明了在以下位置使用的CI/CD流程 [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## Adobe cloud中的主要功 [!UICONTROL Cloud Manager] 能 {#key-features-in-cloud-manager}

组织可以利用以下功能，包括 [!UICONTROL Cloud Manager]:

### 自助服务界面 {#self-service-interface}

客户使用的用户界面(UI) [!UICONTROL Cloud Manager] 可轻松访问和管理云环境以及Experience manager应用程序的CI/CD管道。

客户定义特定于应用程序的关键绩效指标(KPI)-每分钟峰值页面查看次数和页面加载的预期响应时间，这些最终构成了衡量成功部署的基础。 可以轻松定义不同团队成员的角色和权限。 新的自助服务界面将控制权交还给您，同时它还提供最佳实践链接并与Adobe内的专家联系，这些专家可以根据需要提供必要的指导。

要浏览UI并开始使 [!UICONTROL Cloud Manager]用，请参阅首 [次登录](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html)。

### CI/CD管道 {#ci-cd-pipeline}

其中一项关键功能 [!UICONTROL Cloud Manager] 是能够运行经过优化的CI/CD管道，以加快自定义代码或更新的交付，例如在网站上添加新组件。

通过 [!UICONTROL Cloud Manager] UI，客户可以配置CI/CD管道并启动CI/CD管道。 在这个管道中，执行彻底的代码扫描以确保只有高质量的应用程序才能通过生产环境。

要了解有关从UI配置管道的更 [!UICONTROL Cloud Manager]多信息，请参阅 [配置您的CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)。

### 灵活的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 为客户提供灵活、可配置的部署模式，使他们能够根据不断变化的业务需求提供体验。

使用自动触发模式，代码根据诸如代码提交之类的特定事件自动部署到环境。 您还可以在指定的时间范围内（甚至在工作时间以外）计划代码部署。

与部署触发器无关，质量检查始终作为CI/CD管道执行的一部分执行，每次触发部署时。 质量检查包括、代码检查、安全测试和开箱即用的性能测试，客户或其合作伙伴无需付出任何努力。

要了解有关部署代码和质量检查的更多信息，请参阅 [部署代码](deploying-code.md)

### 自动缩放 {#autoscaling}

[!UICONTROL Cloud Manager] 在生产环境面临异常高的负载时检测对额外容量的需求，并通过自动缩放功能自动将额外容量带到线上。

在自动缩放事件期 [!UICONTROL Cloud Manager] 间，自动触发自动缩放供应过程，发送自动缩放事件通知，并在几分钟内使附加容量联机。 将在生产环境中提供额外的容量，该容量位于与运行中的调度程序／发布节点相同的区域并匹配相同的系统规范。

自动缩放功能将仅应用于Dispatcher/Publish层，并且始终使用水平缩放方法执行，Dispatcher/Publish对中至少有一个额外段，最多十个段。 任何额外的容量将在由CSE（客户成功工程师）确定的十个工作日内手动扩展。
