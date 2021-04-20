---
title: 与Adobe Cloud Manager集成
description: 一个视频系列，可指导客户管理的（内部部署）git存储库与Adobe Cloud Manager的设置和集成。
seo-title: 与Adobe Cloud Manager集成
seo-description: 一个视频系列，可指导客户管理的（内部部署）git存储库与Adobe Cloud Manager的设置和集成。
feature: Git Repositories
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 5%

---


# 与Adobe Cloud Manager集成

Adobe Cloud Manager附带一个git存储库，用于使用Cloud Manager的CI/CD管道部署代码。 客户可以立即使用Cloud Manager的git存储库。 客户还可以选择将内部部署或&#x200B;**客户管理的** git存储库与Cloud Manager集成。

## Git集成概述

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此视频系列探讨了在将客户管理的git存储库与Cloud Manager集成时的几个使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支开发](#feature-development)
* [生产部署](#production-deployment)
* [同步发布标记](#sync-tags)

有关完整概述，请查阅[Cloud Manager用户指南](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。 该视频系列假设您对git和源代码管理有了基本的了解。 有关git的更多详细信息，请参阅以下[其他资源。](#additional-resources)

>[!NOTE]
>
> 此视频系列中概述的步骤和命名约定代表了使用客户管理的git存储库和Cloud Manager的一些最佳实践。 预计所描述的公约和工作流将适用于个别发展小组。

## 初始同步{#initial-sync}

将客户管理的Git存储库与Cloud Manager的Git存储库同步的最初步骤。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略{#branching-strategy}

设置基本的分支策略，以利用Cloud Manager的[生产和非生产管道](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支开发{#feature-development}

使用功能分支隔离客户管理的git存储库中的代码更改，并与Cloud Manager的git存储库同步，以便使用非生产渠道进行代码质量和验证测试。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生产部署{#production-deployment}

在由客户管理的git存储库中准备生产版本的代码，并与Cloud Manager的git存储库同步，以部署到暂存和生产环境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 正在同步发布标记{#sync-tags}

将Cloud Manager Git存储库中的发行标记同步到客户管理的git存储库中，以便能够查看已部署到暂存和生产环境的代码。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他资源 {#additional-resources}

* [Cloud Manager 文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)
* [GitHub资源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)