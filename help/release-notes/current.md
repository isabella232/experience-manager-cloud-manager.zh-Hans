---
title: 2024.2.0 的发行说明
description: 这些是 Cloud Manager 2024.2.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: cc87246503ab63d6dd60c691f15fc4759fcf6939
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 68%

---


# Cloud Manager 2024.2.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2024.2.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.2.0 版的发布日期为 2024 年 2 月 15 日。下一个版本计划于 2024 年 3 月 16 日发布。

## 新增功能 {#what-is-new}

* 作为的一部分 [部署，](/help/using/code-deployment.md) Dispatcher缓存在 **附加Dispatcher** 步骤。 为了允许您在将每个节点附加到应用程序负载平衡器之前测试其上的更改，在将代码部署到特定发布者后，现在可以在将相关Dispatcher附加到负载平衡器之前直接从该Dispatcher测试更改。
* [构建环境](/help/getting-started/build-environment.md) 已更新至Maven版本3.9.4和JDK版本jdk-11.0.22和jdk1.8.0_401。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/managing-code/byo-github.md)此集成使得无需始终与 Adobe 存储库同步代码，并使您可验证拉取请求后再将其合并到主分支中。此功能为公共 GitHub 所独有。不支持自托管 GitHub。

如果您有兴趣测试这项新功能并共享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。

## 错误修复 {#bug-fixes}

* 内部版本容器的JDK已更新到可以解决此问题的版本 [JDK-8313765。](https://bugs.openjdk.org/browse/JDK-8313765)
§