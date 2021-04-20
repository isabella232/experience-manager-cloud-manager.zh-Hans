---
title: 2020.8.0 版发行说明
seo-title: AEM Cloud Manager 2020.8.0发行说明
description: 可查看本页以获取Cloud Manager 2020.8.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.8.0版的信息
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 7%

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

* 使用单个发布、单个调度程序和冷备用作者部署到拓扑时，从负载平衡器中错误地删除了调度程序。

* 在某些情况下，已完成的管道执行没有被成功记录为已完成，从而防止管道的新执行。

* 由于内部通信问题，管道执行偶尔会遇到&#x200B;*卡住*。

* 项目卡上的工具提示并不一致。

* **概述**&#x200B;页面上存在颜色不匹配。

* 站点性能测试现在支持可选使用身份验证。

* 当通过Cloud Manager部署调度程序配置时，创作实例的调度程序缓存会自动刷新。

