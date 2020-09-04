---
title: 2019.8.0 版发行说明
seo-title: AEM Cloud Manager 2019.8.0发行说明
description: 可查看本页以获取Cloud Manager Release 2019.8.0的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2019.8.0版的相关信息。
translation-type: tm+mt
source-git-commit: 2ada697ca21acd0c73dbce2bce3e9481ac50272c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---

# 2019.8.0 版发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 8.0版本增加了对选择性构建内容包的支持，改进了构建性能并修复了各种小错误。

## 发布日期 {#release-date}

版本2019.8.0 [!UICONTROL Cloud Manager] 的发布日期为2019年8月19日。

## 新增功能 {#whats-new}

* 由AdobeI/O CLI提供支持的Cloud Manager API的新 [命令行界面](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
* 生成生成的特定内容包可声明为跳过且不会部署。 有关更多 [详细信息，请参](/help/using/setting-up-project.md#skipping-content-packages) 阅跳过内容包。
* 构建容器中预加载的依赖关系集已重新处理，以避免一些不必要的网络请求。
* 某些配置不正确的项目的概述页面上的消息已得到改进。

## 错误修复 {#bug-fixes}

* 访问SLA报告时，默认年份为2018，而不是2019。
* 对于长环境名，“报告”屏幕上的环境选择器未正确增加大小。
* ConfigAndInstallShowOnlyContainOsgiNodes ***代码质量规则在使用Sling Rewriter组件时*** ，会产生误报。
* ConfigAndInstallShoudOnlyContainOsgiNodes ***代码质量规则对某些不常见的路径结构*** 产生误报。
* 仅限资产的客户可能无法始终导航到AEM环境。
* “创建分支”和“项目”对话框在不同浏览器中的呈现方式不同。
