---
title: 2021.3.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.3.0版的信息
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# 2021.3.0 版发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 版本2021.3.0。

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2021.3.0版是2021年3月11日。
下一版本计划于2021年4月8日发布。

## 新增功能 {#whats-new}

* 新的代码质量工具 [Dispatcher优化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) 已引入以验证客户dispatcher配置。

* 用户现在可以通过选择 **查看Cloud Manager角色** 选项。

* 标签 **申请批准** 已重新标记为 **生产审批** 更清楚。

* 的 **版本** 标签已重新标记为 **Git标记** 在生产管道执行屏幕中。

* 重新标记了在重要量度未达到定义的阈值时定义行为的标签，以反映其真实行为 —  **立即取消** 和 **立即批准**. 请参阅 [配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) 以了解更多详细信息。

* 类和方法弃用列表已根据版本进行了更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID。

## 错误修复 {#bug-fixes}

* 将包嵌入到其他包中时，未正确发现某些质量问题。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，指出操作失败，尽管实际开始执行。
