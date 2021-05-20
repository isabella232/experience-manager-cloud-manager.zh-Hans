---
title: 基于角色的权限
description: 可查看本页以了解有关基于角色的权限的信息。
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: 用户角色
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 17%

---

# 基于角色的权限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 已预配置了具有相应权限的角色。例如，开发人员开发代码，并有权将代码推送到&#x200B;**Git存储库**。 或者，业务所有者具有不同的权限，允许他们定义关键绩效指标(KPI)并批准部署。

## 用户角色 {#user-roles}

[!UICONTROL Cloud Manager]的角色管理在[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)内完成。 [!UICONTROL Cloud Manager]的任何用户都必须是客户IMS组织的成员，并具有Adobe Managed Services产品上下文。 通过将用户添加到Admin Console中的[!UICONTROL Cloud Manager]产品用户档案，可提供特定角色成员关系。

要详细了解如何设置角色，请参阅[设置用户和角色](setting-up-users-and-roles.md)。

下表列出了可在Admin Console中分配的可能角色。

| **[!UICONTROL Cloud Manager]角色** | **描述** |
|---|---|
| 业务所有者 | 完成初始[!UICONTROL Cloud Manager]设置的主用户。 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 项目经理 | 使用[!UICONTROL Cloud Manager]执行团队设置、查看状态和查看KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使用[!UICONTROL Cloud Manager]执行暂存和生产部署。 可以批准重要的3层故障。 有权访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使用[!UICONTROL Cloud Manager]查看状态。 具有对Git存储库的提交访问权限。 |
| 客户成功工程师 | 通常支持AMS客户取得成功。 与[!UICONTROL Cloud Manager]交互以执行需要客户成功工程师(CSE)监督的部署。 |
| 内容作者 | 通常不与[!UICONTROL Cloud Manager]进行交互。 此用户可以使用[!UICONTROL Cloud Manager]程序切换器（从[!UICONTROL Experience Cloud]导航）访问Adobe Experience Manager(AEM)。 |

## 用户权限 {#user-permissions}

每个角色都有相关联的特定权限、预配置的任务或权限。此表列出了可用的功能以及能够执行该功能的角色。

要详细了解如何设置用户，请参阅[设置用户和角色](setting-up-users-and-roles.md)。

| 权限 | 描述 | 业务所有者 | 部署管理器 | 项目经理 | 开发人员 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 读取应用程序 | 阅读计划KPI。 | x | x | x | x | x |
| 写入应用程序 | 程序设置或编辑。 | x |  |  |  |  |
| 添加程序 | 添加新程序。 | x |  |  |  |  |
| 读取环境 | 请参阅环境详细信息。 | x | x | x | x | x |
| 创建执行 | 启动管道。 | x | x | x |  |  |
| 读取执行 | 请参阅执行状态。 | x | x | x | x | x |
| 恢复执行 | 可以在暂停时继续执行。 | x | x | x |  | x |
| 执行批准部署到生产环境 | 提供GoLive批准。 | x | x | x |  |  |
| 执行计划部署到生产环境 | 计划生产部署。 | x | x | x |  | x |
| 执行部署到生产环境 | 暂停CSE监督时，将应用程序部署到生产环境。 |  |  |  |  | x |
| 执行取消 | 取消当前执行。 |  |  | x |  |  |
| 执行覆盖质量门失败 | 批准重要的质量门故障。 | x | x | x |  |  |
| 管道创建 | 设置/编辑管道。 |  | x |  |  |  |
| 管道读取 | 请参阅管道详细信息。 | x | x | x | x | x |
| 管道写入 | 设置/编辑管道。 |  | x |  |  |  |
| 管道修改批准 | 允许编辑“业务所有者”选项。 |  | x |  |  |  |
| 管道修改托管部署 | 允许编辑CSE监督选项。 |  | x |  |  |  |
| 管道删除 | 允许删除管道。 |  | x |  |  |  |
| 步骤读取 | 请参阅步骤质量量度结果。 | x | x | x | x | x |
| 生成个人访问令牌 | 访问Git。 |  | x |  | x |  |
