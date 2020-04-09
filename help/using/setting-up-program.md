---
title: 设置程序
seo-title: 设置程序
description: 入职后，企业所有者需要对项目进行一些初始设置。
seo-description: '入职后，业务所有者需要进行Adobe AEM Cloud Manager的一些初始设置。 这包括设置项目描述和定义用于性能测试的KPI。 '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 16893b8bcd2b2d681a14bb6be3786e358e1952fb

---


# 设置程序 {#setup-your-program}

入职后，企业所有者需要完成项目的一些初始设置。 这包括设置项目描述和定义用于性能测试的关键绩效指标(KPI)。 （可选）可以上传缩略图。 此外，业务所有者可以在设置环境时配置项目供应。

定义的KPI用作每次管线执行时通过的性能测试的基准。

>[!NOTE]
>
>定义的KPI是根据在舞台环境上运行的测试 **来衡量** 。 通常，这些KPI会按比例缩小以适合舞台环境的功能。
>
>例如，在生产视图中，预期每分钟平均1000页环境的用户和在生产中有四个调度程序／发布服务器的用户应将此环境缩放到每分钟250页视图（假定其舞台仅包含一个调度程序／发布服务器对）。 ****
>
>此外，许多用户在其生产投放前还将有内容环境网络(CDN)，如Akamai或CloudFront。 由于 [!UICONTROL Cloud Manager] 直接针对舞台环境进行测试，因此KPI应仅反映通过CDN（即缓存未命中）的预期流量。 通常，这是总生产流量中相对较小的子集。

## 使用 [!UICONTROL Cloud Manager] 设置项目 {#using-cloud-manager-to-setup-your-program}

请按照以下步骤设置项目并定义KPI:

1. 单击 **设置项目** ，以在中开始设置过程 [!UICONTROL Cloud Manager]。

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始终可以从操作栏中切换、编辑或添加新项目，如下图所示。

   ![image1](assets/set-up-program/setup2.png)


1. “设 **置项目** ”屏幕显示“编辑项目信息”。

1. 您将看到三个选项，如“ **常规**”、“ **KPI**”和“ **配置** ”选项卡。

1. 在“ **常规** ”选项卡中，将缩略图上传到您的项目。 您还可以向项目添加相关说明。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI下**，您可以定义两个KPI（每个部署的预期）。 为AEM Sites和 **AEM Assets定义了单独的KPI******。 您将能够指定已许可产品的KPI。

   **AEM Sites**

   1. 您可以接受的第95百分点响应时间是多少？

      * 推荐值- 3秒
   1. 在峰值负载下，每分钟有多少页面视图?

      * 推荐值——每分钟200页视图
   **AEM Assets**

   自从最初发布以来，Cloud Manager便能够执行AEM Sites项目的性能测试。 在此版本中，已添加该功能以执行AEM资产项目的性能测试。 通过在30分钟的测试期内重复上传资产并衡量每个资产的处理时间以及各种系统级指标，可以完成资产性能测试。
在项目设置过程中，会指定特定于资产的KPI:

   * 第95百分位数处理时间
   * 每分钟上传的资产
   ![](assets/Setup_Program-KPIs.png)

1. 在“ **配置**”下，您可以在项目中视图或编辑生产环境和非生产环境的配置配置。 如果为项目 **打开了自动缩放**，您将看到自动缩放处于打开状态。

   >[!NOTE]
   >
   >* 自动缩放功能仅适用于生产环境，可能不适用于所有客户项目。
   >* 此版本的不提供按需缩放功 [!UICONTROL Cloud Manager]能。


   ![](assets/Setup_Program-Provisioning.png)

1. 单击 **保存** ，以完成设置向导。

   >[!NOTE]
   >
   >设置初始项目后，您始终可以编辑项目。 请按照以下步骤了解更多详细信息。

## 编辑项目

1. 导航到 **Cloud Manager主屏幕上的解决方** 案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案，然后单击 **编辑** ，以更新或修改项目，如下图所示。

   ![](assets/SetUpProgram6.png)

1. 此时 **会显示“编辑项目** ”屏幕，通过该屏幕可更新或修改项目。

   ![](assets/Editing_Program-screen3.png)

## 后续步骤 {#the-next-steps}

如果您已经设置了 **Pipeline**，则下次执行时将考虑您的更新设置。 如果尚未设置管道，请按照以下步骤先设置管道。

请参 [阅配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) ，以设置管道。
