---
title: 使用向导
description: 请阅读本页，了解如何使用向导创建AEM应用程序项目
feature: 入门
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 10%

---

# 使用向导{#using-wizard-to-create-an-aem-application-project}

将客户载入Cloud Manager后，他们将获得一个空的git存储库。 当前的Adobe Managed Services(AMS)客户(或迁移到AMS的内部部署AEM客户)通常已在git（或其他版本控制系统）中包含其项目代码，并将其项目导入Cloud Manager git存储库。 但是，新客户没有现有项目。

为了帮助开始新客户，Cloud Manger现在能够创建一个最小的AEM项目作为起点。 此过程基于&#x200B;[**AEM项目原型**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. 登录到Cloud Manager并完成基本程序设置后，如果存储库为空，“ **Overview** ”屏幕上将显示一张特殊的行动动员卡。

   ![](assets/image2018-10-3_14-29-44.png)

1. 单击&#x200B;**创建到**&#x200B;打开一个对话框，该对话框允许用户提供AEM项目原型所需的参数。 在默认表单中，对话框要求输入两个值：

   * **标题**  — 默认情况下，此名称将设置为“项目 *名称”*

   * **新分支名称**  — 默认情况下，此名称 *主控*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   该对话框有一个抽屉，通过向对话框底部单击手柄可打开该抽屉。 该对话框以扩展形式显示原型的所有配置参数。 其中许多参数具有基于&#x200B;**Title**&#x200B;生成的默认值。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果&#x200B;**Title**&#x200B;为&#x200B;***We.Finance***，则Base Maven Artifact Id参数将生成为&#x200B;***com.wefinance***。 如有需要，可以更改这些值。
   >
   >
   >例如，您可以将生成的&#x200B;***值com.wefinance***&#x200B;更改为&#x200B;***net.wefinance***。

1. 在上一步中，单击&#x200B;**创建**&#x200B;以使用原型创建起始项目并提交到命名的git分支。 完成此操作后，您可以设置管道。
