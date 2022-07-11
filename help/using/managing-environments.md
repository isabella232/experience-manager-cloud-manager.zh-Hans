---
title: 管理环境
description: 了解如何使用Cloud Manager管理您的环境。
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 80f8707e00357f5a08dd835b846c9ee610f3e573
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---


# 管理环境 {#managing-environments}

了解如何使用Cloud Manager管理您的环境。

## 概述页面 {#overview-page}

的 **概述** Cloud Manager的页面包括 **环境** 列出所有托管AEM环境的拼贴。

列出的每个环境都会显示其关联状态。

![“概述”页面](/help/assets/Manage-Environ-Overview.png)

## 环境拼贴 {#environments-tile}

的 **环境** “拼贴”显示您的程序中设置的生产和暂存环境以及状态。

状态是按以下优先级顺序在环境中的节点之间汇总的电源状态。

* 绿色 — 所有节点都在运行
* 红色 — 停止一个或多个节点。
* 蓝色 — 即将出现一个或多个节点。
* 黄色 — 一个或多个节点的电源状态不可用。

![环境拼贴](/help/assets/Environments-card-new.png)

## 管理环境 {#managing-environments-with-cloud-manager}

在 **环境** 拼贴，单击 **管理** 以显示 **环境** 屏幕。

的 **环境** 屏幕会针对您的项目中的生产和暂存环境（如果适用）分别显示一个卡片。 环境的名称显示在每张卡的上方。 该卡包括环境中的节点表，以及cpu的t恤大小、存储、区域和状态。

>[!NOTE]
>
>的 **状态** 节点的表示虚拟机的电源状态，而不反映服务器上AEM的状态。 状态可以是：

* 绿色 — 正在运行
* 红色 — 已停止
* 蓝色 — 即将显示
* 黄色 — 不可用

![“环境”选项卡](/help/assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要环境日志，可以通过客户成功工程师请求获取这些日志。

## 视频教程 {#video-tutorial}

此视频概述了由AEM创作、发布和调度程序实例组成的Cloud Manager环境。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
