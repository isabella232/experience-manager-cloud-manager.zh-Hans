---
title: 源代码存储库
seo-title: Source Code Repository for Adobe AEM Cloud Manager
description: 可查看本页面以了解为Cloud Manager中的每个程序配置的git存储库。
seo-description: Follow this page to learn about the git repository that is provisioned for each program you have in Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: Provisioning
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 源代码存储库 {#source-code-repository}

## Cloud Manager存储库 {#cloud-manager-repository}

您的 [!UICONTROL AEM Managed Services] 订阅将包括由Adobe设置和管理的源代码存储库。 每个客户的项目都分配了一个唯一的 **Git存储库**，将存储和保护您的关联代码。

作为最佳实践，您应始终使用Cloud Manager的Git存储库，该存储库为空，且未配置任何分支或示例项目。 要使用Cloud Manager的Git存储库，您将获得 **专用访问令牌** 它将允许您使用任何与Git兼容的客户端创建分支、存储和检索您的代码、列出提交历史记录等。

有关如何在Git中设置分支的更多信息，请参阅 [配置发行分支](configure-your-release-branches.md).

有关如何使用Cloud Manager的 **Git存储库** 与CI/CD管道，请参阅相关文档 [配置生产管道](configuring-production-pipelines.md) 和 [配置非生产管道](configuring-non-production-pipelines.md) 以了解更多。

## 内部部署存储库 {#on-premise-repository}

在某些情况下，您将拥有一个现有的Git存储库，并希望继续使用它。 在这些情况下，您可以对多个远程存储库使用Git支持的功能。 您的Git存储库中将继续进行日常开发。 当发行分支准备好部署到生产环境时，您会将最新代码推送到Cloud Manager的Git存储库，并触发Cloud Manager CI/CD管道。

>[!NOTE]
>
>要查看常用的Git命令，请参阅 [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf).
