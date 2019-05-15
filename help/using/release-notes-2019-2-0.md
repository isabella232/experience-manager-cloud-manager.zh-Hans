---
title: 2019.2.0发行说明
seo-title: 适用于2019.2.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.2.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.2.0的信息。
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2019.2.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0版本添加了新的系统监视功能。这使客户能够在系统级别查看其Adobe Managed Services环境的状态。


## 发布日期 {#release-date}

版本2019.2.0 [!UICONTROL Cloud Manager] 的发布日期为2019年月21日。

## 新增功能 {#whats-new}

* 新的系统监视功能。请参阅 [监控您的环境](monitor-your-environments.md) 以了解更多信息。
* 向导生成项目中的调度程序模块现在包含一个README文件。
* 已改进代码扫描问题的排序顺序，以匹配优先级。
* 在部署失败时，Stage实例现在始终恢复到负载平衡器。
* Admin Console中提供了新的API开发人员角色，允许特定用户授予在Adobe I/控制台中创建集成的权限。请参阅 [管理开发人员](https://www.adobe.com/go/aac_api_prod_learn) 以了解更多信息。
* 版本的Maven Archetype更新为版本16。
* 版本的Maven更新为3.6.0版。

## 错误修复 {#bug-fixes}

* 在某些情况下，在Azure中托管目标环境时，渠道将不会执行。
* 环境订购不一致。
* 在发现页面路径包含逗号字符时，性能测试可能会失败。
* 从Web UI启动管道执行时，浏览器返回按钮无法正常工作。
* “概述”页面上的“学习更多链接”未打开新选项卡。
* 上传程序缩略图时，可能无法立即看到该缩略图。
* 在某些情况下，由于特定于项目的配置，代码扫描失败。
* “非生产管道”卡上的“了解更多”链接转到了错误的位置。
* 覆盖质量门时，状态显示不一致。
* 使用冷待机拓扑的客户对于安全测试收到错误的结果。
* 使用向导创建新项目时，无法创建包含虚线字符的分支。

## 已知问题 {#known-issues}

* 当监视数据刷新时，隐藏任何隐藏的系列。
* 希望查看现有SLA报表的客户需要手动导航到下一个版本。

   要构建此URL，请遵循模式(`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`)，例如，如果Experience Cloud的URL为(`https://weretailprod.experiencecloud.adobe.com`)，则您的SLA报表URL为(`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`)。

   希望在下一个版本中解决此问题，并在内部提供SLA报告 [!UICONTROL Cloud Manager]。
