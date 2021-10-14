---
title: 配置 CI/CD 管线
seo-title: Configure your CI/CD Pipeline
description: 可以按照本页从Cloud Manager配置管道设置。
seo-description: Before you start to deploy your code, you must configure your pipeline settings from the AEM Cloud Manager.
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: fd172a7168074630e85f3b110e032f783d39ddca
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 1%

---

# 配置 CI/CD 管线 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>要了解如何在AEMas a Cloud Service中为Cloud Manager配置CI/CD管线，请参阅[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)。

以下页介绍如何配置&#x200B;**Pipeline**。 要查看有关管道工作方式的更多概念信息，请参阅[CI/CD管道概述](ci-cd-pipeline.md)。

## 视频教程 {#video-tutorial-one}

### 在Cloud Manager中配置管道 {#config-pipeline-video}

CI/CD生产管道配置定义将启动管道的触发器、控制生产部署和性能测试参数的参数。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## 了解流量 {#understanding-the-flow}

您可以在 UI中通过“管 **线设置** ”拼贴配 [!UICONTROL Cloud Manager]置管道 。

部署管理器负责设置管道。 这样做时，首先从&#x200B;**Git存储库**&#x200B;中选择一个分支。 管道配置包括：

* 定义将启动管道的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 设置管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存储库至少有一个分支且[程序设置](setting-up-program.md)完成之前，无法设置管道。

在开始部署代码之前，必须从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>在初始设置后，可以更改管道设置。

## 从管道卡添加新的生产管线 {#adding-production-pipeline}

设置程序并使用[!UICONTROL Cloud Manager] UI至少有一个环境后，即可添加生产管道。

请按照以下步骤配置生产管道的行为和首选项：

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**Pipelines**&#x200B;卡。

1. 单击&#x200B;**+Add**&#x200B;并选择&#x200B;**添加生产管道**。

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **此时会显** 示“添加生产管道”对话框。

   1. 输入管道名称。 您可以选择&#x200B;**Repository**&#x200B;和&#x200B;**Git分支**。

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. 您可以从&#x200B;**部署选项**&#x200B;中设置&#x200B;**部署触发器**&#x200B;和&#x200B;**重要失败行为**。

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      您可以定义启动管道的触发器：

      * **手动**  — 使用UI手动启动管道。
      * **在Git更改中**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。即使选择此选项，也始终可以手动启动管道。

         >[!NOTE]
         >在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。
      这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

      * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
      * **立即取消**  — 如果选中此选项，则每当发生重要故障时，管道都将被取消。这实质上是在模拟用户手动拒绝每个故障。
      * **立即批准**  — 如果选中此选项，则每当发生重要故障时，管道将自动继续。这实质上是在模拟用户手动批准每次失败。
   1. 选择&#x200B;**部署选项**。

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **在Stage部署后** 进行批准的功能与在生产部署前进行批准的功能类似，但是会在Stage部署步骤之后立即进行，即在完成任何测试之前，与在生产部署前进行批准（在所有测试完成后完成）进行比较。

      * **跳过负载平衡器**
   1. 为Stage选择&#x200B;**Dispatcher配置**。 输入路径，从&#x200B;**Type**&#x200B;中选择操作，然后单击&#x200B;**Add Path**。 每个环境最多可以指定100个路径。

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. 为生产选择&#x200B;**部署选项**。 现在，您可以定义控制生产部署的参数。 以下是三个可用选项：

      * **使用上线批准**  — 部署必须由业务所有者、项目经理或部署经理通过UI手动 [!UICONTROL Cloud Manager] 批准。
      * **使用CSE监督**  — 使用CSE来实际开始部署。在管道设置或启用CSE监督时进行编辑期间，部署管理器可以选择：

      * **任何CSE**:是指任何可用的案例
      * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）

      * **已计划**  — 此选项允许用户启用已计划的生产部署。

         >[!NOTE]
         >如果选择了&#x200B;**Scheduled**&#x200B;选项，则可以在阶段部署(和&#x200B;**使用GoLive批准**，如果已启用)之后，将生产部署计划到管道&#x200B;**之后。**&#x200B;用户还可以选择立即执行生产部署。
         >
         >请参阅[部署代码](deploying-code.md)，以设置部署计划或立即执行生产。
   1. 为生产设置&#x200B;**Dispatcher配置**。 输入路径，从&#x200B;**Type**&#x200B;中选择操作，然后单击&#x200B;**Add Path**。 每个环境最多可以指定100个路径。

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      作为部署管理器，您可以配置一组内容路径，在设置或编辑管道时，这些路径将从AEM Dispatcher缓存中为publish实例配置失效的&#x200B;****&#x200B;或&#x200B;**flushed**。

      您可以为暂存和生产部署配置一组单独的路径。 如果已配置，则在部署任何内容包后，这些缓存操作将作为部署管道步骤的一部分执行。 这些设置使用标准AEM Dispatcher行为 — 无效执行缓存失效，与从创作到发布激活内容时类似；刷新执行缓存删除。

      通常，最好使用无效操作，但有时可能需要刷新，尤其是在使用AEMHTML客户端库时。

      >[!NOTE]
      >
      >请参阅[Dispatcher概述](dispatcher-configurations.md)获取有关Dispatcher缓存的更多信息。





1. 选择所有选项后，单击&#x200B;**继续**。

1. 从&#x200B;**暂存测试**&#x200B;步骤中选择您的选项。 您可以配置&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;性能测试，具体取决于您已获得许可的产品。 有关更多详细信息，请参阅[性能测试](understand-your-test-results.md#performance-testing)。

   1. 从&#x200B;**站点内容交付/分布式负载权重**&#x200B;中选择您的选项。 有关更多详细信息，请参阅性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites)中的[AEM Sites。

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. 从&#x200B;**Assets性能测试分发**&#x200B;中选择您的选项。 有关更多详细信息，请参阅性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets)中的[AEM Assets。

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. 单击&#x200B;**Save**&#x200B;以完成添加生产管道。

### 编辑生产管道 {#editing-prod-pipeline}

可以从&#x200B;**程序概述**&#x200B;页面编辑管道配置。

请按照以下步骤编辑已配置的管道：

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡。

1. 单击&#x200B;**...从**&#x200B;管道&#x200B;**卡中单击**&#x200B;编辑&#x200B;**，如下图所示。**


1. 此时将显示&#x200B;**编辑生产管道**&#x200B;对话框。

   1. 通过&#x200B;**Configuration**&#x200B;选项卡，可更新&#x200B;**管道名称**、**部署触发器**&#x200B;和&#x200B;**重要量度失败行为**。

      >[!NOTE]
      >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，以了解如何在Cloud Manager中添加和管理存储库。


   1. **Source**&#x200B;选项卡提供了选项，用于选中或取消选中&#x200B;**Pause before deploying to Production**&#x200B;和&#x200B;**Scheduled**&#x200B;选项（从&#x200B;**Production Deployment Options**）。


   1. 通过&#x200B;**体验审核**&#x200B;选项，您可以更新或添加新页面。


1. 编辑完管道后，单击&#x200B;**更新**。

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/Setup-Pipeline.png)




## 仅限非生产和代码质量管道

除了部署到暂存和生产的主管道之外，客户还能够设置其他管道，称为&#x200B;**非生产管道**。 这些管道始终执行生成和代码质量步骤。 它们也可以选择部署到Adobe Managed Services环境。

## 视频教程 {#video-tutorial-two}

### Cloud Manager非生产和仅代码质量管道 {#non-prod-video}

CI/CD非生产管道分为两类：代码质量管道和部署管道。 代码质量会从Git分支中管道所有代码，以根据Cloud Manager的代码质量扫描构建和评估这些代码。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### 添加非生产管道 {#add-non-production-pipeline}

在主屏幕上，这些管道将列在新卡中：

1. 从Cloud Manager主屏幕中访问&#x200B;**Pipelines**&#x200B;卡。 单击&#x200B;**+Add**&#x200B;并选择&#x200B;**添加非生产管道**。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **此时将显示“添加非生**  产管道”对话框。选择要创建的管道类型，包括&#x200B;**代码质量管道**&#x200B;或&#x200B;**部署管道**。

   此外，您还可以从&#x200B;**部署选项**&#x200B;中设置&#x200B;**部署触发器**&#x200B;和&#x200B;**重要失败行为**。 单击&#x200B;**继续**。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. 现在，新创建的非生产管道会显示在&#x200B;**Pipelines**&#x200B;卡中。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   管道显示在主屏幕的卡片上，带有三个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管线文档资源。

### 编辑非生产管道 {#editing-nonprod-pipeline}

可以从&#x200B;**程序概述**&#x200B;页面的&#x200B;**管道卡**&#x200B;编辑管道配置。

请按照以下步骤编辑配置的非生产管道：

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡。

1. 选择非生产管道并单击&#x200B;**...**。 单击&#x200B;**编辑**，如下图所示。

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. 此时会显示&#x200B;**编辑生产管道**&#x200B;对话框，用于更新&#x200B;**管道名称**、**存储库**、**Git分支**、**部署触发器**&#x200B;和&#x200B;**重要量度失败行为**。

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >请参阅[添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，以了解如何在Cloud Manager中添加和管理存储库。


1. 编辑完非生产管道后，单击&#x200B;**更新**。


## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关更多详细信息，请参阅[部署代码](deploying-code.md)。
