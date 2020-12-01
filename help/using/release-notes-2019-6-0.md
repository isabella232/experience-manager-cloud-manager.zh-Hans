---
title: 2019.6.0 版发行说明
seo-title: AEM Cloud Manager 2019.6.0发行说明
description: 可查看本页以获取Cloud Manager Release 2019.6.0的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2019.6.0版的相关信息。
translation-type: tm+mt
source-git-commit: 7cfa0cf66efd5891263bfcc83a5149daec5c8b67
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 8%

---

# 2019.6.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.6.0版本新增了代码质量规则和产品更新向导。 有关更多详细信息，请按照以下部分进行操作。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.6.0的发布日期为2019年6月20日。

## 新增功能 {#whats-new}

* “新产品更新”向导可帮助客户成功执行AEM更新。 请参阅[产品更新向导](overview-productupdate-wizard.md)以了解更多信息。
* 检查内容结构的代码质量规则。 有关详细信息，请参阅[自定义代码质量规则](custom-code-quality-rules.md)。
* git推送的最大大小已增加到1 GB。

## 错误修复 {#bug-fixes}

* 在某些情况下，由于以前的故障，无法启动管道。

## 已知问题 {#known-issues}

* 代码质量CSV下载并不始终按严重性排序。
* 如果OSGi配置位于&#x200B;*config*&#x200B;文件夹下的嵌套文件夹中，则&#x200B;*ConfigAndInstallShouldOnlyContainOsgiNodes*&#x200B;规则可能会报告误报。