---
title: 设置程序
seo-title: Set Up Your Program
description: 入门后，业务所有者需要对程序进行一些初始设置。
seo-description: After onboarding, the business owner will need to do some initial setup of Adobe AEM Cloud Manager. This involves setting the program description and defining the KPIs which will be used for performance testing.
feature: Getting Started
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 设置程序 {#setup-your-program}

入门后，业务所有者需要完成程序的一些初始设置。 这包括设置计划描述并定义将用于性能测试的关键绩效指标(KPI)。 或者，也可以上传缩略图。 此外，业务所有者可以在设置程序时配置环境配置。

定义的KPI用作性能测试的基线，每次执行管道时都会通过该基线。

>[!NOTE]
>定义的KPI是在 **阶段** 环境。 通常，会缩小这些KPI以适合暂存环境的功能。
>例如，用户在生产中平均每分钟需要1000次页面查看 **环境** 并且在生产中拥有四台dispatcher/publish服务器应该会将此时间范围扩展到每分钟250次页面查看（假定其暂存环境只包含一个dispatcher/publish服务器对）。
>此外，许多用户在其生产环境之前还将拥有内容交付网络(CDN)，例如Akamai或CloudFront。 自 [!UICONTROL Cloud Manager] 直接针对暂存环境进行测试，KPI应仅反映预期通过CDN的流量，即缓存缺失。 通常，这将是生产流量总量中相对较小的一部分。

## 使用 [!UICONTROL Cloud Manager] 设置程序 {#using-cloud-manager-to-setup-your-program}

按照以下步骤设置计划并定义KPI:

1. 单击 **安装程序** 要在 [!UICONTROL Cloud Manager].

   ![图像1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始终可以从操作栏中切换、编辑或添加新程序，如下图所示。

   ![图像1](assets/set-up-program/setup2.png)


1. 的 **安装程序** 屏幕上会显示“编辑项目信息”。

1. 您将看到三个选项，如 **常规**, **KPI**&#x200B;和 **配置** 选项卡。

1. 在 **常规** 选项卡，将缩略图上传到您的项目。 您还可以向项目添加相关描述。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI**，您可以定义两个KPI（对每个部署的预期）。 为 **AEM Sites** 和 **AEM Assets**. 您将能够为已获许可的产品指定KPI。

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

1. 在 **配置**，则可以查看或编辑项目中生产环境和非生产环境的配置配置。 您将看到 **自动缩放已开启**，如果为程序打开了自动缩放。

   >[!NOTE]
   >自动缩放功能仅适用于生产环境，并且可能不适用于所有客户程序。

   ![](assets/Setup_Program-Provisioning.png)

1. 单击 **保存** 完成安装向导。

   >[!NOTE]
   >设置初始程序后，您始终可以编辑该程序。 有关更多详细信息，请执行以下步骤。

## 编辑程序 {#editing-program}

1. 从 **Cloud Manager** 主屏幕。

1. 单击 **编辑程序** 要更新或修改您的程序，请使用 **概述** 页面，如下图所示。

   ![](assets/set-up-program/edit-program1.png)

1. 的 **编辑程序** 屏幕，可用于更新或修改程序。

   您可以从 **常规** 选项卡。

   ![](assets/set-up-program/edit-program-general.png)

   导航到 **KPI** 选项卡，以更新有关AEM Sites和Assets的信息。

   ![](assets/set-up-program/edit-program-kpi.png)

   此外，您还可以导航到 **配置** 选项卡，以编辑项目中生产环境和非生产环境的配置配置。

   ![](assets/set-up-program/edit-program-provision.png)

1. 单击 **更新** 以保存所做的编辑。

## 后续步骤 {#the-next-steps}

如果已设置管道，则下次执行时将考虑更新的设置。 如果尚未设置管道，请按照步骤先设置管道。

请查看相关文档 [配置生产管道](configuring-production-pipelines.md) 和 [配置非生产管道](configuring-non-production-pipelines.md) 来设置管道。
