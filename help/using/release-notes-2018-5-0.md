---
title: 2018.5.0 版发行说明
seo-title: AEM Cloud Manager 2018.5.0发行说明
description: 可查看本页以获取Cloud Manager Release 2018.5.0的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2018.5.0版的相关信息。
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# 2018.5.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2018.5.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.5.0的发布日期为2018年7月12日。

## 新增功能 {#what-s-new}

* **CI/CD管道通知** -用户现在将看到 [!UICONTROL Experience Cloud] 管道事件的通知。请参阅[通知](notifications.md)以了解更多信息。

* **计划生产部署** -用户现在可以计划某个日期或时间进行生产部署。请参阅[部署代码](deploying-code.md)以了解更多信息。

* **状** 态页已重新命名 **为活动**。

* 在主页上显示有关管道执行过程中遇到的问题的更多特定信息。
* 性能测试基础架构改进。

## 错误修复 {#bug-fixes}

* 在某些情况下，使用了不正确的SonarQube用户档案，导致代码质量指标不正确。
* SonarQube检查CQBP-75会忽略某些OSGi注释。
* 取消CI/CD管道时，状态显示不一致。

## 已知问题 {#known-issues}

* 从项目列表屏幕到&#x200B;**AEM**&#x200B;和&#x200B;**监视**&#x200B;的链接会替换当前浏览器选项卡并打开到新选项卡。

