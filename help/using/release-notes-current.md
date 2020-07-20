---
title: 2020.7.0 版发行说明
seo-title: AEM Cloud Manager 2020.7.0版本说明
description: 可查看本页以获取Cloud Manager Release 2020.7.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager Release 2020.7.0的相关信息
translation-type: tm+mt
source-git-commit: 0d46abc386460ccbaf7ba10b93286bc8e4af2395
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 6%

---

# 2020.7.0 版发行说明 {#release-notes-for}

以下部分概述了2020.7.0 [!UICONTROL Cloud Manager] 版的一般发行说明。

## 发布日期 {#release-date}

版本2020.7.0 [!UICONTROL Cloud Manager] 的发布日期为2020年7月9日。

## 新增功能 {#whats-new}

* 现在，在生产部署过程中从负载平衡器分离和附加调度程序实例可以以更一致的方式工作。

* Cloud Manager构建容器现在支持Java 8和Java 11。

* Cloud Manager管道现在支持客户集变量和秘密。
有关更多 [详细信息](/help/using/create-an-application-project.md#pipeline-variables) ，请参阅管道变量。

## 错误修复 {#bug-fixes}

* “非 **生** 产管道编 **辑”(Non-Production Pipeline** Edit)页面上的“取消”(Cancel)和“保存”(Save)选项并不总是可见。

* 代码质量过程中的某些失败可能导致日志文件无法正确生成。

* 无法通过用户界面一致地下载某些大型管道步骤日志。

## 已知问题 {#known-issues}

* 当AMS环境包含待机实例时，已记录的消息会声明该实例已关闭，而不是处于待机模式。

* 由于代码覆盖率的计算方式发生 _更改_ ,Jacoco插件的最低版本现在为0.7.5.201505241946（发布于2015年5月）。 明确引用旧版本的客户将在代码质量过程中收到错误消息。
