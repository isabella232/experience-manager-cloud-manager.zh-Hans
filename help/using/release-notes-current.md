---
title: 2020.8.0 版发行说明
seo-title: AEM Cloud Manager 2020.8.0发行说明
description: 可查看本页以获取Cloud Manager Release 2020.8.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.8.0版的相关信息
translation-type: tm+mt
source-git-commit: cff6f23a674fda2f57ea481d89644de9be3f5722
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 7%

---

# 2020.8.0 版发行说明 {#release-notes-for}

以下部分概述了2020.8.0 [!UICONTROL Cloud Manager] 版的一般发行说明。

## 发布日期 {#release-date}

版本2020.8.0 [!UICONTROL Cloud Manager] 的发布日期为2020年8月06日。

## 新增功能 {#whats-new}

现在支持身份验证绑定的私有Maven存储库。

## 错误修复 {#bug-fixes}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 当使用单个发布、单个调度程序和一个冷备用作者部署到拓扑时，调度程序被错误地从负载平衡器中删除。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 管道执行偶尔会因 *内部* 通信问题而卡住。

* 项目卡上的工具提示不一致正确。

* 概述页面上的颜色不匹配。

