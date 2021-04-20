---
title: 2019.10.0 版发行说明
seo-title: AEM Cloud Manager 2019.10.0发行说明
description: 可查看本页以获取Cloud Manager 2019.10.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.10.0版的信息。
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 5%

---

# 2019.10.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2019.10.0版的一般发行说明，并为部署步骤添加了更新并实现了对项目版本的处理。
有关更多详细信息，请参阅以下各节。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.10.0的发布日期为2019年10月10日。

## 新增功能 {#whats-new}

* 部署步骤中的大部分都提高了性能。
* 在适当时，内部版本Maven项目的版本现在将以git格式并入项目版本。
* 在构建时，有新的环境变量可用。
* 可从&#x200B;**概述**&#x200B;页面和API上的卡中删除非生产管道。
* 在阶段部署步骤之后，但在安全测试步骤之前，会立即有一个新的可选批准步骤。
* 配置CI/CD管道时，可以跳过从负载平衡器分离和附加调度程序实例，以用于开发和舞台环境。
有关详细信息，请参阅**[部署进程](deploying-code.md#deployment-process)**。
* Cloud Manager CLI已得到扩展，支持访问执行步骤日志。
* Cloud Manager API现在支持编辑管道的已配置分支。
* 性能测试期间执行的请求现在在用户代理中包含特定令牌&#x200B;***CloudManagerTest***。

## 错误修复 {#bug-fixes}

* **概述**&#x200B;页面上的某些卡未正确垂直对齐。
* 某些故障情况未导致管道执行被正确标记，并阻止后续执行。
