---
title: 2019.10.0 版发行说明
seo-title: AEM Cloud Manager 2019.10.0发行说明
description: 请访问本页以获取Cloud Manager版本2019.10.0的信息。
seo-description: 请参阅本页以获取有关AEM Cloud Manager版本2019.10.0的信息。
feature: 发行信息
exl-id: b58f7a1b-2063-4ac8-b676-bb74200d7ac9
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 5%

---

# 2019.10.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2019.10.0的常规发行说明，并添加了对部署步骤和Maven项目版本处理的更新。
有关更多详细信息，请参阅以下部分。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.10.0的发行日期为2019年10月10日。

## 新增功能 {#whats-new}

* 部署步骤的重要部分性能更高。
* 现在，如果适用，内部版本的Maven项目将在git中包含项目版本。
* 在生成时，可以使用新的环境变量。
* 可以从&#x200B;**Overview**&#x200B;页面和API的卡中删除非生产管道。
* 在暂存部署步骤之后，但在安全测试步骤之前，会立即提供一个新的可选批准步骤。
* 配置CI/CD管道时，可以为开发和暂存环境跳过从负载平衡器分离和附加调度程序实例的步骤。
有关更多详细信息，请参阅**[部署进程](deploying-code.md#deployment-process)**。
* 扩展了Cloud Manager CLI以支持访问执行步骤日志。
* Cloud Manager API现在支持编辑管道的已配置分支。
* 性能测试期间执行的请求现在包含用户代理中的特定令牌&#x200B;***CloudManagerTest***。

## 错误修复 {#bug-fixes}

* **概述**&#x200B;页面上的某些卡未正确垂直对齐。
* 某些失败条件未导致管道执行被正确标记并阻止后续执行。
