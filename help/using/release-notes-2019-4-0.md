---
title: 2019.4.0发行说明
seo-title: AEM Cloud manager 2019.4.0版本说明
description: 可查看本页以获取Cloud Manager 2019.4.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.4.0版的信息。
translation-type: tm+mt
source-git-commit: b368c46c2a9f40d0c3867db6eb2a333bd71fe22a

---


# 2019.4.0发行说明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 4.0版本不包含重大功能更改。 有关更多详细信息，请按照以下部分进行操作。

## 发布日期 {#release-date}

版本2019.4.0 [!UICONTROL Cloud Manager] 的发布日期为2019年4月18日。

## 新增功能 {#whats-new}

* Cloud Manager UI现在提供英语、法语、德语和日语版。
* 部署步骤现在包含当前正在运行的进程，即，当备份运行时，正在安装包，并且正在重新配置负载平衡器

## 错误修复 {#bug-fixes}

* 已改进用于Dispatcher更改的部署方法以处理其他用例。
* 某些实例大小类型未在“环境”页面上正确显示。
* 代码质量规则CQBP-84-dependencies为嵌入的Adobe库（如WCM核心组件和资源共享公域）产生了误报。
* 当详细信息不可用时，代码扫描步骤的详细信息按钮处于启用状态。
* 为每分钟的页面查看次数指定无效值时的错误消息KPI的下界错误。
* 非生产管道上的部署类别被错误地加大为大写。
* 当git存储库未正确配置时，“ **概述** ”页面上的行动动员卡包含错误的文本。

## 已知问题 {#known-issues}

* SLA值可能被错误舍入。
