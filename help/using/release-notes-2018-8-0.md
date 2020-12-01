---
title: 2018.8.0 版发行说明
seo-title: AEM Cloud Manager 2018.8.0发行说明
description: 可查看本页以获取Cloud Manager Release 2018.8.0的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2018.8.0版的相关信息。
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 4%

---


# 2018.8.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版本增加了在git提交时自动触发CI/CD管道的支持，并增加了一个新向导，用于根据AEM Project Archetype在git中创建应用程序项目。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.8.0的发布日期为2018年10月4日。

## 新增功能 {#what-s-new}

* **项目设置** -使用AEM Project Archetype在git中创建应用程序项目的新向导

* **CI/CD管道** -以下更改已添加到CI/CD管道。请参阅[配置CI/CD管道](configuring-pipeline.md)以了解更多信息。

   * 在Git更改触发器上，当向配置的git分支添加提交时，该触发器将开始CI/CD管道。
   * 主屏幕上的卡现在深入链接到管道执行页面的特定部分。
   * 活动页现在列表用于每次执行的特定分支。
   * 活动页现在以小时和分钟为单位指示持续时间。
   * 管道执行页面现在显示为执行创建的版本／标签名称。
   * Apache Maven版本已更新至3.5.3。

* **导航** -在中添加了以下更改 [!UICONTROL Cloud Manager]。

   * 全局导航中的资源链接将导航到Sharepoint中的Runbook。
   * 帮助菜单已重新组织，以包含更多特定于[!UICONTROL Cloud Manager]的内容。

## 错误修复 {#bug-fixes}

* “性能测试”对话框中的某些详细信息在Firefox中不可见。
* 内部系统之间的超时偶尔会导致报告部署失败。
* 对于某些成功的管道执行，活动页面上的图标颜色不正确。
* 在某些情况下，“性能测试”对话框多次列出同一指标。
* 如果在CI/CD管道启动后添加了新实例，则不会对新创建的实例执行部署。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含虚线。
* [!UICONTROL Experience Cloud]通知提要栏可能无法一致加载通知。 但是，通知在[!UICONTROL Experience Cloud]中可见，如果配置，仍将通过电子邮件发送。

