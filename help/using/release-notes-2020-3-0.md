---
title: 2020.3.0 版发行说明
seo-title: AEM Cloud Manager 2020.3.0版本说明
description: 可查看本页以获取Cloud Manager 2020.3.0版的相关信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.3.0版的相关信息
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# 2020.3.0 版发行说明 {#release-notes-for}

以下部分概述了2020.3.0版 [!UICONTROL Cloud Manager] 的一般发行说明。

## Release Date {#release-date}

版本2020.3.0 [!UICONTROL Cloud Manager] 的发布日期为2020年3月5日。

## 新增功能 {#whats-new}

* 现在，在构建步骤运行时，会提供构建步骤的日志。
* 为清楚起见，管道执行详细信息页面上的某些消息进行了编辑。

## 错误修复 {#bug-fixes}

* 如果部署失败，某些部署配置可能导致部署步骤的日志不可用。
* 托管服务项目的部署步骤中的特定失败可能导致后续执行无法开始。
* 偶尔，构建步骤中使用的临时 SonarQube 实例无法在配置的超时时间内启动。
* 在特定项目中，应始终关闭 *ResourceResolver对象*，这将产生空指针异常；不过，这并不影响管道执行。