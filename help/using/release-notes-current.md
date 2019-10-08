---
title: 2019.10.0发行说明
seo-title: AEM Cloud Manager 2019.10.0版本说明
description: 可查看本页以获取Cloud Manager 2019.10.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.10.0版的信息。
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c

---

# 2019.10.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 10.0版本更新了安全测试标准，添加了可下载的监控图形，并修复了客户报告的一些可用性问题。

## 发布日期 {#release-date}

版本2019.10.0 [!UICONTROL Cloud Manager] 的发布日期为2019年10月12日。

## 新增功能 {#whats-new}

* 部署步骤中的重要部分提高了性能。
* 如果适用，内部版本Maven项目的版本现在将以git的形式并入项目版本。
* 在构建时，新的环境变量可用。
* 非生产管道可以从概述页面上的卡以及API中删除。
* 在阶段部署步骤之后，但在安全测试步骤之前，会立即出现一个新的可选批准步骤。
* 在配置CI/CD管道时，可以跳过从负载平衡器分离和附加调度程序实例，以用于开发和舞台环境。
* Cloud Manager CLI已得到扩展，可支持访问执行步骤日志。
* Cloud Manager API现在支持编辑管道的已配置分支。
* 性能测试期间执行的请求现在在用户代理中包含特定令牌(“CloudManagerTest”)。

## 错误修复 {#bug-fixes}

* “概述”页面上的某些卡未正确垂直对齐。
* 某些故障情况未导致管道执行被正确标记并阻止后续执行。
