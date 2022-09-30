---
title: 安全性和隐私
description: 了解 Cloud Manager 中的代码和工件资产的安全性和隐私性。
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: d7751757c1d3bda3d60406a1d39cb41c61f5c863
workflow-type: ht
source-wordcount: '189'
ht-degree: 100%

---


# 安全性和隐私 {#security-and-privacy}

了解 Cloud Manager 中的代码和工件资产的安全性和隐私性。

## 角色和权限 {#roles}

[!UICONTROL Cloud Manager] 预配置了一些具有适当权限的角色。

要了解可以在 Admin Console 中分配的角色和用户角色权限，请参阅[基于角色的权限](/help/requirements/role-based-permissions.md)文档。

## 资源隔离 {#resource-isolation}

[!UICONTROL Cloud Manager] 客户需要使用 IMS 凭据进行身份验证，因为所有与 [!UICONTROL Cloud Manager] 关联的权限都会关联到其 IMS 组织。在新用户引导过程中，配置团队需确保在 [!UICONTROL Cloud Manager] 中实施资源隔离。

## 数据安全性 {#data-security}

对 [!UICONTROL Cloud Manager] 中的代码进行传输中加密。Cloud Manager 生成的二进制文件也将进行传输中加密，并且会在存储时进行加密。

每个客户都有自己的 Git 存储库，并且代码是安全的且不会与任何其他组织共享。

## 数据隐私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守 Adobe 制定的隐私原则。开发人员通过 HTTPS 将代码安全地推送到 Git 存储库中。

[!UICONTROL Cloud Manager] 的用户界面基于遵循 Adobe 通用控制框架的服务而构建。[!UICONTROL Cloud Manager] 的用户界面使用来自多个云提供商的安全服务。
