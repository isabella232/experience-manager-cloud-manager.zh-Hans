---
title: 主要概念
seo-title: 主要概念
description: 本页列出了与Cloud manager关联的关键术语。
seo-description: 可查看本页以了解与Cloud manager相关的关键术语。
uuid: 2a37810b-98f8-4f01-90de-1e52c754ad16
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 简介
discoiquuid: b702dfc0-3534-4d90-af19-8559d8baf6a6
translation-type: tm+mt
source-git-commit: aa4ff4eb2f3292fe4cb0baf8087b4d0213443cf4

---


# 主要概念 {#key-concepts}

本页介绍了Cloud manager中使用的一些基本术语。 我们强烈建议您先阅读本页，然后再查看Cloud manager文档的其余部分。

**应用** ：由客户（或其自定义器）创建的自定义和配置集，用于根据其特定用例和需求调整底层解决方案。 应用程序是可由多个伪像组成的逻辑单元。

例如， *We.Retail*。

**伪像** ，一个可展开的单元。 将源代码转换为单个单元的某些构建过程的结果。 例如，包含源代码的Zip文件。

**对象存储库** ：保存和保护客户特定对象的存储位置。

**环境** ：程序中的单个虚拟机群集。 对于AEM，这由作者实例（可选地，还有一个额外的冷备用作者实例）、零个或多个发布实例、一个或多个调度程序实例和负载平衡器组成。

**Git存储库** -存储客户特定源代码的位置，可使用Git协议访问。

**实例** ：运行AEM解决方案的特定虚拟服务器。 实例从部署角度表示单个逻辑单元。

**组织** Adobe构建代表企业客户的组织。 一家公司可能有多个组织，具体取决于最初在Adobe Identity Management system中设置它们的方式。

**Pipeline** A set of deployment set which are sequencely executed.

**产品** -组织许可的解决方案中的一组特定功能。 组织内的不同程序可以被标识为不同的产品集。 例如，站点、表单的资产。

**计划** -支持客户活动的逻辑分组的一组环境，通常对应于购买的服务级别协议(SLA)。 每个计划只有一个生产环境，并且可能有许多非生产环境。

**解决方案** Adobe解决方案之 [!UICONTROL Experience Cloud] 一。 例如，Adobe Experience Manager、Adobe Target或Adobe Analytics。

**步骤** ：配置的指令集，用于完成流水线的某些单元和构件。
