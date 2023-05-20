---
title: 管理环境
description: 了解如何使用 Cloud Manager 管理环境。
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 80f8707e00357f5a08dd835b846c9ee610f3e573
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 100%

---


# 管理环境 {#managing-environments}

了解如何使用 Cloud Manager 管理环境。

## “概述”页面 {#overview-page}

Cloud Manager 的&#x200B;**概述**&#x200B;页面包含&#x200B;**环境**&#x200B;图块，它列出了所有托管的 AEM 环境。

每个列出的环境都会显示其关联状态。

![“概述”页面](/help/assets/Manage-Environ-Overview.png)

## “环境”图块 {#environments-tile}

**环境**&#x200B;图块显示项目中配置的生产和暂存环境以及状态。

状态是按以下优先级顺序跨环境中的节点排列的电源状态。

* 绿色 – 所有节点都正在运行。
* 红色 – 一个或多个节点已停止。
* 蓝色 – 一个或多个节点即将启动。
* 黄色 – 一个或多个节点的电源状态为不可用。

![“环境”图块](/help/assets/Environments-card-new.png)

## 管理环境 {#managing-environments-with-cloud-manager}

在&#x200B;**环境**&#x200B;图块上，单击&#x200B;**管理**&#x200B;以显示&#x200B;**环境**&#x200B;屏幕。

**环境**&#x200B;屏幕为项目中的每个生产和暂存环境显示一个信息卡（如果适用）。每张信息卡的上方将显示环境名称。信息卡包括环境中的节点表以及 CPU 尺寸、存储、区域和状态。

>[!NOTE]
>
>节点的&#x200B;**状态**&#x200B;表示 VM 的电源状态，而不会反映服务器上 AEM 的状态。状态可以是：

* 绿色 – 正在运行
* 红色 – 已停止
* 蓝色 – 即将运行
* 黄色 – 不可用

![“环境”信息卡](/help/assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要环境日志，可以向您的客户成功工程师索要。

## 视频教程 {#video-tutorial}

此视频概述了由 AEM 创作、发布和 Dispatcher 实例组成的 Cloud Manager 环境。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
