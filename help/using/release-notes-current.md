---
title: 2022.3.0 版发行说明
description: 以下是Cloud Manager 2022.3.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 6e98f9d2fcd69799bad86d1e247212b26273bd0b
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---


# Cloud Manager 2022.3.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.3.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.3.0版于2022年3月10日发布。 下一版本计划于2022年4月7日发布。

## 新增功能 {#what-is-new}

* [的 `reliability_rating` 关键量度](understand-your-test-results.md) 已被禁用。
* 用户现在可以对 **管道** 页面。

## 错误修复 {#bug-fixes}

* [的 **跳过负载平衡器更改** 选项](configuring-production-pipelines.md#adding-production-pipeline) 现在可以正确禁用。
* [的 **跳过负载平衡器更改** 选项](configuring-production-pipelines.md#adding-production-pipeline) 现在将显示为编辑部署管道工作流。
* 手动创建的Git存储库的子集具有不正确的名称值，这会影响 [构建对象重用功能。](setting-up-project.md#build-artifact-reuse) 这些存储库的名称已更改，用户将在Cloud Manager API/UI中看到更正的名称。
* [添加或编辑代码质量管道时，](configuring-non-production-pipelines.md) 不再显示用于处理量度失败的选项。
* 意外的管道变量配置不再导致生成步骤出错。
