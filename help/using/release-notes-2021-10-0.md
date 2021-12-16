---
title: 2021.10.0 版发行说明
description: 请阅读本页以了解Cloud Manager版本2021.10.0的相关信息
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# 2021.10.0 版发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 版本2021.10.0。

>[!NOTE]
>请参阅 [最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) 以在AEMas a Cloud Service中查看Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 版本2021.10.0为2021年10月14日。

## 新增功能 {#whats-new}

* 现在，可以以“紧急”模式执行生产管道，从而绕过用于紧急部署的安全和性能测试步骤。

* 为了与Cloud Service保持一致，现在将在UI中引用现有部署管道并将其标记为“完整堆栈”管道。

* 管道卡已刷新，现在可显示单个集成的表面，该表面既显示生产管道，也显示非生产管道，用户可以直接从与每个管道关联的操作菜单中选择“运行/暂停/恢复”。

* 具有部署管理器角色的用户现在可以通过UI以自助方式删除生产管道。

* 添加和编辑管道体验已刷新，现在可以使用熟悉的现代模型。

* Cloud Manager的用户现在可以通过 **反馈** 按钮。

* 现在可以从Cloud Manager用户界面下载每年的SLA图表。

* 现在，代码质量和非生产管道执行将在构建步骤中使用更高效的浅层克隆过程，从而为具有特别大的git存储库的客户缩短构建时间。

* Cloud Manager API文档现在包含一个交互式操场，允许已登录的用户从其浏览器中试用该API。 请参阅 [Cloud Manager API操场](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以了解更多详细信息。

* 如果禁用了“导航到”下的选择选项，则程序卡上的工具提示更具描述性。 此时将显示“生产环境不存在”。


## 错误修复 {#bug-fixes}

* 如果从内部系统读取的数据未正确输入，则可能会导致CSE提供的不相关数据未正确反映在Cloud Manager中。

* 在特定客户情况下，在生成步骤期间下载的应导致生成失败的无效工件将被忽略。
