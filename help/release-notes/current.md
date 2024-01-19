---
title: 2024.1.0 的发行说明
description: 这些是 Cloud Manager 2024.1.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b235e398b42e9da3dd2efacdc0ef38b6803bd213
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 77%

---


# Cloud Manager 2024.1.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2024.1.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.1.0 版的发布日期为 2024 年 1 月 17 日。下一个版本计划于 2024 年 2 月 16 日发布。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/managing-code/byo-github.md)此集成使您无需始终与 Adobe 存储库同步代码，并可在将拉取请求合并到主分支之前对其进行验证。

如果您有兴趣测试这项新功能并共享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。

## 错误修复 {#bug-fixes}

* 对于某些极端情况，由于测试应用程序解释数据的方式导致下载失败，从而导致总错误百分比无法通过测试，现已更正错误。
* 当构建步骤以状态完成时 `FAILED` 应付 `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR`，由于与目标分支存在合并冲突，因此现在可将其正确描述为错误。
