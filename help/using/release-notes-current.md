---
title: 2022.6.0 版发行说明
description: 以下是Cloud Manager 2022.6.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: dab08a2499b521b7026ab2bd17b82cb241f26fb6
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 3%

---


# Cloud Manager 2022.6.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.6.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.6.0版于2022年6月9日发布。 下一版本计划于2022年6月30日发布。

## 新增功能 {#what-is-new}

* Cloud Manager登录页面上新增的欢迎卡使用户能够快速访问与租户相关的入门教程和进度量度。
   * 此功能将在2022.06.0版后的一周内分阶段推出。
* [现在可以重复使用生成工件](/help/using/setting-up-project.md#build-artifact-reuse) 使用git镜像时。

## API更改 {#api-changes}

* 的 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API已弃用，并且 [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 的值。
   * `List Programs` 仍然有效，但其使用情况将在日志中生成警告消息。
   * 三个月后将不再支持该选件。
