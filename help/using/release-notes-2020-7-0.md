---
title: 2020.7.0 版发行说明
seo-title: AEM Cloud Manager 2020.7.0发行说明
description: 可查看本页面以获取Cloud Manager 2020.7.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.7.0版的信息
feature: 发行信息
exl-id: c0272d9d-0a6d-4abd-add1-f82280b7ecec
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 52%

---

# 2020.7.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2020.7.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.7.0的发行日期是2020年7月9日。

## 新增功能 {#whats-new}

* 现在，在生产部署期间从负载平衡器分离和附加调度程序实例的工作方式更加一致。

* Cloud Manager 内部版本容器现在同时支持 Java 8 和 Java 11。

* Cloud Manager 管道现在支持由客户设置的变量和密钥。
有关更多详细信息，请参阅[管道变量](/help/using/build-environment-details.md#pipeline-variables)。

## 错误修复 {#bug-fixes}

* 非生产管道编辑页面上的&#x200B;**取消**&#x200B;和&#x200B;**保存**&#x200B;选项并非始终可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

## 已知问题 {#known-issues}

* 当AMS环境包含备用实例时，记录的消息会声明该实例已关闭，而不是处于备用模式。

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;_最低_&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户将在代码质量控制过程中收到一条错误消息。
