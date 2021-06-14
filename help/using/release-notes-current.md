---
title: 2021.6.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.6.0版的信息
feature: 发行信息
source-git-commit: 5ddbf718ad01b11dcba5dc2c5d1ab5d3cff2e9a9
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 4%

---

# 2021.6.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.6.0的常规发行说明。

>[!NOTE]
>请参阅[当前发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as a Cloud Service中Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.6.0的发布日期是2021年6月10日。
下一版本计划于2021年7月15日发布。

## 新增功能 {#whats-new}

* 现在，资产和站点测试将并行运行（如果适用），从而缩短总管道执行时间。 未来几周，将为客户启用此功能。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 在项目创建期间和通过管理git工作流在默认推送命令中使用的默认分支名称已更改为`main`。

* 在UI中编辑项目体验已刷新。 请参阅[编辑程序](/help/using/setting-up-program.md#editing-program)以了解更多信息。

* 质量规则`ImmutableMutableMixCheck`已更新，可将`/oak:index`节点分类为不可变。

* 质量规则`CQBP-84`和`CQBP-84--dependencies`已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 在某些情况下，如果无法计算跳过的测试量度，则会导致管道执行失败。

## 错误修复 {#bug-fixes}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 在某些情况下，当管道执行到达部署到生产步骤，用户停止执行时，UI中的部署状态消息无法正确反映实际发生的情况。
