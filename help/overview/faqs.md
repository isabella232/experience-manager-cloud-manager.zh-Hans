---
title: Cloud Manager 常见问题
description: 本文档为 AMS 客户提供有关 Cloud Manager 最常见问题的解答。
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6be659e02df0657ec7d3dbce8c18c44a327a36f4
workflow-type: ht
source-wordcount: '776'
ht-degree: 100%

---


# Cloud Manager 常见问题 {#cloud-manager-faqs}

本文档为 AMS 客户提供有关 Cloud Manager 最常见问题的解答。

## 是否可以将 Java 11 与 Cloud Manager 构建一起使用？ {#java-11}

是。您将需要添加 `maven-toolchains-plugin` 和正确的 Java 11 设置。

* [此处](/help/getting-started/using-the-wizard.md)记录了该流程。
* 有关示例，请参阅 [wknd 示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

## 从 Java 8 切换到 Java 11 后，我的构建失败，并显示一个有关 maven-scr-plugin 的错误。我该怎么办？ {#maven-src-plugin}

尝试将构建从 Java 8 切换到 Java 11 时，您的 AEM Cloud Manager 构建可能会失败。 如果您遇到以下错误，则需要移除 `maven-scr-plugin` 并将所有 OSGi 注释转换为 OSGi R6 注释。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

有关如何移除此插件的说明，请[参阅此处](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

## 从 Java 8 切换到 Java 11 后，我的构建失败，并显示一个有关 RequireJavaVersion 的错误。我该怎么办？ {#requirejavaversion}

对于 Cloud Manager 构建，`maven-enforcer-plugin` 可能会失败，并显示此错误

```text
[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion
```

这是一个已知问题，导致此问题的原因是 Cloud Manager 使用其他版本的 Java 来运行 maven 命令而不是编译代码。只需从 `maven-enforcer-plugin` 配置中忽略 `requireJavaVersion`。

## 代码质量检查失败，并且我们的部署出现卡滞。 是否能通过某种方式绕过此检查？ {#deployment-stuck}

是。除了安全性评级之外，所有代码质量故障都是非关键量度，因此，可以在部署管道中，通过扩展结果 UI 中的项目来绕过它们。

具有[部署经理、项目经理或业务负责人](/help/requirements/users-and-roles.md#role-definitions)角色的用户既可以覆盖问题，也可以接受问题，在前一种情况下，管道将继续运行，在后一种情况下，管道将停止并显示故障。

有关更多详细信息，请参阅[运行管道时的三层审核](/help/using/code-quality-testing.md#three-tier-gates-while-running-a-pipeline)和[配置非生产管道](/help/using/non-production-pipelines.md#understanding-the-flow)文档。

## Cloud Manager 部署在 Adobe Managed Services 环境中执行性能测试步骤时失败。我们如何进行调试才能通过关键量度？ {#debug-critical-metrics}

此问题的答案不是唯一的。但是，您应牢记以下有关性能测试步骤的一些要点：

* 此步骤是一个 Web 性能步骤，即使用 Web 浏览器加载页面所需的时间。
* 在测试期间，结果 .csv 文件中列出的 URL 将加载到 Cloud Manager 基础架构的 Chrome 浏览器中。
* 一个未通过的常见量度是错误率。
   * 为了使 URL 通过，主 URL 必须以 `200` 状态加载，并且加载时间必须少于 `20` 秒。
   * 超过 `20` 秒的页面加载将标记为 `504` 错误。
* 如果网站要求实施用户身份验证，请参阅[了解测试结果](/help/using/code-quality-testing.md#authenticated-performance-testing)文档，了解如何配置测试以针对网站进行身份验证。

有关质量检查的更多信息，请参阅[了解测试结果](/help/using/code-quality-testing.md)文档。

## 我是否能将 SNAPSHOT 用于 Maven 项目版本？ {#snapshot}

是。对于开发人员部署，Git 分支 `pom.xml` 文件必须在 `<version>` 值的末尾包含 `-SNAPSHOT`。

这样一来，在版本未更改的情况下，仍能安装后续部署。 在开发人员部署中，不会为 Maven 构建添加或生成自动版本。

您也可以为暂存和生产构建或部署将版本设置为 `-SNAPSHOT`。 Cloud Manager 会自动设置适当的版本号并在 Git 中为您创建标记。 如果需要，可以稍后参考此标记。

[此处记录了](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/project-version-handling.html)有关版本处理的更多详细信息。

## 包和捆绑包版本控制如何用于暂存和生产部署？ {#staging-production}

在暂存和生产部署中，将生成自动版本，[如该处所记录](/help/managing-code/maven-project-version.md)。

对于暂存和生产部署中的自定义版本控制，请设置包含三个部分的正确 maven 版本，如 `1.0.0`。每次部署到生产环境时提高版本。

Cloud Manager 自动将其版本添加到暂存和生产构建，并创建 Git 分支。 无需特殊配置。 如果您未如前所述设置 maven 版本，部署仍将成功，并且会自动设置版本。

## 虽然在 Cloud Manager 部署中，我的 maven 构建失败，但它会在本地构建，并且不会产生错误。 有什么问题吗？ {#maven-build-fail}

有关更多详细信息，请参阅此 [Git 资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 我无法使用 aio 命令设置变量。我该怎么办？ {#set-variable}

在尝试通过 `aio` 命令列出或设置管道变量时，您可能会收到如下所示的 403 错误。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在此情况下，需要在 Admin Console 中将执行这些命令的用户添加到&#x200B;**部署经理**&#x200B;角色。

有关更多详细信息，请参阅 [API 权限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)。
