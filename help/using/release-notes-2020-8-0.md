---
title: 2020.8.0 版发行说明
seo-title: AEM Cloud Manager 2020.8.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2020.8.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.8.0版的信息
feature: 发行信息
exl-id: 94163e28-5c29-4a00-9a2b-e45bf6f71098
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 7%

---

# 2020.8.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2020.8.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.8.0的发行日期是2020年8月6日。

## 新增功能 {#whats-new}

现在支持绑定身份验证的专用Maven存储库。

## 错误修复 {#bug-fixes}

* 在代码质量扫描中，正在执行一些不必要的和不需要的SonarQube插件。

* 在管道执行页面上，分支名称的格式不正确。

* 当使用单个发布、单个调度程序和冷备用作者部署到拓扑时，会错误地从负载平衡器中删除调度程序。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而阻止管道的新执行。

* 由于内部通信问题，管道执行有时会遇到&#x200B;*卡住*&#x200B;的问题。

* 程序卡片上的工具提示并不一致。

* **Overview**&#x200B;页面上存在颜色不匹配的问题。

* 站点性能测试现在支持可选使用身份验证。

* 当通过Cloud Manager部署调度程序配置时，创作实例的调度程序缓存会自动刷新。
