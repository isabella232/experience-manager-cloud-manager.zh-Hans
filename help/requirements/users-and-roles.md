---
title: 添加用户和角色
description: 了解如何使用 Admin Console 添加用户和角色以及创建配置文件。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: ht
source-wordcount: '536'
ht-degree: 100%

---


# 添加用户和角色 {#add-users-and-roles}

必须具有特定的权限，才能使用 [!UICONTROL Cloud Manager] 中的许多功能。例如，仅允许某些用户为项目设置关键绩效指标 (KPI)。这些权限将在逻辑上按角色分组。

[!UICONTROL Cloud Manager] 目前为用户定义了四个角色来控制特定功能的可用性：

* 业务负责人
* 项目经理
* 部署经理
* 开发人员

>[!NOTE]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有 Adobe ID 和 Adobe Managed Services 产品上下文。

## 角色定义 {#role-definitions}

此表汇总了角色。

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 业务负责人 | 此用户负责定义 KPI、审批生产部署和覆盖重要三层失败（如有必要）。 |
| 项目经理 | 此用户使用 [!UICONTROL Cloud Manager] 执行团队设置、审查状态、查看 KPI，并且可以在必要时审批重要三层失败。 |
| 部署经理 | 此用户管理部署操作，并使用 [!UICONTROL Cloud Manager] 执行暂存/生产部署，编辑 CI/CD 管道，在必要时审批重要三层失败，并且有权访问 Git 存储库。 |
| 开发人员 | 此用户开发和测试自定义应用程序代码，并主要使用 [!UICONTROL Cloud Manager] 来查看部署状态，并且有权访问 Git 存储库进行代码提交。 |
| 客户成功工程师 | 此用户通常帮助 AMS 客户获得成功，并与 [!UICONTROL Cloud Manager] 交互以便执行需要 CSE 监督的部署。 |
| 内容作者 | 此用户通常不会与 [!UICONTROL Cloud Manager] 进行交互，但可以使用 [!UICONTROL Cloud Manager] 项目切换器来访问 AEM。 |

>[!NOTE]
>
>Admin Console 中的开发人员角色与 [!UICONTROL Cloud Manager] 中的开发人员角色无关。

## 使用 Admin Console 创建配置文件 {#using-admin-console-to-create-a-profile}

从 Admin Console 管理 [!UICONTROL Cloud Manager] 角色。通过将用户添加到 [!UICONTROL Cloud Manager] 产品配置文件来提供特定的角色成员资格。

Admin Console 是一个中央位置，用于管理整个组织内的 Adobe 授权。要详细了解 Adobe Admin Console，请参阅 [Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 文档。

>[!NOTE]
>
>要访问 Admin Console 并设置您的团队（用户和角色），请访问 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

要向 [!UICONTROL Cloud Manager] 用户提供基于角色的适当权限，客户组织内的管理员必须在 [!UICONTROL AEM Managed Services] 产品上下文中创建与四个 [!UICONTROL Cloud Manager] 角色中的每一个相对应的新产品配置文件：

* 业务负责人
* 部署经理
* 开发人员
* 项目经理

您可以使用 Admin Console 创建用户/组或将用户/组添加到这些产品配置文件中。

1. 登录到 Admin Console 并单击&#x200B;**新配置文件**&#x200B;来添加新的配置文件。

   ![新配置文件](/help/assets/admin_console_roles-1.png)

1. 提供信息以便为 [!UICONTROL Cloud Manager] 设置新角色。

   * **配置文件名称**
   * **显示名称**
   * **权限组**

1. 单击&#x200B;**完成**&#x200B;以完成配置文件创建步骤。

在创建产品配置文件时，**显示名称**&#x200B;必须是 [!UICONTROL Cloud Manager] 定义的技术值（见下表）。**配置文件名称**&#x200B;可以是任何内容，但为避免混淆，建议使用&#x200B;**建议的配置文件名称**&#x200B;列中的值。为此，在创建产品配置文件时，请取消选中&#x200B;**与配置文件名称相同**，并指定对应的值作为&#x200B;**显示名称**。

| **角色** | **显示名称（必需）** | **建议的配置文件名称** |
|---|---|---|
| 业务负责人 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 业务负责人角色 |
| 部署经理 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 部署经理角色 |
| 开发人员 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 开发人员角色 |
| 项目经理 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 项目经理角色 |

![创建新配置文件](/help/assets/screen_shot_2018-05-04at171819.png)

在创建产品配置文件后，您可以将用户（或组）添加到这些产品配置文件中。

![编辑用户](/help/assets/image2018-4-9_15-19-26.png)

![用户组](/help/assets/image2018-4-9_15-16-47.png)
