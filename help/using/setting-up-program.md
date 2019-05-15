---
title: 设置您的计划
seo-title: 设置您的计划
description: 在入门培训之后，业务所有者需要进行一些初始设置。
seo-description: '在入门培训之后，业务所有者需要进行Adobe AEM Cloud Manager的初步设置。这涉及设置程序描述并定义将用于性能测试的KPI。 '
uuid: 9ecf8743-1f5a-4744-86aff-e226567642 f
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: 快速入门
discoiquuid: c2393540-e852-4f7 c-aafd-142720900065d2
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 设置您的计划 {#setup-your-program}

在入门培训之后，业务所有者需要完成程序的初始设置。这包括设置计划描述并定义将用于性能测试的主要性能指标(KPI)。或者，也可以上传缩略图。此外，企业所有者还可以在设置程序时配置环境配置。

定义的KPI用作性能测试的基准，每次执行渠道时都通过该基准。

>[!NOTE]
>
>定义的KPI会度量 **在舞台** 环境上运行的测试。通常，这些KPI会缩小以适合舞台环境的功能。
>
>例如，用户在生产 **环境** 中平均每分钟需要1000次页面查看，并且在生产中具有四个调度程序/发布服务器的用户应将此设置为每分钟250次页面查看(假定他们的舞台环境只包含单个调度程序/发布服务器对)。
>
>此外，许多用户将在生产环境前具有内容交付网络(CDN)，如Akamai或CloudFront。由于 [!UICONTROL Cloud Manager] 直接针对舞台环境进行测试，KPI应该只反映传递CDN的流量，即缓存错误。通常，这将是总生产流量的相对较小子集。

## 使用 [!UICONTROL Cloud Manager] 设置您的程序 {#using-cloud-manager-to-setup-your-program}

请按照以下步骤设置计划并定义KPI：

1. 单击 **设置程序** 以启动设置过程 [!UICONTROL Cloud Manager]。

   ![](assets/SetUpProgram1.png)

1. **设置程序** 屏幕显示编辑程序信息。

1. 您将看到三个选项： **“常规”**、“ **KPI**和 **配置** ”选项卡。

1. 在 **“常规** ”选项卡中，将缩略图上传到您的程序。您还可以为程序添加相关描述。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI**下，您可以定义两个KPI(每个部署期望)。为 **AEM Sites** 和 **AEM Assets定义了单独的KPI**。您将能够为您已获得许可的产品指定KPI。

   **AEM Sites**

   1. 您可以接受的95%的感知响应时间是什么？

      * 建议的值-秒
   1. 峰值负载下每分钟的页面查看次数是多少？

      * 推荐值-每分钟200页查看次数
   **AEM Assets**

   自最初发布以来，Cloud Manager已经能够执行AEM Sites计划的性能测试。在此版本中，还添加了该功能以执行AEM Assets程序的性能测试。资产性能测试是通过在30分钟测试期内重复上传资产并测量每个资产的处理时间以及各种系统级别指标来完成的。
在计划设置期间，指定特定于资产的KPI：

   * 95th Percentile处理时间
   * 每分钟上传的资产
   ![](assets/Setup_Program-KPIs.png)

1. 在 **Provisioning**(供应)下，您可以查看或编辑程序中生产和非生产环境的供应配置。如果程序已开启自动缩放，您将看到 **自动缩放打开**。

   >[!NOTE]
   >
   >* 自动缩放功能仅适用于生产环境，可能无法用于所有客户计划。
   >* 此版本的点播扩展不可用 [!UICONTROL Cloud Manager]。


   ![](assets/Setup_Program-Provisioning.png)

1. 单击 **保存** 以完成设置向导。

   >[!NOTE]
   >
   >在初始程序设置完毕后，您始终可以编辑该程序。请按照以下步骤了解更多详细信息。

## 编辑程序

1. 导航到 **Cloud Manager** 主页屏幕上的解决方案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案并单击 **编辑** 以更新或修改您的程序，如下图所示。

   ![](assets/SetUpProgram6.png)

1. 此时会显示 **“编辑程序** ”屏幕，用于更新或修改您的程序。

   ![](assets/Editing_Program-screen3.png)

## 后续步骤 {#the-next-steps}

如果您已经设置 **了渠道**，则下一次执行将会考虑更新的设置。如果尚未设置管道，请按照步骤先设置管道。

请参阅 [配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) 以设置管道。
