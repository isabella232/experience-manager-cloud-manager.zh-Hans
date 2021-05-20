---
title: 2018.7.0 版发行说明
seo-title: 2018.7.0 版发行说明
description: 了解Cloud Manager 2018.7.0版
seo-description: 可查看本页面以获取有关Cloud Manager 2018.7.0版的信息。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
feature: 发行信息
exl-id: fc0214b4-d138-470a-9b04-191224927f7b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 5%

---

# 2018.7.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2018.7.0版本，该版本提供了&#x200B;*autoscaling*&#x200B;功能。

**** 通过在生产环境中横向扩展区段来 `Dispatcher/Publish` 启用自动缩放，以支持负载、卷、访问和其他定义的受监控量度的突然增加。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.7.0的发行日期是2018年9月10日。

## 新增功能 {#what-s-new}

* **配置**  -  [!UICONTROL Cloud Manager] 现在能够通过使用调度程序/发布区段水平扩展来自动缩放客户程序上的生产环境。UI中的新增功能是“程序设置”中的“设置”部分，如果客户程序上启用了自动缩放，则将显示该部分。 请参阅[设置程序](setting-up-program.md)以了解详情。

* **环境**  — 现在，可以查看生产和暂存环境的详细视图，以及与每个环境关联的节点的大小、存储、区域和状态。请参阅[管理环境](manage-your-environment.md)以了解更多信息。

* **代码质量分析**  — 用于识别错误API使用情况的新规则。请参阅[自定义代码质量规则](custom-code-quality-rules.md)以了解更多信息。

* **性能测试**  — 在查看性能测试结果时，可以使用CPU利用率、磁盘I/O等待时间、页错误率、磁盘带宽利用率、网络带宽利用率、峰值页面响应时间和第95个百分位数页面响应时间的图表。请参阅[了解测试结果](understand-your-test-results.md)页面上的&#x200B;*性能测试*&#x200B;部分。

* **性能测试**  — 在查看性能测试结果时，可以下载页面错误和慢速请求的列表。请参阅[了解测试结果](understand-your-test-results.md)页面上的&#x200B;*性能测试*&#x200B;部分。

## 错误修复 {#bug-fixes}

* 在某些情况下，内部系统同步失败，导致数据视图不一致。
* 在某些情况下，未自动选择手动管道触发器，从而导致表单验证问题。
* 基于插件不兼容性的特定客户构建脚本在构建步骤期间可能会导致失败。

## 已知问题 {#known-issues}

* 尽管客户能够选择提交触发器，但管道实际上可能不会基于新提交启动。
* [!UICONTROL Experience Cloud]通知侧栏可能无法始终如一地加载通知。 但是，通知在[!UICONTROL Experience Cloud]中可见，如果配置，仍将通过电子邮件发送。
