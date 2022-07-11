---
title: Cloud Manager存储库
description: 了解如何访问、创建和编辑Cloud Manager程序的存储库。
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 2%

---


# Cloud Manager存储库 {#cloud-manager-repos}

存储库是您使用git管理代码的位置。 了解如何为Cloud Manager程序创建存储库。

## 访问存储库 {#accessing-repos}

您可以从Cloud Manager通过自助服务访问和管理Git存储库。

要访问您的存储库，请使用 **访问存储库信息** 按钮，在管道卡的最突出位置。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，您将看到 **访问存储库信息** 访问和管理git存储库的选项 [已配置此管道。](/help/using/production-pipelines.md)

   ![访问存储库信息按钮](/help/assets/access-repo1.png)

1. 如果您切换到 **非生产** 管道选项卡， **访问存储库信息** 选项在此处也可用为 [为管道配置。](/help/using/non-production-pipelines.md)

   ![非生产管道](/help/assets/access-repo-nonprod.png)

1. 单击 **访问存储库信息** 按钮以打开显示以下内容的对话框：

   * 指向Git存储库的URL
   * 用户名
   * 密码
   * 用于在本地克隆存储库的Git命令

   ![存储库信息对话框](/help/assets/access-repo-create.png)

使用提供的信息在本地克隆存储库，以便开始本地开发。

>[!NOTE]
>
>的 **访问存储库信息** 选项在 **开发人员** 或 **部署管理器** 角色。

## 添加存储库 {#add-repos}

按照以下步骤在Cloud Manager中添加存储库：

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 并选择相应的组织和程序。

1. 从 **计划概述** 页面，单击 **存储库** 选项卡，然后导航到 **存储库** 页面。

1. 单击 **添加存储库** 启动向导。

   >[!NOTE]
   >
   >您必须拥有 **部署管理器** 或 **业务所有者** 角色添加存储库。

   ![添加存储库](/help/assets/create-repo2.png)

1. 根据请求输入名称和描述，然后单击 **保存**.

   ![存储库的详细信息](/help/assets/repo-1.png)

1. 选择&#x200B;**保存**。

此时将显示您新创建的存储库。

![已创建新存储库](/help/assets/create-repo3.png)

在Cloud Manager中创建的存储库可供您选择 [创建管道。](/help/overview/ci-cd-pipelines.md)

## 查看和编辑存储库 {#edit-repos}

按照以下步骤在Cloud Manager中编辑和查看存储库：

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 并选择相应的组织和程序。

1. 从 **计划概述** 页面，单击 **存储库** 选项卡，然后导航到 **存储库** 页面。 您可以在此处查看现有存储库的详细信息。

1. 选择存储库，然后单击表最右侧的省略号按钮以 **复制存储库URL**, **查看和更新** 或 **删除** 您的存储库。

![编辑存储库](/help/assets/create-repo3.png)

## Git子模块支持 {#git-submodule-support}

Git子模块可用于在构建时在git存储库中合并多个分支的内容。

在执行Cloud Manager的生成过程时，如果为管道配置的存储库包含 `.gitmodules` 文件，将执行命令。

```
$ git submodule update --init
```

这会将每个子模块检出到相应的目录中。 此技术是 [使用多个源Git存储库](/help/managing-code/multiple-git-repos.md) 适用于熟悉使用git子模块且不希望管理外部合并流程的组织。

例如，假设有三个存储库，每个存储库都包含一个名为 `main`. 在“主”存储库（即在管道中配置的存储库）中， `main` 分支具有 `pom.xml` 声明其他两个存储库中包含的项目的文件：

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

然后，您将为其他两个存储库添加子模块：

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

这会导致 `.gitmodules` 文件如下所示：

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

有关git子模块的更多信息，请参阅 [Git参考手册](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### 限制 {#limitations}

使用git子模块时，请注意：

* Git URL必须完全遵循上述语法。
* 出于安全考虑，请勿在这些URL中嵌入凭据。
* 仅支持位于分支根的子模块。
* Git子模块引用存储到特定的git提交中。
   * 因此，当对子模块存储库进行更改时，例如，使用 `git submodule update --remote`.
* 除非另有必要，否则强烈建议使用“浅层”子模块。
   * 要执行此操作，请运行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每个子模块。
