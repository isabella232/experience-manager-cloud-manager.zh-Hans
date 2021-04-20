---
title: 客户历程
seo-title: Adobe AEM Cloud Manager客户历程
description: 可查看本页，了解您作为客户开始使用Cloud Manager的旅程。
seo-description: 可查看本页，了解您的AdobeAEM Cloud Manager入门旅程。
uuid: d4468eb6-5bde-48dd-b96e-0cc61e046f96
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: bc9a0d63-ae6b-4fe9-81e5-bf9844f04e54
feature: Getting Started
level: Beginner
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---


# 客户历程 {#customer-journey}

作为客户，您可能是Adobe Experience Manager(AEM)的新用户，目前使用的是AEM 6.4，或者可能需要升级到AEM 6.4版本才能使用[!UICONTROL Cloud Manager]。 以下情形说明了您作为新客户或现有客户开始[!UICONTROL Cloud Manager]的旅程。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 仅适用于使用AEM 6.4或更高版本的Adobe Managed Services客户。

## 上载到[!UICONTROL Cloud Manager]{#on-boarding-to-cloud-manager}

1. **Adobe Managed Services上的新AEM客户**

   作为新客户，您将作为Adobe Managed Services入门流程的一部分，上车到[!UICONTROL Cloud Manager]。

   用于访问[!UICONTROL Cloud Manager]的URL将包含在欢迎电子邮件中，并附上登录[!UICONTROL Experience Cloud]的说明，使用Adobe Admin Console管理您的用户以及需要访问[!UICONTROL Cloud Manager]的用户的相应权限。

1. **Adobe Managed Services上的现有AEM客户**

   作为现有客户，您首先需要将现有生产和非生产环境升级到AEM 6.4版。 同时，您将执行升级，并将上载并提供访问[!UICONTROL Cloud Manager]的URL。 此外，您还需要使用Adobe Admin Console对需要访问[!UICONTROL Cloud Manager]的用户进行开始，以管理您的用户及其各自的权限。

   您现有的AEM项目还需要符合推荐的最佳实践，因为您将使用[!UICONTROL Cloud Manager]开始将新代码更改部署到AEM环境。

   要获取有关升级到AEM 6.4的益处的更多信息，请参阅[升级到AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

## 访问[!UICONTROL Cloud Manager] {#accessing-cloud-manager}

只需登录[!UICONTROL Experience Cloud]登陆页，使用Adobe Identity Management凭据，然后从解决方案切换器界面中选择AEM，即可访问[!UICONTROL Cloud Manager]和AEM环境。

首次登录[!UICONTROL Cloud Manager]后，您将可以直接从[!UICONTROL Cloud Manager] UI访问您的AEM环境。 此时，您已准备好探索[!UICONTROL Cloud Manager]的所有可能性，一旦您的第一个代码分支准备好部署到您的舞台和生产环境。

要浏览并开始使用[!UICONTROL Cloud Manager]，请参阅[首次登录](first-time-login.md)。 有关AEM的其他信息，请参阅[AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/deploy.html)快速入门。 此外，请参阅[AEM资源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&amp;mv=other)以了解更多信息。

## [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}入门

登录[!UICONTROL Cloud Manager]后，首先需要设置代码存储库环境，然后设置团队和角色。 具体而言，通过使用Admin ConsoleUI将用户添加到[!UICONTROL Cloud Manager]用户档案来分配角色成员关系。

接下来，您必须在&#x200B;**Git存储库**&#x200B;中设置源代码分支，根据负载和性能KPI定义目标，并测试方案，以便在所有质量检查均成功通过后将代码成功部署到您的舞台和生产环境。

## 端到端旅程{#end-to-end-journey}

下图说明了在使用[!UICONTROL Cloud Manager] CI/CD管道将代码更改部署到舞台和生产环境时，客户旅程的高度。

![](assets/screen_shot_2018-05-15at124004pm.png)

