---
title: 2019.2.0 版发行说明
seo-title: AEM Cloud Manager 2019.2.0发行说明
description: 可查看本页以获取Cloud Manager 2019.2.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.2.0版的信息。
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 4%

---


# 2019.2.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0版本新增了系统监视功能。 这允许客户在系统级别视图其Adobe Managed Services环境的状态。


## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.2.0的发布日期为2019年2月21日。

## 新增功能 {#whats-new}

* 新增系统监视功能。 请参阅[监视您的环境](monitor-your-environments.md)以了解更多信息。
* 向导生成的项目中的调度程序模块现在包含一个README文件。
* 代码扫描问题的排序已改进，以匹配问题优先级。
* 现在，舞台实例始终恢复到负载平衡器，即使在部署失败时也是如此。
* Admin Console中提供了新的API开发人员角色，允许特定用户获得在Adobe I/O控制台中创建集成的权限。 请参阅[管理开发人员](https://www.adobe.com/go/aac_api_prod_learn)以了解更多信息。
* Maven Archetype的版本已更新为版本16。
* Maven的版本已更新至版本3.6.0。

## 错误修复 {#bug-fixes}

* 在某些情况下，当目标环境在Azure中托管时，管道将不执行。
* 环境的排序不一致。
* 当发现的页面路径包含逗号字符时，性能测试可能会失败。
* 从Web UI启动管道执行时，浏览器后退按钮无法正确工作。
* “概述”页面上的“了解更多”链接未打开新选项卡。
* 上传项目缩略图时，它可能尚未立即可见。
* 在某些情况下，代码扫描失败，因为项目特定配置。
* 非生产管道卡上的“了解更多”链接转到错误位置。
* 当质量门被覆盖时，状态显示不一致。
* 使用冷备用拓扑的客户在安全测试中收到错误结果。
* 使用向导创建新项目时，无法创建包含虚线字符的分支。

## 已知问题 {#known-issues}

* 刷新监视数据时，任何隐藏的系列都将取消隐藏。
* 希望视图其现有SLA报告的客户需要手动导航到下一版本。

   要建立此URL，请遵循模式(`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`)，例如，如果Experience Cloud的URL为(`https://weretailprod.experiencecloud.adobe.com`)，则您的SLA报告URL为(`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`)。

   在下一版本中，预计将通过[!UICONTROL Cloud Manager]内的SLA报告来解决此问题。
