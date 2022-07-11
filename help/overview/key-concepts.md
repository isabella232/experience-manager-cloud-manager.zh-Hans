---
title: 重要概念
description: 与所有强大的工具一样，Cloud Manager包含许多概念和术语。 本文档概述了在您开始使用Cloud Manager时，对您而言最重要的一些内容。
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 73e322cf93dc7709b7581860974079c8d94034ba
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---


# 重要概念 {#key-concepts}

与所有强大的工具一样，Cloud Manager包含许多概念和术语。 本文档概述了在您开始使用Cloud Manager时，对您而言最重要的一些内容。

## 应用程序 {#application}

而应用程序是客户为适应基础环境而创建的一组自定义和配置 [解决方案](#solution) (如AEM Sites或AEM Assets)。 应用程序是可由多个组成的逻辑单元 [工件。](#artifact)

虚构的应用就是一个例子 [WKND生活方式应用程序。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)

## 项目 {#artifact}

伪像是一个可部署的单元，是将源代码转换为单个单元的构建过程的结果。 例如，包含源代码的.zip文件。

## 对象存储库 {#artifact-repository}

对象存储库是客户特定的存储位置 [工件](#artifact) 已保存并已保护。

## 环境 {#environment}

环境是 [项目。](#program) 对于AEM，它由创作实例（可选地附加一个冷备用创作实例）、零个或多个发布实例、一个或多个调度程序实例以及负载平衡器组成。

## git存储库 {#git-repository}

git存储库是存储特定于客户的源代码并可访问的位置 [使用git。](https://git-scm.com)

## 实例 {#instance}

实例是运行AEM的特定虚拟服务器 [解决方案。](#solution) 实例从部署角度表示单个逻辑单元。

## 组织 {#organization}

组织是代表企业客户的Adobe结构。 一个公司可能拥有多个组织，具体取决于在Adobe的Identity Management系统(IMS)中配置这些组织的方式。

## 管道 {#pipeline}

管道是一组按顺序执行的部署步骤。

## 产品 {#product}

产品是 [解决方案](#solution) 由组织授权。 不同 [项目](#program) 组织内部可能有权使用不同的产品集，例如AEM Sites、AEM Assets或AEM Forms。

## 项目 {#program}

计划是一组支持客户计划逻辑分组的环境，通常对应于购买的服务级别协议(SLA)。 每个计划只有一个生产环境，并且可能有许多非生产环境。

## 解决方案 {#solution}

解决方案是Adobe之一 [!UICONTROL Experience Cloud] 解决方案。 例如，Adobe Experience Manager、Adobe Target或Adobe Analytics。

## 步骤 {#step}

步骤是配置的指令集，用于作为构建基块完成某些工作单元 [管线。](#pipeline)
