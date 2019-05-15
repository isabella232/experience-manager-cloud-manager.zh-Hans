---
title: 添加用户和角色
seo-title: 添加用户和角色
description: 'null'
seo-description: 您可以通过在Admin Console中将用户添加到Cloud Manager产品配置文件来分配特定角色会员资格。请按照本节了解更多信息。
uuid: fa204c28-83df-48bb-8360-e158 f080 dee7
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: requirements
discoiquuid: 1b421993-22c3-4de0-ba64-c1080 d07 ad5 e
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 添加用户和角色{#add-users-and-roles}

其中 [!UICONTROL Cloud Manager] 的许多功能需要特定权限才能运行。例如，仅允许某些用户为某个程序设置关键性能指标(KPI)。这些权限逻辑分为角色。

[!UICONTROL Cloud Manager] 目前为控制特定功能可用性的用户定义四个角色：

* 业务所有者
* 计划经理
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有一个Adobe ID和Adobe Managed Services产品上下文。

## 角色定义 {#role-definitions}

>[!NOTE]
>
>Admin Console中的开发人员角色与开发人员角色无关 [!UICONTROL Cloud Manager]。

下表总结了角色：

| [!UICONTROL Cloud Manager] 角色 | 描述 |
|--- |--- |
| 业务所有者 | 负责定义KPI、批准生产部署并覆盖重要的层故障。 |
| 计划经理 | 用于 [!UICONTROL Cloud Manager] 执行团队设置、审核状态和查看KPI。可以批准重要的层故障。 |
| 部署管理器 | 管理部署操作。用于 [!UICONTROL Cloud Manager] 执行舞台/生产部署。可以编辑CI/CD管线。可以批准重要的层故障。可以访问Git存储库。请联系您的CSE/AMS代表以请求它。 |
| 开发人员 | 开发和测试自定义应用程序代码。主要用于 [!UICONTROL Cloud Manager] 查看状态。应访问Git存储库以提交代码。添加具有此角色的用户以授予Git存储库访问权限时，请与CSE/AMS代表联系。 |
| 客户成功工程师 | 通常支持AMS客户的客户成功。与执行 [!UICONTROL Cloud Manager] 需要CSE监控的部署进行交互。 |
| 内容作者 | 通常不与之交互 [!UICONTROL Cloud Manager]。可以使用 [!UICONTROL Cloud Manager] 节目切换程序(导航自 [!UICONTROL Experience Cloud])访问AEM。 |

>[!NOTE]
>
>对 [!UICONTROL Cloud Manager] Git存储库的访问由您的CSE管理。与他们联系以添加和删除用户。
>
>如果新添加的用户需要访问Git存储库，您需要联系CSE/AMS代表才能授予访问权限。这些角色不提供对Git存储库的自动访问。最多可访问Git存储库的用户。

## 使用管理控制台创建配置文件 {#using-admin-console-to-create-a-profile}

角色是通过 [!UICONTROL Cloud Manager] Adobe Admin Console管理的。通过将用户添加到Admin Console中的 [!UICONTROL Cloud Manager] 产品配置文件，可以提供特定的角色会员资格。

您可以通过将用户添加到Adobe Admin Console中 [!UICONTROL Cloud Manager]**的产品配置文件** 分配特定角色会员资格，这是一个用于管理整个组织中的Adobe授权的中央位置。要了解有关Adobe Admin Console的更多信息，请参阅 [Admin Console的文档](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>要调用管理控制台并设置您的团队(用户和角色)，请打开浏览器并访问 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

为了向 [!UICONTROL Cloud Manager] 用户提供基于角色的适当权限，客户 **组织**中的管理员必须在 [!UICONTROL AEM Managed Services] 产品上下文下创建新的产品配置文件。

要向 [!UICONTROL Cloud Manager] 用户提供基于角色的适当权限，您必须以与四个角色每个对应的产品上下文在 [!UICONTROL AEM Managed Services] 产品上下文下创建个新的产品配置文件 [!UICONTROL Cloud Manager] ：

* 业务所有者
* 部署管理器
* 开发人员
* 计划经理

您可以使用 [Admin Console](https://adminconsole.adobe.com/) 创建或添加用户/用户组至这些产品配置文件 [!UICONTROL Cloud Manager]，如下图所示：

1. 登录到Admin Console，然后单击 **新建配置文件** 以添加新配置文件。

   ![](assets/admin_console_roles-1.png)

1. 填写字段以为其设置新角色 [!UICONTROL Cloud Manager]。

   输入 **配置文件名称**， **显示名称** 以创建新配置文件。此外，您还可以为配置文件选择 **权限组** 。

   单击 **完成** 以完成配置文件创建步骤。

   >[!NOTE]
   >
   >创建这些产品配置文件时， **显示名称** 必须是定义的技术值 [!UICONTROL Cloud Manager] (请参阅下表)。**配置文件名称** 可以是任何内容，但为了避免混淆，建议您使用下面 *建议的配置文件名称* 列中的值。为此，请在创建产品配置文件时取消选中 **与配置文件名称** 相同的值，然后指定相应的值作为 **显示名称**。

   | **角色** | **显示名称(必需)** | **建议的配置文件名称** |
   |---|---|---|
   | 业务所有者 | CM_ BUSINESS_ OVERNT_ POLE_ PROFILE | [!UICONTROL Cloud Manager] - 业务所有者角色 |
   | 部署管理器 | CM_ Deployment_ MANAGER_ POLE_ PROFILE | [!UICONTROL Cloud Manager] - 部署管理器角色 |
   | 开发人员 | CM_ Developer_ POLE_ PROFILE | [!UICONTROL Cloud Manager] - 开发人员角色 |
   | 计划经理 | CM_ PROGUMENT_ MANAGER_ POLE_ PROFILE | [!UICONTROL Cloud Manager] - 计划经理角色 |

   ![](assets/screen_shot_2018-05-04at171819.png)

1. 创建产品配置文件后，您可以将用户(或用户组)添加到这些产品配置文件。

   ![](assets/image2018-4-9_15-19-26.png)

   ![](assets/image2018-4-9_15-16-47.png)

