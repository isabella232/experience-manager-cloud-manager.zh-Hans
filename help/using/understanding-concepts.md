---
title: 在使用Cloud manager之前了解概念
seo-title: 在使用Cloud manager之前了解概念
description: 'null'
seo-description: 'null'
page-status-flag: 从未激活
uuid: 55cc551a-e812-4102-96c8-13d2cdd79c84
contentOwner: jsyal
discoiquuid: c3fd3f4e-0b57-4377-b923-a440c74773d8
preview: 'true'
translation-type: tm+mt
source-git-commit: f135526c6a47f1502395e6d53f9e286c0f935da5

---


# 在使用Cloud manager之前了解概念{#understanding-concepts-before-using-cloud-manager}

本节提供在Cloud manager中工作之前非常熟悉的概念和术语，并涵盖以下主题：

* **部署环境**
* **源代码存储库**
* **安全性和隐私**
* **管道概述**
* **帮助资源**

## 部署环境 {#deployment-environment}

您可能是Adobe Experience Manager(AEM)6.4的新用户，或者需要升级到AEM 6.4版本。

如果您是AEM 6.4的新用户，那么您已经有权访问Cloud Manager。

如果您是现有客户，则需要升级到AEM 6.4才能访问Cloud Manager。 从客户成功工程师(CSE)那里收到URL和凭据后，即可开始使用Cloud Manager。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:19:24.147-0400

Section is redundant with the section in the Overview topic

 -->

## 源代码存储库 {#source-code-repository}

**多个Git服务器**:在某些情况下，客户将拥有现有的git存储库并希望继续使用它。

对于这些情况，您可以使用git对多个远程存储库的支持。 日常开发将继续在您的git存储库中进行。 当需要部署时，您只需将最新代码推送到Cloud Manager Git存储库。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:20:46.002-0400

Looks like we lost some content, compared to the previous version

 -->

## 安全性和隐私 {#security-and-privacy}

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-04-21T02:38:21.417-0400

Query for Brad B.

 -->

## 管道概述 {#pipeline-overview}

Cloud manager将支持每个计划（上面的定义）一个管道，用于处理部署到舞台和生产。 ****

用于舞台和生产部署的git分支是主分支。

>[!NOTE]
>
>将master用作舞台和生产的Git分支是最佳实践，但在设置管道时，您可以使用其中的任何分支。

单个管道流程说明如下：

![](assets/screen_shot_2018-04-30at30318pm.png)

### 了解流 {#understanding-the-flow}

您可以从云管理器UI的拼 [!UICONTROL Pipeline Settings] 贴中配置渠道。

有关更 [多信息，请参阅](hhttps://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) “使用云管理器”。

部署管理器负责设置管道，即：

* 分配应用程序分支
* 分配部署环境
* 定义测试选项

执行此操作时，您首先从其git存储库中选择一个分支。 接下来，定义将启动管道的触发器。

接下来，您可以定义控制生产部署的参数。

最后，您将能够配置性能测试参数。

>[!NOTE]
>
>要了解如何配置管道的行为和首选项，请参阅使 **用云管理器**[中的配置管道部分](using-cloud-manager.md)。

### 帮助资源 {#help-resources}

请与Adobe Managed services客户成功工程师联系以获取支持。

### 后续步骤 {#the-next-steps}

现在，您对Cloud manager概念有了更好的了解。

要设置您的项目、环境和团队（用户和角色），请参阅为Cloud manager [设置常规配置](setting-configurations-for-cloud-manager.md)。
