---
title: 2019.4.0 版发行说明
seo-title: AEM Cloud Manager 2019.4.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2019.4.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.4.0版的信息。
feature: 发行信息
exl-id: 8ca6386c-5de9-48b8-9034-466d4913d5a9
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 7%

---

# 2019.4.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0版本不包含重大功能更改。 有关更多详细信息，请参阅以下部分。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.4.0的发行日期是2019年4月18日。

## 新增功能 {#whats-new}

* Cloud Manager UI现在提供英语、法语、德语和日语版。
* 部署步骤现在包含当前正在运行的进程，即，当备份正在运行时，正在安装包，并正在重新配置负载平衡器

## 错误修复 {#bug-fixes}

* 已改进用于Dispatcher更改的部署方法，以处理其他用例。
* “环境”页面上未正确显示某些实例大小类型。
* 代码质量规则CQBP-84依赖项为嵌入的Adobe库（如WCM核心组件和资产共享共用）产生了误报。
* 当详细信息不可用时，代码扫描步骤的详细信息按钮已启用。
* 为每分钟的页面查看次数指定无效值时，KPI的下边界错误。
* 非生产管道上的部署类别资本化不正确。
* 未正确配置Git存储库时，**Overview**&#x200B;页面上的行动动员卡的文本不正确。

## 已知问题 {#known-issues}

* SLA值可能会被错误地四舍五入。
