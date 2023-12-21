---
title: 2023.12.0 的发行说明
description: 这些是 Cloud Manager 2023.12.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 2ac254508e4015fea21c4fcd087703ac5fbeeec6
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 81%

---


# Cloud Manager 2023.12.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.12.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.12.0 版的发布日期为 2023 年 12 月 14 日。下一个版本计划于 2024 年 1 月 18 日发布。

## 新增功能 {#what-is-new}

* 通过 [Cloud Manager 自定义权限](/help/using/custom-permissions.md)，可创建具有可配置的权限的自定义权限配置文件，以限制 Cloud Manager 用户对项目、管道和环境的访问。
* 将更新转出到 [构建环境](/help/getting-started/build-environment.md) 曾经是 [宣布并从10月发布的Cloud Manager开始](/help/release-notes/2023/2023-10-0.md) 已完成。
   * 添加了对节点18的支持 [前端管道和全栈管道。](/help/overview/ci-cd-pipelines.md)
   * Java 8 次要版本已更新到 `jdk1.8.0_371`。
   * Java 11 次要版本已更新到 `jdk-11.0.20`。
   * Maven 已更新到版本 3.8.8
      * Maven现在禁用所有不安全的内容 `http://*` 默认镜像。
      * [Adobe推荐](/help/getting-started/build-environment.md#https-maven) 用户更新其Maven存储库以使用HTTPS而不是HTTP。
* 构建容器基础映像已更新至 Ubuntu 22.04。

## 早期采用计划 {#early-adoption}

成为我们早期采用计划的一部分，并有机会测试一些即将推出的功能

### 自带 GitHub {#byo-github}

如果您使用 GitHub 管理存储库，则[现在可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码。](/help/managing-code/byo-github.md)此集成使您无需始终与 Adobe 存储库同步代码，并可在将拉取请求合并到主分支之前对其进行验证。

如果您有兴趣测试这项新功能并共享您的反馈，请从您的 Adobe ID 关联的电子邮件地址发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com`。
