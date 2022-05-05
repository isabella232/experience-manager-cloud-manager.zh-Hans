---
title: 2022.5.0 版发行说明
description: 以下是Cloud Manager 2022.5.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0ddfd152cb15731882d198d043dd8897b5073ab4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 46%

---


# Cloud Manager 2022.5.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.5.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.5.0版是2022年5月5日。 下一版本计划于2022年6月9日发布。

## 新增功能 {#what-is-new}

使用开发人员角色可以访问AEM环境日志。

## 错误修复 {#bug-fixes}

* 手动创建的 Git 存储库的一个子集的名称值不正确，这使得生成工件的重用功能无法生效。这些存储库的名称已经更改，用户将在 Cloud Manager API/UI 中看到正确的名称。
* 来自非生产管道的生成工件不适当地重新用于生产全堆栈管道。
* 添加或编辑代码质量管道时，不再显示处理度量失败的选项。
* 某些意外的管道变量配置可能会导致生成步骤中出现错误。
