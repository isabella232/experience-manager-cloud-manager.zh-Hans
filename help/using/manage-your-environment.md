---
title: 管理环境
seo-title: 管理环境
description: 了解Cloud Manager环境
seo-description: 可查看本页以视图用于在Cloud Manager中设置和运行CI/CD管道的生产和非生产环境的列表。
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: Environments
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---


# 管理环境 {#manage-your-environments}

Cloud Manager的&#x200B;**概述**&#x200B;页面包括列表所有托管AEM环境的&#x200B;**环境**&#x200B;拼贴。

列出的每个环境都显示其关联状态。

![](assets/Manage-Environ-Overview.png)

## 视频教程{#video-tutorial}

### Cloud Manager环境概述{#environ-video}

以下视频概述了由AEM作者、AEM发布和调度程序实例组成的Cloud Manager环境。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## 在Cloud Manager {#accessing-environments-in-cloud-manager}中访问环境

**环境**&#x200B;拼贴显示在项目中设置的生产和舞台环境以及状态。

状态是环境中节点间的累计电源状态。 如果所有节点都在运行，则为绿色；如果连一个节点都停止，则为红色；如果连一个节点都启动，则为蓝色；如果连一个节点都处于电源状态不可用（按优先级顺序），则为黄色。

![](assets/Environments-card-new.png)

### 环境 {#environments}

单击&#x200B;**管理**&#x200B;以显示&#x200B;**环境**&#x200B;屏幕。

**环境**&#x200B;屏幕显示项目中&#x200B;*生产*&#x200B;和&#x200B;*舞台*&#x200B;环境（如果适用）的卡。 环境的名称显示在每张卡的上方。 该卡包括环境中的节点表以及cpu的t恤尺寸、存储、区域和状态。

>[!NOTE]
>
>节点的&#x200B;**STATUS**&#x200B;表示VM的电源状态，但不反映服务器上AEM的状态。 状态可以是&#x200B;**运行**（绿圈）、**停止**（红圈）、**启动**（蓝圈）或&#x200B;**不可用**（黄圈）。

![](assets/Environments-tab.png)
