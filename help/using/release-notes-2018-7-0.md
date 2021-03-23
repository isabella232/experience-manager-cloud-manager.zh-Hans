---
title: 2018.7.0 版发行说明
seo-title: 2018.7.0 版发行说明
description: 了解Cloud Manager 2018.7.0版
seo-description: 可查看本页以获取Cloud Manager 2018.7.0版的信息。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
feature: 发行信息
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 5%

---


# 2018.7.0 版发行说明 {#release-notes-for}

以下部分概述了提供&#x200B;*自动缩放*&#x200B;功能的[!UICONTROL Cloud Manager] 2018.7.0版本。

**通** 过生产环境上段的水平缩 `Dispatcher/Publish` 减来启用自动缩放，以支持负载、卷、访问和其他定义的监控指标的突然增加。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.7.0的发布日期为2018年9月10日。

## 新增功能 {#what-s-new}

* **配置**  — 现 [!UICONTROL Cloud Manager] 在将能够通过水平扩展Dispatcher/Publish区段，在客户项目上自动缩放生产环境。UI中的新增功能是项目设置中的“设置”部分，如果在客户项目上启用自动缩放，将显示该部分。 请参阅[设置您的项目](setting-up-program.md)以了解更多信息。

* **环境**  — 现在可以查看生产和阶段环境的详细视图，以及与每个环境关联的节点的大小、存储、区域和状态。请参阅[管理环境](manage-your-environment.md)以了解更多信息。

* **代码质量分析**  — 用于识别错误API使用的新规则。请参阅[自定义代码质量规则](custom-code-quality-rules.md)以了解更多信息。

* **性能测试**  — 查看性能测试结果时，可以使用CPU利用率、磁盘I/O等待时间、页错误率、磁盘带宽利用率、网络带宽利用率、峰值页面响应时间和第95百分位页响应时间的图表。请参阅[了解测试结果](understand-your-test-results.md)页上的&#x200B;*性能测试*&#x200B;部分。

* **性能测试**  — 查看性能测试结果时，可以下载页面错误和慢速请求的列表。请参阅[了解测试结果](understand-your-test-results.md)页上的&#x200B;*性能测试*&#x200B;部分。

## 错误修复 {#bug-fixes}

* 在某些情况下，内部系统同步会失败，导致数据视图不一致。
* 在某些情况下，手动管线触发器未自动选择，导致表单验证问题。
* 基于插件不兼容性，特定客户构建脚本在构建步骤中可能导致失败。

## 已知问题 {#known-issues}

* 尽管客户能够选择提交触发器，但管道可能并不实际基于新提交进行开始。
* [!UICONTROL Experience Cloud]通知提要栏可能不会一致地加载通知。 但是，通知在[!UICONTROL Experience Cloud]中可见，如果配置，仍将通过电子邮件发送。

