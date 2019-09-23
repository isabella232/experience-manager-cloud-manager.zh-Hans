---
title: 设置程序
seo-title: 设置程序
description: 入职后，企业所有者需要对计划进行一些初始设置。
seo-description: '入职后，业务所有者需要进行Adobe AEM Cloud Manager的一些初始设置。 这包括设置计划描述和定义用于性能测试的KPI。 '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 入门
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 2c05eb4610e35d5126c6c67e44f4b71f3026c887

---


# 设置程序 {#setup-your-program}

入职后，企业所有者需要完成计划的一些初始设置。 这包括设置计划描述和定义用于性能测试的关键绩效指标(KPI)。 （可选）可以上传缩略图。 此外，业务所有者可以在设置程序时配置环境配置。

定义的KPI用作每次管线执行时通过的性能测试的基准。

>[!NOTE]
>
>定义的KPI是在舞台环境中运行的测 **试中** 。 通常，这些KPI会按比例缩小以适合舞台环境的功能。
>
>例如，在生产环境中，平均每分钟需要1000次页面查看，并且在生产中有四个调度程序／发布服务器的用户应将该页面查看规模缩放到每分钟250次（假定其舞台环境仅包含一个调度程序／发布服务器对）。 ****
>
>此外，许多用户在其生产环境前面还将有一个内容交付网络(CDN)，如Akamai或CloudFront。 由于 [!UICONTROL Cloud Manager] 直接针对舞台环境进行测试，因此KPI应仅反映通过CDN的预期流量，即缓存未命中。 通常，这是总生产流量中相对较小的子集。

## 使用 [!UICONTROL Cloud Manager] 设置程序 {#using-cloud-manager-to-setup-your-program}

请按照以下步骤设置计划并定义KPI:

1. 单击 **“设置程序** ”以在中启动设置过程 [!UICONTROL Cloud Manager]。

   ![](assets/SetUpProgram1.png)

1. “安 **装程序** ”屏幕显示“编辑程序信息”。

1. 您将看到三个选项，如“ **常规**”、“ **KPI**”和“ **配置** ”选项卡。

1. 在“ **常规** ”选项卡中，将缩略图上传到程序。 您还可以向程序添加相关说明。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI下**，您可以定义两个KPI（每个部署的预期）。 为AEM Sites和 **AEM Assets定义了单独的KPI******。 您将能够指定已许可产品的KPI。

   **AEM Sites**

   1. 您可以接受的第95百分点响应时间是多少？

      * 推荐值- 3秒
   1. 在高峰负载下，每分钟页面查看次数是多少？

      * 推荐值——每分钟200次页面查看
   **AEM Assets**

   自从最初发布以来，Cloud Manager便能够执行AEM Sites程序的性能测试。 在此版本中，已添加该功能以执行AEM Assets程序的性能测试。 通过在30分钟的测试期内重复上传资产并衡量每个资产的处理时间以及各种系统级指标，可以完成资产性能测试。
在计划设置过程中，会指定特定于资产的KPI:

   * 第95百分位数处理时间
   * 每分钟上传的资产
   ![](assets/Setup_Program-KPIs.png)

1. 在“ **配置**”下，您可以查看或编辑程序中生产和非生产环境的配置配置。 如果为程 **序打开了自动缩放**，您将看到自动缩放处于打开状态。

   >[!NOTE]
   >
   >* 自动缩放功能仅适用于生产环境，可能不适用于所有客户计划。
   >* 此版本的不提供按需缩放功 [!UICONTROL Cloud Manager]能。


   ![](assets/Setup_Program-Provisioning.png)

1. 单击 **保存** ，以完成设置向导。

   >[!NOTE]
   >
   >初始程序设置完成后，您始终可以编辑程序。 请按照以下步骤了解更多详细信息。

## 编辑程序

1. 导航到 **Cloud Manager主屏幕上的解决方** 案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案，然后单击 **编辑** ，以更新或修改程序，如下图所示。

   ![](assets/SetUpProgram6.png)

1. 此时 **会显示“编辑程序** ”屏幕，允许您更新或修改程序。

   ![](assets/Editing_Program-screen3.png)

## 后续步骤 {#the-next-steps}

如果您已经设置了 **Pipeline**，则下次执行时将考虑您的更新设置。 如果尚未设置管道，请按照以下步骤先设置管道。

请参 [阅配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) ，以设置管道。
