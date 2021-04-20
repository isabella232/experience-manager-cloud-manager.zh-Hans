---
title: 2018.9.0 版发行说明
seo-title: AEM Cloud Manager 2018.9.0发行说明
description: 可查看本页以获取Cloud Manager 2018.9.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.9.0版的信息。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: Release Information
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 9%

---


# 2018.9.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本增加了对基于Adobe I/O的API(包括事件)的支持，用于将[!UICONTROL Cloud Manager]的CI/CD管道与其他系统集成。 此外，该 API 还可以在 React 中重写 UI 层。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.9.0的发布日期为2018年11月01日。

## 新增功能 {#whats-new}

* **CI/CD管道**  — 用于将CI/CD管道与其 [!UICONTROL Cloud Manager]他系统集成的新API和事件系统。有关详细信息，请参阅[!UICONTROL Cloud Manager] API文档(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)。

* **UI**  — 引入响应更快的新UI图层。

## 错误修复 {#bug-fixes}

* 在[!UICONTROL Cloud Manager] 2018.8.0中，活动页面的持续时间以分钟和小时为单位列出，但该信息未反映在表标题中。
* 偶尔，客户无法开始新的应用程序项目向导。
* 新应用程序项目向导对话框中的按钮标签具有误导性。
* 在某些情况下，单击“活动”页面的“详细信息”按钮将重定向到“概述”页面。
* 某些罕见且意外的情况导致“概述”页面上缺少信息卡。
* 资产图标会显示在所有客户的项目列表页面上。
* 当出现后端故障时，有时管道执行会显示在&#x200B;*验证*&#x200B;步骤中。
* 在某些情况下，项目描述的长度计算错误。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含虚线。
* Adobe[!UICONTROL Experience Cloud]通知提要栏可能无法一致加载通知。 但是，Adobe[!UICONTROL Experience Cloud]中会显示通知，如果配置，仍将通过电子邮件发送通知。

