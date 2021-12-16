---
title: 2021.4.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.4.0版的信息
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# 2021.4.0 版发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 版本2021.4.0。

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2021.4.0版是2021年4月8日。

## 新增功能 {#whats-new}

* 性能测试虚拟用户的请求超时已从20秒增加到60秒。

* 即使未配置管道，“管理Git”按钮也会显示在“管道”卡上。

* 在管道执行页面的部署步骤中，除了UI中的当前步骤，用户还将能够查看已完成的和未来的部署步骤 *正在进行* 状态。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，Eclipse项目提供的OSGi包已从规则中排除 `CQBP-84--dependencies`.

## 错误修复 {#bug-fixes}

* 在 *资产测试* 步骤。

* 生产管道负载测试中尾随斜杠导致404失败。

* 的 `Runmode` 检查在非文件夹节点上产生误报。