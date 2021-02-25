---
title: Cloud Manager常见问题解答
seo-title: Cloud Manager常见问题解答
description: 请参阅Cloud Manager常见问题解答，获取一些疑难解答提示
seo-description: 可查看本页以获取有关Cloud Manager常见问题解答的解答
translation-type: tm+mt
source-git-commit: 1d4f07ba0aa4630585ccbb35f2d48f0c7e1f3df2
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---


# Cloud Manager常见问题解答{#cloud-manager-faqs}

以下部分对与Cloud Manager相关的一些常见问题解答提供了解答。

## 1.是否可以将Java 11与Cloud Manager版本一起使用？{#java-11-cloud-manager}

AEM Cloud Manager在尝试将内部版本从Java 8切换到11时，生成失败。 问题可能有许多原因，最常见的原因如下：

* 按照[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)的说明，添加具有Java 11正确设置的maven-toolchains-plugin。  例如，请参阅[wknd示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果您遇到以下错误，则需要删除maven-scr-plugin的使用，并将所有OSGi注释转换为OSGi R6注释。 有关说明，请参阅[此处](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 对于Cloud Manager，生成maven enforcer插件失败，错误为`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 这是一个已知问题，因为Cloud Manager使用不同版本的java运行maven命令而不是编译代码。 目前，请在maven-enforcer-plugin配置中忽略`requireJavaVersion`。

## 2.由于代码质量检查失败，我们的部署卡住。 有办法绕过这张支票吗？{#deployment-stuck}

除&#x200B;*安全等级*&#x200B;之外的所有代码质量故障都是非关键量度，因此可以通过扩展结果UI中的项来绕过这些故障。

具有[部署管理器、项目经理或业务所有者](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)角色的用户可以覆盖问题，在这种情况下，管道继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。  有关详细信息，请参阅[运行管线时的三层门。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)

## 3. Cloud Manager部署在Adobe Managed Services环境的性能测试步骤失败。 我们如何调试它以传递关键量度？{#debug-critical-metrics}

请参阅[了解测试结果](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)了解测试结果。

有关性能测试步骤的一些注意事项：

* *性能步骤*&#x200B;是Web性能步骤 — 表示是使用Web浏览器加载页面的时间。
* 测试过程中，结果CSV文件中列出的URL将加载到Cloud Manager基础架构中的Chrome浏览器中。
* 失败的常见度量是&#x200B;*错误率*。 要传递URL，主URL必须以200状态在20秒内加载。 超过20秒的页面加载被标记为504个错误。
* 如果您的站点需要用户身份验证，请参阅[已验证性能测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use)以配置测试以验证您的站点。

## 4.我们是否允许在主项目的版本中使用SNAPSHOT? 包和捆绑jar文件的版本控制如何用于舞台和生产部署？{#snapshot-version}

1. 对于开发部署，git分支pom.xml文件必须在`<version>`值末尾包含 — SNAPSHOT。 这允许后续部署版本未更改的位置，以便仍安装。 在开发部署中，不会为主版本添加或生成任何自动版本。

1. 在舞台和生产部署中，将生成一个自动版本，如此处所述。

1. 对于舞台和生产部署中的自定义版本控制，请设置3个部分正确的授权版本，如`1.0.0`。 每次您必须进行其他部署到生产时都增加版本。

1. Cloud Manager会自动将其版本添加到舞台和生产构建中，甚至创建一个git分支。 无需特殊配置。 如果跳过上述步骤3，部署仍可正常工作，并且会自动设置一个版本。

1. 如果将版本保留为`-SNAPSHOT`用于舞台和生产构建或部署，则即使这样也可以。 Cloud Manager会自动设置适当的版本号，并在git中为您创建标记。 如果需要，可以稍后引用此标记。

1. 如果要在开发人员上尝试一些实验代码，您可以创建一个新的git分支并设置管道以使用该不同的分支。  当部署开始失败，并且您希望使用旧版本的代码进行测试，以查看代码何时断开时，此功能非常有用。

   下面的git命令针对特定的预先存在的commit `485548e4fbafbc83b11c3cb12b035c9d26b6532b`创建名为&#x200B;*testbranch1*&#x200B;的远程分支。  此特殊分支可在Cloud Manager中使用，而不会影响任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   有关详细信息，请参阅[Git文档](https://git-scm.com/book/en/v2/Git-Internals-Git-References)。

   如果稍后要删除测试分支，则使用delete命令（显然，请注意此命令）：

   `git push origin --delete testbranch1`

## 5.在Cloud Manager部署中，Maven生成失败，但在本地生成时没有错误。 如何调试？{#maven-build-fail}

有关详细信息，请参阅[Git资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 6.无法通过aio cloud manager设置管道变量来设置变量。 如何调试这些问题？{#set-variable}

如果您尝试通过类似于以下命令的命令列表或设置管道变量时遇到403错误，则需要在Admin Console中将您添加为&#x200B;*部署管理器*&#x200B;云管理器产品角色。\
有关详细信息，请参阅[API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)。

相关命令和错误：

`$ aio cloudmanager:list-pipeline-variables 222`

错误: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

错误: `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`
