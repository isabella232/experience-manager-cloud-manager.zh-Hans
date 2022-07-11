---
title: 安全性和隐私
description: 了解Cloud Manager中代码和对象资产的安全性和隐私。
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: d7751757c1d3bda3d60406a1d39cb41c61f5c863
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 3%

---


# 安全性和隐私 {#security-and-privacy}

了解Cloud Manager中代码和对象资产的安全性和隐私。

## 角色和权限 {#roles}

[!UICONTROL Cloud Manager] 已预配置了具有相应权限的角色。

要了解在Admin Console权限和用户角色权限中可分配的可能角色，请参阅此文档 [基于角色的权限。](/help/requirements/role-based-permissions.md)

## 资源隔离 {#resource-isolation}

[!UICONTROL Cloud Manager] 客户需要其IMS凭据来进行身份验证，因为所有权限都与 [!UICONTROL Cloud Manager] 与IMS组织绑定。 在载入过程中，配置团队可确保在 [!UICONTROL Cloud Manager].

## 数据安全 {#data-security}

中的代码 [!UICONTROL Cloud Manager] 在传输中加密。 Cloud Manager构建的二进制文件在传输中也会进行加密，并在存储时进行加密。

每个客户都会获得其自己的git存储库，并且代码是安全的，不会与任何其他组织共享。

## 数据隐私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守由Adobe定义的隐私原则。 开发人员通过HTTPS将代码安全地推送到Git存储库。

[!UICONTROL Cloud Manager]的用户界面基于符合Adobe共同控制框架的服务而构建。 [!UICONTROL Cloud Manager]的用户界面使用来自多个云提供商的安全服务。
