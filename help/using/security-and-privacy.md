---
title: 安全性和隐私
seo-title: AEM Cloud Manager的安全性和隐私
description: 可查看本页以了解资产的安全性和隐私(代码/伪像)。
seo-description: 查看本页，了解使用AEM Cloud Manager的资产(代码/人工代码)的安全性和隐私。
uuid: 68bc2330-a62 c-4c-4c-925c-daa6788 b143 a
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3cc98
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 安全性和隐私 {#security-and-privacy}

[!UICONTROL Cloud Manager] 具有相应权限的预配置角色。例如，开发人员开发代码并有权将代码推送到 **Git存储库**。或者，企业主具有不同的权限，允许他们定义关键绩效指标(KPI)和批准部署。

## 基于角色的权限 {#role-based-permissions}

### 用户角色 {#user-roles}

在Adobe [!UICONTROL Cloud Manager][Admin Console内进行角色管理](https://helpx.adobe.com/enterprise/using/admin-console.html)。任何用户 [!UICONTROL Cloud Manager] 都必须是客户IMS组织的成员，并具有Adobe Managed Services产品上下文。通过将用户添加到Admin Console中的 [!UICONTROL Cloud Manager] 产品配置文件，可以提供特定的角色会员资格。

要详细了解如何设置角色，请参阅 [设置用户和角色](setting-up-users-and-roles.md)。

下表列出了可在Admin Console中分配的潜在角色。

| **[!UICONTROL Cloud Manager]角色** | **描述** |
|---|---|
| 业务所有者 | 完成初始 [!UICONTROL Cloud Manager] 设置的主要用户。负责定义KPI、批准生产部署并覆盖重要的层故障。 |
| 计划经理 | 用于 [!UICONTROL Cloud Manager] 执行团队设置、审核状态和查看KPI。可能批准重要的层故障。 |
| 部署管理器 | 管理部署操作。用于 [!UICONTROL Cloud Manager] 执行舞台和生产部署。可能批准重要的层故障。有权访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。主要用于 [!UICONTROL Cloud Manager] 查看状态。承诺访问Git存储库。 |
| 客户成功工程师 | 通常支持AMS客户的客户成功。与执行 [!UICONTROL Cloud Manager] 部署需要客户成功工程师(CSE)监督的目的交互。 |
| 内容作者 | 通常不与之交互 [!UICONTROL Cloud Manager]。此用户可使用 [!UICONTROL Cloud Manager] 计划切换程序(导航自 [!UICONTROL Experience Cloud])访问Adobe Experience Manager(AEM)。 |

### 用户权限 {#user-permissions}

每个角色都具有与每个角色关联的特定权限、预配置任务或权限。下表列出了可用的函数以及可以执行该函数的角色。

要进一步了解如何设置用户，请参阅 [设置用户和角色](setting-up-users-and-roles.md)。

| 权限 | 描述 | 业务所有者 | 部署管理器 | 计划经理 | 开发人员 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 阅读应用程序 | 查看计划的详细信息。 | x | x | x | x | x |
| 编写应用程序 | 配置程序(包括KPI)。 | x |
| 阅读环境 | 请参阅环境详细信息。 | x | x | x | x | x |
| 创建执行 | 启动管道。 | x | x | x |
| 阅读执行 | 请参阅执行状态。 | x | x | x | x | x |
| 继续执行 | 可以在暂停时继续执行。 | x | x | x | x |
| 执行批准部署到生产 | 提供GoLive Approval。 | x | x | x |
| 执行计划部署到生产 | 计划生产部署。 | x | x | x | x |
| 执行部署到生产 | 在进行CSE监控时将应用程序部署到生产。 | x |
| 执行取消 | 取消当前执行。 | x | x | x |
| 执行覆盖质量门失败 | 批准重要质量门槛故障。 | x | x | x |
| 管道创建 | 设置/编辑管道。 | x |
| 管道读取 | 请参阅管道详细信息。 | x | x | x | x | x |
| 管道写入 | 设置/编辑管道。 | x |
| 管道修改批准 | 允许编辑“企业主”选项。 | x |
| 管道修改托管部署 | 允许编辑“CSE监控”选项。 | x |
| 解决方案阅读 | 阅读计划KPI。 | x | x | x | x | x |
| 解决方案写入 | 配置计划(包括KPI)设置/编辑管道。 | x |
| 步骤阅读 | 查看步骤质量指标的结果。 | x | x | x | x | x |

## 资源隔离 {#resource-isolation}

使用的 [!UICONTROL Cloud Manager] 客户将需要其IMS凭据进行身份验证，因为绑定到的 [!UICONTROL Cloud Manager] 所有权限将被配置并绑定到其IMS组织。在入门培训过程中，供应团队确保实施了资源隔离 [!UICONTROL Cloud Manager]。

## 数据安全性 {#data-security}

传入的代码 [!UICONTROL Cloud Manager] 在传输过程中加密。Courd Manager构建的二进制文件也在传输中加密，并在存储时加密。

每个客户都获得自己的 **Git存储库** 及其代码，而不会与任何其他 **组织共享**。

## 数据隐私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守Adobe定义的隐私权原则。开发人员通过HTTPS安全地将代码推送到 **Git存储库** 中。

the[！DNL用户界面(UI) [!UICONTROL Cloud Manager]构建在服务顶部，这些服务符合由Adobe定义的通用控制框架。[！DNL用户界面(UI)使用 [!UICONTROL Cloud Manager]来自多个云提供商的安全服务。
