---
title: 重要概念
seo-title: 重要概念
description: 本页列表了与Cloud Manager相关的主要术语。
seo-description: 可查看本页以了解与Cloud Manager相关的关键术语。
uuid: 2a37810b-98f8-4f01-90de-1e52c754ad16
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: b702dfc0-3534-4d90-af19-8559d8baf6a6
translation-type: tm+mt
source-git-commit: ace032fbb26235d87d61552a11996ec2bb42abce
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---


# 重要概念 {#key-concepts}

本页介绍Cloud Manager中使用的一些基本术语。 我们强烈建议您在查看Cloud Manager文档的其余部分之前阅读此页面。

**应用** -由客户创建的自定义和配置集，以根据其特定用例和需求调整底层解决方案。 应用程序是可由多个伪像组成的逻辑单元。

例如， *We.Retail*。

**伪像** ，一个可部署的单元。 将源代码转换为单个单元的某些构建过程的结果。 例如，包含源代码的Zip文件。

**Artifact Repository** (存储库)保存和保护客户特定对象的位置。

**环境** :项目中的单个虚拟机群集。 对于AEM，它由作者实例（可选地附加一个冷备用作者实例）、零个或多个发布实例、一个或多个调度程序实例和负载平衡器组成。

**Git Repository** 存储客户特定源代码的位置，可使用Git协议访问。

**实例** 运行AEM解决方案的特定虚拟服务器。 实例从部署角度代表单个逻辑单元。

**组织** Adobe结构，代表企业客户。 一个公司可能有多个组织，具体取决于在Adobe的Identity Management系统中最初设置这些组织的方式。

**管道** (Pipeline)按顺序执行的一组部署步骤。

**产品** -组织授权的解决方案中的一组特定功能。 组织内的不同项目可以获得不同的产品集。 例如，Sites, Assets ofForms。

**项目** 一组环境，它们支持客户计划的逻辑分组，通常与购买的服务级别协议(SLA)相对应。 每个项目仅有一个生产环境，并且可能有许多非生产环境。

**解决方** 案Adobe解决方案 [!UICONTROL Experience Cloud] 之一。 例如，Adobe Experience Manager、Adobe Target或Adobe Analytics。

**步骤** ：配置指令集，用于完成流水线的一些单元、构件。
