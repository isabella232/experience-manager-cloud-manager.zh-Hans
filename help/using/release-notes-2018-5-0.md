---
title: 2018.5.0发行说明
seo-title: 适用于2018.5.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2018.5.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2018.5.0的信息。
uuid: 37f8b155-6984-454d-83a8-83f5fb081
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56 e-4172-8373-486f186 f3 d53
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.5.0发行说明 {#release-notes-for}

以下部分概述 [!UICONTROL Cloud Manager] 了发行版2018.5.0的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.5.0版本的发行日期为2018年月12日。

## 新增功能 {#what-s-new}

* **CI/CD管道通知** -用户现在将看到 [!UICONTROL Experience Cloud] 管道事件通知。请参阅 [通知](notifications.md) 以了解更多信息。

* **计划生产部署** -用户现在可以安排生产部署的日期或时间。请参阅 [部署代码](deploying-code.md) 以了解更多信息。

* **状态** 页面已恢复 **为活动**。

* 在主页上显示的更多特定信息，用于在执行管道过程中遇到的问题。
* 性能测试基础结构改进。

## 错误修复 {#bug-fixes}

* 在某些情况下，使用了不正确的SonarQue配置文件，导致代码质量度量错误。
* sonarque check CQBP-75忽略某些OSGi注释。
* 取消CI/CD管线后，状态无法一致显示。

## 已知问题 {#known-issues}

* 从计划列表屏幕到 ******AEM和监视** 的链接都替换了当前浏览器选项卡，并打开了一个新选项卡。

