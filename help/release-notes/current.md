---
title: 2022.9.0 版发行说明
description: 以下是Cloud Manager 2022.9.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: e74d386d0b2d50a7e276bb7ead7594ef448742ae
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 4%

---


# Cloud Manager 2022.9.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.9.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.9.0版是2022年9月8日。 下一版本计划于2022年10月6日发布。

## 新增功能 {#what-is-new}

* Cloud Manager支持水平多区域自动缩放。
* 为仅具有Cloud Manager用户角色的用户自定义了新的欢迎页面卡片，可指导他们如何导航到AEM环境和受限的项目访问。
* 没有任何Cloud Manager角色的客户将无法访问计划详细信息。 但是，他们可以从CM登陆页面导航到“创作”端点。
* 消除因通过构建更强的可复原性实现的重试失败而导致的管道故障。

## 错误修复 {#bug-fixes}

* 改进了当maven遇到与私有repo的连接问题时与客户AEM应用程序构建相关的客户反馈。
* 在极少数情况下，当运行状况检查系统无法检索有效的运行状况得分时，将不会触发自动缩放事件。
