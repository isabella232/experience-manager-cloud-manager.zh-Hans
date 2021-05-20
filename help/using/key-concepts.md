---
title: 重要概念
seo-title: 重要概念
description: 本页列出了与Cloud Manager关联的关键术语。
seo-description: 请阅读本页以了解与Cloud Manager关联的关键术语。
uuid: 2a37810b-98f8-4f01-90de-1e52c754ad16
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: b702dfc0-3534-4d90-af19-8559d8baf6a6
feature: 入门
level: Beginner
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 重要概念 {#key-concepts}

本页介绍Cloud Manager中使用的一些基本术语。 我们强烈建议您在查看Cloud Manager文档的其余部分之前阅读此页面。

**** 应用程序由客户创建的一组自定义和配置，用于根据其特定用例和需求调整基础解决方案。应用程序是一个逻辑单元，可以由多个工件组成。

例如， *We.Retail*。

**** Artifact可部署单元。将源代码转换为单个单位的构建过程的结果。 例如，包含源代码的Zip文件。

**对象** 存储库保存和保护客户特定对象的存储位置。

**** 环境：程序中的单个虚拟机群集。对于AEM，它由创作实例（可选地附加一个冷备用创作实例）、零个或多个发布实例、一个或多个调度程序实例以及负载平衡器组成。

**Git存** 储库存储特定于客户的源代码的位置，可使用Git协议访问。

**** 实例运行AEM解决方案的特定虚拟服务器。实例从部署角度表示单个逻辑单元。

**** 组织Adobe构建代表企业客户。一个公司可能有多个组织，具体取决于AdobeIdentity Management系统中最初配置组织的方式。

**** 管道一组按顺序执行的部署步骤。

**** 产品组织许可的解决方案中的一组特定功能。一个组织内的不同方案可能有权使用不同的产品集。 例如，网站、Forms的资产。

**** 计划支持客户计划的逻辑分组的一组环境，通常与购买的服务级别协议(SLA)相对应。每个计划只有一个生产环境，并且可能有许多非生产环境。

**** 解决方案Adobe解决 [!UICONTROL Experience Cloud] 方案之一。例如，Adobe Experience Manager、Adobe Target或Adobe Analytics。

**** 步骤一个配置的指令集，用于完成管道的某个工作单元（构建基块）。
