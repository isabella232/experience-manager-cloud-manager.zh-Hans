---
title: 2019.12.0 版发行说明
seo-title: AEM Cloud Manager 2019.12.0版本说明
description: 可查看本页以获取Cloud Manager 2019.12.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.12.0版的信息。
translation-type: tm+mt
source-git-commit: a96500b57c980d31d3a70341d8be7b92ae73a1c5

---

# 2019.12.0 版发行说明 {#release-notes-for}

下节概述了2019.12.0版的一般发行说明，并添加了管道执行更新和代码质量扫描增强功能。 [!UICONTROL Cloud Manager] 
有关更多详细信息，请按照以下部分进行操作。

## Release Date {#release-date}

版本2019.12.0 [!UICONTROL Cloud Manager] 的发布日期为2019年12月12日。

## 新增功能 {#whats-new}

* 管道执行中的步骤现在显示每个步骤的完成时间戳。
* 对于不包含Java代码的项目，代码质量扫描现在报告100%的代码覆盖率。
* CQ调度程序配置运行状况检查已被删除。


## 错误修复 {#bug-fixes}

* 某些浏览器中未正确显示日期。
* 在少数情况下，在性能测试仍在运行时，生产管道将转到批准步骤。
* 在某些状态下，概述页面顶部区域上的按钮未正确对齐。
* 在某些情况下，未经授权的用户看到一个按钮以启动管道，但该按钮本身不可单击。
* 非生产管道的操作按钮有时会显示在错误的位置。
* 具有granite的包：无法扫描排名节点类型是否存在某些质量规则违规。
* 代码质量过程中的某些失败被错误地计为错误。
* 无法为某些拓扑加载监视数据。
