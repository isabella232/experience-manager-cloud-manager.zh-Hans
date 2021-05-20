---
title: Cloud Manager常见问题解答
seo-title: Cloud Manager常见问题解答
description: 请参阅Cloud Manager常见问题解答，以获取一些疑难解答提示
seo-description: 请阅读本页以了解Cloud Manager常见问题解答
feature: 入门
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Cloud Manager常见问题解答{#cloud-manager-faqs}

以下部分提供了与Cloud Manager相关的常见问题解答。

## 能否将Java 11与Cloud Manager内部版本结合使用？{#java-11-cloud-manager}

尝试将内部版本从Java 8切换到11时，AEM Cloud Manager内部版本失败。 问题可能有多种原因，最常见的原因如下：

* 按照[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)的说明，使用正确的Java 11设置添加maven-toolchains-plugin。  例如，请参阅[wknd示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果遇到以下错误，则需要删除对`maven-scr-plugin`的使用，并将所有OSGi批注转换为OSGi R6批注。 有关说明，请参阅[此处](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 对于Cloud Manager内部版本， maven enforcer插件失败，出现错误`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 这是一个已知问题，因为Cloud Manager使用不同版本的Java来运行maven命令而不是编译代码。 目前，请在maven-enforcer-plugin配置中忽略`requireJavaVersion`。

## 由于代码质量检查失败，我们的部署卡住。 有办法绕过这张支票吗？{#deployment-stuck}

除&#x200B;*安全评级*&#x200B;之外的所有代码质量故障都是非关键量度，因此可以通过扩展结果UI中的项目来绕过这些故障。

具有[部署管理器、项目经理或业务所有者](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)角色的用户可以覆盖问题，在这种情况下，管道会继续运行，或者他们可以接受问题，在这种情况下，管道会因故障而停止运行。  有关更多详细信息，请参阅运行管道时的[三层门。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)

## 在Adobe Managed Services环境中，Cloud Manager部署在性能测试步骤失败。 我们如何调试此参数以传递关键量度？{#debug-critical-metrics}

请参阅[了解测试结果](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)以了解测试结果。

有关性能测试步骤的一些说明：

* *性能步骤*&#x200B;是Web性能步骤，即使用Web浏览器加载页面的时间。
* 结果&#x200B;*CSV*&#x200B;文件中列出的URL在测试期间将加载到Cloud Manager基础架构的Chrome浏览器中。
* 失败的常见量度是&#x200B;*错误率*。 要传递URL，主URL必须以`200`状态在`20`秒内加载。 超过`20`秒的页面加载会被标记为`504`错误。
* 如果您的网站需要用户身份验证，请参阅[已验证的性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use)以配置测试以对您的网站进行身份验证。

## 我们是否允许在Maven项目的版本中使用SNAPSHOT? 包和捆绑jar文件的版本控制如何用于暂存和生产部署？{#snapshot-version}

请参阅以下方案，了解有关用于暂存和生产部署的包和包jar文件的版本化信息：

1. 对于开发人员部署，Git分支`pom.xml`文件必须在`<version>`值的末尾包含`-SNAPSHOT`。 这样，版本未更改的后续部署仍可以安装。 在开发人员部署中，不会为Maven内部版本添加或生成自动版本。

1. 在暂存和生产部署中，将生成一个自动版本，如[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)所述。

1. 对于Stage和Production部署中的自定义版本控制，请设置3个部分正确的Maven版本，如`1.0.0`。 每次必须进行其他部署到生产环境时，请增加该版本。

1. Cloud Manager会自动将其版本添加到暂存和生产内部版本，甚至会创建Git分支。 无需特殊配置。 如果跳过上述步骤3，则部署仍可正常工作，并且会自动设置一个版本。

1. 如果将版本保留为`-SNAPSHOT`（用于Stage和Production内部版本或部署），则不会出现任何问题。 Cloud Manager会自动设置正确的版本号，并在Git中为您创建一个标记。 如果需要，可以稍后引用此标记。

1. 如果要在开发环境中尝试一些实验代码，可以创建新的Git分支并设置管道以使用该不同分支。 当部署开始失败，并且您想使用旧版本的代码进行测试以查看何时被中断时，此功能非常有用。

   下面的Git命令会针对特定的预先存在的commit `485548e4fbafbc83b11c3cb12b035c9d26b6532b`创建一个名为&#x200B;*testbranch1*&#x200B;的远程分支。  此特殊分支可在Cloud Manager中使用，而不会影响任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   有关更多详细信息，请参阅[Git文档](https://git-scm.com/book/en/v2/Git-Internals-Git-References)。

   如果要稍后删除测试分支，请使用delete命令：

   `git push origin --delete testbranch1`

## 在Cloud Manager部署中，Maven生成失败，但在本地生成时没有出现错误。 如何调试？{#maven-build-fail}

有关更多详细信息，请参阅[Git资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 无法通过aio cloud manager设置管道变量来设置变量。 如何调试这些问题？{#set-variable}

如果您在尝试通过类似于以下命令的命令列出或设置管道变量时遇到`403`错误，则需要将您添加为Admin Console中的&#x200B;*部署管理器* Cloud Manager产品角色。\
有关更多详细信息，请参阅[API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)。

相关命令和错误：

`$ aio cloudmanager:list-pipeline-variables 222`

*错误*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*错误*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
