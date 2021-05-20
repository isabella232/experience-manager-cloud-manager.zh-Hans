---
title: 客户历程
seo-title: AdobeAEM Cloud Manager客户历程
description: 请阅读本页，了解您作为客户开始使用Cloud Manager的历程。
seo-description: 请阅读本页，了解您作为客户的历程，以开始使用AdobeAEM Cloud Manager。
uuid: d4468eb6-5bde-48dd-b96e-0cc61e046f96
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: bc9a0d63-ae6b-4fe9-81e5-bf9844f04e54
feature: 入门
level: Beginner
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 2%

---

# 客户历程 {#customer-journey}

作为客户，您可能是Adobe Experience Manager(AEM)的新用户，目前使用的是AEM 6.4，或者可能需要升级到AEM 6.4版本才能使用[!UICONTROL Cloud Manager]。 以下情形将说明您作为新客户或现有客户开始使用[!UICONTROL Cloud Manager]的历程。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 仅适用于使用AEM 6.4或更高版本的Adobe Managed Services客户。

## [!UICONTROL Cloud Manager]{#on-boarding-to-cloud-manager}入门

1. **Adobe Managed Services上的新AEM客户**

   作为新客户，您将作为Adobe Managed Services入门流程的一部分，载入到[!UICONTROL Cloud Manager]。

   用于访问[!UICONTROL Cloud Manager]的URL将包含在欢迎电子邮件中，并附有关于登录[!UICONTROL Experience Cloud]的说明，以及使用Adobe Admin Console管理需要访问[!UICONTROL Cloud Manager]的用户及其各自的权限。

1. **Adobe Managed Services上的现有AEM客户**

   作为现有客户，您首先需要将现有的生产和非生产环境升级到AEM 6.4版本。 在执行升级的同时，您将被载入并获得访问[!UICONTROL Cloud Manager]的URL。 此外，您还需要开始使用Adobe Admin Console来管理用户及其各自的权限，以供需要访问[!UICONTROL Cloud Manager]的用户使用。

   您现有的AEM项目还将需要符合建议的最佳实践，因为您将开始使用[!UICONTROL Cloud Manager]将新代码更改部署到AEM环境。

   要获取有关升级到AEM 6.4的好处的其他信息，请参阅[升级到AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

## 访问[!UICONTROL Cloud Manager] {#accessing-cloud-manager}

您只需登录到[!UICONTROL Experience Cloud]登录页面，使用您的AdobeIdentity Management凭据，然后从解决方案切换器界面中选择AEM即可访问[!UICONTROL Cloud Manager]和AEM环境。

首次登录[!UICONTROL Cloud Manager]后，您将可以直接从[!UICONTROL Cloud Manager] UI访问AEM环境。 此时，您已准备好探索[!UICONTROL Cloud Manager]的所有可能性，只要您准备好将第一个代码分支部署到暂存环境和生产环境即可。

要探索[!UICONTROL Cloud Manager]并开始使用，请参阅[首次登录](first-time-login.md)。 有关AEM的其他信息，请参阅[AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/deploy.html)快速入门。 此外，有关更多信息，请参阅[AEM Resources](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&amp;mv=other)。

## [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}快速入门

登录[!UICONTROL Cloud Manager]后，首先需要设置代码存储库环境，然后设置团队和角色。 具体而言，角色成员关系是通过使用Admin ConsoleUI将用户添加到[!UICONTROL Cloud Manager]配置文件来分配的。

接下来，您必须在&#x200B;**Git存储库**&#x200B;中设置源代码分支，根据负载和性能KPI定义目标，并测试方案，以便在所有质量检查均成功通过后，将代码成功部署到暂存和生产环境。

## 端到端历程{#end-to-end-journey}

下图从高层说明了在使用[!UICONTROL Cloud Manager] CI/CD管线将代码更改部署到暂存和生产环境时的客户历程。

![](assets/screen_shot_2018-05-15at124004pm.png)
