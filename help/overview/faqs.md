---
title: Cloud Manager 常见问题解答
description: 本文档提供了有关面向AMS客户的Cloud Manager的最常见问题的解答。
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6be659e02df0657ec7d3dbce8c18c44a327a36f4
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 1%

---


# Cloud Manager 常见问题解答 {#cloud-manager-faqs}

本文档提供了有关面向AMS客户的Cloud Manager的最常见问题的解答。

## 能否将Java 11与Cloud Manager内部版本结合使用？ {#java-11}

是。您需要将 `maven-toolchains-plugin` ，且设置正确。

* 此过程已记录 [这里。](/help/getting-started/using-the-wizard.md)
* 有关示例，请参阅 [wknd示例项目代码。](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)

## 从Java 8切换到Java 11后，我的生成失败，并出现有关maven-scr-plugin的错误。 我能做什么？ {#maven-src-plugin}

尝试将AEM Cloud Manager内部版本从Java 8切换到11时，该内部版本可能会失败。 如果您遇到以下错误，则需要删除 `maven-scr-plugin` 并将所有OSGi批注转换为OSGi R6批注。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

有关如何删除此插件的说明，请 [请参见此处。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## 从Java 8切换到Java 11后，我的生成失败，并出现有关RequireJavaVersion的错误。 我能做什么？ {#requirejavaversion}

对于Cloud Manager内部版本， `maven-enforcer-plugin` 可能因此错误而失败

```text
[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion
```

这是一个已知问题，因为Cloud Manager使用不同版本的Java来运行maven命令而不是编译代码。 只是省略 `requireJavaVersion` 从 `maven-enforcer-plugin` 配置。

## 代码质量检查失败，我们的部署卡住。 有办法绕过这张支票吗？ {#deployment-stuck}

是。除安全评级之外的所有代码质量故障都是非关键量度，因此可以通过扩展结果UI中的项目，将它们作为部署管道的一部分进行绕过。

具有 [部署经理、项目经理或业务所有者](/help/requirements/users-and-roles.md#role-definitions) 角色可以覆盖问题，在这种情况下，管道继续进行，或者他们可以接受问题，在这种情况下，管道会因失败而停止。

查看文档 [运行管道时的三层门](/help/using/code-quality-testing.md#three-tier-gates-while-running-a-pipeline) 和 [配置非生产管道](/help/using/non-production-pipelines.md#understanding-the-flow) 以了解更多详细信息。

## 在Adobe Managed Services环境中，Cloud Manager部署在性能测试步骤失败。 我们如何调试此参数以传递关键量度？ {#debug-critical-metrics}

这个问题没有一个单一的答案。 但是，对于性能测试步骤，您应牢记以下几点：

* 此步骤是Web性能步骤，即使用Web浏览器加载页面的时间。
* 测试期间，结果.csv文件中列出的URL将加载到Cloud Manager基础架构的Chrome浏览器中。
* 失败的常见量度是错误率。
   * 要传递URL，主URL必须通过加载 `200` 状态和小于 `20` 秒。
   * 超过 `20` 秒数标记为 `504` 错误。
* 如果您的网站需要用户身份验证，请参阅此文档 [了解测试结果](/help/using/code-quality-testing.md#authenticated-performance-testing) 用于配置测试以对您的网站进行身份验证。

请查看文档 [了解测试结果](/help/using/code-quality-testing.md) 以了解有关质量检查的详细信息。

## 我能否将SNAPSHOT用于Maven项目的版本？ {#snapshot}

是。对于开发人员部署，请使用git分支 `pom.xml` 文件必须包含 `-SNAPSHOT` 在 `<version>` 值。

这样，当版本未发生更改时，仍然可以安装后续部署。 在开发人员部署中，不会为Maven内部版本添加或生成自动版本。

您还可以将版本设置为 `-SNAPSHOT` 用于暂存和生产内部版本或部署。 Cloud Manager会自动设置正确的版本号，并在git中为您创建一个标记。 如果需要，可以稍后引用此标记。

有关版本处理的更多详细信息包括 [记录在此。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/project-version-handling.html)

## 包和捆绑版本控制如何用于暂存和生产部署？ {#staging-production}

在暂存和生产部署中，会生成一个自动版本 [如此处所述。](/help/managing-code/maven-project-version.md)

要在暂存和生产部署中进行自定义版本控制，请设置一个由三部分组成的适当版本，如 `1.0.0`. 每次部署到生产环境时，请增加该版本。

Cloud Manager会自动将其版本添加到暂存和生产内部版本并创建git分支。 无需特殊配置。 如果您没有按照之前所述设置Maven版本，部署仍将成功，并且会自动设置版本。

## 我的Maven内部版本在Cloud Manager部署中失败，但它在本地生成，并且没有错误。 怎么了？ {#maven-build-fail}

请参阅 [git资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 以了解更多详细信息。

## 我无法使用aio命令设置变量。 我能做什么？ {#set-variable}

尝试通过列出或设置管道变量时，可能会收到如下403错误 `aio` 中。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在这种情况下，执行这些命令的用户需要添加到 **部署管理器** 角色。

请参阅 [API权限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/) 以了解更多详细信息。
