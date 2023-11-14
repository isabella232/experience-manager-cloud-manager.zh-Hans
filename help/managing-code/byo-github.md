---
title: 在Cloud Manager中使用您自己的存储库GitHub
description: 了解如何设置Cloud Manager以使用您自己的GitHub存储库。
feature: Release Information
source-git-commit: 76a3dc6df41032488a3cfe11d0c72769562b96df
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 2%

---


# 在Cloud Manager中使用您自己的存储库GitHub {#byo-github}

通过配置Cloud Manager以使用您自己的GitHub存储库，您可以通过Cloud Manager直接在GitHub存储库中验证代码，而无需始终如一地将代码与Adobe存储库同步。

>[!NOTE]
>
>此功能仅适用于[早期采用者计划。](/help/release-notes/current.md#early-adoption)

## 配置 {#configuration}

配置包含两个主要步骤：

1. [添加存储库](#add-repo)
1. [私有存储库所有权验证](#validate-ownership)

### 添加存储库 {#add-repo}

1. 在Cloud Manager中，从 **项目概述** 页面，点按或单击 **存储库** 制表符以切换到 **存储库** 页面并单击 **添加存储库**.

1. 在 **添加存储库** 对话框，选择 **专用存储库** 作为存储库类型。

1. 提供存储库的详细信息

   * **存储库名称**  — 一个表情符号的名称
   * **存储库URL**  — 存储库的URL，必须以结尾 `.git`
   * **描述** （可选） — 根据需要提供对存储库的更长描述

   ![添加自己的存储库](/help/assets/repositories/add-own-github.png)

1. 点按或单击&#x200B;**保存**。

>[!TIP]
>
>有关在Cloud Manager中管理存储库的详细信息，请参阅文档 [Cloud Manager存储库。](/help/managing-code/repositories.md)

### 私有存储库所有权验证 {#validate-ownership}

Cloud Manager现在知道您的GitHub存储库，但仍需要访问它。 要授予访问权限，您需要安装AdobeGitHub应用程序并验证您是否拥有指定的存储库。

1. 添加您自己的存储库后， **私有存储库所有权验证** 此时将打开对话框。

   ![私有存储库所有权验证](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager使用GitHub应用程序与您的存储库安全交互。
   * GitHub组织的所有者必须安装位于 `https://github.com/apps/cloud-manager-for-aem-stage` 并授予对存储库的访问权限。
   * 有关如何执行此操作的详细信息，请参阅GitHub文档。

1. 要增强安全性，必须在存储库的默认分支中创建机密文件。 点击或单击 **生成**.

1. 通过点击或单击确认生成机密文件 **确认**.

   ![确认密钥生成](/help/assets/repositories/confirm-generation.png)

1. 返回 **私有存储库所有权验证** 窗口中，Cloud Manager已生成私有文件的内容 **机密文件内容** 字段。 复制该字段中的内容。

   * 机密文件的内容只显示一次。 如果在关闭此窗口之前没有复制内容，则需要重新生成密码。

   ![复制密钥文件内容](/help/assets/repositories/new-secret.png)

1. 在GitHub存储库的默认分支中创建一个名为的新文件 `.well-known/adobe/cloud-manager-challenge` 并将机密文件内容粘贴到该文件中并保存。

1. 安装应用程序且存储库中存在机密文件后，您可以点按或单击 **验证** 在 **私有存储库所有权验证** 对话框。

可以按任意顺序安装应用程序并创建机密文件。 但是，必须先完成这两个步骤，然后才能进行验证。

在验证之前，存储库将以红色图标列出，指示它尚未验证并且尚无法使用。

![未验证的存储库](/help/assets/repositories/unvalidated-repo.png)

请注意 **类型** 列可以轻松识别Adobe提供的存储库(**Adobe**)和您自己的GitHub存储库(**GitHub**)。

如果您以后需要返回到存储库以完成验证，请在 **存储库** 页面，点按或单击表示您刚刚添加的GitHub存储库的行中的省略号按钮，然后选择 **所有权验证** 从下拉菜单中。

## 在Cloud Manager中使用您自己的GitHub存储库 {#using}

在Cloud Manager中验证GitHub存储库后，集成已完成，您可以将该存储库与Cloud Manager结合使用。

1. 在创建拉取请求时，将会自动启动GitHub检查。

   ![GitHub检查](/help/assets/repositories/github-checks.png)

1. 对于每个拉取请求， [全栈代码质量管道](/help/using/managing-pipelines.md) 将自动创建。 此管道在每次拉取请求更新时启动。

1. 在代码质量检查完成之前，GitHub检查将保持运行状态。 代码质量结果随后将传播到GitHub检查中。

   ![GitHub代码质量检查](/help/assets/repositories/github-code-quality.png)

关闭或合并拉取请求时，将自动删除创建的全栈代码质量管道。

## 限制 {#limitations}

在将GitHub存储库与Cloud Manager结合使用时，请记住以下限制。

* 您无法将GitHub存储库用作您管理的管道的直接存储库源。
   * 此功能已在计划中。
* 使用Cloud Manager中的GitHub检查无法暂停拉取请求验证。
   * 如果在Cloud Manager中验证GitHub存储库，则Cloud Manager将始终尝试验证为该存储库创建的拉取请求。
如果从您的GitHb组织中删除了AdobeGitHub应用程序，这将删除适用于所有存储库的拉取请求验证功能。
