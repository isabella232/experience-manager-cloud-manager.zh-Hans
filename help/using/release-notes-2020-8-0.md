---
title: 2020.8.0 版发行说明
seo-title: AEM Cloud Manager 2020.8.0发行说明
description: 可查看本页以获取Cloud Manager Release 2020.8.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.8.0版的相关信息
translation-type: tm+mt
source-git-commit: c1d07c95088a279376ef495001a5165c7e459642
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---

# 2020.8.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2020.8.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.8.0的发布日期为2020年8月06日。

## 新增功能 {#whats-new}

现在支持身份验证绑定的私有Maven存储库。

## 错误修复 {#bug-fixes}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 当使用单个发布、单个调度程序和一个冷备用作者部署到拓扑时，调度程序被错误地从负载平衡器中删除。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 由于内部通信问题，管道执行偶尔会被卡住&#x200B;*。*

* 项目卡上的工具提示不一致正确。

* **概述**&#x200B;页面的颜色不匹配。

* 站点性能测试现在支持身份验证的可选使用。

* 当通过云管理器部署调度程序配置时，创作实例的调度程序缓存会自动刷新。

