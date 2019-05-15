---
title: 使用云管理器前了解概念
seo-title: 使用云管理器前了解概念
description: 'null'
seo-description: 'null'
page-status-flag: 从未激活
uuid: 55cc551a-e812-4102-96c8-13d2 cdd79 c84
contentOwner: jsyal
discoiquuid: c3fd3f4e-0b57-4377-b923-a440 c7473 d8
preview: 'true'
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 使用云管理器前了解概念{#understanding-concepts-before-using-cloud-manager}

本节提供在使用Cloud Manager之前很好了解的概念和术语，并涵盖以下主题：

* **部署环境**
* **源代码存储库**
* **安全性和隐私**
* **管道概述**
* **帮助资源**

## 部署环境 {#deployment-environment}

您可能是Adobe Experience Manager(AEM)6.4的新用户或需要升级到AEM6.4版本。

如果您是AEM6.4的新用户，则您已经有权访问云管理器。

如果您是现有客户，则需要升级到AEM6.4才能访问云管理器。从客户成功工程师(CSE)收到URL和凭据后，您可以开始使用Cloud Manager。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:19:24.147-0400

Section is redundant with the section in the Overview topic

 -->

## 源代码存储库 {#source-code-repository}

**多个Git服务器**：在某些情况下，客户将拥有现有的git存储库并希望继续使用它。

在这些情况下，您可以对多个远程存储库使用git支持。日常开发将继续在您的Git存储库中进行。当需要部署时，您只需将最新代码推送到Cloud Manager Git存储库。

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

Cloud Manager将支持每个程序(上面定义的定义)，它负责处理舞台和生产的部署。****

用于舞台和生产部署的git分支为主集合。

>[!NOTE]
>
>最好将主视图用作舞台和生产的git分支，但您可以在设置管道时使用任何分支。

单一管道流程如下所示：

![](assets/screen_shot_2018-04-30at30318pm.png)

### 了解流程 {#understanding-the-flow}

您可以从云管理器UI [!UICONTROL Pipeline Settings] 的拼贴中配置管道。

有关更多信息，请参阅 [](hhttps://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) 使用云管理器。

部署经理负责设置渠道，即：

* 指定应用程序分支
* 分配部署环境
* 定义测试选项

在执行此操作时，您首先从其git存储库中选择一个分支。接下来，定义将启动管道的触发器。

接下来，您可以定义控制生产部署的参数。

最后，您将能够配置性能测试参数。

>[!NOTE]
>
>要了解如何配置渠道的行为和首选项，请参阅 **使用云管理器中的配置渠道**[部分](using-cloud-manager.md)。

### 帮助资源 {#help-resources}

联系Adobe Managed Services客户成功工程师以获得支持。

### 后续步骤 {#the-next-steps}

现在，您可以更好地了解Cloud Manager概念。

要设置项目、环境以及团队(用户和角色)，请参阅 [设置云管理器的常规配置](setting-configurations-for-cloud-manager.md)。
