---
title: 2021.5.0 版发行说明
description: 可查看本页面以获取有关Cloud Manager 2020.5.0版的信息
feature: 发行信息
source-git-commit: 5111a918b8063ab576ef587dc3c8d66ad976fc1a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# 2021.5.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.5.0的常规发行说明。

>[!NOTE]
>请参阅[当前发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as a Cloud Service中Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.5.0的发行日期是2021年5月6日。
下一版本计划于2021年6月10日发布。

## 新增功能 {#whats-new}

* PackageOverlaps质量规则现在会检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入位置中部署同一包的情况。

* 现在，公共API中的存储库端点包含Git URL。

* 在编辑项目群工作流中，用户将只能设置非十进制KPI值。

* 现在，解决了将代码推送到AdobeGit时遇到的间歇性故障。

* 编辑程序体验已刷新。

## 错误修复 {#bug-fixes}

* 管道变量API不会删除“已删除”变量，而是仅将其标记为状态为“已删除”。

* 某些代码气味类型的质量问题错误地影响了可靠性评级。

* 当从午夜UTC到凌晨1点之间开始管道执行时，Cloud Manager生成的对象版本不保证大于前一天创建的版本。

* 某些Adobe Managed Services(AMS)客户无法使用Cloud Manager API在Adobe I/O开发人员控制台中创建新项目。
