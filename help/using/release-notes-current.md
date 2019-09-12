---
title: 2019.9.0发行说明
seo-title: 适用于2019.9.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.9.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.9.0的信息。
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---

# 2019.9.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版增加了Sling Referrer Filter Health检查和监控图表的更新。

## 发布日期 {#release-date}

版本2019.9.0 [!UICONTROL Cloud Manager] 的发布日期为2019年月11日。

## 新增功能 {#whats-new}

* Sling Referrer Filter Health检查的分类已从关键更改为重要。
* HTML库管理器配置健康检查的分类已从关键更改为重要。
* 现在可以下载监视图。有关更多详细信息，请参阅 [监视您的环境](monitor-your-environments.md) 。
* 如果某个程序没有生产AEM环境，则从登陆页面单击该程序卡将导航到Cloud Manager概述页面，而不会生成错误对话框。
* 概述页面上的渠道设置卡已被弃用至 **生产管道设置**。
* 重要的故障行为单选按钮已从仅代码质量的渠道中删除。
* 活动页面现在显示每个执行的渠道名称。
* 执行页面现在显示渠道的名称。
* “代码质量”摘要对话框现在显示每个评级的描述。

## 错误修复 {#bug-fixes}

* 某些用户在等待批准时无法查看执行详细信息。
* 在概述页面上，右边距不一致。
* 在大型项目中，构建容器可能内存不足。
* 在某些情况下，BannedPath OkPAL规则未在/libs下识别已安装的内容。
* 当质量门被拒绝时，对话框标题仍显示“部分传递”。

## 已知问题 {#known-issues}

在Safari中无法下载监视图。
