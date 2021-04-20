---
title: 配置 CI/CD 管线
seo-title: 配置 CI/CD 管线
description: 可查看本页以从云管理器配置您的管道设置。
seo-description: '在开始部署代码之前，您必须从AEM Cloud Manager配置渠道设置。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
translation-type: tm+mt
source-git-commit: 12a7d6199983e2d19ef401051f60e3f24bb6d4f8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 2%

---


# 配置 CI/CD 管线 {#configure-your-ci-cd-pipeline}

以下页介绍如何配置&#x200B;**Pipeline**。 要查看有关管道工作原理的更多概念信息，请参阅[CI/CD管道概述](ci-cd-pipeline.md)。

## 视频教程{#video-tutorial-one}

### 在Cloud Manager {#config-pipeline-video}中配置管道

CI/CD生产管道配置定义将启动管道的触发器，参数控制生产部署和性能测试参数。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## 了解流{#understanding-the-flow}

您可以在 UI中通过“管 **线设置** ”拼贴配 [!UICONTROL Cloud Manager]置管道 。

部署管理器负责设置管道。 执行此操作时，您首先从&#x200B;**Git存储库**&#x200B;中选择分支。 管道配置包括：

* 定义将开始管线的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 设置管道{#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存储库至少有一个分支且[项目设置](setting-up-program.md)已完成之前，无法设置管道。

在开始部署代码之前，必须从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>初始设置后，可以更改管线设置。

### 从[!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}配置管道设置

使用[!UICONTROL Cloud Manager] UI设置项目后，即可设置管道。

按照以下步骤配置管道的行为和首选项：

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/Setup-Pipeline.png)

1. 将显示&#x200B;**设置管线**&#x200B;屏幕。

   三步向导允许您设置&#x200B;**Branch**、**环境**&#x200B;和&#x200B;**测试**环境。
选择您的Git分支，然后单击**下一步**。

   >[!NOTE]
   >
   >在Git存储库中找到的分支链接到您的项目。


1. 访问&#x200B;**环境**&#x200B;选项卡以选择&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;选项。

   可以定义触发器以开始管线：

   * **在Git更改中**  — 只要向配置的git分支添加提交，就会开始CI/CD管道。即使您选择此选项，也始终可以手动开始管线。
   * **手动**  — 使用UI手动开始管线。

   在管道设置或编辑期间，当在任何质量门（如“代码质量”、“安全测试”和“性能测试”）中遇到重要故障时，部署管理器可以选择定义管道的行为。

   这对于希望实现更自动化流程的客户很有用。 可用选项有：

* **每次询问**  — 这是默认设置，对于任何重要故障，都需要手动干预。
* **立即取消**  — 如果选中此项，则在出现重要故障时管道将被取消。这实际上是在模拟用户手动拒绝每个失败。
* **立即批准**  — 如果选中此项，则在出现重要故障时管道将自动继续。这实际上是在模拟用户手动批准每个失败。

   现在，您可以定义控制生产部署的参数。 以下是三个可用选项：

* **使用开始**  — 部署必须由业务所有者、项目经理或部署经理通过UI手动 [!UICONTROL Cloud Manager] 批准。
* **使用CSE监督** - CSE来实际开始部署。在管道设置或启用CSE监督时进行编辑期间，部署管理器可以选择：

   * **任何CSE**:引用任何可用的CSE
   * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）

* **计划**  — 此选项允许用户启用计划生产部署。

>[!NOTE]
>如果选择了&#x200B;**Scheduled**&#x200B;选项，则可以在阶段部署&#x200B;**之后将生产部署计划到管道**(如果已启用，则使用GoLive批准&#x200B;**)，以等待设置计划。**&#x200B;用户还可以选择立即执行生产部署。
>
>请参阅&#x200B;[**部署代码**](deploying-code.md)&#x200B;以设置部署计划或立即执行生产。

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>并非所有客户都可以使用&#x200B;**使用CSE Osgelist**&#x200B;选项。

**阶段部署后批准**

在Stage Deployment **之后有一个可选步骤**批准，可在生产管道中进行配置。
在**管线编辑**&#x200B;屏幕上的新选项中启用了此选项：

![](assets/post_deployment1.png)

然后，在管道执行期间，它将显示为一个单独的步骤：

![](assets/post_deployment2.png)

>[!NOTE]
>
>**在阶段部署** 后进行批准的功能与生产部署前的批准类似，但在阶段部署步骤后立即进行，即在完成任何测试之前，与在完成所有测试后完成的生产部署前的批准相比。

**调度程序失效**

作为部署管理器，您可以配置一组内容路径，在设置或编辑管道时，这些内容路径将从发布实例的AEM Dispatcher缓存中&#x200B;**失效**&#x200B;或&#x200B;**刷新**。

可以为舞台和生产部署配置一组单独的路径。 如果配置，则这些缓存操作将作为部署管道步骤的一部分执行，就在部署任何内容包之后执行。 这些设置使用标准AEM Dispatcher行为 — invalidate执行缓存失效，类似于从创作到发布激活内容时；flush执行缓存删除。

通常，最好使用失效操作，但有时可能需要刷新，尤其是在使用AEM HTML客户端库时。

>[!NOTE]
>
>请参阅[Dispatcher Overview](dispatcher-configurations.md)获取有关Dispatcher缓存的详细信息。

请按照以下步骤配置调度程序失效：

1. 单击“调度程序配置”标题下的&#x200B;**配置**

   ![](assets/image2018-8-7_14-53-24.png)

1. 输入路径，从&#x200B;**Type**&#x200B;中选择操作，然后单击&#x200B;**添加**。 每个环境最多可指定100个路径。 添加路径后，单击&#x200B;**应用**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 返回&#x200B;**管线设置**&#x200B;页后，您将看到所选内容的更新摘要。

   单击&#x200B;**保存**&#x200B;以保留此配置。

   ![](assets/image2018-8-7_15-4-30.png)

1. 访问&#x200B;**测试**&#x200B;选项卡，为项目定义测试条件。 您现在可以配置性能测试参数。

   您可以配置&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;性能测试，具体取决于您已授权哪些产品。 有关详细信息，请参阅[性能测试](understand-your-test-results.md#performance-testing)。

1. 单击&#x200B;**保存**&#x200B;以完成管线进程的设置。

   >[!NOTE]
   >此外，设置管线后，您仍可以使用[!UICONTROL Cloud Manager] UI中的&#x200B;**生产管线设置**&#x200B;拼贴编辑相同的设置。

   ![](assets/Production-Pipeline.png)


## 仅限非生产和代码质量管道

除了部署到舞台和生产的主管道外，客户还能够建立额外的管道，称为&#x200B;**非生产管道**。 这些管线始终执行构建和代码质量步骤。 他们也可以选择部署到Adobe Managed Services环境。

## 视频教程{#video-tutorial-two}

### Cloud Manager非生产和代码质量专用管道{#non-prod-video}

CI/CD非生产管道分为两个类别，代码质量管道和部署管道。 “代码质量”可以管道Git分支中的所有代码，以根据Cloud Manager的代码质量扫描构建和评估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

在主屏幕上，这些管道列在新卡中：

1. 从Cloud Manager主屏幕访问&#x200B;**非生产管道**&#x200B;拼贴。

   ![](assets/Non-Production-Pipeline.png)

1. 单击“添加”按钮，以指定“管线名称”、“管线类型”和“Git分支”。

   此外，您还可以从“管道选项”设置部署触发器和重要失败行为。

   ![](assets/non-prod-pipe.png)

1. 单击&#x200B;**保存**，主屏幕上的卡上将显示管道，其中有三个操作：

   * **编辑**  — 允许编辑管道设置
   * **Detail**  — 显示上次管线执行（如果有）
   * **构建**  — 导航到可从中执行管线的执行页面

   ![](assets/Non-prod-2.png)

   >[!NOTE]
   >
   >管线运行时，将显示当前步骤，并且仅&#x200B;**Details**&#x200B;操作可用。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关详细信息，请参阅[部署代码](deploying-code.md)。
