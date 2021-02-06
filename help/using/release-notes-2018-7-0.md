---
title: 2018.7.0 版发行说明
seo-title: 2018.7.0 版发行说明
description: 'null'
seo-description: 可查看本页以获取Cloud Manager Release 2018.7.0的相关信息。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
translation-type: tm+mt
source-git-commit: ace032fbb26235d87d61552a11996ec2bb42abce
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 5%

---


# 2018.7.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2018.7.0版本，它提供&#x200B;*自动缩放*&#x200B;功能。

**通** 过在生产环境上对段进行水 `Dispatcher/Publish` 平缩放来启用自动缩放，以支持负载、卷、访问和其他定义的监视指标的突然增加。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.7.0的发布日期为2018年9月10日。

## 新增功能 {#what-s-new}

* **配置** - [!UICONTROL Cloud Manager] 现在可以通过水平扩展调度程序／发布区段，在客户项目上自动缩放生产环境。UI中的新增功能是项目设置中的“设置”部分，如果在客户项目上启用自动缩放，则显示该部分。 请参阅[设置项目](setting-up-program.md)以了解更多信息。

* **环境** -现在可以查看生产和阶段环境的详细视图以及与每个环境关联的节点的大小、存储、区域和状态。请参阅[管理环境](manage-your-environment.md)以了解更多信息。

* **代码质量分析** -用于识别错误API使用的新规则。请参阅[自定义代码质量规则](custom-code-quality-rules.md)以了解更多信息。

* **性能测试** -在查看性能测试结果时，可以使用CPU利用率、磁盘I/O等待时间、页错误率、磁盘带宽利用率、网络带宽利用率、峰值页面响应时间和第95百分点页面响应时间等图表。请参阅[了解测试结果](understand-your-test-results.md)页上的&#x200B;*性能测试*&#x200B;一节。

* **性能测试** -查看性能测试结果时，可下载页面错误和慢速请求的列表。请参阅[了解测试结果](understand-your-test-results.md)页上的&#x200B;*性能测试*&#x200B;一节。

## 错误修复 {#bug-fixes}

* 在某些情况下，内部系统同步失败，导致视图不一致。
* 在某些情况下，手动管线触发器未自动选择，从而导致表单验证问题。
* 特定客户构建脚本可能在基于插件不兼容性的构建步骤中导致失败。

## 已知问题 {#known-issues}

* 尽管客户能够选择提交触发器，但管道可能并不实际基于新提交进行开始。
* [!UICONTROL Experience Cloud]通知提要栏可能无法一致加载通知。 但是，通知在[!UICONTROL Experience Cloud]中可见，如果配置，仍将通过电子邮件发送。

