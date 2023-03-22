---
title: Cloud Manager 存储库
description: 了解如何访问、创建和编辑 Cloud Manager 项目的存储库。
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 63cbcf8724a840efa67b8fafc4c321e04a5d70d9
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 80%

---


# Cloud Manager 存储库 {#cloud-manager-repos}

可以在存储库中使用 Git 管理代码。了解如何为 Cloud Manager 项目创建存储库。

## 访问存储库 {#accessing-repos}

您可以通过 Cloud Manager 中的自助服务来访问和管理您的 Git 存储库。

要访问存储库，请使用 Cloud Manager 中提供的&#x200B;**访问存储库信息**&#x200B;按钮（位于管道信息卡上最显眼的位置）。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 中登录 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡，您将看到&#x200B;**访问存储库信息**&#x200B;选项，该选项可用于访问和管理[已配置此管道](/help/using/production-pipelines.md)的 Git 存储库。

   ![“访问存储库信息”按钮](/help/assets/access-repo1.png)

1. 如果您切换到&#x200B;**非生产**&#x200B;管道选项卡，则也可使用&#x200B;**访问存储库信息**&#x200B;选项，操作与[为管道配置](/help/using/non-production-pipelines.md)一样。

   ![非生产管道](/help/assets/access-repo-nonprod.png)

1. 单击&#x200B;**访问存储库信息**&#x200B;按钮，会打开显示以下内容的对话框：

   * Git 存储库的 URL
   * 用户名
   * 密码
   * 用于本地克隆存储库的 Git 命令

   ![“存储库信息”对话框](/help/assets/access-repo-create.png)

使用提供的信息本地克隆存储库，以便开始本地开发。

>[!NOTE]
>
>**访问存储库信息**&#x200B;选项对具有&#x200B;**开发人员**&#x200B;或&#x200B;**部署经理**&#x200B;角色的用户可见。

## 添加存储库 {#add-repos}

执行以下步骤可在 Cloud Manager 中添加存储库：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 中登录 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面中，单击&#x200B;**存储库**&#x200B;选项卡，然后导航到&#x200B;**存储库**&#x200B;页面。

1. 单击&#x200B;**添加存储库**&#x200B;启动向导。

   >[!NOTE]
   >
   >您必须具有&#x200B;**部署经理**&#x200B;或&#x200B;**业务负责人**&#x200B;角色才能添加存储库。

   ![添加存储库](/help/assets/create-repo2.png)

1. 输入请求的名称和描述，然后单击&#x200B;**保存**。

   ![存储库的详细信息](/help/assets/repo-1.png)

1. 选择&#x200B;**保存**。

此时将显示您新创建的存储库。

![创建的新存储库](/help/assets/create-repo3.png)

在[创建管道](/help/overview/ci-cd-pipelines.md)时，可以选择已在 Cloud Manager 中创建的存储库。

## 查看和编辑存储库 {#edit-repos}

执行以下步骤可在 Cloud Manager 中编辑和查看存储库：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 中登录 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面中，单击&#x200B;**存储库**&#x200B;选项卡，然后导航到&#x200B;**存储库**&#x200B;页面。您可以在此处查看现有存储库的详细信息。

1. 选择存储库，然后单击表最右侧的省略号按钮以 **复制存储库URL** 或 **查看和更新** 您的存储库。

![编辑存储库](/help/assets/create-repo3.png)

## 删除存储库 {#delete-repos}

要删除存储库，请执行相同的步骤 [查看和编辑存储库](#edit-repos) 但在 **存储库** 页面选择 **删除** 从要删除的存储库的省略号按钮。

请注意，在Cloud Manager中删除某个存储库后，该存储库会标记为已删除，用户将无法再访问该存储库，但出于恢复目的，它将在系统中进行维护。

如果在删除具有相同名称的存储库后尝试创建新存储库，您将收到错误消息“尝试创建存储库时出错。 请联系您的CSE或Adobe支持。”

如果收到此错误消息，请联系Adobe支持，以便他们协助重命名已删除的存储库或为新存储库选择其他名称。

## Git 子模块支持 {#git-submodule-support}

Git 子模块可用于在构建时跨 Git 存储库合并多个分支的内容。

Cloud Manager 的构建过程执行期间，在克隆为管道配置的存储库并签出配置的分支后，如果该分支在根目录中包含 `.gitmodules` 文件，则执行此命令。

```
$ git submodule update --init
```

这会将每个子模块签出到适当的目录中。对于能够轻松使用 Git 子模块并且不想管理外部合并过程的组织来说，此方法是[使用多个源 Git 存储库](/help/managing-code/multiple-git-repos.md)的潜在替代方法。

例如，假设有三个存储库，每个存储库均包含一个名为 `main` 的分支。在“主”存储库（即，在管道中配置的存储库）中，`main` 分支包含一个 `pom.xml` 文件，声明其他两个存储库所包含的项目：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

之后，您将为其他两个存储库添加子模块：

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

这将生成一个 `.gitmodules` 文件，与以下内容类似：

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

可以在 [Git 参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules)中找到有关 Git 子模块的更多信息。

### 限制 {#limitations}

在使用 Git 子模块时，请注意：

* Git URL 必须完全遵循上述语法。
* 为安全起见，请勿在这些 URL 中嵌入凭据。
* 仅支持分支的根目录中的子模块。
* Git 子模块引用将存储到特定的 git 承诺中。
   * 因此，在对子模块存储库进行更改时，需要更新引用的承诺，例如使用 `git submodule update --remote` 进行更新。
* 除非另有必要，否则强烈建议使用“浅”子模块。
   * 为此，请为每个子模块运行 `git config -f .gitmodules submodule.<submodule path>.shallow true`。
