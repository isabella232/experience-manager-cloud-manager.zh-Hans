---
title: 2018.6.0发行说明
seo-title: 适用于2018.6.0的AEM Cloud Manager发行说明
description: 浏览本页可获取Cloud Manager版本2018.6.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2018.6.0的信息。
uuid: 211b6e1b-10b-46b0-b591-44d5 e44 abd77
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79 e68 c86469
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.6.0发行说明 {#release-notes-for}

以下部分概述 [!UICONTROL Cloud Manager] 了发行版2018.6.0的一般发行说明，并增加了部署过程中调度程序失效的支持、额外通知和可用性改进。

## 发布日期 {#release-date}

版本2018.6.0 [!UICONTROL Cloud Manager] 的发布日期为2018年月日。

## 新增功能 {#what-s-new}

* **CI/CD管线** -可配置的调度程序失效和缓存在CI/CD管线执行期间同时在舞台和生产上刷新。请参阅 [配置CI/CD管道](configuring-pipeline.md) 以了解更多信息。

* **CI/CD管线** -在管道设置过程中，现在可以定义管道在某个质量门中遇到严重故障时的行为方式。请参阅 [配置CI/CD管道](configuring-pipeline.md) 以了解更多信息。

* **CI/CD管线** -在管道设置过程中，现在可以选择由CSE还是任何可用CSE执行CSE监控。请参阅 [配置CI/CD管道](configuring-pipeline.md) 以了解更多信息。

* **CI/CD管线** -当CI/CD管线到达业务批准步骤时，将向有权批准部署的用户发送通知。请参阅 [通知](notifications.md) 以了解更多信息。

* **CI/CD管线** -当CI/CD管线达到计划集时，将向有权设置计划的用户发送通知。请参阅 [通知](notifications.md) 以了解更多信息。

* **代码质量分析** -识别错误配置的出站HTTP/HTTPS请求的新规则。请参阅 [自定义代码质量规则](custom-code-quality-rules.md) 以了解更多信息。

## 错误修复 {#bug-fixes}

* 在某些情况下，性能测试未完全分布在多个调度程序和发布实例之间。
* 标题导航在窄浏览器窗口中消失。
* 某些管道设置在管道运行时未禁用。
* 从计划列表屏幕到AEM和监视的链接替换了当前浏览器选项卡，并打开了一个新选项卡。
* 在某些情况下，长期批准的批准可能导致部署失败。
