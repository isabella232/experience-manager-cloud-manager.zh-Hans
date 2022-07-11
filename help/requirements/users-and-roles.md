---
title: 添加用户和角色
description: 了解如何使用Admin Console添加用户和角色以及创建用户档案。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 9%

---


# 添加用户和角色 {#add-users-and-roles}

的许多功能 [!UICONTROL Cloud Manager] 需要特定权限才能使用。 例如，只允许某些用户为项目设置关键绩效指标(KPI)。 这些权限在逻辑上分组为角色。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义了四个角色：

* 业务所有者
* 项目经理
* 部署管理器
* 开发人员

>[!NOTE]
>
>使用 [!UICONTROL Cloud Manager]，则必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义 {#role-definitions}

此表汇总了角色。

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 业务所有者 | 此用户负责定义KPI、批准生产部署，并在必要时覆盖重要的3层故障。 |
| 项目经理 | 此用户使用 [!UICONTROL Cloud Manager] 要执行团队设置、审核状态、查看KPI，并可在必要时批准重要的3层故障。 |
| 部署管理器 | 此用户管理部署操作和使用 [!UICONTROL Cloud Manager] 要执行暂存/生产部署、编辑CI/CD管道、在必要时批准重要的3层故障，并可以访问git存储库。 |
| 开发人员 | 此用户开发和测试自定义应用程序代码，主要使用 [!UICONTROL Cloud Manager] 查看部署状态，并可以访问用于代码提交的git存储库。 |
| 客户成功工程师 | 此用户通常支持AMS客户取得客户成功，并与 [!UICONTROL Cloud Manager] 执行需要CSE监督的部署。 |
| 内容作者 | 此用户通常不会与交互 [!UICONTROL Cloud Manager] 但是可以使用 [!UICONTROL Cloud Manager] 用于访问AEM的程序切换器。 |

>[!NOTE]
>
>Admin Console中的开发人员角色与 [!UICONTROL Cloud Manager].

## 使用Admin Console创建用户档案 {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] 角色可从Admin Console中进行管理。 通过将用户添加到 [!UICONTROL Cloud Manager] 产品配置文件。

Admin Console是管理整个组织中Adobe权限的中心位置。 要进一步了解Adobe Admin Console，请参阅 [Admin Console。](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)

>[!NOTE]
>
>要访问Admin Console并设置您的团队（用户和角色），请访问 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

为了向 [!UICONTROL Cloud Manager] 用户，客户组织中的管理员必须在 [!UICONTROL AEM Managed Services] 对应于这四个产品中每个产品上下文 [!UICONTROL Cloud Manager] 角色：

* 业务所有者
* 部署管理器
* 开发人员
* 项目经理

您可以使用Admin Console创建用户/组或将其添加到这些产品配置文件。

1. 登录到Admin Console并单击 **新建用户档案** 添加新用户档案。

   ![新建用户档案](/help/assets/admin_console_roles-1.png)

1. 提供信息以为 [!UICONTROL Cloud Manager].

   * **配置文件名称**
   * **显示名称**
   * **权限组**

1. 单击 **完成** 完成用户档案创建步骤。

创建产品配置文件时， **显示名称** 必须是 [!UICONTROL Cloud Manager] （请参阅下表）。 的 **配置文件名称** 可为任何内容，但为避免混淆，建议在 **推荐的配置文件名称** 列。 为此，在创建产品配置时，请取消选中“与配置 **名称相同”** ，并指定相应的值作为“显 **示名称”**。

| **角色** | **显示名称（必需）** | **推荐的配置文件名称** |
|---|---|---|
| 业务所有者 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 业务所有者角色 |
| 部署管理器 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 部署管理员角色 |
| 开发人员 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 开发人员角色 |
| 项目经理 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 项目经理角色 |

![创建新用户档案](/help/assets/screen_shot_2018-05-04at171819.png)

创建产品配置文件后，您可以向这些产品配置文件添加用户（或组）。

![编辑用户](/help/assets/image2018-4-9_15-19-26.png)

![用户组](/help/assets/image2018-4-9_15-16-47.png)
