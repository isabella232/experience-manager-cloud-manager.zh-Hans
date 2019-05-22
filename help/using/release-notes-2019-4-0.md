---
title: 2019.4.0发行说明
seo-title: 适用于2019.4.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.4.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.4.0的信息。
translation-type: tm+mt
source-git-commit: 8031df1c1ce9d7fee4ef33de289c6952370b7589

---


# 2019.4.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0版本不包含重大功能更改。请按照以下部分了解更多详细信息。

## 发布日期 {#release-date}

版本2019.4.0 [!UICONTROL Cloud Manager] 的发布日期为2019年月18日。

## 新增功能 {#whats-new}

* Cloud Manager UI现在提供英语、法语、德语和日语版本。
* 部署步骤现在包含当前正在运行的进程，即，当备份正在运行时，正在安装包，以及负载平衡器正在重新配置

## 错误修复 {#bug-fixes}

* Dispatcher更改的部署方法已得到改进，可处理其他用例。
* 某些实例大小类型在“环境”页面上无法正确显示。
* CQBP-84-依赖项的代码质量规则为嵌入式Adobe库(如WCM核心组件和资源共享Commons)生成了虚假提示。
* 当详细信息不可用时，启用了代码扫描步骤的详细信息按钮。
* 为每分钟页面查看指定无效值的错误消息的边界较小。
* 非生产管道上的部署类别不正确。
* 当git存储库未正确配置时 **，概述** 页面上的行动卡调用有错误的文本。

## 已知问题 {#known-issues}

* SLA值可能会被错误舍入。
