---
title: 2018.5.0发行说明
seo-title: AEM Cloud Manager 2018.5.0版本说明
description: 可查看本页以获取Cloud Manager 2018.5.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.5.0版的信息。
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 发行说明
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b

---


# 2018.5.0发行说明 {#release-notes-for}

以下部分概述了2018.5.0版 [!UICONTROL Cloud Manager] 的一般发行说明。

## 发布日期 {#release-date}

版本2018.5.0 [!UICONTROL Cloud Manager] 的发布日期为2018年7月12日。

## 新增功能 {#what-s-new}

* **CI/CD管道通知** -用户现在将看到管道 [!UICONTROL Experience Cloud] 事件的通知。 请参阅通 [知](notifications.md) ，了解更多。

* **计划生产部署** -用户现在可以为生产部署计划日期或时间。 请参阅 [部署代码](deploying-code.md) ，了解更多。

* **状态页** (已标题为“活 **动”)**。

* 在主页上显示的有关管线执行过程中遇到的问题的更多特定信息。
* 性能测试基础架构改进。

## 错误修复 {#bug-fixes}

* 在某些情况下，使用的SonarQube配置文件不正确，导致代码质量指标不正确。
* SonarQube检查CQBP-75会忽略某些OSGi注释。
* 取消CI/CD管道时，状态显示不一致。

## 已知问题 {#known-issues}

* 指向 **AEM** 和“程序列 **** 表”屏幕的监视链接会替换当前浏览器选项卡并打开到新选项卡。

