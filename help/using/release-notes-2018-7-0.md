---
title: 2018.7.0发行说明
seo-title: 2018.7.0发行说明
description: 'null'
seo-description: 请参阅本页获取Cloud Manager版本2018.7.0的信息。
uuid: d7b49e32-01dc-48ce-b744-e6 a806 fbdd8 a
contentOwner: jsyal
topic-tags: release-notes
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73 d34094 f1 b
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.7.0发行说明 {#release-notes-for}

以下部分概述了提供 [!UICONTROL Cloud Manager]*自动缩放* 功能的2018.7.0版本。

**自动缩放** 是通过在生产环境中对 `Dispatcher/Publish` 区段进行水平缩小来支持负载、体积、访问和其他定义的监视指标突然增加的。

## 发布日期 {#release-date}

版本2018.7.0 [!UICONTROL Cloud Manager] 的发布日期为2018年月10日。

## 新增功能 {#what-s-new}

* **配置** -现在 [!UICONTROL Cloud Manager] 可以通过使用调度程序/发布区段水平缩小，自动缩放客户计划上的生产环境。UI中新增的“配置”部分是计划设置中的“配置”部分，如果客户程序启用了自动缩放功能，则该部分将显示。请参阅 [设置您的计划](setting-up-program.md) 以了解更多信息。

* **环境** -现在可以查看生产和舞台环境的详细视图以及与每个环境关联的节点的大小、存储、区域和状态。请参阅 [管理您的环境](manage-your-environment.md) 以了解更多信息。

* **代码质量分析** -用于识别错误API使用情况的新规则。请参阅 [自定义代码质量规则](custom-code-quality-rules.md) 以了解更多信息。

* **性能测试** -在查看性能测试结果的同时，CPU利用率、磁盘I/等待时间、页面错误率、磁盘带宽利用率、网络带宽利用率、峰值页面响应时间和第95个百分点页面响应时间都可用。请参阅 [“了解测试结果](understand-your-test-results.md) ”页面上的* Performance Testing*部分。

* **性能测试** -查看性能测试结果时，可以下载页面错误和慢速请求列表。请参阅 [“了解测试结果](understand-your-test-results.md) ”页面上的* Performance Testing*部分。

## 错误修复 {#bug-fixes}

* 在某些情况下，内部系统同步不适当，导致数据视图不一致。
* 在某些情况下，手动管道触发器不会自动被选中，导致表单验证问题。
* 特定客户构建脚本可能会在基于插件的构建步骤中导致失败。

## 已知问题 {#known-issues}

* 尽管客户能够选择提交触发器，但渠道实际上并不基于新的提交。
* [!UICONTROL Experience Cloud] 通知提要栏不能一致地加载通知。但是，通知在中可见，如果配置， [!UICONTROL Experience Cloud] 仍将通过电子邮件发送。

