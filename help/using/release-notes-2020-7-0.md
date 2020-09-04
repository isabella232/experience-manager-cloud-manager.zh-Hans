---
title: 2020.7.0 版发行说明
seo-title: AEM Cloud Manager 2020.7.0发行说明
description: 可查看本页以获取Cloud Manager Release 2020.7.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.7.0版的相关信息
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 51%

---

# 2020.7.0 版发行说明 {#release-notes-for}

以下部分概述了2020.7.0 [!UICONTROL Cloud Manager] 版的一般发行说明。

## 发布日期 {#release-date}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.7.0 is July 09, 2020.

## 新增功能 {#whats-new}

* 现在，在生产部署过程中从负载平衡器分离和附加调度程序实例可以以更一致的方式工作。

* Cloud Manager 内部版本容器现在同时支持 Java 8 和 Java 11。

* Cloud Manager 管道现在支持由客户设置的变量和密钥。
有关更多详细信息，请参阅[管道变量](/help/using/build-environment-details.md#pipeline-variables)。

## 错误修复 {#bug-fixes}

* The **Cancel** and **Save** options on the Non-Production Pipeline Edit page were not always visible.

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

## 已知问题 {#known-issues}

* 当AMS环境包含待机实例时，已记录的消息会声明该实例已关闭，而不是处于待机模式。

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;_最低_&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户将在代码质量控制过程中收到一条错误消息。
