---
title: 用户历程
description: 本文档阐述了不同的入门方案，并介绍了Cloud Manager快速入门历程。
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# 用户历程 {#user-journey}

作为Adobe Experience Manager用户，您可以：

* 是AEM的新用户。
* 当前正在使用AEM 6.x。
* 需要升级到AEM 6.5版本才能使用 [!UICONTROL Cloud Manager].

本文档阐述了这些情景并说明了您的入门历程 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 仅适用于使用AEM 6.4或更高版本的Adobe Managed Services(AMS)客户。

## 入门 {#onboarding}

载入过程因您是AMS的新客户还是现有AMS客户而异。

### Adobe Managed Services的新用户 {#new-to-ams}

作为新客户，您将被载入 [!UICONTROL Cloud Manager] 作为Adobe Managed Services入门流程的一部分。

在入门过程中，您将收到一封欢迎电子邮件，其中包括：

* 要访问的URL [!UICONTROL Cloud Manager]
* 登录说明 [!UICONTROL Experience Cloud]
* 有关使用Admin Console管理用户及其各自权限以便他们可以访问的说明 [!UICONTROL Cloud Manager] （如果需要）。

### 现有Adobe Managed Services客户 {#existing-customer}

作为现有AMS客户，您首先需要将现有的生产和非生产环境升级到AEM 6.4或更高版本。

执行升级时，您将被载入到Cloud Manager，并且会向您提供用于访问的URL [!UICONTROL Cloud Manager]. 此外，对于需要访问 [!UICONTROL Cloud Manager]，则需要开始使用Admin Console管理权限及其各自的权限。

由于您将开始使用，因此您现有的AEM项目还将需要符合推荐的最佳实践 [!UICONTROL Cloud Manager] ，以将新代码更改部署到AEM环境。

要获取有关升级到AEM 6.5的好处的其他信息，请参阅此文档 [升级到AEM 6.5。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)

## 访问 [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

您将能够访问 [!UICONTROL Cloud Manager] 和AEM环境，只需登录到 [!UICONTROL Experience Cloud] 登陆页面，使用您的AdobeIdentity Management凭据并从解决方案切换器界面中选择AEM。

登录后 [!UICONTROL Cloud Manager] 首次，您将可以直接从 [!UICONTROL Cloud Manager] UI。 此时，您已准备好探索 [!UICONTROL Cloud Manager] 并准备要部署到暂存和生产环境的第一个代码分支。

开始使用 [!UICONTROL Cloud Manager]，请参阅文档 [首次登录](/help/getting-started/first-time-login.md).

有关AEM的其他信息，请参阅此文档 [部署和维护。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

## 入门 [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

登录后 [!UICONTROL Cloud Manager] 您可以通过以下方式开始使用AEM项目：

1. 设置代码存储库环境。
1. 设置您的团队和角色。
   * 通过将用户添加到 [!UICONTROL Cloud Manager] 用户档案。
1. 在git存储库中设置源代码分支。
1. 根据负载和性能KPI定义您的目标。
1. 定义测试方案，以便在所有质量检查均成功通过后，将代码成功部署到暂存环境和生产环境。

## 端到端历程 {#end-to-end-journey}

此图表在使用 [!UICONTROL Cloud Manager] 用于将代码更改部署到暂存和生产环境的CI/CD管道。

![端到端历程](/help/assets/screen_shot_2018-05-15at124004pm.png)
