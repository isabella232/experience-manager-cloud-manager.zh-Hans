---
title: 2019.9.0 版发行说明
seo-title: AEM Cloud Manager 2019.9.0发行说明
description: 可查看本页以获取Cloud Manager 2019.9.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.9.0版的信息。
feature: 发行信息
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 2019.9.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版本更新了安全测试标准，添加了可下载的监控图形，并修复了客户报告的一些可用性问题。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.9.0的发布日期为2019年9月12日。

## 新增功能 {#whats-new}

* Sling推荐人过滤器运行状况检查的分类已从“关键”更改为“重要”。
* HTML库管理器配置运行状况检查的分类已从“关键”更改为“重要”。
* 现在可以下载监视图形。 有关详细信息，请参阅[监视环境](monitor-your-environments.md)。
* 如果项目没有生产AEM环境，则单击登陆页中的项目卡将导航到Cloud Manager概述页面，而不会生成错误对话框。
* **概述**&#x200B;页面上的&#x200B;**管道设置**&#x200B;卡已重新命名为&#x200B;**生产管道设置**。
* “重要故障行为”单选按钮已从仅代码质量的管道中删除。
* 现在，**活动**&#x200B;页显示每个执行的管道名称。
* 执行页面现在显示管道的名称。
* “代码质量”摘要对话框现在显示每个评级的说明。

## 错误修复 {#bug-fixes}

* 某些用户在等待批准时无法视图执行详细信息。
* 在&#x200B;**概述**&#x200B;页面上，右边距不一致。
* 生成容器可能会在大型项目中内存不足。
* 在某些情况下，UnbandedPaths OakPAL规则未识别/libs下的安装内容。
* 当质量门被拒绝时，对话框标题仍显示&#x200B;*部分传递*。

## 已知问题 {#known-issues}

* Safari中不提供监视图形的下载。
