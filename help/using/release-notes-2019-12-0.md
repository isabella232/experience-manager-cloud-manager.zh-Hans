---
title: 2019.12.0 版发行说明
seo-title: AEM Cloud Manager 2019.12.0发行说明
description: 可查看本页以获取Cloud Manager 2019.12.0版的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2019.12.0版的相关信息。
translation-type: tm+mt
source-git-commit: 0fa1fedccb013e82c8df5838a612ce26a1efb7e8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# 2019.12.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2019.12.0版的一般发行说明，并添加了管道执行更新和代码质量扫描增强功能。
有关更多详细信息，请按照以下部分进行操作。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.12.0的发布日期为2019年12月12日。

## 新增功能 {#whats-new}

* 管道执行中的步骤现在显示每个步骤的完成时间戳。
* 对于不包含Java代码的项目，代码质量扫描现在报告的代码覆盖率为100%。
* 已删除CQ调度程序配置运行状况检查。

## 错误修复 {#bug-fixes}

* 某些浏览器中未正确显示日期。
* 在极少数情况下，在性能测试仍在运行时，生产管道将转向批准步骤。
* 在某些状态下，概述页面顶部区域上的按钮未正确对齐。
* 在某些情况下，未经授权的用户看到一个按钮来开始管道，但该按钮本身不可单击。
* 非生产管线的操作按钮有时会在错误的位置显示。
* 具有granite：排名节点类型的包无法扫描某些质量规则违规。
* 代码质量过程中的某些失败被错误地计为错误。
* 无法为某些拓扑加载监视数据。
