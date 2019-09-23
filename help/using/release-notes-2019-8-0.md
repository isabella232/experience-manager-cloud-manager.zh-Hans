---
title: 2019.8.0发行说明
seo-title: AEM Cloud manager 2019.6.0发行说明
description: 可查看本页以获取Cloud Manager 2019.8.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.8.0版的信息。
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---

# 2019.8.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 8.0版本增加了对选择性构建内容包的支持，提高了构建性能并修复了各种小错误。

## 发布日期 {#release-date}

版本2019.8.0 [!UICONTROL Cloud Manager] 的发布日期为2019年8月19日。

## 新增功能 {#whats-new}

* Cloud Manager API的新命令行界面，由 [Adobe I/O CLI提供支持](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
* 由构建生成的特定内容包可声明为可跳过且不会部署。 有关更多 ***详细信息，请参***[](create-an-application-project.md) 阅创建AEM应用程序项目中的跳过内容包一节。
* 构建容器中的预加载依赖关系集已重新处理，以避免某些不必要的网络请求。
* 针对某些配置错误的程序的概述页面上的消息已得到改进。

## 错误修复 {#bug-fixes}

* 访问SLA报告时，默认年份为2018，而不是2019。
* 对于较长的环境名称，“报告”屏幕上的环境选择器未正确增加大小。
* 当使 ***用Sling Rewriter组件时，ConfigAndInstallShouldOnlyContainOsgiNodes*** 代码质量规则产生误报。
* ConfigAndInstallShoudOnlyContainOsgiNodes ****** 代码质量规则对某些不常见的路径结构产生误报。
* 仅资产客户可能无法一致地导航到其AEM环境。
* 该对 [!UICONTROL Create a Branch and Project] 话框在不同浏览器中呈现不同。
