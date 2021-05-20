---
title: 添加用户和角色
seo-title: 添加用户和角色
description: 了解用户和角色以及如何使用Admin Console创建用户档案
seo-description: 您可以通过将用户添加到Admin Console中的Cloud Manager产品配置文件来分配特定角色成员关系。 请阅读本节内容，以了解更多信息。
uuid: fa204c28-83df-48bb-8360-e158f080dee7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 1b421993-22c3-4de0-ba64-c1080d07ad5e
feature: 用户角色
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 28%

---

# 添加用户和角色 {#add-users-and-roles}

[!UICONTROL Cloud Manager]中的许多功能需要特定权限才能运行。 例如，只允许某些用户为项目设置关键绩效指标(KPI)。 这些权限在逻辑上分组为角色。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义了四个角色：

* 业务所有者
* 项目经理
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用[!UICONTROL Cloud Manager]，您必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义{#role-definitions}

>[!NOTE]
>
>Admin Console中的开发人员角色与[!UICONTROL Cloud Manager]中的开发人员角色无关。

下表概述了角色：

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 业务所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 项目经理 | 使用[!UICONTROL Cloud Manager]执行团队设置、查看状态和查看KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使用[!UICONTROL Cloud Manager]执行暂存/生产部署。 可以编辑CI/CD管线。 可以批准重要的3层故障。 可以访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使用[!UICONTROL Cloud Manager]查看状态。 可以访问Git存储库以进行代码提交。 |
| 客户成功工程师 | 通常支持AMS客户取得成功。 与[!UICONTROL Cloud Manager]交互，以执行需要CSE监督的部署。 |
| 内容作者 | 通常不与[!UICONTROL Cloud Manager]进行交互。 可以使用[!UICONTROL Cloud Manager]程序切换器（从[!UICONTROL Experience Cloud]导航）访问AEM。 |

## 使用Admin Console创建配置文件{#using-admin-console-to-create-a-profile}

可从Adobe Admin Console为[!UICONTROL Cloud Manager]管理角色。 通过将用户添加到Admin Console中的[!UICONTROL Cloud Manager]产品用户档案，可提供特定角色成员关系。

您可以通过在 [!UICONTROL Cloud Manager]Adobe Admin Console中将用户添加到&#x200B;**** Product Profile来分配特定角色成员关系，Adobe Admin Console是管理整个组织中Adobe授权的一个中心位置。 要进一步了解Adobe Admin Console，请参阅 [Admin Console文档](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)。

>[!NOTE]
>
>要访问admin console并设置您的团队（用户和角色），请打开浏览器并访问[https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

为了向 [!UICONTROL Cloud Manager] （客户&#x200B;**组织**&#x200B;中的管理员）用户提供相应的基于角色的权限，必须在 [!UICONTROL AEM Managed Services] Product Context 下创建新“产品配置文件”。

要向[!UICONTROL Cloud Manager]用户提供相应的基于角色的权限，作为管理员，您必须在[!UICONTROL AEM Managed Services]产品上下文下创建新的四个产品配置文件，每个产品上下文对应于四个[!UICONTROL Cloud Manager]角色中的每个角色：

* 业务所有者
* 部署管理器
* 开发人员
* 项目经理

您可以创建用户/组，或将其添加到这些产品配置文件中，其中[Admin Console](https://adminconsole.adobe.com/)用于[!UICONTROL Cloud Manager]，如下图所示：

1. 登录到Admin Console，然后单击&#x200B;**新建配置文件**&#x200B;以添加新配置文件。

   ![](assets/admin_console_roles-1.png)

1. 填写字段以为[!UICONTROL Cloud Manager]设置新角色。

   输入 **配置文件名称**、 **显示名称** ，以创建新配置文件。 此外，您还可以为配置 **文件选择权限组** 。

   单击&#x200B;**完成**&#x200B;以完成配置文件创建步骤。

   >[!NOTE]
   >
   >创建这些产品配置时， **显示名称** ，必须是 [!UICONTROL Cloud Manager] 定义的技术值（请参阅下表）。 “配 **置文件名称** ”可以是任何内容，但为避免混淆，建议使用下面“建议的配置文件名称” *列中的值* 。 为此，在创建产品配置时，请取消选中“与配置 **名称相同”** ，并指定相应的值作为“显 **示名称”**。

   | **角色** | **显示名称（必需）** | **推荐的配置文件名称** |
   |---|---|---|
   | 业务所有者 | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager]  — 业务所有者角色 |
   | 部署管理器 | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager]  — 部署管理员角色 |
   | 开发人员 | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager]  — 开发人员角色 |
   | 项目经理 | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager]  — 项目经理角色 |

   ![](assets/screen_shot_2018-05-04at171819.png)

1. 创建产品配置文件后，您可以向这些产品配置文件添加用户（或组）。

   ![](assets/image2018-4-9_15-19-26.png)

   ![](assets/image2018-4-9_15-16-47.png)
