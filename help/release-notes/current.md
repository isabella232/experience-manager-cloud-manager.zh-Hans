---
title: 2023.8.0 的发行说明
description: 这些是 Cloud Manager 2023.8.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: f930f12b5f50dd96a1677ff7a56cf0e92a400556
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 39%

---


# Cloud Manager 2023.8.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.8.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.8.0 版的发布日期为 2023 年 8 月 10 日。下一个版本计划于 2023 年 7 月 9 日发布。

## 新增功能 {#what-is-new}

* 增强了以提高Cloud Manager UI中错误消息的可理解性和显示性。

## 错误修复 {#bug-fixes}

* 不常见的情况 [内容复制](/help/using/content-copy.md) 进程卡住问题已得到解决。
* 解决了对于不使用New Relic One的客户存在的临时测试问题。
* [自定义代码质量规则](/help/using/custom-code-quality-rules.md) `SupportedRunmode` 和 `ImmutableMutableMixedPackage` 已从SonarQube中删除，因为它们仅适用于AEMas a Cloud Service。
* 用户将不再遇到似乎处于运行状态的卡住管道。
* 此 **环境** 现在，菜单在触发 **[复制内容](/help/using/content-copy.md)** 模式。
* [管道重新执行](/help/using/code-deployment.md#reexecute-deployment) 如果上一个执行没有 `commitId` 在构建阶段状态上设置。
* 现在，当用户单击中的管道时，会显示一条更易于理解的消息，指出罕见的错误 **活动** 或 **管道** 屏幕。
