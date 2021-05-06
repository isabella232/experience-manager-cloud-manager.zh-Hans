---
title: 2021.5.0 版发行说明
description: 可查看本页以获取Cloud Manager 2021.5.0版的信息
feature: 发行信息
translation-type: tm+mt
source-git-commit: 3d6f9a760a1e5bafdae6ece5627358524467a0d2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 2021.5.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2021.5.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.5.0的发布日期为2021年5月06日。
下一版本计划于2021年6月03日发布。

## 新增功能 {#whats-new}

* PackageOverlaps质量规则现在检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入式位置中部署同一包。

* 公共API中的存储库端点现在包括Git URL。

* 在“编辑”项目工作流中，用户只能设置非十进制KPI值。

* 将代码推送到Adobe Git时遇到间歇性故障现已解决。

* 编辑项目体验已刷新。

## 错误修复 {#bug-fixes}

* 有时，即使未部署IP，用户也可能在IP旁看到绿色的&#x200B;*活动允许列表*&#x200B;状态。

* 管道变量API将仅以状态“DELETED”标记它们，而不是删除“deleted”变量。

* 某些“代码气味”类型的质量问题错误地影响了“可靠性等级”。

* 当在午夜和凌晨1点之间启动管道执行时，Cloud Manager生成的伪像版本不能保证大于前一天创建的版本。
