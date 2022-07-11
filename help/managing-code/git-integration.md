---
title: 与Git Cloud Manager的集成Adobe
description: 此视频系列将介绍如何设置和集成由Adobe管理（内部部署）的git存储库与Adobe Cloud Manager。
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 91e909273bf2b21d7f6413731923011915079e45
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# 与Git Cloud Manager的集成Adobe

AdobeCloud Manager配置了单个git存储库，该存储库用于使用Cloud Manager的CI/CD管道部署代码。 您可以使用Cloud Manager的即装即用git存储库，也可以选择将内部部署或客户管理的git存储库与Cloud Manager集成。

## Git集成概述

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此视频系列探讨了有关将客户管理的git存储库与Cloud Manager集成的几个用例。

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步发行标记](#sync-tags)

此视频系列假定您对git和源代码管理有基本的了解。 请参阅 [下文](#additional-resources) 有关git的更多详细信息。

此视频系列中概述的步骤和命名约定体现了使用客户管理的git存储库和Cloud Manager的一些最佳实践。 预计所描述的公约和工作流程将适合各个开发小组。

有关Cloud Manager的完整概述，请查看此文档 [Cloud Manager简介。](/help/introduction.md)

## 初始同步 {#initial-sync}

将客户管理的git存储库与Cloud Manager的git存储库同步的首要步骤。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

设置基本的分支策略以利用Cloud Manager的 [生产](/help/using/production-pipelines.md) 和 [非生产管道。](/help/using/non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发 {#feature-development}

使用功能分支可隔离客户管理的git存储库中的代码更改，并与Cloud Manager的git存储库同步，以便使用非生产管道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署 {#production-deployment}

在客户管理的git存储库中为生产版本准备代码，并与Cloud Manager的git存储库同步，以便部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步发行标记 {#sync-tags}

将Cloud Manager git存储库中的发行标记同步到客户管理的git存储库中，以便提供有关已部署到暂存和生产环境的代码的可见性。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [Cloud Manager简介](/help/introduction.md)
* [GitHub资源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)
