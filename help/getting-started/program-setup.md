---
title: 程序设置
description: 入门后，业务所有者需要对程序进行一些初始设置。
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---


# 程序设置 {#program-setup}

入门后，业务所有者将完成程序的初始设置，包括设置程序说明并定义用于性能测试的关键绩效指标(KPI)。

## 程序设置 [!UICONTROL Cloud Manager] {#program-setup-cloud-manager}

按照以下步骤设置计划并定义KPI。

1. 登录Cloud Manager(位于 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 并选择相应的组织。

1. 单击 **安装程序** 以启动设置过程。

   ![设置程序](/help/assets/set-up-program/setup1.png)

1. 在 **安装程序** 对话框，可以在三个选项卡中输入项目信息：

   * **常规**
   * **KPI**
   * **配置**

1. 在 **常规** 选项卡上，为程序添加描述，并（可选）通过单击 **更改照片**.

   ![“常规”选项卡](/help/assets/Setup_Program-General.png)

1. 在 **KPI** 选项卡，定义您的KPI。 在本例中，为 **AEM Sites** 和 **AEM Assets**. 您将能够为已获许可的产品指定KPI。

   * 请参阅部分 [KPI](#kpis) 有关如何在Cloud Manager中测量KPI的更多详细信息。

   ![定义KPI](/help/assets/Setup_Program-KPIs.png)

1. 在 **配置** 选项卡中，如果为程序启用了自动缩放，则可以为环境定义按需缩放选项。

   * 自动缩放功能仅适用于生产环境，并且可能不适用于所有客户程序。

   ![配置选项](/help/assets/Setup_Program-Provisioning.png)

1. 单击 **保存** 完成安装向导。

将创建您的程序。 在项目准备就绪之前，可能需要几分钟时间才能配置资源。

## 编辑程序 {#editing-program}

在程序设置完成后，您可以对其进行编辑。 按照以下步骤编辑程序。

1. 登录Cloud Manager(位于 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 并选择相应的组织。

1. 从Cloud Manager主屏幕导航到程序。

1. 单击 **编辑程序** 要更新或修改您的程序，请使用 **概述** 页面。

   ![编辑程序选项](/help/assets/set-up-program/edit-program1.png)

1. 的 **编辑程序** 对话框，用于更新程序。 请参阅部分 [使用Cloud Manager设置程序](#program-setup-cloud-manager) 以了解有关可用字段的详细信息。

   ![“编辑项目”对话框](/help/assets/set-up-program/edit-program-general.png)

1. 单击 **更新** 以保存更改。

请注意，这些更改会立即保存到Cloud Manager，但在下一个管道运行之前不会反映在您的环境中。

如果尚未创建管道，请参阅文档 [配置生产管道](/help/using/production-pipelines.md) 和 [配置非生产管道。](/help/using/non-production-pipelines.md)

## 在程序之间切换 {#swithing-programs}

处理项目时，您可以快速切换到其他项目，而无需返回Cloud Manager概述页面。

使用操作栏可切换到其他程序、编辑当前程序或添加新程序。

![程序切换器](/help/assets/set-up-program/setup2.png)

## KPI {#kpis}

网站KPI是在测试环境中运行的测试中测量的。 通常，会缩小这些KPI以适合暂存环境的功能。

例如，如果用户在生产环境中平均每分钟需要1000次页面查看，而在生产中有四个调度程序/发布服务器，则该用户应将该页面查看次数扩展为每分钟250次页面查看。 这假定其暂存环境只包含一个调度程序/发布服务器对。

资产性能测试是通过在30分钟测试期间重复上传资产来完成的，测试方法是：测量每个资产的处理时间以及各种系统级别量度。

您的生产环境之前可能有一个内容交付网络(CDN)，例如Akamai或CloudFront。 自 [!UICONTROL Cloud Manager] 直接针对暂存环境进行测试，KPI应仅反映预期通过CDN的流量，即缓存缺失。 通常，这将是生产流量总量中相对较小的一部分。

## 视频概述 {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
