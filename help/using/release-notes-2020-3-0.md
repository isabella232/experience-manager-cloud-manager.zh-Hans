---
title: 2020.3.0 版发行说明
seo-title: AEM Cloud Manager 2020.3.0发行说明
description: 可查看本页以获取Cloud Manager 2020.3.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.3.0版的信息
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 51%

---

# 2020.3.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2020.3.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.3.0的发布日期为2020年3月05日。

## 新增功能 {#whats-new}

* 现在，在构建步骤运行时，会提供构建步骤的日志。
* 为清楚起见，管道执行详细信息页面上的某些消息进行了编辑。

## 错误修复 {#bug-fixes}

* 如果部署失败，某些部署配置可能导致部署步骤的日志不可用。
* Managed Services项目的部署步骤中的特定失败可能导致后续执行无法开始。
* 偶尔，构建步骤中使用的临时 SonarQube 实例无法在配置的超时时间内启动。
* 在特定项目中，应始终关闭 *ResourceResolver对象*，这将产生空指针异常；不过，这并不影响管道执行。