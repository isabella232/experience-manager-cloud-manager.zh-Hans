---
title: 设置程序
seo-title: 设置程序
description: 入职后，业主需要对项目进行一些初始设置。
seo-description: '入门后，业务所有者需要进行AdobeAEM Cloud Manager的初始设置。 这包括设置项目描述和定义将用于性能测试的KPI。 '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 6851884b08c0c0a971242a958f72a7673a1a1196
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---


# 设置程序 {#setup-your-program}

入职后，业主需要完成项目的一些初始设置。 这包括设置项目描述和定义用于性能测试的关键绩效指标(KPI)。 （可选）可以上传缩略图。 此外，业务所有者可以在设置环境时配置项目设置。

定义的KPI用作每次管道执行时通过的性能测试的基准。

>[!NOTE]
>
>定义的KPI是在&#x200B;**stage**&#x200B;环境上运行的测试中衡量的。 通常，这些KPI会按比例缩小以适合阶段环境的功能。
>
>例如，用户在生产&#x200B;**环境**&#x200B;中平均每分钟需要1000页视图，并且生产中有四个调度程序／发布服务器时，应将此视图缩放到每分钟250页(假定其阶段环境仅包含一个调度程序／发布服务器对)。
>
>此外，许多用户在其生产投放前面还将有内容环境网络(CDN)，如Akamai或CloudFront。 由于[!UICONTROL Cloud Manager]直接针对阶段环境进行测试，因此KPI应仅反映预期通过CDN的流量，即高速缓存未命中。 通常，这是总生产流量中相对较小的子集。

## 使用[!UICONTROL Cloud Manager]设置项目{#using-cloud-manager-to-setup-your-program}

请按照以下步骤设置项目和定义KPI:

1. 单击&#x200B;**设置项目**&#x200B;以在[!UICONTROL Cloud Manager]中开始设置过程。

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始终可以从操作栏切换、编辑或添加新项目，如下图所示。

   ![image1](assets/set-up-program/setup2.png)


1. **设置项目**&#x200B;屏幕显示编辑项目信息。

1. 您将看到三个选项，如&#x200B;**General**、**KPI**&#x200B;和&#x200B;**Provisioning**&#x200B;选项卡。

1. 在&#x200B;**常规**&#x200B;选项卡中，将缩略图上传到项目。 您还可以向项目添加相关描述。

   ![](assets/Setup_Program-General.png)

1. 在&#x200B;**KPI**&#x200B;下，您可以定义两个KPI（每个部署的预期值）。 为&#x200B;**AEM Sites**&#x200B;和&#x200B;**AEM Assets**&#x200B;定义单独的KPI。 您将能够指定已授权产品的KPI。

   **AEM Sites**

   1. 您可以接受的第95百分点响应时间是多少？

      * 推荐值- 3秒
   1. 在高峰负载下，每分钟有多少页面视图?

      * 推荐值——每分钟200页视图

   **AEM Assets**

   从最初发布起，Cloud Manager便能够执行AEM Sites项目的性能测试。 在此版本中，该功能也被添加为执行AEM Assets项目的性能测试。 资产性能测试通过在30分钟的测试期内重复上传资产并衡量每个资产的处理时间以及各种系统级别指标来完成。
在项目设置过程中，会指定特定于资产的KPI:

   * 第95百分点处理时间
   * 每分钟上传的资产

   ![](assets/Setup_Program-KPIs.png)

1. 在&#x200B;**配置**&#x200B;下，您可以视图或编辑项目中生产和非生产环境的配置配置。 如果为项目启用了自动缩放，您将看到&#x200B;**自动缩放处于**&#x200B;状态。

   >[!NOTE]
   >
   >* 自动缩放功能仅适用于生产环境，可能不适用于所有项目。
   >* 此版本的[!UICONTROL Cloud Manager]不提供按需扩展。


   ![](assets/Setup_Program-Provisioning.png)

1. 单击&#x200B;**保存**&#x200B;以完成安装向导。

   >[!NOTE]
   >
   >初始项目设置完成后，您始终可以编辑项目。 请按照以下步骤了解更多详细信息。

## 编辑项目

1. 在&#x200B;**云管理器**&#x200B;主屏幕上导航到解决方案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案并单击&#x200B;**编辑**&#x200B;以更新或修改项目，如下图所示。

   ![](assets/SetUpProgram6.png)

1. 将显示&#x200B;**编辑项目**&#x200B;屏幕，通过该屏幕可更新或修改项目。

   ![](assets/Editing_Program-screen3.png)

## 后续步骤 {#the-next-steps}

如果您已经设置了&#x200B;**管道**，则下次执行将考虑您的更新设置。 如果尚未设置管道，请按照步骤先设置管道。

请参阅[配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)以设置管道。
