---
title: 2020.8.0 版发行说明
seo-title: AEM Cloud Manager 2020.8.0发行说明
description: 可查看本页以获取Cloud Manager Release 2020.8.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.8.0版的相关信息
translation-type: tm+mt
source-git-commit: 68330a3a6d9e1f95782418dbd72cbc0e6ee7362c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 20%

---

# 2020.8.0 版发行说明 {#release-notes-for}

以下部分概述了2020.8.0 [!UICONTROL Cloud Manager] 版的一般发行说明。

## 发布日期 {#release-date}

版本2020.8.0 [!UICONTROL Cloud Manager] 的发布日期为2020年8月06日。

## 新增功能 {#whats-new}

* 站点性能测试现在支持身份验证的可选使用。

   请参阅经 [身份验证的站点性能测试](configuring-pipeline.md#authenticated-sites-performance) ，了解如何验证AEM Sites性能测试。

* 现在支持身份验证绑定的私有Maven存储库。

## 错误修复 {#bug-fixes}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 当使用单个发布、单个调度程序和一个冷备用作者部署到拓扑时，调度程序被错误地从负载平衡器中删除。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 管道执行偶尔会因 *内部* 通信问题而卡住。

* 项目卡上的工具提示不一致正确。

* 概述页面上的颜色不匹配。

## 已知问题 {#known-issues}

* 当AMS环境包含待机实例时，已记录的消息会声明该实例已关闭，而不是处于待机模式。

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;_最低_&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户将在代码质量控制过程中收到一条错误消息。
