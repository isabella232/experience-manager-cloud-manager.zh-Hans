---
title: 配置您的发行分支
seo-title: 配置您的发行分支
description: 在Git中为AEM Cloud Manager配置发行分支
seo-description: 请阅读本页，了解如何在Git中配置您的发行分支。
uuid: d12a8b85-b7 fd-4b55 b55 a05 a-a0 f874 ce598 c
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: 快速入门
discoiquuid: 53807 ea6-9464-429d-9322-85c9 f405 dff6
translation-type: tm+mt
source-git-commit: 9c0df236c1e800802d62dea09996bb8e1e7033f7

---


# 配置您的发行分支 {#configure-your-release-branches}

## 在Git中设置您的第一个分支 {#setting-up-your-first-branch-in-git}

一个最初 **为空的Git存储库** ，在Cloud Manager中为每个程序提供了Git存储库。在开发过程中，此存储库可以包含任意多个(或少个)分支，但必须至少有一个由CI/CD管线使用的分支才能将应用程序代码部署到舞台和生产。最佳实践是用作 `master` 此分支的名称。很方便，这是Git客户端设置新项目时的默认行为。

例如，设置新项目时，您将运行如下一组命令：

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
>它不要求使用命令行客户端。有各种图形Git客户端可作为独立应用程序或作为集成开发环境(IDE)的一部分提供，如Eclipse或IntelliJ。只要客户端应用程序使用HTTPS支持Git，它就应该兼容 [!UICONTROL Cloud Manager]。

## 推动您的第一部分支 {#pushing-your-first-branch}

在至少已添加一个修订后，您可以将 [!UICONTROL Cloud Manager] 存储库添加为 **远程** 存储库，然后将其提交给它：

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      master -> master
```

>[!NOTE]
>
>您的客户成功工程过程中将提供特定URL及其凭据 [!UICONTROL Cloud Manager] 。

## 其他分支 {#additional-branches}

`master` 单个分支可能需要非常简单的项目，但在大多数情况下，需要更复杂的分支战略。许多客户遵循一个流程，该流程在调用 `develop` 分支的情况下执行日常开发活动，并且开发分支在部署时合并到 `master` 分支中。

>[!NOTE]
>
>要查看常用的git命令，请参阅 [Git Cheat工作表](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
