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
source-git-commit: 2be8f290b58fff2991f876c37dd1b499bc6c5352
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 1%

---

# 配置 CI/CD 管线 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>要了解如何在AEMas a Cloud Service中为Cloud Manager配置CI/CD管线，请参阅 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager).

以下页面介绍如何配置 **管道**. 要查看有关管道工作方式的更多概念信息，请参阅 [CI/CD管线概述](ci-cd-pipeline.md).


## 了解流量 {#understanding-the-flow}

您可以在 UI中通过“管 **线设置** ”拼贴配 [!UICONTROL Cloud Manager]置管道 。

部署管理器负责设置管道。 这样做时，首先从 **Git存储库**. 管道配置包括：

* 定义将启动管道的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 视频教程 {#video-tutorial-one}

### 在Cloud Manager中配置管道 {#config-pipeline-video}

CI/CD生产管道配置定义将启动管道的触发器、控制生产部署和性能测试参数的参数。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## 设置管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存储库至少具有一个分支和 [程序设置](setting-up-program.md) 完成。

在开始部署代码之前，必须先从 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>在初始设置后，可以更改管道设置。

### 从管道卡添加新的生产管线 {#adding-production-pipeline}

设置程序并使用 [!UICONTROL Cloud Manager] UI，您就可以添加生产管道。

请按照以下步骤配置生产管道的行为和首选项：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **+添加** 选择 **添加生产管道**.

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **添加生产管道** 对话框。

   1. 输入 **管道名称**. 您可以选择 **存储库** 和 **Git分支**.

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. 您可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**.

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      您可以分配以下部署触发器以启动管道：

      * **手动**  — 使用UI手动启动管道。
      * **在Git更改时**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。 即使选择此选项，也始终可以手动启动管道。

      在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。

      这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

      * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
      * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
      * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。
   1. 选择 **部署选项**.

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **在暂存部署后批准** 功能与生产部署前的批准类似，但会立即在阶段部署步骤之后（即，在完成任何测试之前）执行，而与生产部署前的批准（在完成所有测试后完成）则相比。

      * **跳过负载平衡器更改** 跳过更改。
   1. 选择 **调度程序配置** 为舞台。 输入路径，从中选择操作 **类型**，然后单击 **添加路径**. 每个环境最多可以指定100个路径。

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. 选择 **部署选项** 用于生产。 现在，您可以定义控制生产部署的参数。

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      以下是三个可用选项：

      * **使用上线批准**  — 部署必须由业务所有者、项目经理或部署经理通过 [!UICONTROL Cloud Manager] UI。

      * **已计划**  — 此选项允许用户启用计划的生产部署。

         >[!NOTE]
         >如果 **已计划** 选项时，您可以将生产部署计划到管道 **after** 暂存部署(和 **使用GoLive批准**，如果已启用)以等待设置计划。 用户还可以选择立即执行生产部署。
         >
         >请参阅 [部署代码](deploying-code.md)，以设置部署计划或立即执行生产。

         * **使用CSE监督** - CSE参与以实际开始部署。 在管道设置或启用CSE监督时进行编辑期间，部署管理器可以选择：

            * **任意CSE**:是指任何可用的案例
            * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）
   1. 设置 **调度程序配置** 用于生产。 输入路径，从中选择操作 **类型**，然后单击 **添加路径**. 每个环境最多可以指定100个路径。

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      作为部署管理器，您有机会配置一组内容路径，这些路径将 **失效** 或 **已刷新** 设置或编辑管道时，从发布实例的AEM Dispatcher缓存中访问。

      您可以为暂存和生产部署配置一组单独的路径。 如果已配置，则在部署任何内容包后，这些缓存操作将作为部署管道步骤的一部分执行。 这些设置使用标准AEM Dispatcher行为 — 无效执行缓存失效，与从创作到发布激活内容时类似；刷新执行缓存删除。

      通常，最好使用无效操作，但有时可能需要刷新，尤其是在使用AEMHTML客户端库时。

      >[!NOTE]
      >
      >请参阅 [Dispatcher概述](dispatcher-configurations.md) 获取有关Dispatcher缓存的更多信息。





1. 单击 **继续** 选择所有选项后。

1. 从 **阶段测试** 中。 您可以配置 *AEM Sites* 和 *AEM Assets* 性能测试，具体取决于您已获许可的产品。 请参阅 [性能测试](understand-your-test-results.md#performance-testing) 以了解更多详细信息。

   1. 从 **站点内容交付/分布式负载权重**. 请参阅 [AEM Sites的性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites) 以了解更多详细信息。

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. 从 **资产性能测试分发**. 请参阅 [AEM Assets的性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets) 以了解更多详细信息。

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

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

## 仅限非生产和代码质量管道

除了部署到暂存和生产的主管道之外，客户还能够设置其他管道，称为 **非生产管道**. 这些管道始终执行生成和代码质量步骤。 它们也可以选择部署到Adobe Managed Services环境。

## 视频教程 {#video-tutorial-two}

### Cloud Manager非生产和仅代码质量管道 {#non-prod-video}

CI/CD非生产管道分为两类：代码质量管道和部署管道。 代码质量会从Git分支中管道所有代码，以根据Cloud Manager的代码质量扫描构建和评估这些代码。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### 添加非生产管道 {#add-non-production-pipeline}

在主屏幕上，这些管道将列在新卡中：

1. 访问 **管道** Cloud Manager主屏幕中的信息卡。 单击 **+添加** 选择 **添加非生产管道**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **添加非生产管道**  对话框。 选择要创建的管道类型 **代码质量管道** 或 **部署管道**.

   此外，您还可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**. 单击 **继续**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. 现在，新创建的非生产管道将显示在 **管道** 卡。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   管道显示在主屏幕的卡片上，带有三个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管道文档资源。

### 编辑非生产管道 {#editing-nonprod-pipeline}

可以通过 **管道卡** 从 **计划概述** 页面。

请按照以下步骤编辑配置的非生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 选择非生产管道并单击 **...**. 单击 **编辑**，如下图所示。

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. 的 **编辑生产管道** 显示用于更新 **管道名称**, **存储库**, **Git分支**, **部署触发器**&#x200B;和 **重要量度失败行为**.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >请参阅 [添加和管理存储库](/help/using/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   您可以分配以下部署触发器以启动管道：

   * **手动**  — 使用UI手动启动管道。
   * **在Git更改时**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。 即使选择此选项，也始终可以手动启动管道。

   在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。 这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
   * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。


1. 单击 **更新** 编辑完非生产管道后。

### 其他非生产管道操作 {#additional-nonprod-actions}

#### 运行非生产管道 {#run-nonprod}

可以从管道卡运行生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **运行**，如下图所示。

   ![](/help/using/assets/configure-pipelines/nonprod-run1.png)

#### 删除非生产管道 {#delete-nonprod}

可以从管道卡中删除生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **删除**，如下图所示。

   ![](/help/using/assets/configure-pipelines/nonprod-delete.png)


## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

请参阅 [部署代码](deploying-code.md) 以了解更多详细信息。
