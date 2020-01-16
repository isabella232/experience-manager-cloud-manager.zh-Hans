---
title: 添加用户和角色
seo-title: 添加用户和角色
description: 'null'
seo-description: 您可以通过在管理控制台中将用户添加到Cloud Manager产品配置来分配特定角色成员关系。 请按照本节的说明了解更多信息。
uuid: fa204c28-83df-48bb-8360-e158f080dee7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 1b421993-22c3-4de0-ba64-c1080d07ad5e
translation-type: tm+mt
source-git-commit: a96500b57c980d31d3a70341d8be7b92ae73a1c5

---


# 添加用户和角色 {#add-users-and-roles}

中的许多功 [!UICONTROL Cloud Manager] 能需要特定权限才能运行。 例如，仅允许某些用户为程序设置关键绩效指标(KPI)。 这些权限按逻辑分组为角色。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义四个角色：

* 企业所有者
* 计划经理
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义 {#role-definitions}

>[!NOTE]
>
>Admin Console中的开发人员角色与中的开发人员角色无关 [!UICONTROL Cloud Manager]。

下表总结了这些角色：

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 企业所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 计划经理 | 用于 [!UICONTROL Cloud Manager] 执行团队设置、审核状态和查看KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 用于 [!UICONTROL Cloud Manager] 执行舞台／生产部署。 可以编辑CI/CD管道。 可以批准重要的3层故障。 可以访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要用 [!UICONTROL Cloud Manager] 于查看状态。 可以访问Git存储库以进行代码提交。 |
| 客户成功工程师 | 通常支持AMS客户的成功。 与之交 [!UICONTROL Cloud Manager] 互以执行需要CSE监督的部署。 |
| 内容作者 | 通常不与交互 [!UICONTROL Cloud Manager]。 可使用 [!UICONTROL Cloud Manager] 程序切换程序(已从中导航 [!UICONTROL Experience Cloud])访问AEM。 |

## 使用Admin Console创建配置文件 {#using-admin-console-to-create-a-profile}

角色可从Adobe [!UICONTROL Cloud Manager] Admin Console进行管理。 通过将用户添加到Admin Console中的产品配置，可以提供特 [!UICONTROL Cloud Manager] 定的角色成员关系。

您可以通过在Adobe Admin Console中将用户添加到产品配置文件( [!UICONTROL Cloud Manager] Adobe Admin Console **** )来分配特定角色成员资格，该配置文件是管理整个组织中的Adobe授权的一个中心位置。 要进一步了解Adobe Admin Console，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>要访问管理控制台并设置您的团队（用户和角色），请打开浏览器并访问 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

为了向用户提供相应的基于角色的权限， [!UICONTROL Cloud Manager] 客户组织中的管理员必须在“产品上下文”( ****[!UICONTROL AEM Managed Services] Product Context)下创建新的产品配置。

要向用户提供相应的基于角色的权限，作为管 [!UICONTROL Cloud Manager] 理员，您必须在“产品上下文”下为四个新的产品配置创建四个，分别对应于四个角 [!UICONTROL AEM Managed Services][!UICONTROL Cloud Manager] 色：

* 企业所有者
* 部署管理器
* 开发人员
* 计划经理

您可以使用 [Admin Console为创建或添加用户／用户组至这些产品配置](https://adminconsole.adobe.com/) , [!UICONTROL Cloud Manager]如下图所示：

1. 登录到Admin Console，然后单击“新 **建配置文件** ”以添加新配置文件。

   ![](assets/admin_console_roles-1.png)

1. 填写字段以设置新角色 [!UICONTROL Cloud Manager]。

   输入 **配置文件名称**、 **显示名称** ，以创建新配置文件。 此外，您还可以为配置 **文件选择权限组** 。

   单击 **完成** ，以完成配置文件创建步骤。

   >[!NOTE]
   >
   >创建这些产品配置时， **显示名称** ，必须是由定义的技术 [!UICONTROL Cloud Manager] 值（请参阅下表）。 “配 **置文件名称** ”可以是任何内容，但为避免混淆，建议使用下面“建议的配置文件名称” *列中的值* 。 为此，在创建产品配置时，请取消选中“与配置 **名称相同”** ，并指定相应的值作为“显 **示名称”**。

   | **角色** | **显示名称（必需）** | **推荐的配置文件名称** |
   |---|---|---|
   | 企业所有者 | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -业务所有者角色 |
   | 部署管理器 | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Deployment manager角色 |
   | 开发人员 | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -开发人员角色 |
   | 计划经理 | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -计划经理角色 |

   ![](assets/screen_shot_2018-05-04at171819.png)

1. 创建产品配置文件后，您可以将用户（或用户组）添加到这些产品配置文件。

   ![](assets/image2018-4-9_15-19-26.png)

   ![](assets/image2018-4-9_15-16-47.png)

