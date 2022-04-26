---
title: 管理环境
seo-title: Manage your Environments
description: 了解Cloud Manager环境
seo-description: Follow this page to view the list of production and non-production environments that are used for setting up and running the CI/CD pipeline in Cloud Manager.
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: Environments
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 6ff704ec11dd4a5f73d5b5df5721c4fee649527b
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 6%

---

# 管理环境 {#manage-your-environments}

>[!NOTE]
>要了解如何在AEMas a Cloud Service中管理Cloud Manager的环境，请参阅 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=zh-hans#using-cloud-manager).

的 **概述** Cloud Manager的页面包括 **环境** 列出所有托管AEM环境的拼贴。

列出的每个环境都会显示其关联状态。

![](assets/Manage-Environ-Overview.png)

## 视频教程 {#video-tutorial}

### Cloud Manager环境概述 {#environ-video}

以下视频为由AEM创作、AEM发布和调度程序实例组成的Cloud Manager环境提供了概述。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## 在Cloud Manager中访问环境 {#accessing-environments-in-cloud-manager}

的 **环境** “拼贴”显示在项目中设置的生产和暂存环境以及状态。

状态是环境中各节点的累计电源状态。 如果所有节点都在运行，则为绿色；如果一个节点停止运行，则为红色；如果某个节点启动，则为蓝色；如果某个节点的电源状态不可用，则为黄色（按此优先级顺序）。

![](assets/Environments-card-new.png)

### 环境 {#environments}

单击 **管理** 以显示 **环境** 屏幕。

的 **环境** 屏幕会显示每个 *生产* 和 *阶段* 环境（如果适用）。 环境的名称显示在每张卡的上方。 该卡包括环境中的节点表，以及cpu的t恤大小、存储、区域和状态。

>[!NOTE]
>
>的 **状态** 节点的表示虚拟机的电源状态，而不反映服务器上AEM的状态。 状态可以是 **正在运行** （绿色圆圈）、 **已停止** （红色圆圈）、 **即将推出** （蓝色圆圈）或 **不可用** （黄色圆圈）。

![](assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要环境日志，可以通过客户成功工程师请求获取这些日志。
