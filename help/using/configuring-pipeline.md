---
title: 配置 CI/CD 管线
seo-title: 配置 CI/CD 管线
description: 可查看本页以从云管理器配置管道设置。
seo-description: '在开始部署代码之前，必须从AEM Cloud Manager配置渠道设置。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
translation-type: tm+mt
source-git-commit: d02292e4f6369e0e0bf8fcf60cb8fe299854b3cc
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 1%

---


# 配置 CI/CD 管线 {#configure-your-ci-cd-pipeline}

以下页介绍如何配置&#x200B;**管道**。 要查看有关管道工作方式的更多概念性信息，请参阅[CI/CD管道概述](ci-cd-pipeline.md)。

## 视频教程{#video-tutorial-one}

### 在云管理器{#config-pipeline-video}中配置管道

CI/CD生产管道配置定义将启动管道的触发器、控制生产部署和性能测试参数的参数。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## 了解流{#understanding-the-flow}

您可以在 UI中通过“管 **线设置** ”拼贴配 [!UICONTROL Cloud Manager]置管道 。

部署管理器负责设置管道。 这样做时，您首先从&#x200B;**Git存储库**&#x200B;中选择分支。 管道配置包括：

* 定义将开始管道的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 设置管道{#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存储库至少有一个分支且[项目设置](setting-up-program.md)完成之前，无法设置管道。

在开始部署代码之前，必须从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>初始设置后，可以更改管线设置。

### 从[!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}配置管道设置

使用[!UICONTROL Cloud Manager] UI设置项目后，即可设置管道。

按照以下步骤配置管道的行为和首选项：

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/Setup-Pipeline.png)

1. 将显示&#x200B;**设置管道**&#x200B;屏幕。

   三步向导允许您设置&#x200B;**分支**、**环境**&#x200B;和&#x200B;**测试**环境。
选择您的Git分支，然后单击**下一步**。

   >[!NOTE]
   >
   >在Git存储库中找到的分支链接到您的项目。


1. 访问&#x200B;**环境**&#x200B;选项卡以选择&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;选项。

   可以定义触发器以开始管线：

   * **在Git更改中** -只要向配置的git分支添加提交，就会开始CI/CD管道。即使选择此选项，也始终可以手动开始管线。
   * **手动** -使用UI手动开始管道。

   在管道设置或编辑过程中，当在任何质量门中遇到重要故障时，部署管理器可以选择定义管道的行为，如代码质量、安全测试和性能测试。

   这对于希望获得更自动化流程的客户非常有用。 可用选项有：

* **每次询问** -这是默认设置，需要手动干预任何重要故障。
* **立即失败** -如果选中此选项，则在出现重要故障时将取消管线。这实质上是模拟用户手动拒绝每个失败。
* **立即继续** -如果选中此项，管线将在出现重要故障时自动继续。这实际上是模拟用户手动批准每个失败。

   现在，您可以定义控制生产部署的参数。 三个可用选项如下：

* **使用开始** -部署必须由业务所有者、项目经理或部署经理通过UI手动 [!UICONTROL Cloud Manager] 批准。
* **使用CSE监督** -参与CSE来实际开始部署。在管道设置或启用CSE监督时进行编辑期间，部署管理器可以选择：

   * **任何CSE**:引用任何可用的CSE
   * **我的CSE**:是指分配给客户或其备份的特定CSE（如果CSE不在办公室）

* **计划** -此选项允许用户启用计划生产部署。

>[!NOTE]
>
>如果选择了&#x200B;**计划**&#x200B;选项，则可以在阶段部署&#x200B;**之后将生产部署计划到管道**(如果已启用GoLive批准&#x200B;**，则使用计划批准&lt;a5/>)，以等待设置。**&#x200B;用户还可以选择立即执行生产部署。
>
>请参阅&#x200B;[**部署代码**](deploying-code.md)&#x200B;以设置部署计划或立即执行生产。

![](assets/configure-pipeline3.png)

>[!NOTE]
>
>**使用CSE监督**&#x200B;选项并非所有客户都可用。

**阶段部署后批准**

在Stage Deployment **之后有一个可选步骤**批准，可在生产管道中进行配置。
在**管线编辑**&#x200B;屏幕上的新选项中启用此选项：

![](assets/post_deployment1.png)

然后，在管道执行过程中，它将显示为一个单独的步骤：

![](assets/post_deployment2.png)

>[!NOTE]
>
>**在阶段部** 署后进行批准的功能与生产部署前的批准功能类似，但是在阶段部署步骤后立即进行，即在完成任何测试之前，与在完成所有测试后完成的生产部署前进行批准相比。

**调度程序失效**

作为部署管理器，您有机会在设置或编辑管道时配置一组内容路径，这些内容路径将从AEM Dispatcher缓存中失效&#x200B;****&#x200B;或&#x200B;**刷新**&#x200B;用于发布实例。

您可以为舞台和生产部署配置一组单独的路径。 如果已配置，则这些缓存操作将作为部署管道步骤的一部分执行，就在部署任何内容包之后。 这些设置使用标准的AEM Dispatcher行为- invalidate执行缓存失效，与从创作到发布激活内容时类似；flush执行缓存删除。

通常，最好使用失效操作，但有时可能需要刷新，尤其是在使用AEM HTML客户端库时。

>[!NOTE]
>
>请参阅[Dispatcher Overview](dispatcher-configurations.md)获取有关Dispatcher缓存的详细信息。

请按照以下步骤配置调度程序失效：

1. 单击“调度程序配置”标题下的&#x200B;**配置**

   ![](assets/image2018-8-7_14-53-24.png)

1. 输入路径，从&#x200B;**Type**&#x200B;中选择操作，然后单击&#x200B;**添加**。 每个环境最多可指定100个路径。 添加路径后，单击&#x200B;**应用**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 返回&#x200B;**管道设置**&#x200B;页面后，您将看到选择的更新摘要。

   单击&#x200B;**保存**&#x200B;以保留此配置。

   ![](assets/image2018-8-7_15-4-30.png)


1. 访问&#x200B;**测试**&#x200B;选项卡，为项目定义测试条件。

   现在，您可以配置性能测试参数。

   您可以配置&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;性能测试，具体取决于您已授权哪些产品。

   **AEM Sites:**

   Cloud Manager在30分钟的测试期内在舞台发布服务器上请求页面（默认为未验证的用户），并测量每个页面的响应时间以及各种系统级度量，从而执行AEM Sites项目的性能测试。 这些请求是从一组已知的专用地址发出的。 地址范围可从客户成功工程师或Adobe代表处获取。

   在30分钟测试期开始之前，云管理器将使用客户成功工程师配置的一组或多个&#x200B;*种子* URL爬网舞台环境。 从这些URL开始，将检查每个页面的HTML，并以宽度优先的方式遍历链接。 此搜索过程最多限制为5000页。 来自Crawler的请求的固定超时为10秒。

   页面由三个&#x200B;**页集**&#x200B;选择；您可以选择从一个集合到全部三个集合的任意位置。 流量分配基于所选集数，即如果全部三个集合都被选中，则每个集合将占总页面视图的33%;如果选择两个，则50%将转至每个集合；如果选择了一个，则100%的流量将流向该集。

   例如，假设“常用实时页面”和“新页面”集（在本例中，不使用“其他实时页面”）之间存在50%/50%的拆分，而“新页面”集包含3000页。 页面视图每分钟KPI设置为200。 在30分钟的测试期内：

   * 热门实时页面集中的25个页面中的每个页面将被点击240次-((200 * 0.5)/ 25)* 30 = 120

   * 新页面集中的3000页中每页将点击一次-((200 * 0.5)/ 3000)* 30 = 1

   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   有关详细信息，请参阅[已验证的性能测试](#authenticated-performance-testing)。

   **AEM Assets:**

   Cloud Manager通过在30分钟的测试期内重复上传资产并衡量每个资产的处理时间以及各种系统级别指标，执行AEM Assets项目的性能测试。 此功能可以上传图像和PDF文档。 每分钟上传的每种类型的资产数量分布在“管道设置”或“编辑”屏幕中设置。

   例如，如果使用70/30拆分，如下图所示。 每分钟上传10个资产，每分钟上传7个图像，3个文档。

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >存在默认图像和PDF文档，但在大多数情况下，客户需要上传自己的资产。 这可以从“管线设置”(Pipeline Setup)或“编辑”(Edit)屏幕中完成。 支持JPEG、PNG、GIF和BMP等常见图像格式以及Photoshop、Illustrator和Postscript文件。

1. 单击&#x200B;**保存**&#x200B;以完成管线进程的设置。

   >[!NOTE]
   >
   >此外，设置管线后，您仍可以使用[!UICONTROL Cloud Manager] UI中的&#x200B;**生产管线设置**&#x200B;拼贴编辑相同设置。

   ![](assets/Production-Pipeline.png)

### 已验证的性能测试{#authenticated-performance-testing}

具有已验证站点的AMS客户可以指定Cloud Manager在站点性能测试期间用来访问网站的用户名和密码。

用户名和口令指定为[管道变量](/help/using/build-environment-details.md#pipeline-variables)，名称为`CM_PERF_TEST_BASIC_USERNAME`和`CM_PERF_TEST_BASIC_PASSWORD`。

尽管并非严格要求，但建议将字符串变量类型用于用户名，将secretString变量类型用于密码。 如果同时指定了这两个凭据，则性能测试Crawler和测试虚拟用户的每个请求都将包含这些凭据作为HTTP Basic身份验证。

要使用[Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)设置这些变量，请运行：

`$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>`

## 仅限非生产和代码质量的管道

除了部署到舞台和生产的主管道外，客户还能够建立额外的管道，称为&#x200B;**非生产管道**。 这些管线始终执行构建和代码质量步骤。 它们还可以选择部署到Adobe Managed Services环境。

## 视频教程{#video-tutorial-two}

### Cloud Manager非生产和代码质量专用管道{#non-prod-video}

CI/CD非生产管道分为两个类别，代码质量管道和部署管道。 代码质量将从Git分支中输入所有代码，以根据Cloud Manager的代码质量扫描进行构建和评估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

在主屏幕上，新卡中列出了以下管线：

1. 从Cloud Manager主屏幕访问&#x200B;**非生产管道**&#x200B;拼贴。

   ![](assets/Non-Production-Pipeline.png)

1. 单击“添加”按钮，指定“管道名称”、“管道类型”和“Git分支”。

   此外，您还可以从管道选项设置部署触发器和重要失败行为。

   ![](assets/non-prod-pipe.png)

1. 单击&#x200B;**保存**，主屏幕上的卡上将显示管道，其中有三个操作：

   * **编辑** -允许编辑管道设置
   * **Detail**  —— 显示上次管线执行（如果有）
   * **构建** -导航到执行页面，从该页面可以执行管道

   ![](assets/Non-prod-2.png)

   >[!NOTE]
   >
   >管线运行时，显示当前步骤，并且仅&#x200B;**Details**&#x200B;操作可用。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关详细信息，请参阅[部署代码](deploying-code.md)。
