---
title: 配置生产管道
description: 了解如何使用Cloud Manager创建和配置生产管道以部署代码。
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 205113735cc743e11e140b1161413002844f5b79
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 0%

---

# 配置生产管道 {#configuring-production-pipelines}

了解如何使用Cloud Manager创建和配置生产管道以部署代码。 如果您首先想要更概念化地概述Cloud Manager中管道的工作方式，请参阅 [CI/CD管道概述文档。](ci-cd-pipeline.md)

>[!NOTE]
>
>要了解如何在AEMas a Cloud Service中为Cloud Manager配置CI/CD管道，请参阅 [aemaCS文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html#using-cloud-manager)

## 概述 {#understanding-the-flow}

使用 **管道设置** 图块 [!UICONTROL Cloud Manager] UI。

可以创建两种不同类型的管线。

* **生产管道**  — 生产管道是由一系列精心策划的步骤组成的专门构建的管道，从始至终将源代码引入生产。
* **非生产管道**  — 非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境。

本文档重点介绍生产管道。 有关如何配置非生产管道的详细信息，请参阅此文档 [配置非生产管道。](configuring-non-production-pipelines.md)

的 **部署管理器** 角色负责设置管道。 管道配置包括：

1. 定义将启动管道的触发器。
1. 定义控制生产部署的参数。
1. 配置性能测试参数。

>[!NOTE]
>
>只有在其关联的git存储库具有至少一个分支和 [程序设置](setting-up-program.md) 完成。

>[!NOTE]
>
>在初始设置后，可以更改管道设置。

## 视频教程 {#video-tutorial-one}

请观看此视频，了解管道创建过程的概述。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## 添加新的生产管道 {#adding-production-pipeline}

使用 [!UICONTROL Cloud Manager] 要设置程序并至少拥有一个环境的UI，您可以添加生产管道。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，单击 **+添加** 选择 **添加生产管道**.

   ![添加生产管道](/help/using/assets/configure-pipelines/add-prod1.png)

1. 的 **添加生产管道** 对话框打开 **配置** 选项卡，其中必须定义管道的多个选项。 这些选项分组为可折叠的部分，并在以下步骤中进行说明。

   1. 为中的管道提供一个描述性名称 **管道名称** 字段。

   1. 在 **源代码** 部分，可定义管道在何处检索它将处理的代码。

      * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
      >[!TIP]
      >
      >查看文档 [设置程序](setting-up-program.md) 了解如何在Cloud Manager中添加和管理存储库。

      * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
      * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。

      ![为管道定义repo](/help/using/assets/configure-pipelines/add-prod2.png)

   1. 在 **环境** 部分，您可以定义触发部署的因素以及应如何根据环境进行部署。

      1. 在 **阶段** 部分，您可以定义管道如何转出到暂存环境。

         * **部署触发器**  — 您可以使用以下选项定义启动管道的部署触发器。

            * **手动**  — 使用此选项可使用Cloud Manager UI手动启动管道。
            * **在Git更改时**  — 只要将提交添加到配置的git分支，此选项就会启动CI/CD管道。 通过此选项，您仍可以根据需要手动启动管道。
         * **重要量度失败行为**  — 在管道设置或编辑期间，当在任何质量门中遇到重要故障时，部署管理器可以选择定义管道的行为。 可用选项包括：

            * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
            * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
            * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。

         ![部署触发器](/help/using/assets/configure-pipelines/add-prod3.png)

         * **部署选项**  — 您可以加速某些部署任务。

            * **在暂存部署后批准**  — 在完成任何测试之前，将此批准部署到暂存环境。 否则，将在生产部署之前进行批准，该部署将在所有测试完成后完成。

            * **跳过负载平衡器更改**  — 未进行负载平衡器更改。

         ![暂存部署选项](/help/using/assets/configure-pipelines/add-prod4.png)

         * **调度程序配置** - **部署管理器** 角色可以配置一组内容路径，这些路径将在运行管道时从AEM Dispatcher缓存中失效或刷新。 这些缓存操作将在部署任何内容包后作为部署管道步骤的一部分执行。 这些设置使用标准AEM Dispatcher行为。 要配置：

            1. 在 **路径** 提供内容路径。
            1. 在 **类型**，选择要对该路径执行的操作。
            * **刷新**  — 执行缓存失效，与从创作实例激活内容到发布实例时类似。
            * **无效**  — 执行缓存删除。
            1. 单击 **添加路径** 添加您指定的路径。 每个环境最多可以添加100个路径。

         ![调度程序配置](/help/using/assets/configure-pipelines/dispatcher-stage.png)

         >[!TIP]
         >
         >通常，最好使用无效操作，但有时可能需要刷新，尤其是在使用AEMHTML客户端库时。

      1. 在 **生产** 部分，则可以定义管道如何转出到生产环境。

         * **部署选项**  — 您可以定义控制生产部署的参数。

            * **使用上线批准**  — 部署必须由使用 **业务所有者**, **项目经理**&#x200B;或 **部署管理器** 角色 [!UICONTROL Cloud Manager] UI。
            * **已计划**  — 此选项会在生产部署之前中止管道，以允许计划管道。 如果选择此选项，则管道将在部署到暂存环境后停止，并提示用户执行操作。
               * **现在**  — 此选项将立即部署到生产环境，从而有效地完成管道。
               * **日期**  — 此选项允许用户安排完成部署的时间。
               * **停止执行**  — 此选项将中止部署到生产。

            >[!TIP]
            >
            >请参阅该文档 [部署代码，](deploying-code.md) 了解如何设置部署计划或立即执行管道。

            * **使用CSE监督**  — 如果选择此选项，则CSE将参与以实际启动部署。 在启用此选项时创建或编辑管道时， **部署管理器** 角色具有以下选项。

               * **任意CSE**  — 此选项允许任何可用的CSE开始部署。
               * **我的CSE**  — 此选项仅允许分配给客户的特定CSE开始部署。 如果分配的CSE不可用，这也适用于CSE的指定备份。

            ![生产部署选项](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

         * **调度程序配置**  — 为生产环境定义调度程序配置。 选项与暂存环境的选项相同。











1. 单击 **继续** 向 **阶段测试** 选项卡，您可以在此处配置AEM Sites和AEM Assets性能测试，具体取决于您已获许可的产品。

   >[!TIP]
   >
   >请参阅文档 [了解测试结果](understand-your-test-results.md#performance-testing) 有关 **阶段测试** 选项卡。

   1. 在 **站点内容交付/分布式负载权重** 部分，您可以根据三个页面集之间页面请求的权重来定义如何配置站点性能测试，这些页面集可以启用或禁用。

      * **热门实时页面**
      * **其他实时页面**
      * **新页面**

      ![站点负载权重](/help/using/assets/configure-pipelines/add-prod5.png)

   1. 在 **资产性能测试分发** 部分，您可以定义图像和PDF的测试分布，并定义您自己的测试资产。

      * **图像**  — 调整滑块以调整图像和PDF之间的测试拆分。
      * **PDF**  — 调整滑块以调整图像和PDF之间的测试拆分。

      * 通过上传自定义资产来定义自己的资产。

         1. **格式**  — 选择自定义资产是否为图像PDF。
         1. **文件名**  — 使用文件浏览器按钮从本地计算机中选择图像。
         1. **添加测试文件**  — 单击以上传选定的资产。

      ![资产测试分发](/help/using/assets/configure-pipelines/add-prod6.png)



1. 单击 **保存** 完成添加生产管道。














### 编辑生产管道 {#editing-prod-pipeline}

可以通过 **计划概述** 页面。

请按照以下步骤编辑已配置的管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **编辑**，如下图所示。

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. 的 **编辑生产管道** 对话框。

   1. 的 **配置** 选项卡 **管道名称**, **存储库**, **Git分支**, **部署触发器**, **重要量度失败行为**, **部署选项** 和 **调度程序配置**.

      >[!NOTE]
      >请参阅 [添加和管理存储库](/help/using/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。


   1. 的 **阶段测试** 选项卡中提供了用于从 **站点内容交付/分布式负载权重** 和 **资产性能测试分发**.

1. 单击 **更新** 编辑管道后。

### 其他生产管道操作 {#additional-prod-actions}

#### 运行生产管道 {#run-prod}

可以从管道卡运行生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **运行**，如下图所示。

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### 删除生产管道 {#delete-prod}

可以从管道卡中删除生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **删除**，如下图所示。

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

   >[!NOTE]
   >具有部署管理器角色的用户现在可以通过 **删除** 选项。

