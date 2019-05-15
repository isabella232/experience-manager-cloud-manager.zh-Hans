---
title: 2018.9.0发行说明
seo-title: 适用于2018.9.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2018.9.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2018.9.0的信息。
uuid: af5808f-828f-4846-bee4-1e62194 b48 ad
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8ba8d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.9.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本增加了对基于Adobe I/的API(包括Events)的支持，以便将 [!UICONTROL Cloud Manager]CI/CD管线与其他系统集成。它还开始响应UI层的重写。

## 发布日期 {#release-date}

版本2018.9.0 [!UICONTROL Cloud Manager] 的发布日期为2018年11月日。

## 新增功能 {#whats-new}

* **CI/CD管线** -新API和事件系统，用于将 [!UICONTROL Cloud Manager]CI/CD管线与其他系统集成。请参阅 [!UICONTROL Cloud Manager] API文档(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)以了解更多信息。

* **UI** -更具响应性和响应度的新UI层的引入。

## 错误修复 {#bug-fixes}

* 在 [!UICONTROL Cloud Manager] 2018.8.0中，活动页面持续时间在几分钟和几小时内列出，但该信息未反映在表标题中。
* 在少数情况下，客户无法启动新的应用程序项目向导。
* 新应用程序项目向导对话框中的按钮标签令人误解。
* 在某些情况下，单击活动页面中的详细信息按钮将重定向到概述页面。
* 一些罕见而意外的情况导致概述页面上缺少卡。
* 资产图标显示在所有客户的计划列表页面上。
* 返回失败时，有时管道执行将显示在 *验证* 步骤中。
* 在某些情况下，程序描述的长度会被错误计算。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含虚线。
* Adobe [!UICONTROL Experience Cloud] 通知提要栏不能一致地加载通知。但是，通知在Adobe [!UICONTROL Experience Cloud] 中可见，如果配置，则仍将通过电子邮件发送。

