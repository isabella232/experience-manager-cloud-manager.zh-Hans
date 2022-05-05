---
title: 2022.5.0 版发行说明
description: 以下是Cloud Manager 2022.5.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 84cc4352488002ad40102ea2c507af652d9012a1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 29%

---


# Cloud Manager 2022.5.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.5.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.5.0版是2022年5月5日。 下一版本计划于2022年6月9日发布。

## 新增功能 {#what-is-new}

现在，来自资产测试的出站HTTP请求将来自固定IP范围。

## 错误修复 {#bug-fixes}

* 无法禁用“跳过负载平衡器”更改选项。
* AMS开发部署编辑管道工作流中未显示跳过负载平衡器更改选项。
* 手动创建的GIT存储库的子集具有不正确的名称值，这会阻止生成对象重用功能生效。 这些存储库的名称已经更改，用户将在 Cloud Manager API/UI 中看到正确的名称。
* 来自非生产管道的生成工件不适当地重新用于生产全堆栈管道。
* 添加或编辑代码质量管道时，不再显示处理度量失败的选项。
* 某些意外的管道变量配置可能会导致生成步骤中出现错误。
