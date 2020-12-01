---
title: 2018.6.0 版发行说明
seo-title: AEM Cloud Manager 2018.6.0发行说明
description: 浏览此页，获取Cloud Manager 2018.6.0版的相关信息。
seo-description: 可查看本页以获取AEM Cloud Manager 2018.6.0版的相关信息。
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 3%

---


# 2018.6.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2018.6.0版的一般发行说明，并增加了对部署期间调度程序失效的支持、其他通知和可用性改进。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.6.0的发布日期为2018年8月9日。

## 新增功能 {#what-s-new}

* **CI/CD管道** -在CI/CD管道执行期间，舞台和生产上的可配置调度程序失效和缓存刷新。请参阅[配置CI/CD管道](configuring-pipeline.md)以了解更多信息。

* **CI/CD管道** -在管道设置过程中，现在可以定义管道在其中一个质量门中遇到重要故障时的行为方式。请参阅[配置CI/CD管道](configuring-pipeline.md)以了解更多信息。

* **CI/CD管道** -在管道设置过程中，现在可以选择您是希望CSE还是任何可用的CSE执行CSE监督。请参阅[配置CI/CD管道](configuring-pipeline.md)以了解更多信息。

* **CI/CD管道** -当CI/CD管道到达业务批准步骤时，将向有权批准部署的用户发送通知。请参阅[通知](notifications.md)以了解更多信息。

* **CI/CD管道** -当CI/CD管道到达计划集时，将向有权设置计划的用户发送通知。请参阅[通知](notifications.md)以了解更多信息。

* **代码质量分析** -用于识别配置不正确的出站HTTP/HTTPS请求的新规则。请参阅[自定义代码质量规则](custom-code-quality-rules.md)以了解更多信息。

## 错误修复 {#bug-fixes}

* 在某些情况下，性能测试未完全分布于多个调度程序和发布实例。
* 标题导航在窄的浏览器窗口中消失。
* 在管线运行期间，某些管线设置未禁用。
* 从项目列表屏幕链接到AEM和监视会替换当前浏览器选项卡并打开一个新选项卡。
* 在某些情况下，长时间的批准期可能导致部署失败。
