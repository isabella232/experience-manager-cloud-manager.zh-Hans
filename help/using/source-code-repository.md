---
title: 源代码存储库
seo-title: AdobeAEM Cloud Manager的源代码存储库
description: 可查看本页面以了解为Cloud Manager中的每个程序配置的git存储库。
seo-description: 可查看本页以了解为您在Adobe AEM Cloud Manager中拥有的每个程序配置的git存储库。
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: 配置
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---

# 源代码存储库 {#source-code-repository}

## Cloud Manager存储库{#cloud-manager-repository}

您的[!UICONTROL AEM Managed Services]订阅将包含由Adobe配置和管理的源代码存储库。 每个客户的程序都会分配一个唯一的&#x200B;**Git存储库**，您的关联代码将存储并保护在该存储库中。

作为最佳实践，您应始终使用Cloud Manager的Git存储库，该存储库为空，且未配置任何分支或示例项目。 要使用Cloud Manager的Git存储库，您将获得&#x200B;**专用访问令牌**，该令牌允许您使用任何与Git兼容的客户端创建分支、存储和检索代码、列出提交历史记录等。

有关如何在Git中设置分支的更多信息，请参阅[配置发行分支](configure-your-release-branches.md)。

有关如何将Cloud Manager的&#x200B;**Git存储库**&#x200B;与CI/CD管道一起使用的更多信息，请参阅[配置CI/CD管道](configuring-pipeline.md)。

## 内部部署存储库{#on-premise-repository}

在某些情况下，您将拥有一个现有的Git存储库，并希望继续使用它。 在这些情况下，您可以对多个远程存储库使用Git支持的功能。 您的Git存储库中将继续进行日常开发。 当发行分支准备好部署到生产环境时，您会将最新代码推送到Cloud Manager的Git存储库，并触发Cloud Manager CI/CD管道。

>[!NOTE]
>
>要查看常见的Git命令，请参阅[Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf)。
