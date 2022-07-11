---
title: 配置分支
description: 了解如何在git中设置您的第一个分支，以及CI/CD管道如何使用该分支来部署应用程序代码。
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: 4c051cd1696f8a00d0278131c9521ad4dcb956a3
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 配置分支 {#configuring-branches}

了解如何在git中设置您的第一个分支，以及CI/CD管道如何使用该分支来部署应用程序代码。

## 在Git中设置您的第一个分支 {#setting-up-your-first-branch-in-git}

单个初始为空的Git存储库 [已设置](/help/requirements/environment-provisioning.md) 适用于在Cloud Manager中载入的每个项目。 此存储库可以包含开发流程所需的任意数量的分支，但必须至少有一个分支，CI/CD管道使用该分支来部署应用程序代码以存放和生产。 最佳做法是使用 `main` 作为此分支的名称。 很方便，这是Git客户端在设置新项目时的默认行为。

例如，在设置新项目时，您将运行一组类似于以下内容的命令。

```shell
$ git init
Initialized empty Git repository in /Users/myname/workspace/new-project/.git/
... steps which add Maven build files and source code ...
$ git add pom.xml core/pom.xml core/src ui.apps/pom.xml ui.apps/src
$ git commit -m "initial commit"
 19 files changed, 777 insertions(+)
 create mode 100644 core/pom.xml
 create mode 100644 pom.xml
 create mode 100644 ui.apps/pom.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/config.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/definition/.content.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/filter.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/nodetypes.cnd
 create mode 100644 ui.apps/src/main/content/META-INF/vault/properties.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/apps/my-aem-project/install/.vltignore
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/_rep_policy.xml
```

>[!NOTE]
>
>它不要求使用命令行客户端。 有多种图形git客户端可用作独立应用程序或集成开发环境(IDE)的一部分，如Eclipse或IntelliJ。 只要客户端应用程序支持使用HTTPS的git，它就应该与 [!UICONTROL Cloud Manager].

## 推送第一个分支 {#pushing-your-first-branch}

提交至少一个修订版本后，您可以添加 [!UICONTROL Cloud Manager] 存储库作为远程存储库，然后将您的提交推送到该存储库。

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      main -> main
```

>[!NOTE]
>
>在 [!UICONTROL Cloud Manager] 入门。

## 其他分支 {#additional-branches}

单个 `main` 分支可以满足非常简单的项目，但在大多数情况下，需要更复杂的分支策略。 许多客户遵循的流程是，在称为 `develop` 并将开发分支合并到 `main` 分支。

>[!TIP]
>
>要查看常用的git命令，请参阅 [Git备忘单](https://github.github.com/training-kit/downloads/github-git-cheat-sheet).
