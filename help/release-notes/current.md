---
title: 2024.3.0 的发行说明
description: 这些是 Cloud Manager 2024.3.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 22730ba281f7c1c4720158a3a813c56b815a0af1
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 93%

---


# Cloud Manager 2024.3.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2024.3.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.3.0 版的发布日期为 2024 年 3 月 14 日。下一个版本计划于 2024 年 4 月 11 日发布。

## 新增功能 {#what-is-new}

* Cloud Manager UI中现在会显示包括绿色服务器的IP/DNS (FQDN)信息的详细信息。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/managing-code/byo-github.md)此集成使得无需始终与 Adobe 存储库同步代码，并使您可验证拉取请求后再将其合并到主分支中。此功能为公共 GitHub 所独有。不支持自托管 GitHub。

如果您有兴趣测试这项新功能并共享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。

## 错误修复 {#bug-fixes}

* 修复了性能测试步骤中错误率量度失败时未生成相应日志的错误。
* 性能测试服务负责检测网站上是否存在页面 (404)，改进后的服务逻辑现在可确保更顺畅、不间断的部署。
