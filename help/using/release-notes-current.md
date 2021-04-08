---
title: 2021.4.0 版发行说明
description: 可查看本页以获取Cloud Manager 2021.4.0版的相关信息
feature: 发行信息
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
translation-type: tm+mt
source-git-commit: 1f7f87a4b944d1fadc708958a96a1bda7d41da5d
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---

# 2021.4.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2021.4.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.4.0的发布日期为2021年4月08日。
下一版本计划于2021年5月06日发布。

## 新增功能 {#whats-new}

* 性能测试虚拟用户的请求超时已从20秒增加到60秒。

* 即使未配置管道，“管理Git”按钮也会显示在管道卡上。

* 在“管道”执行页的部署步骤期间，除了UI中&#x200B;*正在进行*&#x200B;状态的当前步骤之外，用户还可以查看已完成和将来的部署步骤。

* Cloud Manager使用的AEM项目原型版本已更新为版本27。

* 澄清了删除环境时启动管线时的错误消息。

* 现在，规则`CQBP-84--dependencies`中不包括Eclipse项目提供的OSGi捆绑包。

## 错误修复 {#bug-fixes}

* 在生产流水线中的&#x200B;*资产测试*&#x200B;步骤可能发生的罕见临时错误。

* 生产管道负载测试中的尾部斜杠导致404故障。

* `Runmode`检查在非文件夹节点上产生误报。