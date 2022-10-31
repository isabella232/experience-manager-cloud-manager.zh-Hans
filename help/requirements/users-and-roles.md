---
title: 添加用户和角色
description: 了解如何使用 Admin Console 添加用户和角色以及创建配置文件。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: dd96d773ea3e6b9c45886fe41b28d3dd70cb8a61
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 22%

---


# 添加用户和角色 {#add-users-and-roles}

的许多功能 [!UICONTROL Cloud Manager] 需要特定权限才能使用。 例如，仅允许某些用户为项目设置关键绩效指标 (KPI)。这些权限将在逻辑上按角色分组。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义了四个角色：

* 业务负责人
* 项目经理
* 部署经理
* 开发人员

>[!NOTE]
>
>使用 [!UICONTROL Cloud Manager]，则必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义 {#role-definitions}

此表汇总了角色。

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 业务负责人 | 此用户负责定义 KPI、审批生产部署和覆盖重要三层失败（如有必要）。 |
| 项目经理 | 此用户使用 [!UICONTROL Cloud Manager] 要执行团队设置、审核状态、查看KPI，并可在必要时批准重要的3层故障。 |
| 部署管理员 | 此用户管理部署操作和使用 [!UICONTROL Cloud Manager] 要执行暂存/生产部署、编辑CI/CD管道、在必要时批准重要的3层故障，并可以访问git存储库。 |
| 开发人员 | 此用户开发和测试自定义应用程序代码，主要使用 [!UICONTROL Cloud Manager] 查看部署状态，并可以访问用于代码提交的git存储库。 |
| 客户成功工程师 | 此用户通常支持AMS客户取得客户成功，并与 [!UICONTROL Cloud Manager] 执行需要CSE监督的部署。 |
| 内容作者 | 此用户通常不会与交互 [!UICONTROL Cloud Manager] 但是可以使用 [!UICONTROL Cloud Manager] 用于访问AEM的程序切换器。 |

>[!NOTE]
>
>Admin Console中的开发人员角色与 [!UICONTROL Cloud Manager].

## 使用 Admin Console 创建配置文件 {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] 角色可从Admin Console中进行管理。 通过将用户添加到 [!UICONTROL Cloud Manager] 产品配置文件。

Admin Console 是一个中央位置，用于管理整个组织内的 Adobe 授权。要详细了解 Adobe Admin Console，请参阅 [Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 文档。

为了向 [!UICONTROL Cloud Manager] 用户，客户组织中的管理员必须在 [!UICONTROL AEM Managed Services] 对应于这四个产品中每个产品上下文 [!UICONTROL Cloud Manager] 角色：

* 业务负责人
* 部署经理
* 开发人员
* 项目经理

您可以使用 Admin Console 创建用户/组或将用户/组添加到这些产品配置文件中。

1. 登录到Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 单击 **概述** ，单击 **产品和服务** 卡。 如果它未列在此处，请使用 **产品** 选项卡，找到产品并单击它。

   ![“管理控制台概述”选项卡](/help/assets/admin-console-overview.png)

1. 在 **产品** 选项卡上，单击要将用户/群组添加到其产品配置文件的环境。

   ![“管理控制台产品”选项卡](/help/assets/admin-console-product.png)

1. 在 **产品配置文件** ，请单击 **新建用户档案** 添加新用户档案。

   ![新配置文件](/help/assets/admin-console-product-profiles.png)

1. 提供信息以为 [!UICONTROL Cloud Manager].

   * **配置文件名称** - **配置文件名称** 可为任何内容，但为避免混淆，建议在 **推荐的配置文件名称** 列。
   * **显示名称** - **显示名称** 必须是 [!UICONTROL Cloud Manager] （请参阅下表）。
   * **权限组**  — 您可以为配置文件选择权限组（并非始终可用）。

   ![创建新配置文件](/help/assets/screen_shot_2018-05-04at171819.png)

   | 角色 | 显示名称（必需） | 建议的配置文件名称 |
   |---|---|---|
   | 业务负责人 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 业务所有者角色 |
   | 部署管理员 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 部署管理员角色 |
   | 开发人员 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 开发人员角色 |
   | 程序管理员 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 项目经理角色 |


1. 单击 **完成** 以保存新用户档案。

## 将配置文件分配给用户或用户组 {#assign-profiles}

创建产品配置文件后，您可以为其分配用户或用户组。

1. 登录到Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 在Admin Console中，选择 **用户** 选项卡。

   ![“用户”选项卡](/help/assets/admin-console-users.png)

1. 单击 **用户** 在左侧导航面板中，然后单击某个用户以对其进行修改。

1. 单击 **产品** 选择 **编辑**.

   ![编辑用户](/help/assets/admin-console-edit-user.png)

1. 在 **编辑产品和用户组** 对话框中，单击加号按钮，然后选择要分配给用户的配置文件。

   * 如果用户已被分配到角色，则加号按钮将是一个编辑按钮（铅笔），但其工作方式相同。

   ![编辑产品和用户组](/help/assets/admin-console-edit-products-and-user-groups.png)

1. 单击 **保存** 将用户档案保存到用户。

重复相同步骤以将用户档案分配给用户组，但选择 **用户组** 的左侧导航面板 **用户** 选项卡。 单击用户群组，然后选择 **已分配的产品配置文件** 选项卡，单击 **分配产品配置文件** 来分配用户档案。

![将用户档案分配给组](/help/assets/admin-console-edit-user-groups.png)
