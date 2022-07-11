---
title: 环境配置
description: 了解如何在Cloud Manager载入过程中配置环境。
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: d033b7cf53d4d9faf074f1dc09e2958eb91afe3b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# 环境配置 {#environments-provisioning}

了解如何在Cloud Manager载入过程中配置环境。

## 配置 {#provisioning}

在载入过程中，您购买的所有AEM云环境都会按Adobe自动进行配置，并且会链接回其在中的项目 [!UICONTROL Cloud Manager]. 这些AEM云环境包含在每个Adobe Managed Services订阅中，通常至少由一个生产环境、一个暂存环境以及可选的一个或多个开发或测试环境组成。

## 欢迎电子邮件 {#welcome-email}

在环境配置过程完成后，指定的客户管理员将收到一封欢迎电子邮件，确认他们已获得Adobe访问权限 [!UICONTROL Experience Cloud]. 欢迎电子邮件包含有关如何开始使用的详细信息 [!UICONTROL Experience Cloud] 服务， [!UICONTROL AEM Managed Services] 云环境，以及 [!UICONTROL Cloud Manager] 自助服务门户。 此外，电子邮件还包含重要信息，如客户成功工程师(CSE)联系信息，以及支持资源、论坛、常见问题解答等的去向。 在电子邮件中提供的资源列表中，您还将获得有关如何访问的详细信息 [!UICONTROL Cloud Manager] 适用于您的AEM云环境。

## 后续步骤 {#next-steps}

收到欢迎电子邮件后，您便可以登录到 [!UICONTROL Cloud Manager] 作为系统管理员，使用您的Adobe IMS凭据。 登录后，您将能够验证AEM云生产和非生产环境是否可用且运行成功。

这些AEM云环境将由 [!UICONTROL Cloud Manager] 要在部署代码时执行CI/CD管线，请从 [!UICONTROL Cloud Manager]的git存储库（通过暂存环境），直到您的AEM生产环境。 您还可以直接从 [!UICONTROL Cloud Manager] 当您准备好开始为web资产创建数字体验时。
