---
title: 2018.8.0发行说明
seo-title: 适用于2018.8.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2018.8.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2018.8.0的信息。
uuid: e8aiba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9 d22 e3 d559
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.8.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版本增加了在Git提交时自动触发CI/CD管线的支持，以及用于基于AEM项目类型创建应用程序项目的新向导。

## 发布日期 {#release-date}

版本2018.8.0 [!UICONTROL Cloud Manager] 的发布日期为2018年10月日。

## 新增功能 {#what-s-new}

* **计划设置** -新向导在使用AEM项目类型创建应用程序项目时，请参阅 [创建AEM应用程序项目](create-an-application-project.md) 以了解更多信息。

* **CI/CD管线** -以下更改已添加到CI/CD管线。请参阅 [配置CI/CD管道](configuring-pipeline.md) 以了解更多信息。

   * 在“Git更改”触发器中，每当有提交到已配置的git分支的注释时，将启动CI/CD管线。
   * 主屏幕上的卡现在深层链接到管道执行页面的特定部分。
   * 活动页面现在列出用于每次执行的特定分支。
   * 活动页面现在以小时和分钟为单位指示持续时间。
   * 管道执行页面现在显示为执行创建的版本/标记名称。
   * Apache Maven版本更新为3.5.3。

* **导航** -将会将以下更改添加 [!UICONTROL Cloud Manager]到。

   * 全局导航中的资源链接将导航到SharePoint中的“运行簿”。
   * “帮助”菜单已重新组织，以包含更多 [!UICONTROL Cloud Manager]特定内容。

## 错误修复 {#bug-fixes}

* “性能测试”对话框中的一些详细信息在Firefox中不可见。
* 内部系统之间的超时有时会导致报告部署失败。
* 某些成功的管道执行过程中，活动页面上的图标颜色不正确。
* 在某些情况下，“性能测试”对话框多次列出同一个量度。
* 如果在启动CI/CD管线之后添加了新实例，则不会在新创建的实例上执行部署。

## 已知问题 {#known-issues}

* 使用应用程序项目向导创建的分支不能包含虚线。
* [!UICONTROL Experience Cloud] 通知提要栏不能一致地加载通知。但是，通知在中可见，如果配置， [!UICONTROL Experience Cloud] 仍将通过电子邮件发送。

