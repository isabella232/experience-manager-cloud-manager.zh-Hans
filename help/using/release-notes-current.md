---
title: 2020.3.0 版发行说明
seo-title: AEM Cloud Manager 2020.3.0版本说明
description: 可查看本页以获取Cloud Manager 2020.3.0版的相关信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.3.0版的相关信息
translation-type: tm+mt
source-git-commit: 44671d89edad0ccb6ded998b62beb5fa012678e9

---

# 2020.3.0 版发行说明 {#release-notes-for}

以下部分概述了2020.3.0版 [!UICONTROL Cloud Manager] 的一般发行说明。

## Release Date {#release-date}

版本2020.3.0 [!UICONTROL Cloud Manager] 的发布日期为2020年3月5日。

## 新增功能 {#whats-new}

* 构建步骤运行时，构建步骤的日志现在可用。
* 管道执行详细信息页面上的某些消息已经编辑，以便清晰明了。

## 错误修复 {#bug-fixes}

* 如果部署失败，某些部署配置可能导致部署步骤的日志不可用。
* Managed Services程序部署步骤中的特定失败可能导致后续执行无法启动。
* 构建步骤中使用的短暂SonarQube实例在配置的超时内偶尔无法启动。
* 在特定项目中， *应始终关闭ResourceResolver对象* ，将产生空指针异常；然而，这并不影响管道执行。


