---
title: 2022.3.0 版发行说明
description: 以下是Cloud Manager 2022.3.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 7611667d8c617d501f9b69cbc7c854c195a5ebbe
workflow-type: tm+mt
source-wordcount: '210'
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

* 现在，来自资产测试的出站HTTP请求将来自固定IP范围。


## 错误修复 {#bug-fixes}

* 的 **跳过负载平衡器更改** 无法禁用选项。
* **跳过负载平衡器更改** 选项未显示在AMS开发部署中 **编辑管道工作流**.
* 手动创建的git存储库的子集具有不正确的名称值，这会阻止生成对象重用功能生效。 这些存储库的名称已更改，用户将在Cloud Manager API/UI中看到更正的名称。
* 非生产管道的人造物在生产全堆流水线上被不当地重复使用。
* 添加或编辑代码质量管道时，不再显示用于处理量度失败的选项。
* 在生成步骤中，可能会导致一些意外的管道变量配置。
