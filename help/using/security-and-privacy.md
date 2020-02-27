---
title: 安全性和隐私
seo-title: AEM Cloud manager的安全性和隐私
description: 可查看本页以了解资产的安全性和隐私（代码／对象）。
seo-description: 可查看本页以了解使用AEM Cloud manager的资产（代码／对象）的安全性和隐私。
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
translation-type: tm+mt
source-git-commit: 7cbc42108a6ccc8f7303eb76fd8ca2e9027f49e0

---


# 安全性和隐私 {#security-and-privacy}

[!UICONTROL Cloud Manager] 具有预配置的角色，并具有相应的权限。 本节重点介绍使用AEM Cloud manager的资产（代码／对象）的安全性和隐私。 此外， [!UICONTROL Cloud Manager] 还预配置了具有相应权限的角色。

要了解您可以在Admin Console中分配的角色和用户角色权限，请参阅基于角 [色的权限](/help/using/role-based-permissions.md)。


## 资源隔离 {#resource-isolation}

使用IMS [!UICONTROL Cloud Manager] 凭据的客户需要进行身份验证，因为将配置所有与其IMS组 [!UICONTROL Cloud Manager] 织关联的权限并将其绑定到其IMS组织。 在入门过程中，供应团队确保在中实施资源隔离 [!UICONTROL Cloud Manager]。

## 数据安全 {#data-security}

传输中的 [!UICONTROL Cloud Manager] 代码经过加密。 Coud manager构建的二进制文件在传输中也经过加密，并在存储时经过加密。

每位客户都会获得自己的 **Git存储库** ，并且其代码是安全的，不会与任何其他组织共 **享**。

## 数据隐私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守Adobe定义的隐私原则。 开发人员通过HTTPS将代码安全地推 **送到Git存储库** 。

用户界面(UI)构建 [!UICONTROL Cloud Manager] 在符合Adobe定义的通用控制框架的服务之上。 用户界面， [!UICONTROL Cloud Manager] 使用来自多个云提供商的安全服务。
