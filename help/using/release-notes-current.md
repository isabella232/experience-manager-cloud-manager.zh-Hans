---
title: 2019.6.0发行说明
seo-title: 适用于2019.6.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.6.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.6.0的信息。
translation-type: tm+mt
source-git-commit: 7373f674b9804c83fad0871a74ef85280ea24962

---

# Release Notes for 2019.6.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.6.0版本新增了代码质量规则和新的产品更新向导。请按照以下部分了解更多详细信息。

## Release Date {#release-date}

The Release Date for [!UICONTROL Cloud Manager] Version 2019.6.0 is June 20, 2019 .

## 新增功能 {#whats-new}

* 可帮助客户成功执行AEM更新的新产品更新向导。Refer to [Product Update Wizard](overview-productupdate-wizard.md) to learn more.
* 检查内容结构的代码质量规则。Refer to [Custom Code Quality Rules](custom-code-quality-rules.md) for more information.
* Git推送的最大大小已增加至GB。

## Bug Fixes {#bug-fixes}

* 在某些情况下，由于先前失败，渠道无法启动。

## 已知问题 {#known-issues}

* 代码质量CSV下载并不总是按照严重程度排序。
* *如果* OSGi配置位于 *config* 文件夹下的嵌套文件夹中，则可能由configandInstallShodonlyContainosgiNetwork规则报告虚假位置。
