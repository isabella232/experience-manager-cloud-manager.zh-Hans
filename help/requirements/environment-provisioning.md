---
title: 环境配置
description: 了解如何在 Cloud Manager 新用户引导过程中配置环境。
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: d033b7cf53d4d9faf074f1dc09e2958eb91afe3b
workflow-type: ht
source-wordcount: '314'
ht-degree: 100%

---


# 环境配置 {#environments-provisioning}

了解如何在 Cloud Manager 新用户引导过程中配置环境。

## 配置 {#provisioning}

在新用户引导过程中，Adobe 会自动配置您购买的所有 AEM 云环境，并且这些环境将链接回它们在 [!UICONTROL Cloud Manager] 中的项目。这些 AEM 云环境包含在每个 Adobe Managed Services 订阅中，通常由至少一个生产环境、一个暂存环境以及（可选）一个或多个开发或测试环境组成。

## 欢迎电子邮件 {#welcome-email}

环境配置过程完成后，指定的客户管理员会收到一封欢迎电子邮件，用于确认他们已被授予 Adobe [!UICONTROL Experience Cloud] 访问权限。欢迎电子邮件包含有关如何开始使用 [!UICONTROL Experience Cloud] 服务、[!UICONTROL AEM Managed Services] 云环境以及 [!UICONTROL Cloud Manager] 自助式门户的详细信息。该电子邮件还包含了重要信息，例如客户成功工程师 (CSE) 联系信息、从何处获得支持资源、论坛、常见问题等。在该电子邮件中提供的资源列表中，您还将获得有关如何访问 AEM 云环境的 [!UICONTROL Cloud Manager] 的详细信息。

## 后续步骤 {#next-steps}

收到欢迎电子邮件后，您便能使用 Adobe IMS 凭据以系统管理员身份登录到 [!UICONTROL Cloud Manager]。登录后，您将能够验证您的 AEM 云生产环境和非生产环境是否可用并且已成功运行。

在部署代码时，[!UICONTROL Cloud Manager] 将使用这些 AEM 云环境执行 CI/CD 管道，其顺序依次为 [!UICONTROL Cloud Manager] 的 Git 存储库、暂存环境和 AEM 生产环境。此外，当您准备好开始为您的 Web 资产创建数字体验时，可以直接从 [!UICONTROL Cloud Manager] 访问您的 AEM 云环境。
