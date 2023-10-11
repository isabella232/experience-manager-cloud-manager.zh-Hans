---
title: 2023.10.0 的发行说明
description: 这些是 Cloud Manager 2023.10.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 851364e74864c28b3bcd9285dfbe06ddb530eb10
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 77%

---


# Cloud Manager 2023.10.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.10.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.10.0 版的发布日期为 2023 年 10 月 5 日。下一个版本计划于 2023 年 11 月 2 日发布。

## 新增功能 {#what-is-new}

* **部署经理**&#x200B;角色可以[配置一组内容路径，在运行非生产管道时将使这些路径失效或从 AEM Dispatcher 缓存中刷新这些路径。](/help/using/non-production-pipelines.md)
   * 就在部署任何内容包之后，将作为部署管道步骤的一部分执行这些缓存操作。
   * 这些设置使用标准 AEM Dispatcher 行为。
* 随着 2023 年 10 月发布 Cloud Manager，将通过分阶段推出的方式更新 Java 版本。
   * Java 8和11以及Maven的次要版本已更新，并将在未来2个月内分阶段推出。 新版本包含多个安全修复和错误修复。 新版本包括：
   * *Maven： 3.8.8*
   * *Java 8版本： /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11版本： /usr/lib/jvm/jdk-11.0.20*
   * 有关这些 JDK 更新中的安全性和错误修复的详细信息，[请参阅 OpenJDK 公告](https://openjdk.org/groups/vulnerability/advisories/)。
