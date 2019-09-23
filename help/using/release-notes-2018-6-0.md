---
title: 2018.6.0发行说明
seo-title: AEM Cloud manager 2018.6.0发行说明
description: 浏览此页，获取Cloud Manager 2018.6.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.6.0版的信息。
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 发行说明
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b

---


# 2018.6.0发行说明 {#release-notes-for}

下节概述了2018.6.0版的一般发行说明，并增加了对部署期间调度程序失效的支持、其他通知和可用性改进。 [!UICONTROL Cloud Manager]

## 发布日期 {#release-date}

版本2018.6.0 [!UICONTROL Cloud Manager] 的发布日期为2018年8月9日。

## 新增功能 {#what-s-new}

* **CI/CD管道** -在CI/CD管道执行期间，舞台和生产上的可配置调度程序失效和缓存刷新。 请参阅配 [置您的CI/CD管道](configuring-pipeline.md) ，了解更多信息。

* **CI/CD管道** -在管道设置过程中，现在可以定义管道在其中一个质量门中遇到重要故障时的行为方式。 请参阅配 [置您的CI/CD管道](configuring-pipeline.md) ，了解更多信息。

* **CI/CD管道** -在管道设置过程中，现在可以选择您希望CSE还是任何可用的CSE执行CSE监督。 请参阅配 [置您的CI/CD管道](configuring-pipeline.md) ，了解更多信息。

* **CI/CD管道** -当CI/CD管道到达业务批准步骤时，将向获得批准部署授权的用户发送通知。 请参阅通 [知](notifications.md) ，了解更多。

* **CI/CD管道** -当CI/CD管道到达计划集时，将向有权设置计划的用户发送通知。 请参阅通 [知](notifications.md) ，了解更多。

* **代码质量分析** -用于识别未正确配置的出站HTTP/HTTPS请求的新规则。 请参阅自定 [义代码质量规则](custom-code-quality-rules.md) ，了解更多信息。

## 错误修复 {#bug-fixes}

* 在某些情况下，性能测试未在多个调度程序和发布实例之间完全分发。
* 标题导航在狭窄的浏览器窗口中消失。
* 在管线运行期间，某些管线设置未禁用。
* 指向AEM和“从程序列表”屏幕监视的链接替换了当前浏览器选项卡并打开了一个新选项卡。
* 在某些情况下，长时间的批准期可能导致部署失败。
