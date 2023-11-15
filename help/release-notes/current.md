---
title: 2023.11.0 的发行说明
description: 这些是 Cloud Manager 2023.11.0 版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 264c7ffcbc9e10903880a511a4ca605be666f7e8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 28%

---


# Cloud Manager 2023.11.0 版的发行说明 {#release-notes}

此页面记载 [!UICONTROL Cloud Manager] 2023.11.0 版的发行说明。

>[!NOTE]
>
>有关 AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明，请参阅 [AEM as a Cloud Service 中的 Cloud Manager 的最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.11.0 版的发布日期为 2023 年 11 月 14 日。下一个版本计划于2023年12月7日发布。

## 新增功能 {#what-is-new}

* [管道执行详细信息页面](/help/using/managing-pipelines.md#view-details) 现在将显示管道执行中的所有步骤，其中尚未开始的步骤将显示为灰色。
* 在两者上 **[活动](/help/using/managing-pipelines.md#activity)** 和 **[管道](/help/using/managing-pipelines.md#pipelines)** 现在，在单击处于运行状态的管道时，会显示管道执行摘要。
* 新 **持续时间** 部分已添加到 [管道详细信息页面](/help/using/managing-pipelines.md#view-details) 这包括基于该项目历史趋势的管道步骤的平均持续时间。
* 在 [管道执行页面，](/help/using/managing-pipelines.md#activity-window) 完成的步骤现在显示持续时间
* Cloud Manager [内容复制工具](/help/using/content-copy.md) 允许用户按需将可变内容从其AMS托管的AEM 6.x生产环境复制到较低环境以进行测试。
* 以下内容的执行 [重用生成工件](/help/getting-started/project-setup.md#build-artifact-reuse) 现在将显示最初构建这些工件的执行的链接。
* 要选择的选项 **重要量度失败** 现在可以配置 [代码质量管道](/help/using/non-production-pipelines.md) 也一样。

## 早期采用计划 {#early-adoption}

加入我们的早期采用计划，并有机会测试即将推出的某些功能

### 自带GitHub {#byo-github}

如果您使用GitHub管理存储库， [您现在可以通过Cloud Manager直接在GitHub存储库中验证代码。](/help/managing-code/byo-github.md) 此集成消除了对代码与Adobe存储库保持一致同步的需求，并允许您在将拉取请求合并到主分支之前对其进行验证。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `Grp-CloudManager_BYOG@adobe.com` 从与Adobe ID关联的电子邮件地址中查找。

### 自定义权限 {#custom-permissions}

[Cloud Manager 自定义权限](/help/using/custom-permissions.md)可让您创建具有可配置权限的新的自定义权限配置文件，以限制 Cloud Manager 用户对项目、管道和环境的访问。

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至 `Grp-CloudManager_ams_custompermissions@adobe.com` 从与Adobe ID关联的电子邮件地址中查找。
