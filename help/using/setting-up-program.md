---
title: 设置程序
seo-title: 设置程序
description: 入门后，业务所有者需要对程序进行一些初始设置。
seo-description: '入门后，业务所有者将需要执行一些初始设置AdobeAEM Cloud Manager。 这包括设置计划描述并定义将用于性能测试的KPI。 '
feature: 入门
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: a65c413e9ffa96f950cf1c59771b45ce0f810bc0
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 2%

---

# 设置程序 {#setup-your-program}

入门后，业务所有者需要完成程序的一些初始设置。 这包括设置计划描述并定义将用于性能测试的关键绩效指标(KPI)。 或者，也可以上传缩略图。 此外，业务所有者可以在设置程序时配置环境配置。

定义的KPI用作性能测试的基线，每次执行管道时都会通过该基线。

>[!NOTE]
>定义的KPI是在&#x200B;**stage**环境中运行的测试中测量的。 通常，会缩小这些KPI以适合暂存环境的功能。
>例如，如果用户在生产&#x200B;**环境**中平均每分钟需要1000次页面查看，并且在生产中有四个调度程序/发布服务器，则该用户每分钟应该可以查看250次页面（假定其暂存环境仅包含一个调度程序/发布服务器对）。
>此外，许多用户在其生产环境之前还将拥有内容交付网络(CDN)，例如Akamai或CloudFront。 由于[!UICONTROL Cloud Manager]直接针对暂存环境进行测试，因此KPI应仅反映预期通过CDN的流量，即缓存缺失。 通常，这将是生产流量总量中相对较小的一部分。

## 使用[!UICONTROL Cloud Manager]设置程序{#using-cloud-manager-to-setup-your-program}

按照以下步骤设置计划并定义KPI:

1. 单击&#x200B;**Setup Program**&#x200B;以在[!UICONTROL Cloud Manager]中启动设置过程。

   ![图像1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始终可以从操作栏中切换、编辑或添加新程序，如下图所示。

   ![图像1](assets/set-up-program/setup2.png)


1. **设置程序**&#x200B;屏幕显示编辑程序信息。

1. 您将看到三个选项，分别作为&#x200B;**General**、**KPI**&#x200B;和&#x200B;**Provisioning**&#x200B;选项卡。

1. 在&#x200B;**常规**&#x200B;选项卡中，将缩略图上传到您的程序。 您还可以向项目添加相关描述。

   ![](assets/Setup_Program-General.png)

1. 在&#x200B;**KPI**&#x200B;下，您可以定义两个KPI（对每个部署的预期）。 为&#x200B;**AEM Sites**&#x200B;和&#x200B;**AEM Assets**&#x200B;定义单独的KPI。 您将能够为已获许可的产品指定KPI。

   **AEM Sites**

   1. 您可以接受的第95个百分位数响应时间是多少？

      * 推荐值 — 3秒
   1. 在峰值负载下，每分钟有多少次页面查看？

      * 推荐值 — 每分钟200次页面查看

   **AEM Assets**

   自初始版本发布以来，Cloud Manager便能够对AEM Sites程序执行性能测试。 在此版本中，还添加了为AEM Assets程序执行性能测试的功能。 资产性能测试是通过在30分钟测试期间重复上传资产来完成的，测试方法是：测量每个资产的处理时间以及各种系统级别量度。
在项目群设置过程中，会指定特定于资产的KPI:

   * 第95个百分位数处理时间
   * 每分钟上传的资产

   ![](assets/Setup_Program-KPIs.png)

1. 在&#x200B;**Provisioning**&#x200B;下，您可以查看或编辑程序中生产环境和非生产环境的配置配置。 如果为程序打开了自动缩放功能，则会看到&#x200B;**自动缩放功能在**&#x200B;上。

   >[!NOTE]
   >自动缩放功能仅适用于生产环境，并且可能不适用于所有客户程序。

   ![](assets/Setup_Program-Provisioning.png)

1. 单击&#x200B;**Save**&#x200B;以完成安装向导。

   >[!NOTE]
   >设置初始程序后，您始终可以编辑该程序。 有关更多详细信息，请执行以下步骤。

## 编辑程序

1. 在&#x200B;**Cloud Manager**&#x200B;主屏幕上导航到解决方案。

   ![](assets/SetUpProgram5.png)

1. 选择解决方案并单击&#x200B;**编辑**&#x200B;以更新或修改程序，如下图所示。

   ![](assets/set-up-program/edit-program1.png)

1. 将显示&#x200B;**编辑程序**&#x200B;屏幕，用于更新或修改程序。

   您可以从&#x200B;**General**&#x200B;选项卡更新程序名称和说明。

   ![](assets/set-up-program/edit-program-general.png)

   导航到&#x200B;**KPI**&#x200B;选项卡，以更新有关AEM Sites和Assets的信息。

   ![](assets/set-up-program/edit-program-kpi.png)

   此外，您还可以导航到&#x200B;**Provisioning**&#x200B;选项卡，以编辑程序中生产环境和非生产环境的配置配置。

   ![](assets/set-up-program/edit-program-provision.png)

1. 单击&#x200B;**Update**&#x200B;以保存所做的编辑。

## 后续步骤 {#the-next-steps}

如果已设置管道，则下次执行时将考虑更新的设置。 如果尚未设置管道，请按照步骤先设置管道。

请参阅[配置CI/CD管线](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)以设置管线。
