---
title: 设置程序
seo-title: 设置程序
description: 入职后，企业所有者需要对项目进行一些初始设置。
seo-description: '入职后，业务所有者需要初始设置Adobe AEM Cloud Manager。 这包括设置项目描述和定义将用于性能测试的KPI。 '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
feature: 入门
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# 设置程序 {#setup-your-program}

入职后，业务所有者需要完成项目的一些初始设置。 这包括设置项目描述和定义用于性能测试的关键绩效指标(KPI)。 （可选）可以上传缩略图。 此外，业务所有者可以在设置环境时配置项目设置。

定义的KPI用作每次管道执行时通过的性能测试基准。

>[!NOTE]
>
>定义的KPI是在&#x200B;**stage**&#x200B;环境上运行的测试上度量的。 通常，这些KPI会按比例缩小以适合舞台环境的功能。
>
>例如，在生产&#x200B;**环境**&#x200B;中，需要平均每分钟1000页视图的用户和在生产中有四个调度程序/发布服务器的用户应将此环境缩放到每分钟250页视图（假定其舞台仅包含一个调度程序/发布服务器对）。
>
>此外，许多用户在生产环境前还会有一个内容投放网络(CDN)，如Akamai或CloudFront。 由于[!UICONTROL Cloud Manager]直接针对舞台环境进行测试，因此KPI应仅反映预期通过CDN的流量，即高速缓存未命中。 通常，这是总生产流量中相对较小的子集。

## 使用[!UICONTROL Cloud Manager]设置项目{#using-cloud-manager-to-setup-your-program}

请按照以下步骤设置项目和定义KPI:

1. 单击&#x200B;**设置项目**&#x200B;以开始[!UICONTROL Cloud Manager]中的设置过程。

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始终可以从操作栏切换、编辑或添加新项目，如下图所示。

   ![image1](assets/set-up-program/setup2.png)


1. **设置项目**&#x200B;屏幕显示编辑项目信息。

1. 您将看到以下三个选项：**General**、**KPI**&#x200B;和&#x200B;**Provisioning**&#x200B;选项卡。

1. 在&#x200B;**“常规”**&#x200B;选项卡中，将缩略图上传到您的项目。 您还可以向项目添加相关描述。

   ![](assets/Setup_Program-General.png)

1. 在&#x200B;**KPI**&#x200B;下，您可以定义两个KPI（每个部署的预期）。 为&#x200B;**AEM Sites**&#x200B;和&#x200B;**AEM Assets**&#x200B;定义单独的KPI。 您将能够指定已授权许可产品的KPI。

   **AEM Sites**

   1. 您可以接受的第95百分点响应时间是多少？

      * 推荐值 — 3秒
   1. 在峰值负载下，每分钟有多少页面视图?

      * 推荐值 — 每分钟200页视图

   **AEM Assets**

   Cloud Manager自初始发布以来，已经能够执行AEM Sites项目的性能测试。 在此版本中，还添加了该功能以执行AEM Assets项目的性能测试。 资产性能测试是通过在30分钟的测试期内重复上传资产并衡量每个资产的处理时间以及各种系统级别指标来完成的。
在项目设置过程中，会指定特定于资产的KPI:

   * 第95百分点处理时间
   * 每分钟上传的资产

   ![](assets/Setup_Program-KPIs.png)

1. 在&#x200B;**预配**&#x200B;下，您可以视图或编辑项目中生产和非生产环境的预配配置。 如果已为项目打开自动缩放，您将看到&#x200B;**自动缩放在**&#x200B;上。

   >[!NOTE]
   >
   >* 自动缩放功能仅适用于生产环境，可能不适用于所有项目。
   >* 此版本[!UICONTROL Cloud Manager]不提供按需扩展。


   ![](assets/Setup_Program-Provisioning.png)

1. 单击&#x200B;**保存**&#x200B;以完成安装向导。

   >[!NOTE]
   >
   >设置初始项目后，您始终可以编辑项目。 有关更多详细信息，请按照以下步骤操作。

## 编辑项目

1. 在&#x200B;**Cloud Manager**&#x200B;主屏幕上导航到解决方案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案并单击&#x200B;**编辑**&#x200B;以更新或修改项目，如下图所示。

   ![](assets/SetUpProgram6.png)

1. 此时将显示&#x200B;**编辑项目**&#x200B;屏幕，允许您更新或修改项目。

   ![](assets/Editing_Program-screen3.png)

## 后续步骤 {#the-next-steps}

如果您已经设置了&#x200B;**Pipeline**，则下次执行将考虑您的更新设置。 如果尚未设置管道，请按照以下步骤先设置管道。

请参阅[配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)以设置管道。
