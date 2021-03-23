---
title: 使用向导
description: 可查看本页以了解如何使用向导创建AEM应用程序项目
feature: 入门
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 10%

---


# 使用向导{#using-wizard-to-create-an-aem-application-project}

当客户已上载到Cloud Manager时，他们会获得一个空的git存储库。 当前Adobe Managed Services(AMS)客户(或迁移到AMS的预置AEM客户)通常已将其项目代码放在git（或其他版本控制系统）中，并将其项目导入Cloud Manager存储库。 但是，新客户没有现有项目。

为了帮助新客户入门，Cloud Manger现在可以创建最少的AEM项目作为起点。 此过程基于&#x200B;[**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. 登录到Cloud Manager并完成基本程序设置后，如果存储库为空，“ **Overview** ”屏幕上将显示一张特殊的行动动员卡。

   ![](assets/image2018-10-3_14-29-44.png)

1. 单击&#x200B;**创建以**&#x200B;打开一个对话框，该对话框允许用户提供AEM Project Archetype所需的参数。 在默认表单中，对话框要求输入两个值：

   * **标题**  — 默认情况下，它设置为 *项目名*

   * **新分支名称**  — 默认情况下，这是 *主控*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   该对话框有一个抽屉，可通过单击对话框底部的手柄来打开该抽屉。 在其扩展形式中，该对话框显示Archetype的所有配置参数。 其中许多参数具有默认值，这些默认值是根据&#x200B;**Title**&#x200B;生成的。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果&#x200B;**Title**&#x200B;为&#x200B;***We.Finance***，则Base Maven Artifact Id参数将生成为&#x200B;***com.wefinance***。 如果需要，可以更改这些值。
   >
   >
   >例如，您可以将生成的&#x200B;***值com.wefinance***&#x200B;更改为&#x200B;***net.wefinance***。

1. 单击上一步中的&#x200B;**创建**，使用原型创建启动项目并提交到指定的git分支。 完成此操作后，可以设置管道。