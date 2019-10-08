---
title: 2019.9.0发行说明
seo-title: AEM Cloud Manager 2019.9.0版本说明
description: 可查看本页以获取Cloud Manager 2019.9.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.9.0版的信息。
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c

---

# 2019.9.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 9.0版本更新了安全测试标准，添加了可下载的监视图形，并修复了客户报告的一些可用性问题。

## 发布日期 {#release-date}

版本2019.9.0 [!UICONTROL Cloud Manager] 的发布日期为2019年9月12日。

## 新增功能 {#whats-new}

* Sling Referrer过滤器运行状况检查的分类已从“关键”更改为“重要”。
* HTML库管理器配置运行状况检查的分类已从“关键”更改为“重要”。
* 现在可以下载监视图形。 有关更多详细信息， [请参阅监视您的环境](monitor-your-environments.md) 。
* 如果某个程序没有生产AEM环境，则单击登录页面中的程序卡将导航到Cloud manager概述页面，而不会生成错误对话框。
* “概 **述”(Overview** )页面上的“管线设 **置卡”(Pipeline Settings** Card)已被标题为“生产管 **线设置”(Production Pipeline Settings**)。
* “重要故障行为”单选按钮已从仅代码质量的管道中删除。
* “活 **动** ”页面现在显示每个执行的管道名称。
* 执行页面现在显示管道的名称。
* “代码质量”摘要对话框现在显示每个评级的说明。

## 错误修复 {#bug-fixes}

* 某些用户在等待批准时无法查看执行详细信息。
* 在“ **概述** ”页面上，右边距不一致。
* 构建容器可能会在大型项目中内存不足。
* 在某些情况下，UnbardPaths OakPAL规则未在/libs下识别已安装的内容。
* 拒绝质量门时，对话框标题仍显示“部 *分通过”*。

## 已知问题 {#known-issues}

* Safari中不提供监视图形的下载。
