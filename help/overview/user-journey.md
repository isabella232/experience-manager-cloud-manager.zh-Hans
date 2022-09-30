---
title: 用户历程
description: 本文档列出了不同的新用户引导场景，并解释了您的 Cloud Manager 快速入门历程。
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: ht
source-wordcount: '504'
ht-degree: 100%

---


# 用户历程 {#user-journey}

作为 Adobe Experience Manager 用户，您：

* 可以是 AEM 新手。
* 可以是现有 AEM 6.x 客户。
* 需要升级到 AEM 6.5 版以便使用 [!UICONTROL Cloud Manager]。

本文档列出了这些场景，并解释了您的 [!UICONTROL Cloud Manager] 快速入门历程。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 仅适用于使用 AEM 6.4 或更高版本的 Adobe Managed Services (AMS) 客户。

## 新用户引导 {#onboarding}

根据您是 AMS 新手还是现有 AMS 客户，新用户引导过程会有所不同。

### Adobe Managed Services 新手 {#new-to-ams}

作为新客户，在 Adobe Managed Services 新用户引导过程中，您将登录 [!UICONTROL Cloud Manager]。

在新用户引导过程中，您将收到一封欢迎电子邮件，其中包括：

* 用于访问 [!UICONTROL Cloud Manager] 的 URL
* [!UICONTROL Experience Cloud] 登录说明
* 有关使用 Admin Console 管理您的用户及其相应权限以便他们能够访问 [!UICONTROL Cloud Manager]（如果需要）的说明。

### 现有 Adobe Managed Services 客户 {#existing-customer}

作为现有 AMS 客户，您首先需要将现有的生产环境和非生产环境升级到 AEM 6.4 或更高版本。

在执行此升级时，您将登记到 Cloud Manager 并获得用于访问 [!UICONTROL Cloud Manager] 的 URL。此外，对于那些需要访问 [!UICONTROL Cloud Manager] 的用户，您将需要开始使用 Admin Console 来管理这些用户及其相应权限。

您现有的 AEM 项目还需要符合推荐的最佳实践，因为您将开始使用 [!UICONTROL Cloud Manager] 将新的代码更改部署到 AEM 环境。

要获取有关升级到 AEM 6.5 的好处的其他信息，请参阅[升级到 AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html) 文档。

## 访问 [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

只需通过使用 Adobe Identity Management 凭据登录到 [!UICONTROL Experience Cloud] 登陆页面并从解决方案切换器界面选择 AEM，即可获得对 [!UICONTROL Cloud Manager] 和 AEM 环境的访问权限。

在首次登录 [!UICONTROL Cloud Manager] 后，您将有权直接从 [!UICONTROL Cloud Manager] UI 访问 AEM 环境。此时，您已能开始探索 [!UICONTROL Cloud Manager] 的所有可能性，并准备好您的第一个代码分支以部署到暂存和生产环境。

要开始使用 [!UICONTROL Cloud Manager]，请参阅[首次登录](/help/getting-started/first-time-login.md)文档。

有关 AEM 的其他信息，请参阅[部署和维护](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)文档。

## [!UICONTROL Cloud Manager] 快速入门 {#getting-started-with-cloud-manager}

在登录到 [!UICONTROL Cloud Manager] 后，您可以通过以下方式开始使用 AEM 项目：

1. 设置您的代码存储库环境。
1. 设置您的团队和角色。
   * 通过使用 Admin Console 将用户添加到 [!UICONTROL Cloud Manager] 配置文件来分配角色成员资格。
1. 在 Git 存储库中设置源代码分支。
1. 根据负载和性能 KPI 定义您的目标。
1. 定义测试场景，以便在成功通过所有质量检查后将代码成功部署到暂存环境和生产环境。

## 端到端历程 {#end-to-end-journey}

此图从较高层面说明了使用 [!UICONTROL Cloud Manager] CI/CD 管道将代码更改部署到暂存环境和生产环境时的客户历程。

![端到端历程](/help/assets/screen_shot_2018-05-15at124004pm.png)
