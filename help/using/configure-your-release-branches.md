---
title: 配置发布分支
seo-title: 配置发布分支
description: 在Git中为AEM Cloud Manager配置发行分支
seo-description: 请阅读本页，了解如何在git中配置发行分支。
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
feature: Git存储库
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 配置发布分支 {#configure-your-release-branches}

## 在Git {#setting-up-your-first-branch-in-git}中设置您的第一个分支

为Cloud Manager中已载入的每个程序配置一个最初为空的&#x200B;**Git存储库**。 此存储库可以包含您的开发流程所遵循的任意数量（或任意数量的）分支，但必须至少有一个分支，CI/CD管道使用该分支来将应用程序代码部署到暂存和生产环境。 最佳做法是使用`master`作为此分支的名称。 很方便，这是Git客户端在设置新项目时的默认行为。

例如，在设置新项目时，您将运行一组命令，如下所示：

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
>它不要求使用命令行客户端。 有许多图形Git客户端可作为独立应用程序或集成开发环境(IDE)的一部分（如Eclipse或IntelliJ）提供。 只要客户端应用程序支持使用HTTPS的Git，它就应该与[!UICONTROL Cloud Manager]兼容。

## 推送第一个分支{#pushing-your-first-branch}

提交至少一个修订版本后，您可以将[!UICONTROL Cloud Manager]存储库添加为&#x200B;**remote**，然后将提交推送到该版本：

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
>在[!UICONTROL Cloud Manager]入门期间，客户成功工程团队将向您提供特定URL和您的凭据。

## 其他分支{#additional-branches}

单个`master`分支可以满足非常简单的项目，但在大多数情况下，需要更复杂的分支策略。 许多客户遵循的流程是，在名为`develop`的分支上执行日常开发活动，并在需要部署时将开发分支合并到`master`分支中。

>[!NOTE]
>
>要查看常见的git命令，请参阅[Git备忘单](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
