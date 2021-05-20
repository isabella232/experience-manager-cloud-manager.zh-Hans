---
title: 2021.4.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.4.0版的信息
feature: 发行信息
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 5f81fdb86b1dfa6c748bb7784ef00dc062c9f8ef
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# 2021.4.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.4.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.4.0的发行日期是2021年4月8日。

## 新增功能 {#whats-new}

* 性能测试虚拟用户的请求超时已从20秒增加到60秒。

* 即使未配置管道，“管理Git”按钮也会显示在“管道”卡上。

* 在管道执行页的部署步骤中，除了UI中的当前步骤（*进行中*）状态外，用户还将能够看到已完成和未来的部署步骤。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，由Eclipse项目提供的OSGi包已从规则`CQBP-84--dependencies`中排除。

## 错误修复 {#bug-fixes}

* 在生产管道中的&#x200B;*资产测试*&#x200B;步骤中可能发生的极少的临时错误。

* 生产管道负载测试中尾随斜杠导致404失败。

* `Runmode`检查对非文件夹节点产生误报。