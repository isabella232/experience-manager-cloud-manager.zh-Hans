---
title: 2019.8.0 版发行说明
seo-title: AEM Cloud Manager 2019.8.0发行说明
description: 可查看本页以获取Cloud Manager 2019.8.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.8.0版的信息。
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 6%

---

# 2019.8.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版本增加了对选择性构建内容包的支持，提高了构建性能并修复了各种小错误。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.8.0的发布日期为2019年8月19日。

## 新增功能 {#whats-new}

* Cloud Manager API的新命令行接口，由[Adobe I/OCLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)提供支持。
* 生成生成的特定内容包可声明为跳过且不会部署。 有关详细信息，请参阅[跳过内容包](/help/using/setting-up-project.md#skipping-content-packages)。
* 构建容器中预加载的依赖关系集已重新处理，以避免某些不必要的网络请求。
* 已改进概述页面上某些配置不正确的项目的消息。

## 错误修复 {#bug-fixes}

* 访问SLA报告时，默认年份为2018，而不是2019。
* 对于长环境名，“报告”屏幕上的环境选择器未正确增加大小。
* 使用Sling Rewriter组件时，***ConfigAndInstallShoudOnlyContainOsgiNodes***&#x200B;代码质量规则产生误报。
* ***ConfigAndInstallShoudOnlyContainOsgiNodes***&#x200B;代码质量规则针对某些不常见的路径结构产生了误报。
* 仅限资产的客户可能无法一致地导航到其AEM环境。
* “创建分支”和“项目”对话框在不同浏览器中的呈现方式不同。
