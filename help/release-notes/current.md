---
title: 2023.9.0 的发行说明
description: 这些是 Cloud Manager 2023.9.0 版的发行说明。
feature: Release Information
source-git-commit: f15a4b739150ee40b6dc48de0fbc20859093c79c
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 57%

---


# Cloud Manager 2023.9.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.9.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.9.0 版的发布日期为 2023 年 9 月 14 日。下一个版本计划于 2023 年 10 月 5 日发布。

## 错误修复 {#bug-fixes}

* 现在，删除程序时，任何关联的正在运行的管道也会被删除。
* 已修复偶尔出现的错误，其中管道执行的所有步骤均标记为已完成，但管道的状态仍在运行，看起来像是卡住状态。
* 当存储库分支的CI/CD管道生成原型失败时，已更正错误。
