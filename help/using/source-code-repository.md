---
title: 源代码存储库
seo-title: Adobe AEM Cloud Manager的源代码存储库
description: 请查看本页以了解为您在Cloud Manager中提供的每个程序提供的Git存储库。
seo-description: 请查看本页以了解为您在Adobe AEM Cloud Manager中提供的每个程序提供的Git存储库。
uuid: 2c42775f-8703-43f7-bug2-7dc086 ea9 d7
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1 ff-47f6-8d97-ff501851 bf2
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 源代码存储库 {#source-code-repository}

## Cloud Manager存储库 {#cloud-manager-repository}

您的 [!UICONTROL AEM Managed Services] 订阅将包括由Adobe配置和管理的源代码存储库。为每个客户计划分配一个唯一的和独特 **的Git存储库**，在该存储库中将存储并保护您的关联代码。

作为最佳实践，您应始终使用Cloud Manager的Git存储库，该存储库在未配置任何分支或示例项目的情况下为空。要使用Cloud Manager的Git存储库，将提供一个 **私人访问令牌** ，它允许您使用任何兼容Git的客户端创建分支、存储和检索代码、列出提交历史记录等。

有关如何在Git中设置分支的详细信息，请参阅 [配置发行分支](configure-your-release-branches.md)。

有关如何使用Cloud Manager **的Git存储库** 与CI/CD管线的更多信息，请参阅 [配置CI/CD管线](configuring-pipeline.md)。

## 本地存储库 {#on-premise-repository}

在某些情况下，您将拥有现有的Git存储库并希望继续使用它。在这些情况下，您可以对多个远程存储库使用Git支持的功能。日常开发将继续在您的Git存储库中进行。当发布分支准备好部署到生产时，您会将最新代码推送到Cloud Manager的Git存储库，并触发Cloud Manager CI/CD管线。

>[!NOTE]
>
>要查看常用的Git命令，请参阅 [Git Cheat工作表](https://education.github.com/git-cheat-sheet-education.pdf)。

