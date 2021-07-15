---
title: 配置 CI/CD 管线
seo-title: 配置 CI/CD 管线
description: 可以按照本页从Cloud Manager配置管道设置。
seo-description: '在开始部署代码之前，必须从AEM Cloud Manager中配置管道设置。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD管线
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 1c103b1c43a1e5fe7a6fa27110fc692bba6fb8b2
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 2%

---

# 配置 CI/CD 管线 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>要了解如何在AEM as a Cloud Service中为Cloud Manager配置CI/CD管线，请参阅[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)。

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

### 从[!UICONTROL Cloud Manager]配置管道设置 {#configuring-the-pipeline-settings-from-cloud-manager}

使用[!UICONTROL Cloud Manager] UI设置程序后，即可设置管道。

请按照以下步骤配置管道的行为和首选项：

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/Setup-Pipeline.png)

1. 此时将显示&#x200B;**设置管道**&#x200B;屏幕。

   三步向导允许您设置&#x200B;**Branch**、**Environments**&#x200B;和&#x200B;**Testing**环境。
选择您的Git分支，然后单击**Next**。

   >[!NOTE]
   >
   >在Git存储库中找到的分支会链接到您的程序。


1. 访问&#x200B;**Environments**&#x200B;选项卡以选择&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;选项。

   您可以定义启动管道的触发器：

   * **在Git更改中**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。即使选择此选项，也始终可以手动启动管道。
   * **手动**  — 使用UI手动启动管道。

   在管道设置或编辑期间，当在任何质量门（如“代码质量”、“安全测试”和“性能测试”）中遇到重要故障时，部署管理器可以选择定义管道的行为。

   这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

* **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
* **立即取消**  — 如果选中此选项，则每当发生重要故障时，管道都将被取消。这实质上是在模拟用户手动拒绝每个故障。
* **立即批准**  — 如果选中此选项，则每当发生重要故障时，管道将自动继续。这实质上是在模拟用户手动批准每次失败。

   现在，您可以定义控制生产部署的参数。 以下是三个可用选项：

* **使用上线批准**  — 部署必须由业务所有者、项目经理或部署经理通过UI手动 [!UICONTROL Cloud Manager] 批准。
* **使用CSE监督**  — 使用CSE来实际开始部署。在管道设置或启用CSE监督时进行编辑期间，部署管理器可以选择：

   * **任何CSE**:是指任何可用的案例
   * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）

* **已计划**  — 此选项允许用户启用已计划的生产部署。

>[!NOTE]
>如果选择了&#x200B;**Scheduled**&#x200B;选项，则可以在阶段部署(和&#x200B;**使用GoLive批准**，如果已启用)之后，将生产部署计划到管道&#x200B;**之后。**&#x200B;用户还可以选择立即执行生产部署。
>
>请参阅&#x200B;[**部署代码**](deploying-code.md)，以设置部署计划或立即执行生产。

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>**使用CSE Osgels**&#x200B;选项并非对所有客户都可用。

**在暂存部署后批准**

在Stage Deployment **之后有一个可选步骤**批准，该步骤可在生产管道中进行配置。
在**Pipeline Edit**&#x200B;屏幕上的新选项中启用了此选项：

![](assets/post_deployment1.png)

然后，在管道执行期间，该步骤会显示为单独的步骤：

![](assets/post_deployment2.png)

>[!NOTE]
>
>**在Stage部署后** 进行批准的功能与在生产部署前进行批准的功能类似，但是会在Stage部署步骤之后立即进行，即在完成任何测试之前，与在生产部署前进行批准（在所有测试完成后完成）进行比较。

**Dispatcher失效**

作为部署管理器，您可以配置一组内容路径，在设置或编辑管道时，这些路径将从AEM Dispatcher缓存中为publish实例配置失效的&#x200B;****&#x200B;或&#x200B;**flushed**。

您可以为暂存和生产部署配置一组单独的路径。 如果已配置，则在部署任何内容包后，这些缓存操作将作为部署管道步骤的一部分执行。 这些设置使用标准AEM Dispatcher行为 — 无效执行缓存失效，与从创作到发布激活内容时类似；刷新执行缓存删除。

通常，最好使用无效操作，但有时可能需要刷新，尤其是在使用AEM HTML客户端库时。

>[!NOTE]
>
>请参阅[Dispatcher概述](dispatcher-configurations.md)获取有关Dispatcher缓存的更多信息。

请按照以下步骤配置Dispatcher无效：

1. 单击Dispatcher配置标题下的&#x200B;**配置**

   ![](assets/image2018-8-7_14-53-24.png)

1. 输入路径，从&#x200B;**Type**&#x200B;中选择操作，然后单击&#x200B;**Add**。 每个环境最多可以指定100个路径。 添加路径后，单击&#x200B;**Apply**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 返回&#x200B;**管道设置**&#x200B;页面后，您将看到更新的选择摘要。

   单击&#x200B;**Save**&#x200B;以保留此配置。

   ![](assets/image2018-8-7_15-4-30.png)

1. 访问&#x200B;**Testing**&#x200B;选项卡以定义程序的测试标准。 您现在可以配置性能测试参数。

   您可以配置&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;性能测试，具体取决于您已获得许可的产品。 有关更多详细信息，请参阅[性能测试](understand-your-test-results.md#performance-testing)。

1. 单击&#x200B;**Save**&#x200B;以完成管道进程的设置。

   >[!NOTE]
   >此外，在设置管道后，您仍可以使用[!UICONTROL Cloud Manager] UI中的&#x200B;**生产管道设置**&#x200B;拼贴来编辑管道的设置。

   ![](assets/Production-Pipeline.png)


## 仅限非生产和代码质量管道

除了部署到暂存和生产的主管道之外，客户还能够设置其他管道，称为&#x200B;**非生产管道**。 这些管道始终执行生成和代码质量步骤。 它们也可以选择部署到Adobe Managed Services环境。

## 视频教程 {#video-tutorial-two}

### Cloud Manager非生产和仅代码质量管道 {#non-prod-video}

CI/CD非生产管道分为两类：代码质量管道和部署管道。 代码质量会从Git分支中管道所有代码，以根据Cloud Manager的代码质量扫描构建和评估这些代码。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

在主屏幕上，这些管道将列在新卡中：

1. 从Cloud Manager主屏幕中访问&#x200B;**非生产管道**&#x200B;拼贴。

   ![](/help/using/assets/non-prod-add.png)

1. 单击&#x200B;**添加**&#x200B;按钮，以指定管道名称、管道类型和Git分支。

   此外，您还可以从管道选项中设置部署触发器和重要失败行为。

   ![](assets/non-prod-pipe.png)

1. 单击&#x200B;**Save** ，此时主屏幕上的卡片上会显示管道，该管道可执行五个操作：

   * **编辑**  — 允许编辑管线设置
   * **详细信息**  — 显示上次管道执行（如果有）
   * **生成**  — 导航到可从中执行管道的执行页面
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息
   * **了解更多**  — 导航到了解CI/CD管线文档资源。

      ![](assets/prod-one.png)
   >[!NOTE]
   >
   >管道运行时，将显示当前步骤，并且只有&#x200B;**Details**&#x200B;操作可用。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关更多详细信息，请参阅[部署代码](deploying-code.md)。
