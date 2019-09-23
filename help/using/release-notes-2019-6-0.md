---
title: 2019.6.0发行说明
seo-title: AEM Cloud manager 2019.6.0发行说明
description: 可查看本页以获取Cloud Manager 2019.6.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.6.0版的信息。
translation-type: tm+mt
source-git-commit: 7cfa0cf66efd5891263bfcc83a5149daec5c8b67

---

# 2019.6.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 6.0版本新增了代码质量规则和产品更新向导。 有关更多详细信息，请按照以下部分进行操作。

## 发布日期 {#release-date}

版本2019.6.0 [!UICONTROL Cloud Manager] 的发布日期为2019年6月20日。

## 新增功能 {#whats-new}

* “新产品更新”向导可帮助客户成功执行AEM更新。 请参阅产 [品更新向导](overview-productupdate-wizard.md) ，了解更多信息。
* 检查内容结构的代码质量规则。 有关详细 [信息，请参阅自定义代码质量规则](custom-code-quality-rules.md) 。
* git推送的最大大小已增加到1 GB。

## 错误修复 {#bug-fixes}

* 在某些情况下，由于先前的故障，管线无法启动。

## 已知问题 {#known-issues}

* 代码质量CSV下载并不总是按严重性排序。
* 如果OSGi配置位于配置文件夹下的嵌套文件夹中， *则ConfigAndInstallShouldOnlyContainOsgiNodes* 规则可能会报告 ** 误报。