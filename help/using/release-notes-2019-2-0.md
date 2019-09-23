---
title: 2019.2.0发行说明
seo-title: AEM Cloud Manager 2019.2.0版本说明
description: 可查看本页以获取Cloud Manager 2019.2.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.2.0版的信息。
translation-type: tm+mt
source-git-commit: 98395c4413b1b6bfbb3a565388ffa32dc3880dff

---


# 2019.2.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 2.0版本新增了系统监视功能。 这使客户能够在系统级别查看其Adobe Managed services环境的状态。


## 发布日期 {#release-date}

版本2019.2.0 [!UICONTROL Cloud Manager] 的发布日期为2019年2月21日。

## 新增功能 {#whats-new}

* 新增的系统监视功能。 请参阅监 [视您的环境](monitor-your-environments.md) ，了解更多信息。
* 向导生成的项目中的调度程序模块现在包含一个README文件。
* 代码扫描问题的排序顺序已改进，以匹配问题优先级。
* 现在，舞台实例始终恢复到负载平衡器，即使在部署失败时也是如此。
* Admin Console中提供了新的API开发人员角色，该角色允许特定用户获得在Adobe I/O控制台中创建集成的权限。 请参阅管 [理开发人员](https://www.adobe.com/go/aac_api_prod_learn) ，了解更多信息。
* Maven Archetype的版本已更新至版本16。
* Maven的版本已更新至版本3.6.0。

## 错误修复 {#bug-fixes}

* 在某些情况下，当目标环境托管在Azure中时，管道将不会执行。
* 环境排序不一致。
* 当发现的页面路径包含逗号字符时，性能测试可能会失败。
* 从Web UI启动管道执行时，浏览器返回按钮无法正常工作。
* “概述”页面上的“了解更多”链接未打开新选项卡。
* 上传程序缩略图时，它可能尚未立即可见。
* 在某些情况下，代码扫描因项目特定配置而失败。
* “非生产管道”卡上的“了解更多”链接转到错误的位置。
* 当质量门被覆盖时，状态显示不一致。
* 使用冷待机拓扑的客户收到的安全测试结果不正确。
* 使用向导创建新项目时，无法创建包含虚线字符的分支。

## 已知问题 {#known-issues}

* When monitoring data is refreshed, any hidden series are unhidden.
* Customers wishing to view their existing SLA reports will need to manually navigate until the next release.

   To formulate this URL, follow the pattern (), for example, if URL for your Experience Cloud is (), then your SLA reports URL is ().`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html``https://weretailprod.experiencecloud.adobe.com``https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`

   This is expected to be resolved in the next release with the availability of SLA reports inside [!UICONTROL Cloud Manager].
