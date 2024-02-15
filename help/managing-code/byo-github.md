---
title: 在 Cloud Manager 中使用您自己的 GitHub 存储库
description: 了解如何设置 Cloud Manager 以使用您自己的 GitHub 存储库。
feature: Release Information
exl-id: e0d103c9-c147-4040-bf53-835e93d78a0b
source-git-commit: b5907179d3de329e8b86546bb8aa99608a5b351a
workflow-type: ht
source-wordcount: '767'
ht-degree: 100%

---


# 在 Cloud Manager 中使用您自己的 GitHub 存储库 {#byo-github}

通过将 Cloud Manager 配置为使用您自己的 GitHub 存储库，您可以通过 Cloud Manager 直接在 GitHub 存储库中验证代码，而无需始终将代码与 Adobe 存储库同步。

>[!NOTE]
>
>此功能仅适用于[早期采用者计划。](/help/release-notes/current.md#early-adoption)

>[!NOTE]
>
>此功能是公共 GitHub 独有的。不支持自托管 GitHub。

## 配置 {#configuration}

配置包含两个主要步骤：

1. [添加存储库](#add-repo)
1. [专用存储库所有权验证](#validate-ownership)

### 添加存储库 {#add-repo}

1. 在 Cloud Manager 中，从&#x200B;**项目概述**&#x200B;页面中，点按或单击&#x200B;**存储库**&#x200B;选项卡以切换到&#x200B;**存储库**&#x200B;页面，然后单击&#x200B;**添加存储库**。

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**&#x200B;作为存储库类型。

1. 提供您的存储库的详细信息

   * **存储库名称** - 一个富有表现力的名称
   * **存储库 URL** - 存储库的 URL，它必须以 `.git` 结尾
   * **描述**（可选）- 存储库的更详细描述（如有必要）

   ![添加自己的存储库](/help/assets/repositories/add-own-github.png)

1. 点按或单击&#x200B;**保存**。

>[!TIP]
>
>有关在 Cloud Manager 中管理存储库的详细信息，请参阅文档 [Cloud Manager 存储库。](/help/managing-code/repositories.md)

### 专用存储库所有权验证 {#validate-ownership}

Cloud Manager 现已知道您的 GitHub 存储库，但它仍需要其访问权限。要授予访问权限，您需要安装 Adobe GitHub 应用程序并验证您是否拥有指定的存储库。

1. 添加您自己的存储库后，**专用存储库所有权验证**&#x200B;对话框将打开。

   ![专用存储库所有权验证](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager 使用 GitHub 应用程序与您的存储库安全地交互。
   * 您的 GitHub 组织的所有者必须安装位于 `https://github.com/apps/cloud-manager-for-aem` 的应用程序并授予对存储库的访问权限。
   * 有关如何执行此操作的详细信息，请参阅 GitHub 的文档。

1. 为了增强安全性，您必须在存储库的默认分支中创建秘密文件。点按或单击&#x200B;**生成**。

1. 通过点按或单击&#x200B;**确认**&#x200B;以确认秘密文件的生成。

   ![确认密码生成](/help/assets/repositories/confirm-generation.png)

1. 返回&#x200B;**专用存储库所有权验证**&#x200B;窗口中，Cloud Manager 已在&#x200B;**秘密文件内容**&#x200B;字段中生成私有文件内容。复制该字段中的内容。

   * 秘密文件的内容仅显示一次。如果您在关闭此窗口之前未复制该内容，则将需要重新生成密码。

   ![复制秘密文件内容](/help/assets/repositories/new-secret.png)

1. 在 GitHub 存储库的默认分支中创建一个名为 `.well-known/adobe/cloud-manager-challenge` 的新文件，将秘密文件内容粘贴到该文件中并进行保存。

1. 在安装应用程序并将秘密文件保存在存储库中后，可以点按或单击&#x200B;**专用存储库所有权验证**&#x200B;对话框中的&#x200B;**验证**。

可以按任意顺序安装应用程序并创建秘密文件。但必须先完成这两个步骤，之后才能进行验证。

在验证之前，存储库将列出并带红色图标，这表示它尚未经过验证，尚无法使用。

![未经验证的存储库](/help/assets/repositories/unvalidated-repo.png)

请注意，**类型**&#x200B;列可轻松识别 Adobe 提供的存储库 (**Adobe**) 和您自己的 GitHub 存储库 (**GitHub**)。

如果您需要稍后返回存储库以完成验证，请在&#x200B;**存储库**&#x200B;页面上，点按或单击代表刚刚添加的 GitHub 存储库的行中的省略号按钮，然后从下拉菜单中选择&#x200B;**所有权验证**。

## 将您自己的 GitHub 存储库与 Cloud Manager 结合使用 {#using}

在 Cloud Manager 中验证 GitHub 存储库后，便已完成集成，您可以在 Cloud Manager 中使用该存储库。

1. 在创建提取请求时，GitHub 检查将自动启动。

   ![GitHub 检查](/help/assets/repositories/github-checks.png)

1. 对于每个提取请求，将自动创建[全栈代码质量管道](/help/using/managing-pipelines.md)。每次更新提取请求时，此管道将启动。

1. GitHub 检查保持正在运行状态，直到代码质量检查完成。之后，代码质量结果将传播到 GitHub 检查。

   ![GitHub 代码质量检查](/help/assets/repositories/github-code-quality.png)

在关闭或合并提取请求时，将自动删除创建的全栈代码质量管道。

## 限制 {#limitations}

在您将自己的 GitHub 存储库与 Cloud Manager 结合使用时，请记住以下限制。

* 您不能使用 GitHub 存储库作为您管理的管道的直接存储库源。
   * 已规划此功能。
* 您无法从 Cloud Manager 使用 GitHub 检查来暂停提取请求验证。
   * 如果在 Cloud Manager 中验证 GitHub 存储库，则 Cloud Manager 将始终尝试验证为该存储库创建的提取请求。
如果从您的 GitHb 组织中删除 Adobe GitHub 应用程序，这将删除所有存储库的提取请求验证功能。
