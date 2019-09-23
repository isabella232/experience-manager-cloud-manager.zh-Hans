---
title: 2018.7.0发行说明
seo-title: 2018.7.0发行说明
description: 'null'
seo-description: 可查看本页以获取Cloud Manager 2018.7.0版的相关信息。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: 发行说明
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
translation-type: tm+mt
source-git-commit: b78c29520414726ad2bbf86e5b7f8e65710c7f75

---


# 2018.7.0发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 2018.7.0版本，它提供了自动缩 *放功能* 。

**通过在生产环境中对段进行水平缩小**`Dispatcher/Publish` ，可以启用自动缩放，以支持负载、卷、访问和其他定义的监控指标的突然增加。

## 发布日期 {#release-date}

版本2018.7.0 [!UICONTROL Cloud Manager] 的发布日期为2018年9月10日。

## 新增功能 {#what-s-new}

* **配置** - [!UICONTROL Cloud Manager] 现在可以通过水平缩小调度程序／发布区段来自动缩放客户程序上的生产环境。 UI中的新增功能是程序设置中的“配置”部分，如果客户程序启用了自动缩放功能，将显示该部分。 请参阅设置 [您的计划](setting-up-program.md) ，了解更多信息。

* **环境** -现在可以详细查看生产和舞台环境以及与每个环境关联的节点的大小、存储、区域和状态。 请参阅管 [理环境](manage-your-environment.md) ，了解更多信息。

* **代码质量分析** -用于识别错误API使用的新规则。 请参阅自定 [义代码质量规则](custom-code-quality-rules.md) ，了解更多信息。

* **性能测试** -查看性能测试结果时，可使用CPU利用率、磁盘I/O等待时间、页面错误率、磁盘带宽利用率、网络带宽利用率、峰值页面响应时间和第95百分位页响应时间的图表。 请参阅“了解测试结果”页上的“* [性能测试*”部分](understand-your-test-results.md) 。

* **性能测试** -查看性能测试结果时，可下载页面错误和慢速请求列表。 请参阅“了解测试结果”页上的“* [性能测试*”部分](understand-your-test-results.md) 。

## 错误修复 {#bug-fixes}

* 在某些情况下，内部系统同步会失败，导致数据视图不一致。
* 在某些情况下，手动管线触发器未自动选择，从而导致表单验证问题。
* 特定客户构建脚本可能会在基于插件不兼容性的构建步骤中导致失败。

## 已知问题 {#known-issues}

* 尽管客户能够选择提交触发器，但管道可能并不实际基于新提交开始。
* 通知 [!UICONTROL Experience Cloud] 提要栏可能不会一致地加载通知。 但是，通知会显示在中， [!UICONTROL Experience Cloud] 并且如果配置，仍将通过电子邮件发送。

