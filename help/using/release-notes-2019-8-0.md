---
title: 2019.8.0 版发行说明
seo-title: AEM Cloud Manager 2019.8.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2019.8.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.8.0版的信息。
feature: 发行信息
exl-id: 9b3da506-76f1-439f-8de0-a5e2ee88b979
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 6%

---

# 2019.8.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版本增加了对选择性构建内容包的支持，提高了构建性能，并修复了各种次要错误。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.8.0的发行日期是2019年8月19日。

## 新增功能 {#whats-new}

* Cloud Manager API的新命令行接口，由[Adobe I/OCLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)提供支持。
* 由内部版本生成的特定内容包可以声明为跳过且不会部署。 有关更多详细信息，请参阅[跳过内容包](/help/using/setting-up-project.md#skipping-content-packages) 。
* 已重新处理生成容器中预加载的依赖关系集，以避免一些不必要的网络请求。
* 某些配置不正确的程序的概述页面上的消息已得到改进。

## 错误修复 {#bug-fixes}

* 访问SLA报告时，默认年份为2018年，而不是2019年。
* 对于较长的环境名称，“报表”屏幕上的环境选择器未正确增加大小。
* 使用Sling重写程序组件时， ***ConfigAndInstallShouldOnlyContainOsgiNodes***&#x200B;代码质量规则会产生误报。
* ***ConfigAndInstallShouldOnlyContainOsgiNodes***&#x200B;代码质量规则针对某些不常见的路径结构产生了误报。
* 仅资产客户可能无法始终导航到其AEM环境。
* “创建分支”和“项目”对话框在不同浏览器中的呈现方式不同。
