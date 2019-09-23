---
title: 为Cloud manager设置常规配置
seo-title: 为Adobe AEM Cloud manager设置常规配置
description: 设置Cloud manager和从其用户界面管理内容的先决条件。
seo-description: 设置Adobe AEM Cloud manager和从其用户界面管理内容的先决条件。
uuid: 65d795f9-aa97-4816-b66b-03b5ae961f47
contentOwner: jsyal
discoiquuid: 03241b88-8d28-401b-aa42-17ead6183cd8
translation-type: tm+mt
source-git-commit: 093e25fa1cf2f5cdc3d8ea0bffd5c02ade854a88

---


# 为 [!UICONTROL Cloud Manager]{#setting-up-general-configurations-for-cloud-manager}

以下部分重点介绍从其用户界面 [!UICONTROL Cloud Manager] 设置和管理内容的先决条件。

本节页面涵盖以下主题

* **设置用户和角色**
* **AEM应用程序项目设置**
* **调度程序配置**
* **开发最佳实践**

下图说明了不同的功能，这些功能可 [!UICONTROL Cloud Manager] 以持续提供最佳质量代码：

![](assets/screen_shot_2018-05-01at81926pm.png)

## 设置用户和角色 {#setting-up-users-and-roles}

角色可从Adobe [!UICONTROL Cloud Manager] Admin Console进行管理。 通过将用户添加到Admin Console中的产品配置，可以提供特 [!UICONTROL Cloud Manager] 定的角色成员关系。

>[!CAUTION]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有Adobe ID和Adobe Managed Services产品上下文。

您可以通过在管理控制台中将用户添加到产品配置来 [!UICONTROL Cloud Manager] 分配特定的角色成员关系。

使用Admin Console为以下对象创建以下角色 [!UICONTROL Cloud Manager]:

>[!NOTE]
>
>Adobe Admin Console提供了一个中心位置，用于管理整个组织中的Adobe授权。
>
>要进一步了解Adobe Admin Console，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/admin-console.html)。

| **[!UICONTROL Cloud Manager]角色** | **描述** |
|---|---|
| 企业所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 计划经理 | 用于 [!UICONTROL Cloud Manager] 执行团队设置、审核状态和查看KPI。 可能批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 用于 [!UICONTROL Cloud Manager] 执行舞台／生产部署。 可能批准重要的3层故障。 具有git访问权限。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要用 [!UICONTROL Cloud Manager] 于查看状态。 提交git访问权限。 |
| 客户成功工程师 | 通常支持AMS客户的成功。 与之交 [!UICONTROL Cloud Manager] 互以执行需要CSE监督的部署。 |
| 内容作者 | 通常不与交互 [!UICONTROL Cloud Manager]。 可使用 [!UICONTROL Cloud Manager] 程序切换程序(已从中导航 [!UICONTROL Experience Cloud])访问AEM。 |

### 使用Admin Console设置团队 {#using-admin-console-to-set-up-team}

为了向用户提供相应的基于角色的权限，客 [!UICONTROL Cloud Manager] 户组织中的管理员必须在“产品上下文”下创建新的产品 [!UICONTROL AEM Managed Services] 配置文件。

>[!NOTE]
>
>要访问管理控制台并设置您的团队（用户和角色），请打开浏览器并访问 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

将用户（或用户组）添加到这些产品配置是使用常规的Admin Console功能完成的，如下图所示：

1. 登录到Admin Console，然后单击“新 **建配置文件** ”以添加新配置文件。

   ![](assets/admin_console_roles.png)

1. 填写字段以设置新角色 [!UICONTROL Cloud Manager]。

   输入 **配置文件名称**、 **说明** ，以创建新配置文件。 此外，您还可以为配置 **文件选择权限组** 。

   单击 **完成** ，以完成配置文件创建步骤。

   ![](assets/screen_shot_2018-04-23at75014am.png)

## AEM应用程序项目设置 {#aem-application-project-setup}

在中设置应用程序项 [!UICONTROL Cloud Manager]目之前，您必须考虑两种情况之一。 您可能是AEM 6.4的新用户，或者已经是现有客户。

>[!NOTE]
>
>要获得访问权限，请联 [!UICONTROL Cloud Manager]系客户成功工程师(CSE)以获取URL和凭据以开始使用。

您可以根据以下两种情 [!UICONTROL Cloud Manager]况为设置应用程序项目：

* **新AEM项目**:

新的AEM项目将利用您的现有项目并进行处理 [!UICONTROL Cloud Manager]。

有关其他信息，请 [参阅AEM 6.4快速入门](https://chl-author./content/help/en/experience-manager/6-4/sites/deploying/using/deploy.html)。 此外，请参阅 [AEM资源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&mv=other) ，以了解更多信息。

* **现有AEM项目**:

现有AEM项目必须确认要设置项目的规则。 您可以升级现有AEM安装，以获取AEM 6.4中提供的新功能和增强功能，并开始使用 [!UICONTROL Cloud Manager]。 这些标准应在最小的更改量内工作。 联系客户成功工程师(CSE)寻求支持。

要获取有关将AEM实例升级到6.4的其他信息，请参 [阅升级到AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

### 设置存储库 {#setting-up-repository}

为已登录的每个程序配置一个初始为空的git存储库 [!UICONTROL Cloud Manager]。 开发人员和部署经理会从他们的CSE中获得git URL和凭据。

利用此信息，开发人员可以按照下面的**项目设置**中的准则添加其代码，以在使用之前完成设置要求 [!UICONTROL Cloud Manager]。

## 调度程序配置 {#dispatcher-configurations}

[!UICONTROL Cloud Manager] 能够部署Web服务器和调度程序配置文件（假定它们存储在git存储库中），而不是常规AEM内容包。

为了利用此功能，Maven内部版本会生成一个包含两个目录的zip文件- ***conf******和conf.d***。

部署到调度程序实例后，这些目录的内容将覆盖调度程序实例中这些目录的内容。 由于Web服务器和调度程序配置文件经常需要环境特定信息，为了使此功能正确使用，您首先需要与其客户成功工程师(CSE)合作，将这些环境变量解压缩到/etc/sysconfig/httpd中。

按照以下步骤完成配置调度程序的初始过程：

1. 从其CSE获取当前生产配置文件。
1. 删除硬编码的环境特定数据（例如，发布渲染器IP）并替换为变量。
1. 在每个目标调度程序的键值对中定义所需的变量，并请求CSE在每个实例上添加 ***/etc/sysconfig/httpd*** 。
1. 在舞台上测试更新的配置，然后请求CSE部署到生产，以确保它们正常工作。
1. 将文件提交到git。
1. 通过部署 [!UICONTROL Cloud Manager]。

实际的zip文件可以使用maven-assembly-plugin生成。 使用Lazybones AEM多模块模板生成的项目可以在项目创建过程中创建正确的Maven项目结构。

>[!NOTE]
>
>配置调度程序是在入门期间完成的， [!UICONTROL Cloud Manager]但也可以在稍后阶段完成。

### 配置Dispatcher以进行性能测试 {#configuring-dispatcher-for-performance-testing}

为了正确 [!UICONTROL Cloud Manager] 运行性能测试，舞台调度程序服务器必须以与生产调度程序一致的方式响应与生产调度程序相同的主机名。

*例如*，如果客户的生产主机名是 [www.myco.com](http://www.myco.com/) and www.myotherco.com [](http://www.myotherco.com,/) ，而stage-myco.adobecqms.net是其阶段主机名，则此类请求必须相应地作出响应：

```
curl -H"Host: www.myco.com" http://stage-myco.adobecqms.net/en/home.html
```

这不仅要求在调度程序配置中正确配置主机名，而且要求以一致的方式在舞台和生产之间实现 ***/etc/map***、任何Apache重写或真正的任何其他路径 ****** 映射／过滤器规则。

## 开发最佳实践 {#development-best-practices}

在使用 [!UICONTROL Cloud Manager]之前，最好了解一些设置项目和配置Web服务器或分区配置的最佳实践。

### 项目设置 {#project-set-up}

要处理您的项目，必须遵循一些标准 [!UICONTROL Cloud Manager]。

按照以下项目中设置项目的最佳实践进行操 [!UICONTROL Cloud Manager]作：

* 唯一提供和支持的构建工具是Apache Maven。 已安装Apache Maven 3.3.9。
* 内部版本以根用户身份在Docker容器的Linux环境中运行。
* 安装的Java版本为Oracle JDK 8u161。
* 还安装了一些其他系统包，如bzip2、unzip、libpng、imagemagick和graphicsmagick。 如果您需要其他包，您需要通过CSE申请这些包。
* Maven始终使用命令mvn -B clean包运行。
* 您将仅获得一个git存储库。 此存储库的根中必须有pom.xml文件。 此pom.xml文件可以引用多个子模块（这些子模块又可能具有其他子模块等）必要，但只有一个入口点。
* Maven在系统级别上配置了settings.xml文件，该文件自动包括公共Adobe对象存储库(repo.adobe.com)。
* 您可以在pom.xml文件中添加其他存储库。 但是，不支持访问受口令保护或受网络保护的对象存储库。
* 通过扫描包含在名为target的目录中的zip文件，可以发现可部署的内容包。 同样，任意数量的子模块可以生成内容包。
* 如果有多个内容包，则不保证包部署的排序。 如果需要特定的顺序，可以使用内容包依赖关系来定义顺序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-05-02T18:18:15.028-0400

change as per KT

 -->

### 后续步骤 {#the-next-steps}

设置常规配置后，即可使用 [!UICONTROL Cloud Manager]。

请参 [阅使用[!UICONTROL Cloud Manager]](https://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) ，开始使用 [!UICONTROL Cloud Manager]。
