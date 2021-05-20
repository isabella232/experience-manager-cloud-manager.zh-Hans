---
title: 2018.8.0 版发行说明
seo-title: AEM Cloud Manager 2018.8.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2018.8.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.8.0版的信息。
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
feature: 发行信息
exl-id: 20f87048-30f7-4869-aad0-13ca383a404b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 4%

---

# 2018.8.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版本添加了对在git提交时自动触发CI/CD管线的支持，以及一个新向导，用于根据AEM项目原型在git中创建应用程序项目。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.8.0的发行日期是2018年10月4日。

## 新增功能 {#what-s-new}

* **程序设置**  — 新建了一个向导，用于使用AEM项目原型在git中创建应用程序项目

* **CI/CD管道**  — 向CI/CD管道添加了以下更改。请参阅[配置CI/CD管线](configuring-pipeline.md)以了解更多信息。

   * 在Git更改触发器上，当向配置的git分支添加提交时，该触发器将启动CI/CD管道。
   * 现在，主屏幕上的信息卡深度链接到管道执行页面的特定部分。
   * “活动”页面现在列出了用于每次执行的特定分支。
   * “活动”页面现在以小时和分钟为单位指示持续时间。
   * 管道执行页面现在显示为执行创建的版本/标记名称。
   * 已将Apache Maven版本更新至3.5.3。

* **导航**  — 在中添加了以下更 [!UICONTROL Cloud Manager]改。

   * 全局导航中的资源链接将导航到Sharepoint中的Runbook。
   * 帮助菜单已重新组织，以包含更多特定于[!UICONTROL Cloud Manager]的内容。

## 错误修复 {#bug-fixes}

* 在Firefox中，“性能测试”对话框中的一些详细信息不可见。
* 内部系统之间的超时有时会导致报告部署失败。
* 对于一些成功的管道执行，活动页面上的图标颜色不正确。
* 在某些情况下，性能测试对话框会多次列出同一量度。
* 如果在CI/CD管道启动后添加了新实例，则不会在新创建的实例上执行部署。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含破折号。
* [!UICONTROL Experience Cloud]通知侧栏可能无法始终如一地加载通知。 但是，通知在[!UICONTROL Experience Cloud]中可见，如果配置，仍将通过电子邮件发送。
