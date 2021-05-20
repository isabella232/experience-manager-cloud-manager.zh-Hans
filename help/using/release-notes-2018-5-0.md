---
title: 2018.5.0 版发行说明
seo-title: AEM Cloud Manager 2018.5.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2018.5.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2018.5.0版的信息。
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
feature: 发行信息
exl-id: 0034bcaf-00d3-410d-b2f6-a2a232888a2b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---

# 2018.5.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2018.5.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2018.5.0的发行日期是2018年7月12日。

## 新增功能 {#what-s-new}

* **CI/CD管道通知**  — 用户现在将看到管 [!UICONTROL Experience Cloud] 道事件的通知。请参阅[通知](notifications.md)以了解更多信息。

* **计划生产部署**  — 用户现在可以为生产部署计划日期或时间。请参阅[部署代码](deploying-code.md)以了解更多信息。

* **** 状态页面已被 **标题为Activity**。

* 主页上显示的有关管道执行期间遇到的问题的更多特定信息。
* 性能测试基础架构改进。

## 错误修复 {#bug-fixes}

* 在某些情况下，使用的SonarQube配置文件不正确，导致代码质量度量不正确。
* SonarQube检查CQBP-75忽略了某些OSGi注释。
* 取消CI/CD管线时，状态显示不一致。

## 已知问题 {#known-issues}

* 从“程序列表”屏幕到&#x200B;**AEM**&#x200B;和&#x200B;**监视**&#x200B;的链接，都会替换当前浏览器选项卡并打开一个新选项卡。
