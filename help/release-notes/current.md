---
title: 2024.1.0 的发行说明
description: 这些是 Cloud Manager 2024.1.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b235e398b42e9da3dd2efacdc0ef38b6803bd213
workflow-type: ht
source-wordcount: '243'
ht-degree: 100%

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

* 纠正了在某些极端情况下发生的一个错误，其中因测试应用程序解释数据的方式而下载失败，导致总错误率未能通过测试。
* 在构建步骤完成，并因 `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR` 导致状态为 `FAILED` 时，现在正确地将它描述为因与目标分支发生合并冲突而导致的错误。
