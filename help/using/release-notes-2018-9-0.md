---
title: 2018.9.0发行说明
seo-title: AEM Cloud Manager 2018.8.0版本说明
description: 可查看本页以获取Cloud Manager 2018.9.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.9.0版的信息。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 发行说明
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 949d3cf0239a02875ba4ad1888e081f104dec2e2

---


# 2018.9.0发行说明 {#release-notes-for}

2018.9.0 [!UICONTROL Cloud Manager] 版本增加了对基于Adobe I/O的API（包括Events）的支持，以便将其CI/CD管道与其他系统 [!UICONTROL Cloud Manager]集成在一起。 它还会在React中开始重写UI层。

## 发布日期 {#release-date}

版本2018.9.0 [!UICONTROL Cloud Manager] 的发布日期为2018年11月1日。

## 新增功能 {#whats-new}

* **CI/CD管道** -用于将CI/CD管道与其他系统集 [!UICONTROL Cloud Manager]成的新API和事件系统。 请参阅 [!UICONTROL Cloud Manager] API文档(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)以了解更多信息。

* **UI** —— 引入响应更快、性能更高的新UI层。

## 错误修复 {#bug-fixes}

* 2018. [!UICONTROL Cloud Manager] 8.0中，“活动”页面的持续时间以分钟和小时为单位列出，但该信息未反映在表标题中。
* 在极少数情况下，客户无法启动新的应用程序项目向导。
* 新应用程序项目向导对话框中的按钮标签具有误导性。
* 在某些情况下，单击“活动”页面的“详细信息”按钮将重定向到“概述”页面。
* 某些罕见且意外的情况导致“概述”页面上缺少卡。
* 资产图标显示在“计划列表”页面上，以供所有客户使用。
* 当出现后端故障时，有时管道执行似乎仍保留在验 *证步骤* 。
* 在某些情况下，程序描述的长度计算错误。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含虚线。
* Adobe通知 [!UICONTROL Experience Cloud] 提要栏可能无法一致地加载通知。 但是，通知在Adobe中可见，如 [!UICONTROL Experience Cloud] 果已配置，则仍将通过电子邮件发送。

