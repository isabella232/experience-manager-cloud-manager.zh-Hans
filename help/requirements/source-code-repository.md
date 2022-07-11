---
title: 源代码存储库
description: 了解为Cloud Manager中的每个程序配置的git存储库。
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# 源代码存储库 {#source-code-repository}

了解为Cloud Manager中的每个程序配置的git存储库。

## Cloud Manager存储库 {#cloud-manager-repository}

您的 [!UICONTROL AEM Managed Services] 订阅包括由Adobe设置和管理的源代码存储库。 每个程序都会分配一个唯一的git存储库，您的关联代码将存储并保护在该存储库中。

作为最佳实践，您应始终使用Cloud Manager的git存储库，该存储库为空，且未配置任何分支或示例项目。 要使用Cloud Manager的git存储库，您将获得一个专用访问令牌，该令牌将允许您使用任何git客户端创建分支、存储和检索代码、列出提交历史记录等。

有关如何在git中设置分支的更多信息，请参阅 [配置发行分支。](/help/getting-started/configuring-branches.md)

有关如何将Cloud Manager的git存储库与CI/CD管道一起使用的更多信息，请参阅文档 [配置生产管道](/help/using/production-pipelines.md) 和 [配置非生产管道](/help/using/non-production-pipelines.md) 以了解更多。

## 内部部署存储库 {#on-premise-repository}

您可能已拥有一个git存储库，并且希望继续使用该存储库，在这种情况下，您可以将git的功能用于多个远程存储库。 您的git存储库中将继续进行日常开发。 当发行分支准备好部署到生产环境时，您可以将最新代码推送到Cloud Manager的git存储库，并触发Cloud Manager CI/CD管道。

要查看常用的git命令，请参阅 [Git备忘单](https://education.github.com/git-cheat-sheet-education.pdf) 在GitHub网站上。
