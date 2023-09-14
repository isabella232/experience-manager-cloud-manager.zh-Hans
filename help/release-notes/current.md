---
title: 2023.9.0 的发行说明
description: 这些是 Cloud Manager 2023.9.0 版的发行说明。
feature: Release Information
source-git-commit: a3e926fa13d54da1322f3a5219519fae07ddb273
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 52%

---


# Cloud Manager 2023.9.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.9.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.9.0 版的发布日期为 2023 年 9 月 14 日。下一个版本计划于 2023 年 10 月 5 日发布。

## 新增功能 {#what-is-new}

* 此版本仅包含针对Cloud Manager的错误修复。

## 错误修复 {#bug-fixes}

* 删除程序时，还将删除任何关联的正在运行的管道，确保不会将管道错误地指定为失败状态。
* 有时，当管道执行的所有步骤都是“已完成”时，管道的状态会视为“正在运行”，使其似乎处于卡住状态。 它现在被视为“完成”。
* 对于使用代码生成器原型生成的存储库分支，CI/CD管道失败。
