---
title: 配置CI/CD管道
seo-title: 配置CI/CD管道
description: 可查看本页以从云管理器配置渠道设置。
seo-description: '在开始部署代码之前，必须从AEM Cloud manager配置渠道设置。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: 引用
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
translation-type: tm+mt
source-git-commit: dd23fc2277c2e2c51e3ab9b071d6336d2e0d6488

---


# 配置CI/CD管道 {#configure-your-ci-cd-pipeline}

下页介绍如何配置管 **线**。 要查看有关管道工作方式的更多概念性信息，请参阅 [CI/CD管道概述](ci-cd-pipeline.md)。

## 了解流 {#understanding-the-flow}

您可以从UI中的“管线设 **置”拼贴** ，配置 [!UICONTROL Cloud Manager] 管线。

部署管理器负责设置管道。 执行此操作时，您首先从 **Git存储库中选择分支**。 管道配置包括：

* 定义启动管道的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 设置管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存储库至少有一个分支并且“程序设置”完成之前，无法 [设置管道](setting-up-program.md) 。

在开始部署代码之前，必须先从中配置管道设置 [!UICONTROL Cloud Manager]。

>[!NOTE]
>
>可在初始设置后更改管线设置。

### 从以下位置配置管道设 [!UICONTROL Cloud Manager] 置 {#configuring-the-pipeline-settings-from-cloud-manager}

使用 [!UICONTROL Cloud Manager] UI设置程序后，即可设置管道。

按照以下步骤配置管道的行为和首选项：

1. 单击“ **设置管道** ”(Setup Pipeline)以设置和配置管道。

   ![](assets/Configure_ci-cd-1.png)

1. 将显 **示“设置管道** ”屏幕。

   通过三步向导，您可以设置 **Branch**、 **Environments**&#x200B;和 **Testing** 环境。
选择您的Git分支，然后单击“下 **一步**”。

   >[!NOTE]
   >
   >在Git存储库中找到的分支会链接到您的程序。

   ![](assets/Configure_ci-cd-2.png)


1. 访问“环 **境** ”选项卡以选 **择“舞台** ”和“ **生产** ”选项。

   可以定义触发器以启动管线：

   * **在Git更改中** -每当向配置的git分支添加提交时，启动CI/CD管道。 即使选择此选项，也始终可以手动启动管线。
   * **手动** -使用UI手动启动管道。
   * **计划** -此选项即将在即将发布的版本中推出。
   在管道设置或编辑过程中，当在任何质量门（如代码质量、安全测试和性能测试）中遇到重要故障时，部署管理器可以选择定义管道的行为。

   这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

* **每次询问** -这是默认设置，对于任何重要故障都需要手动干预。
* **立即失败** -如果选择此项，则每当出现重要故障时，管道将被取消。 这实际上是模拟用户手动拒绝每个失败。
* **立即继续** -如果选中此项，则每当出现重要故障时，管道将自动继续。 这实际上是在模拟用户手动批准每个失败。

   现在，您可以定义控制生产部署的参数。 三个可用选项如下：

* **使用实时批准** -部署必须由业务所有者、项目经理或部署经理通过 [!UICONTROL Cloud Manager] UI手动批准。
* **使用CSE监督** -参与CSE以实际开始部署。 在管道设置或启用CSE监督时编辑期间，部署管理器可以选择：

   * **任何CSE**:引用任何可用的CSE
   * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）

* **计划** -此选项允许用户启用计划生产部署。

>[!NOTE]
>
>如果 **选择了** “计划”选项，则可以在阶段部署后将生产部署计划到管道中(如果启用了该选项，则 **使用GoLive Approval******)，以等待设置计划。 用户还可以选择立即执行生产部署。
>
>请参阅 [**部署代码**](deploying-code.md)，以设置部署计划或立即执行生产。

![](assets/Configure_ci-cd-3.png)

>[!NOTE]
>
>“使 **用CSE监督** ”选项并不适用于所有客户。

**调度程序失效**

作为部署管理器，您有机会在设置或编辑管道时配置一组路径，这些路径将 **从** AEM **Dispatcher缓存中失效或刷新** 。

您可以为舞台和生产部署配置单独的路径集。 如果配置了缓存，则这些缓存操作将作为部署管道步骤的一部分执行，就在部署任何内容包之后执行。 这些设置使用标准AEM Dispatcher行为- invalidate执行缓存失效，与从创作到发布激活内容时类似；flush执行缓存删除。

通常，最好使用失效操作，但可能有需要刷新的情况，尤其是在使用AEM HTML客户端库时。

>[!NOTE]
>
>请参阅“调度程 [序概述”](dispatcher-configurations.md) ，获取有关Dispatcher缓存的更多信息。

请按照以下步骤配置调度程序失效：

1. 单击“ **调度程序配置** ”标题下的“配置”

   ![](assets/image2018-8-7_14-53-24.png)

1. 输入路径，从“类型”中选择操 **作**，然后单击 **添加**。 每个环境最多可指定100个路径。 添加路径后，单击“应 **用”**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 回到“管线设 **置”页面后** ，您将看到所选内容的更新摘要。

   单击 **保存** ，以保留此配置。

   ![](assets/image2018-8-7_15-4-30.png)

   **在阶段部署后批准**&#x200B;在阶段部署后 **批准有一个可选步骤** ，可以在生产管道中配置该步骤。
在“管线编辑”(Pipeline Edit)屏幕的新选项中启 **用了此选项** :

   ![](assets/post_deployment1.png)

   然后，在管道执行过程中，它将显示为一个单独的步骤：
   ![](assets/post_deployment2.png)

   >[!NOTE]
   >
   >**在Stage Deployment** （在工作阶段部署之前）的功能与在生产部署之前的批准类似，但是在紧接着工作阶段部署步骤之后（即在完成任何测试之前）进行批准，而在生产部署之前（在完成所有测试之后）进行批准。


1. 访问“ **测试** ”选项卡，为程序定义测试条件。

   现在，您可以配置性能测试参数。

   您可以配置 *AEM Sites* 和 *AEM Assets* Performance Testing，具体取决于您已获得许可的产品。

   **AEM Sites:**

   Cloud manager通过在舞台发布服务器上请求页面（作为未经身份验证的用户）长达30分钟的测试时间段，并测量每个页面的响应时间以及各种系统级别指标，从而执行AEM Sites程序的性能测试。页面由三个页面集 **选择**;您可以选择从一个集合到全部三个集合的任意位置。 流量分配基于所选集数，即如果全部三个集合都被选中，则每个集合的页面查看总数占总页面查看次数的33%;如果选择两个，则每组50%;如果选择了一个，则100%的流量将转到该集。

   例如，假设“常用实时页面”和“新页面”集（在本例中，不使用“其他实时页面”）之间存在50%/50%的拆分，而“新页面”集包含3000页。 页面查看次数／分钟KPI设置为200。 在30分钟的测试期内：

   * 热门实时页面集中的25个页面中的每个页面将被点击240次-((200 * 0.5)/ 25)* 30 = 120

   * 新页面集中的3000页中的每页将点击一次-((200 * 0.5)/ 3000)* 30 = 1
   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   **AEM Assets:**

   Cloud manager通过在30分钟的测试期内重复上传资产并测量每个资产的处理时间以及各种系统级别指标，执行AEM资产程序的性能测试。 此功能可以上传图像和PDF文档。 每分钟上传的每种类型的资产数量分布在“管道设置”或“编辑”屏幕中进行设置。

   例如，如果使用70/30拆分，如下图所示。 每分钟上传10个资产，每分钟上传7个图像，3个文档。

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >有默认图像和PDF文档，但在大多数情况下，客户需要上传自己的资产。 这可以从“管线设置”(Pipeline Setup)或“编辑”(Edit)屏幕中完成。 支持JPEG、PNG、GIF和BMP等常见图像格式以及Photoshop、Illustrator和Postscript文件。

1. 单击 **“保存** ”(Save)以完成管线进程的设置。

   >[!NOTE]
   >
   >此外，设置管道后，您仍可以使用 **UI中的“生产管道设置”拼贴来编辑** 管道的设置 [!UICONTROL Cloud Manager] 。

   ![](assets/Prod-Pipeline-Settings-Dialog.png)

## 仅限非生产和代码质量的管道

除了部署到舞台和生产的主要管道外，客户还能建立额外的管道，称为 **非生产管道**。 这些管线始终执行构建和代码质量步骤。 它们也可以选择部署到Adobe Managed services环境。

### 非生产和仅代码质量管道视频

CI/CD非生产管道分为两类：代码质量管道和部署管道。 Code Quality（代码质量）将Git分支中的所有代码输入管道，以根据Cloud manager的代码质量扫描构建和评估。
有关更多详细信息，请参阅以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/26316/?captions=chi_hans)

在主屏幕上，新卡中列出了以下管线：

1. 从Cloud **Manager主屏幕访问非生产管道拼贴** 。

   ![](assets/Configuring_Pipeline_Add-Production.png)

1. 单击“添加”按钮，指定“管线名称”、“管线类型”和“Git分支”。

   此外，您还可以从“管道选项”中设置部署触发器和重要失败行为。

   ![](assets/Configuring_Pipeline_Add-Production2.png)

1. 单 **击** “保存”(Save)，管线将显示在主屏幕的卡片上，并执行以下三个操作：

   * **编辑** -允许编辑管道设置
   * **Detail** —— 显示上次管线执行（如果有）
   * **构建** -导航到执行页面，可从中执行管道
   ![](assets/Configuring_Pipeline_Add-Production3.png)

   >[!NOTE]
   >
   >管线运行时，将显示当前步骤，并且仅“详细信 **息** ”(Details)操作可用。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

请参阅 [部署代码](deploying-code.md) ，了解更多详细信息。
