---
title: 安全性和隐私
seo-title: AEM Cloud Manager的安全性和隐私
description: 可查看本页以了解资产（代码/工件）的安全性和隐私。
seo-description: 请阅读本页内容，了解使用AEM Cloud Manager的资产（代码/工件）的安全性和隐私。
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: 入门
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# 安全性和隐私 {#security-and-privacy}

[!UICONTROL Cloud Manager] 已预配置了具有相应权限的角色。本节重点介绍使用AEM Cloud Manager的资产（代码/工件）的安全性和隐私。 此外，[!UICONTROL Cloud Manager]还预配置了具有相应权限的角色。

要了解在Admin Console和用户角色权限中可分配的可能角色，请参阅[基于角色的权限](/help/using/role-based-permissions.md)。


## 资源隔离{#resource-isolation}

使用[!UICONTROL Cloud Manager]的客户将需要其IMS凭据进行身份验证，因为将配置与[!UICONTROL Cloud Manager]关联的所有权限，并将其绑定到其IMS组织。 在入门过程中，配置小组确保在[!UICONTROL Cloud Manager]中强制执行资源隔离。

## 数据安全{#data-security}

[!UICONTROL Cloud Manager]中的代码在传输中被加密。 Cloud Manager构建的二进制文件在传输中也会进行加密，并在存储时进行加密。

每个客户都会获得自己的&#x200B;**Git存储库**，并且其代码是安全的，不会与任何其他&#x200B;**组织**&#x200B;共享。

## 数据隐私{#data-privacy}

[!UICONTROL Cloud Manager] 遵守由Adobe定义的隐私原则。开发人员通过HTTPS将代码安全地推送到&#x200B;**Git存储库**。

[!UICONTROL Cloud Manager]的用户界面(UI)基于符合由Adobe定义的通用控制框架的服务而构建。 [!UICONTROL Cloud Manager]的用户界面使用来自多个云提供程序的安全服务。
