---
title: 2021.8.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.8.0版的信息
feature: 版本信息
source-git-commit: c4deb06615652736ff7584566507a2b42a88bfb1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---

# 2021.8.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.8.0的常规发行说明。

>[!NOTE]
>请参阅[当前发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as a Cloud Service中Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.8.0的发行日期是2021年8月12日。
下一版本计划于2021年9月9日发布。

## 新增功能 {#whats-new}

* 允许用户通过Cloud Manager UI创建和管理多个存储库的自助服务功能。

* SonarQube不必要地读取git历史数据。 在大型代码库中，这可能会导致不必要的内部版本性能损失。

* 现在有一个API可用于使每个管道的Maven依赖关系缓存失效。

* Cloud Manager使用的AEM项目原型版本已更新至版本29。

## 错误修复 {#bug-fixes}

* 有时，当管道因某些原因触发两次时，会导致其中一次执行失败，并出现&#x200B;*无法更新管道执行状态*&#x200B;错误。
