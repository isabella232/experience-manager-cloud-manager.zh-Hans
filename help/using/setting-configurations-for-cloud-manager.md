---
title: 设置云管理器的常规配置
seo-title: 为Adobe AEM Cloud Manager设置常规配置
description: 用于设置Cloud Manager和从其用户界面管理内容的先决条件。
seo-description: 用于设置Adobe AEM Cloud Manager和从其用户界面管理内容的先决条件。
uuid: 65d795f9-aa97-4816-b66 b-03b5 ae961 f47
contentOwner: jsyal
discoiquuid: 03241b888-401b-aa42-17ead621-17ead6183 cd8
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 设置常规配置 [!UICONTROL Cloud Manager]{#setting-up-general-configurations-for-cloud-manager}

下节突出显示了用于从用户界面设置 [!UICONTROL Cloud Manager] 和管理内容的先决条件。

本节页面涵盖以下主题

* **设置用户和角色**
* **AEM应用程序项目设置**
* **调度程序配置**
* **开发最佳实践**

下图说明了可持续提供最佳质量 [!UICONTROL Cloud Manager] 代码的不同函数：

![](assets/screen_shot_2018-05-01at81926pm.png)

## 设置用户和角色 {#setting-up-users-and-roles}

角色是通过 [!UICONTROL Cloud Manager] Adobe Admin Console管理的。通过将用户添加到Admin Console中的 [!UICONTROL Cloud Manager] 产品配置文件，可以提供特定的角色会员资格。

>[!CAUTION]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有一个Adobe ID和Adobe Managed Services产品上下文。

您可以通过将用户添加到Admin Console中的 [!UICONTROL Cloud Manager] 产品配置文件来分配特定的角色会员资格。

使用Admin Console创建以下角色 [!UICONTROL Cloud Manager]：

>[!NOTE]
>
>Adobe Admin Console提供了一个中心位置，用于在整个组织内管理Adobe权益。
>
>要了解有关Adobe Admin Console的更多信息，请参阅 [Admin Console的文档](https://helpx.adobe.com/enterprise/using/admin-console.html)。

| **[!UICONTROL Cloud Manager]角色** | **描述** |
|---|---|
| 业务所有者 | 负责定义KPI、批准生产部署并覆盖重要的层故障。 |
| 计划经理 | 用于 [!UICONTROL Cloud Manager] 执行团队设置、审核状态和查看KPI。可能批准重要的层故障。 |
| 部署管理器 | 管理部署操作。用于 [!UICONTROL Cloud Manager] 执行舞台/生产部署。可能批准重要的层故障。获得git访问权限。 |
| 开发人员 | 开发和测试自定义应用程序代码。主要用于 [!UICONTROL Cloud Manager] 查看状态。承诺访问git。 |
| 客户成功工程师 | 通常支持AMS客户的客户成功。与执行 [!UICONTROL Cloud Manager] 需要CSE监控的部署进行交互。 |
| 内容作者 | 通常不与之交互 [!UICONTROL Cloud Manager]。可以使用 [!UICONTROL Cloud Manager] 节目切换程序(导航自 [!UICONTROL Experience Cloud])访问AEM。 |

### 使用管理控制台设置团队 {#using-admin-console-to-set-up-team}

为了向 [!UICONTROL Cloud Manager] 用户提供基于角色的适当权限，客户组织中的管理员必须在 [!UICONTROL AEM Managed Services] 产品上下文下创建新的产品配置文件。

>[!NOTE]
>
>要调用管理控制台并设置您的团队(用户和角色)，请打开浏览器并访问 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

使用正常的Admin Console功能将用户(或用户组)添加到这些产品配置文件中，如下图所示：

1. 登录到Admin Console，然后单击 **新建配置文件** 以添加新配置文件。

   ![](assets/admin_console_roles.png)

1. 填写字段以为其设置新角色 [!UICONTROL Cloud Manager]。

   输入 **配置文件名称**， **说明** 以创建新配置文件。此外，您还可以为配置文件选择 **权限组** 。

   单击 **完成** 以完成配置文件创建步骤。

   ![](assets/screen_shot_2018-04-23at75014am.png)

## AEM应用程序项目设置 {#aem-application-project-setup}

在中 [!UICONTROL Cloud Manager]设置应用程序项目之前，您必须考虑两种情况之一。您可能是AEM6.4的新用户，或者已经是现有客户。

>[!NOTE]
>
>要获得访问权限 [!UICONTROL Cloud Manager]，请联系客户成功工程师(CSE)以获取入门的URL和凭据。

您可以根据以下两种情况 [!UICONTROL Cloud Manager]设置应用程序项目：

* **新AEM项目**：

新的AEM项目将利用您现有的项目和处理 [!UICONTROL Cloud Manager]。

有关更多信息，请参阅 [AEM6.4快速入门](https://chl-author./content/help/en/experience-manager/6-4/sites/deploying/using/deploy.html)。此外，请参阅 [AEM资源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&mv=other) 以了解更多信息。

* **现有AEM项目**：

现有AEM项目必须确认设置为项目设置。您可以升级现有AEM安装，获得AEM6.4中提供的新功能和增强功能，并开始使用 [!UICONTROL Cloud Manager]。这些标准的更改幅度最小。联系客户成功工程师(CSE)以获得支持。

要获取有关将AEM实例升级到6.4的更多信息，请参阅 [升级到AEM6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

### 设置存储库 {#setting-up-repository}

单个(最初为空)存储库为传入的每个程序提供一个初始存储库 [!UICONTROL Cloud Manager]。开发人员和部署经理通过CSE提供Git URL和凭据。

利用此信息，开发人员可以在下面的入门部分中按照**项目设置**中**项目设置**中的指导原则添加自己的代码，以便在使用之前完成设置要求 [!UICONTROL Cloud Manager]。

## 调度程序配置 {#dispatcher-configurations}

[!UICONTROL Cloud Manager] 除了普通AEM内容包外，还可以部署Web服务器和调度程序配置文件，假定它们存储在Git存储库中。

要利用此功能，Maven构建生成一个zip文件，其中包含两个目录 ***- conf*** 和 ***conf. d***。

部署到调度程序实例后，这些目录的内容将覆盖调度程序实例上这些目录的内容。由于Web服务器和调度程序配置文件经常需要环境特定的信息，因此，要使此功能能够正确使用，您首先需要与客户成功工程师(CSE)一起将这些环境变量提取到/etc/sysconfig/httpd中。

请按照以下步骤完成配置调度程序中的初始进程：

1. 从CSE获取当前生产配置文件。
1. 删除硬编码的环境特定数据(例如，发布渲染器IP)并替换为变量。
1. 为每个目标调度程序定义键值对中所需的变量，并请求CSE添加到每个实例上的 ***/etc/sysconfig/httpd*** 。
1. 测试更新的配置，然后请求CSE部署到生产以确保它们正常工作。
1. 将文件提交到Git。
1. 部署 [!UICONTROL Cloud Manager]。

实际zip文件可使用maven-assembly-plugin生成。使用Lazbyones AEM Multivariate Template生成的项目可以拥有创建项目的正确Maven项目结构。

>[!NOTE]
>
>配置调度程序是在内置的入门过程中完成 [!UICONTROL Cloud Manager]的，但也可以在以后的阶段完成。

### 为性能测试配置Dispatcher {#configuring-dispatcher-for-performance-testing}

为了正确 [!UICONTROL Cloud Manager] 运行性能测试，舞台调度程序服务器必须以与生产服务器一致的方式响应与生产调度程序相同的主机名。

*例如*，如果客户将 [www.myco.com](http://www.myco.com/) 和 [www.myotherco.com](http://www.myotherco.com,/) 作为生产主机名和stage-myco. adobecqms. net作为其舞台主机名，则如下所示的请求必须适当：

```
curl -H"Host: www.myco.com" http://stage-myco.adobecqms.net/en/home.html
```

这不仅需要在调度程序配置中正确配置主机名，还需要在 ***舞台和生产之间以一致的方式实现/etc/map***、任何Apache重写或真正任何其他路径 ***映射/过滤器*** 规则。

## 开发最佳实践 {#development-best-practices}

在使用 [!UICONTROL Cloud Manager]之前，了解设置项目和配置Web服务器或配置配置的一些最佳实践是明智的。

### 项目设置 {#project-set-up}

您的项目必须符合一些条件才能使用 [!UICONTROL Cloud Manager]。

请遵循以下设置项目的最佳实践 [!UICONTROL Cloud Manager]：

* 提供和支持的唯一构建工具是Apache Maven。Apache Maven3.3.9已安装。
* 构建在Docker容器中的Linux环境中作为根用户运行。
* 安装的Java版本为Oracle JDK8u161。
* 还安装了一些其他系统包，如bzip2、unzip、libpng、imagemagick和graphicsmagick。如果您需要其他包，则需要通过CSE请求这些包。
* Maven始终使用命令mvn -B清理包运行。
* 将只提供一个Git存储库。此存储库的根目录中必须有一个pom.xml文件。此pom.xml文件可以引用任意多个子模块(反过来可能有其他子模块等)。但必须只有一个入口点。
* Maven是在系统级别上配置的，settings.xml文件会自动包含公共Adobe伪像存储库(repo.adobe.com)。
* 您可以在pom.xml文件中添加其他存储库。但是，不支持访问受密码保护或受网络保护的伪像库。
* 可部署内容包是通过扫描包含在名为target的目录中的zip文件来发现的。同样，任何数量的子模块都可能生成内容包。
* 如果有多个内容包，则不保证包部署的顺序。如果需要特定订单，则可使用内容包依赖关系定义订单。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-05-02T18:18:15.028-0400

change as per KT

 -->

### 后续步骤 {#the-next-steps}

设置常规配置 [!UICONTROL Cloud Manager]后，即可使用。

请参阅 [使用[！UICCONTROL Cloud Manager]开始](https://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html)[!UICONTROL Cloud Manager]使用。
