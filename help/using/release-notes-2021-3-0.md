---
title: 2021.3.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.3.0版的信息
feature: 发行信息
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 503d9b25855633737c49e3e278a3a76052ed84d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# 2021.3.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.3.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.3.0的发行日期是2021年3月11日。
下一版本计划于2021年4月8日发布。

## 新增功能 {#whats-new}

* 引入了新的代码质量工具[Dispatcher优化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules)来验证客户Dispatcher配置。

* 现在，用户在导航到Unified Shell的“用户配置文件”图标（右上方）后，通过选择&#x200B;**查看Cloud Manager角色**&#x200B;选项，可以看到其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更加清晰。

* 在“生产管道”执行屏幕中， **版本**&#x200B;标签已重新标记为&#x200B;**Git标记**。

* 重新标记了在重要量度不满足定义的阈值时定义行为的标签，以反映其真实行为 — **Cancel立即**&#x200B;和&#x200B;**Approve立即**。 有关更多详细信息，请参阅[配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) 。

* 类和方法弃用列表已根据AEMCloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

## 错误修复 {#bug-fixes}

* 将包嵌入到其他包中时，未正确发现某些质量问题。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，指出操作失败，尽管实际开始执行。
