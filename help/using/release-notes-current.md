---
title: 2019.8.0发行说明
seo-title: 适用于2019.8.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.8.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.8.0的信息。
translation-type: tm+mt
source-git-commit: 365cd6dfe65059c0c529f774bbcda946d47b0db5

---

# 2019.8.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版增加了对选择性构建内容包的支持、改进了构建性能并修复了各种次要缺陷。

## 发布日期 {#release-date}

版本2019.8.0 [!UICONTROL Cloud Manager] 的发布日期为2019年月19日。

## 新增功能 {#whats-new}

* 指向云管理器API的新命令行界面，由Adobe [I/CLIÉ提供支持](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
* 构建生成的特定内容包可能被声明为可跳过的，并且不会被部署。有关更 ***多详细信息，请参阅***[创建AEM应用程序项目](create-an-application-project.md) 中的“跳过内容包”部分。
* 已重新设计构建容器中预加载的依赖关系集，以避免某些不必要的网络请求。
* 已改进某些未正确配置的程序概述页面上的消息。

## 错误修复 {#bug-fixes}

* 访问SLA报表时，默认年份为2018年而非2019年。
* 对于较长的环境名称，“报告”屏幕上的环境选择器大小不正确。
* ***configandInstallShoDonlyContains*** 代码质量规则在使用sling Rewriter组件时生成虚假提示。
* ***configandInstallShoDonlyContaines*** 代码质量规则为某些不常见的路径结构生成虚假的位置。
* 仅资产的客户可能无法一致地导航到他们的AEM环境。
* [!UICONTROL Create a Branch and Project] 对话框在不同浏览器之间呈现不同的渲染效果。
