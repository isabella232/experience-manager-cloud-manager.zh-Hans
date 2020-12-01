---
title: 配置发布分支
seo-title: 配置发布分支
description: 在Git中为AEM Cloud Manager配置发布分支
seo-description: 可查看本页以了解如何在git中配置您的发行分支。
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
translation-type: tm+mt
source-git-commit: 9c0df236c1e800802d62dea09996bb8e1e7033f7
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 3%

---


# 配置发布分支 {#configure-your-release-branches}

## 在Git {#setting-up-your-first-branch-in-git}中设置您的第一个分支

为Cloud Manager中已载入的每个项目设置单个（最初为空）**Git存储库**。 此存储库可以包含开发流程所遵循的多个（或少的）分支，但至少有一个分支被CI/CD管道使用，以将应用程序代码部署到舞台和生产。 最佳实践是使用`master`作为此分支的名称。 方便的是，这是Git客户端在设置新项目时的默认行为。

例如，在设置新项目时，您将运行一组如下命令：

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
>它不要求使用命令行客户端。 有多种图形Git客户端可作为独立应用程序或集成开发环境(IDE)（如Eclipse或IntelliJ）的一部分提供。 只要客户端应用程序支持使用HTTPS的Git，它就应与[!UICONTROL Cloud Manager]兼容。

## 推送您的第一个分支{#pushing-your-first-branch}

提交至少一个修订版本后，您可以将[!UICONTROL Cloud Manager]存储库添加为&#x200B;**remote**，然后将提交推送到它：

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
>在[!UICONTROL Cloud Manager]入门过程中，客户成功工程部门将向您提供特定URL和凭据。

## 其他分支{#additional-branches}

单个`master`分支可能足以完成非常简单的项目，但在大多数情况下，需要更复杂的分支策略。 许多客户遵循的流程是，在名为`develop`的分支上执行日常开发活动，而在需要部署时，开发分支会合并到`master`分支中。

>[!NOTE]
>
>要视图常见的git命令，请参阅[Git备忘单](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
