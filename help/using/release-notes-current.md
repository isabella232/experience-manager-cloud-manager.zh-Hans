---
title: 2020.7.0 版发行说明
seo-title: AEM Cloud Manager 2020.7.0版本说明
description: 可查看本页以获取Cloud Manager Release 2020.7.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager Release 2020.7.0的相关信息
translation-type: tm+mt
source-git-commit: 26492dc02371d21670778f3cd60d26146439548e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---

# 2020.7.0 版发行说明 {#release-notes-for}

以下部分概述了2020.7.0 [!UICONTROL Cloud Manager] 版的一般发行说明。

## 发布日期 {#release-date}

版本2020.6.0 [!UICONTROL Cloud Manager] 的发布日期为2020年7月9日。

## 新增功能 {#whats-new}

* 现在，在生产部署过程中从负载平衡器分离和附加调度程序实例可以以更一致的方式工作。

* Cloud Manager构建容器现在支持Java 8和Java 11。

* Cloud Manager管道现在支持客户集变量和秘密。

## 错误修复 {#bug-fixes}

* “非 **生** 产管道编 **辑”(Non-Production Pipeline** Edit)页面上的“取消”(Cancel)和“保存”(Save)选项并不总是可见。

* 代码质量过程中的某些失败可能导致日志文件无法正确生成。

* 无法通过用户界面一致地下载某些大型管道步骤日志。

## 已知问题 {#known-issues}

* 当AMS环境包含待机实例时，已记录的消息会声明该实例已关闭，而不是处于待机模式。
