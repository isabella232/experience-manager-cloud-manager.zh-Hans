---
title: 2021.3.0 版发行说明
seo-title: AEM Cloud Manager 2021.3.0发行说明
description: 可查看本页以获取Cloud Manager 2021.3.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2021.3.0版的信息
translation-type: tm+mt
source-git-commit: 47424ea0e087f1f69db0aef8ca2122de2352a6e0
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 3%

---

# 2021.3.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2021.3.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.3.0的发布日期为2021年3月11日。

## 新增功能 {#whats-new}

* 拥有必需权限的用户现在可以编辑项目，允许他们以自助方式执行以下操作：

   * 将“站点”解决方案添加到包含资产的现有项目（反之亦然）。
   * 将站点（或资产）从包含站点和资产的现有项目中删除。
   * 可以对现有项目或作为新项目添加（返回）解决方案。

* 新的代码质量工具[调度程序优化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules)已引入以验证客户调度程序配置。

* 用户现在可以在导航到Unified Shell的“用户用户档案”图标（右上方）后，选择&#x200B;**“视图 Cloud Manager角色”**&#x200B;选项，查看其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更清晰。

* **版本**&#x200B;标签已重新标记到“生产”管线执行屏幕中的&#x200B;**Git标签**。

* 当重要量度未达到定义的阈值时定义行为的标签已重新标记，以反映其真实行为 — **取消立即**&#x200B;和&#x200B;**批准立即**。 有关详细信息，请参阅[配置管道设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager)。

* 类和方法弃用列表已根据AEM Cloud Service SDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

## 错误修复 {#bug-fixes}

* 在将包嵌入到其他包中时，未正确发现某些质量问题。

* 有时，如果用户在启动管道后立即从管道执行页面导航离开，将显示一条错误消息，指出操作失败，尽管实际执行会开始。