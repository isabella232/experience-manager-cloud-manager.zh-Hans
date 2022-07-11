---
title: 基于角色的权限
description: 了解Cloud Manager预配置的基于角色的权限，以管理对云资源的访问。
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 522e5fbc650a8159602eb1aeaf42d64f4e23e8b4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 13%

---


# 基于角色的权限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 已预配置了具有相应权限的角色。 例如，开发人员开发代码，并有权将代码推送到git存储库。 业务所有者具有不同的权限，允许他们定义关键绩效指标(KPI)并批准部署。

## 用户角色 {#user-roles}

角色管理 [!UICONTROL Cloud Manager] 使用完成 [Admin Console。](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 的任意用户 [!UICONTROL Cloud Manager] 必须是客户IMS组织的成员，并且具有Adobe Managed Services产品上下文。 通过将用户添加到 [!UICONTROL Cloud Manager] 产品配置文件中的Admin Console。

要详细了解如何设置角色，请参阅此文档 [设置用户和角色。](/help/requirements/users-and-roles.md)

此表列出了可以在Admin Console中分配的角色。

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|---|---|
| 业务所有者 | 此用户是完成初始操作的主用户 [!UICONTROL Cloud Manager] 设置，并负责定义KPI、批准生产部署，以及在必要时覆盖重要的3层故障。 |
| 项目经理 | 此用户使用 [!UICONTROL Cloud Manager] 要执行团队设置、审核状态、查看KPI，并在必要时批准重要的3层故障。 |
| 部署管理器 | 此用户使用 [!UICONTROL Cloud Manager] 要执行暂存和生产部署，可能会在必要时批准重要的3层故障，并有权访问git存储库。 |
| 开发人员 | 此用户开发和测试自定义应用程序代码，主要使用 [!UICONTROL Cloud Manager] 查看部署状态，并具有对git存储库的提交访问权限。 |
| 客户成功工程师 | 此用户通常支持AMS客户取得客户成功，并与 [!UICONTROL Cloud Manager] 执行需要客户成功工程师(CSE)监督的部署。 |
| 内容作者 | 此用户通常不会与交互 [!UICONTROL Cloud Manager]，但可能使用 [!UICONTROL Cloud Manager] 程序切换程序(从 [!UICONTROL Experience Cloud])访问Adobe Experience Manager(AEM)。 |

## 用户权限 {#user-permissions}

每个角色都具有特定的关联预配置权限。 此表列出了可用权限以及可以执行这些权限的角色。


| 权限 | 描述 | 业务所有者 | 部署管理器 | 项目经理 | 开发人员 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 读取应用程序 | 读取计划KPI | x | x | x | x | x |
| 写入应用程序 | 程序设置或编辑 | x |  |  |  |  |
| 添加程序 | 添加新程序 | x |  |  |  |  |
| 读取环境 | 请参阅环境详细信息 | x | x | x | x | x |
| 创建执行 | 启动管道 | x | x | x |  |  |
| 读取执行 | 请参阅执行状态 | x | x | x | x | x |
| 恢复执行 | 可以在暂停时继续执行 | x | x | x |  | x |
| 执行批准部署到生产环境 | 提供上线批准 | x | x | x |  |  |
| 执行计划部署到生产环境 | 计划生产部署 | x | x | x |  | x |
| 执行部署到生产环境 | 暂停应用程序以供CSE监督时，将应用程序部署到生产环境 |  |  |  |  | x |
| 执行取消 | 取消当前执行 |  |  | x |  |  |
| 执行覆盖质量门失败 | 批准重要质量门故障 | x | x | x |  |  |
| 管道创建 | 设置/编辑管道 |  | x |  |  |  |
| 管道读取 | 请参阅管道详细信息 | x | x | x | x | x |
| 管道写入 | 设置/编辑管道。 |  | x |  |  |  |
| 管道修改批准 | 允许编辑“业务所有者”选项 |  | x |  |  |  |
| 管道修改托管部署 | 允许编辑CSE监督选项 |  | x |  |  |  |
| 管道删除 | 允许删除管道 |  | x |  |  |  |
| 步骤读取 | 查看步骤质量量度结果 | x | x | x | x | x |
| 生成个人访问令牌 | 访问Git |  | x |  | x |  |

要详细了解如何设置用户，请参阅此文档 [设置用户和角色。](/help/requirements/users-and-roles.md)
