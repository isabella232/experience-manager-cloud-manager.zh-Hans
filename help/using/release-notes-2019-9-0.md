---
title: 2019.9.0 版发行说明
seo-title: AEM Cloud Manager 2019.9.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2019.9.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.9.0版的信息。
feature: 发行信息
exl-id: 0aaf969a-f4f9-441b-8b17-7ac2f9b9ad50
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 2019.9.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版本更新了安全测试标准，添加了可下载的监控图表，并修复了一些客户报告的可用性问题。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.9.0的发行日期是2019年9月12日。

## 新增功能 {#whats-new}

* Sling反向链接过滤器运行状况检查的分类已从“关键”更改为“重要”。
* HTML库管理器配置运行状况检查的分类已从“关键”更改为“重要”。
* 现在可以下载监控图表。 有关更多详细信息，请参阅[监视环境](monitor-your-environments.md) 。
* 如果某个程序没有生产AEM环境，则单击登陆页面中的程序卡将导航到Cloud Manager概述页面，而不会生成错误对话框。
* **概述**&#x200B;页面上的&#x200B;**管道设置**&#x200B;卡片已命名为&#x200B;**生产管道设置**。
* “重要失败行为”(Important Failure Behavior)单选按钮已从仅代码质量管道中删除。
* 现在， **Activity**&#x200B;页面会显示每次执行的管道名称。
* 现在，执行页面会显示管道的名称。
* “代码质量”摘要对话框现在显示每个评级的描述。

## 错误修复 {#bug-fixes}

* 某些用户在等待批准时无法查看执行详细信息。
* 在&#x200B;**概述**&#x200B;页面上，右边距不一致。
* 大型项目中的生成容器可能内存不足。
* 在某些情况下， UnbandedPaths OakPAL规则未识别/libs下的已安装内容。
* 当质量门被拒绝时，对话框标题仍显示&#x200B;*部分传递*。

## 已知问题 {#known-issues}

* Safari中无法下载监控图表。
