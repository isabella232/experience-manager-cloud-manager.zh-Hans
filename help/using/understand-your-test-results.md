---
title: 理解测试结果
seo-title: 理解测试结果
description: 了解有关在Cloud Manager中运行管道时三层门的更多信息
seo-description: 可查看本页，了解在Cloud Manager中运行管道、代码扫描、性能和安全测试验证项目时的三层门。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
translation-type: tm+mt
source-git-commit: f62c967feec3960499de93443548422167fedfa7
workflow-type: tm+mt
source-wordcount: '2681'
ht-degree: 3%

---


# 理解测试结果 {#understand-your-test-results}

在管道执行过程中，会捕获许多量度并将其与由业务所有者定义的关键绩效指标(KPI)或Adobe Managed Services设置的标准进行比较。

这些是使用本节中定义的三层门控系统报告的。

## 运行管线{#three-tier-gates-while-running-a-pipeline}时的三层门

有三扇大门正在酝酿之中：

* 代码质量
* 性能测试
* 安全测试

对于每个门，门所识别的问题都有三层结构。

* **关键**  — 这些是门所发现的问题，会导致管道立即失败。
* **重要**  — 这些是由门识别的问题，它们导致管道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，管道继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。
* **Info**  — 这些是门所识别的问题，它们仅用于信息目的，对管道执行没有影响。

>[!NOTE]
>
>在仅代码质量管道中，无法覆盖代码质量测试门中的重要失败，因为代码质量测试步骤是管道中的最后一步。

## 代码质量测试{#code-quality-testing}

此步骤将评估应用程序代码的质量。 它是仅代码质量管道的核心目标，在所有非生产和生产管道中的构建步骤后立即执行。 有关不同类型管道的更多信息，请参阅[配置CI-CD管道](/help/using/configuring-pipeline.md)。

### 了解代码质量测试{#understanding-code-quality-testing}

在“代码质量测试”中，将扫描源代码，以确保它符合某些质量标准。 目前，这是通过SonarQube、使用OakPAL的内容包级别检查和使用Dispatcher Optimization Tool的调度程序验证的组合实现的。 有100多个规则组合通用Java规则和AEM特定规则。 某些特定于AEM的规则是根据AEM工程部门的最佳实践创建的，称为[自定义代码质量规则](/help/using/custom-code-quality-rules.md)。

>[!NOTE]
>您可以在此处](/help/using/assets/CodeQuality-rules-AMS.xlsx)下载规则[的完整列表。

此步骤的结果以&#x200B;*Rating*&#x200B;的形式提供。 下表总结了各种测试标准的评级：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞<br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞<br/>D =至少1个关键漏洞<br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A = 0错误<br/>B =至少1个次要错误<br/>C =至少1个主要错误<br/>D =至少1个关键错误<br/>E =至少1个阻止程序错误 | 重要 | &lt; C |
| 可维护性等级 | 代码气味的未支付补救成本是：<br/><ul><li>&lt;> </li><li>在6%到10%的评级是B </li><li>11%至20%的评级为C </li><li>21%到50%的评级是D</li><li>超过50%的是E</li></ul> | 重要 | &lt; A |
| 范围 | 使用以下公式的单位测试行覆盖和条件覆盖的组合：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>其中：CT =运行单元测试时已至少评估为“true”的条件，运行单元测试时，CF =已评估为“false”的条件，运行单元测试时，LC =覆盖行=行=tocover -uncoveredlines <br/><br/>B =条件总数<br/>EL =可执行行(linestocover)<br/><br/> | 重要 | &lt; 50% |
| 跳过的单元测试 | 已跳过的单元测试数。 | 信息 | > 1 |
| 未解决问题 | 总体问题类型 — 漏洞、错误和代码气味 | 信息 | > 0 |
| 复制行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块：  <br/><ul><li>**非Java项目：**</li><li>至少应有100个连续令牌和重复令牌。</li><li>这些令牌应至少在以下位置进行传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，适用于其他语言</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续的重复语句。</li></ul> <br/>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的Cloud Service兼容性问题数。 | 信息 | > 0 |


>[!NOTE]
>
>有关更详细的定义，请参阅[量度定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)。

>[!NOTE]
>
>要进一步了解由[!UICONTROL Cloud Manager]执行的自定义代码质量规则，请参阅[自定义代码质量规则](custom-code-quality-rules.md)。

### 处理误报{#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际没有问题的问题。 这被称为&quot;假阳性&quot;。

在这些情况下，可以使用标准Java `@SuppressWarnings`注释对源代码进行注释，该注释将规则ID指定为注释属性。 例如，一个常见问题是，用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能具有攻击性。

要查看特定示例，此代码在AEM项目中很常见，该项目包含连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube随后将引发Blocker漏洞。 查看代码后，您会发现这不是漏洞，并可以使用相应的规则ID对此进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代码是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，正确的解决方案是删除硬编码密码。

>[!NOTE]
>
>尽管最好尽可能使`@SuppressWarnings`注释具体化，即仅注释导致问题的特定语句或块，但也可以在类级别添加注释。

## 安全测试{#security-testing}

[!UICONTROL Cloud Manager] 在部署后 ***运行现*** 有的AEM安全健康检查阶段，并通过UI报告状态。结果将从该环境中的所有AEM实例聚集。

可以随时通过Web控制台或操作仪表板执行这些相同的运行状况检查。

如果任何&#x200B;**实例**&#x200B;报告给定运行状况检查失败，则整个&#x200B;**环境**&#x200B;将失败该运行状况检查。 与代码质量和性能测试一样，这些运行状况检查会组织到类别中，并使用三层选通系统报告。 唯一的区别是，在安全测试方面没有阈值。 所有健康检查都是通过或失败的。

下表列表了当前检查：

| **名称** | **运行状况检查实施** | **类别** |
|---|---|---|
| 反序列化防火墙连接API就绪状态为可接受状态 | [反序列化防火墙连接 API 已准备就绪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 关键 |
| 反序列化防火墙功能正常 | [反序列化防火墙运行正常](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 关键 |
| 反序列化防火墙已加载 | [反序列化防火墙已加载](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 关键 |
| AuthorizableNodeName实现不会在节点名称/路径中显示可授权ID。 | [可授权的节点名称生成](https://experienceleague.adobe.com/docs/experience-manager-64/administering/security/security-checklist.html?lang=en#security) | 关键 |
| 默认密码已更改 | [默认登录帐户](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=en#users-and-groups-in-aem) | 关键 |
| Sling默认GETServlet受DOS攻击保护。 | Sling Get Servlet | 关键 |
| Sling Java脚本处理程序已正确配置 | Sling Java 脚本处理程序 | 关键 |
| Sling JSP脚本处理程序已正确配置 | Sling JSP脚本处理程序 | 关键 |
| 正确配置了SSL | SSL 配置 | 关键 |
| 未发现明显不安全的用户用户档案策略 | 用户配置文件默认访问 | 关键 |
| 配置Sling推荐人过滤器以防止CSRF攻击 | [Sling 引用过滤器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#security) | 重要 |
| Adobe Granite HTML库管理器已正确配置 | CQ HTML 库管理器配置 | 重要 |
| 已禁用CRXDE支持包 | CRXDE 支持 | 重要 |
| 已禁用Sling DavEx捆绑包和Servlet | DavEx 运行状况检查 | 重要 |
| 未安装示例内容 | 示例内容包 | 重要 |
| WCM请求过滤器和WCM调试过滤器都被禁用 | [WCM 筛选器配置](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=en#configuring) | 重要 |
| Sling WebDAV包和Servlet已正确配置 | WebDAV 运行状况检查 | 重要 |
| Web服务器配置为防止点击劫持 | Web 服务器配置 | 重要 |
| 复制未使用“admin”用户 | 复制和转移用户 | 信息 |

## 性能测试{#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager可对AEM Sites项目执行性能测试。 通过启动虚拟用户(容器)来运行性能测试约30分钟，这些虚拟用户模拟实际用户访问舞台环境上的页面并模拟流量。 这些页面是使用Crawler找到的。

1. **虚拟用户**

   由Cloud Manager启动的虚拟用户或容器的数量由[创建或编辑项目](setting-up-program.md)时用户在“业务所有者”角色中定义的KPI（响应时间和页面查看次数/分钟）驱动。 根据定义的KPI，最多将生成10个容器，模拟实际用户。 为测试选择的页面将拆分并分配给每个虚拟页面。

1. **Crawler**

   在30分钟测试期开始之前，Cloud Manager将使用由客户成功工程师配置的一组一个或多个种子URL来爬网舞台环境。 从这些URL开始，将检查每个页面的HTML，并以宽度优先的方式遍历链接。 此爬网过程最多限制为5000页。 来自Crawler的请求具有10秒的固定超时。

1. **用于测试的页面集**

   页面由三个页面集选择。 Cloud Manager使用跨生产和舞台的AEM实例中的访问日志来确定以下三个时段：

   * *热门实时页面*:选中此选项可确保测试实时客户访问的最受欢迎页面。Cloud Manager将读取访问日志并确定活动客户访问量最大的25个页面，以生成前`Popular Live Pages`的列表。 这些在舞台中也存在的交集随后在舞台环境上爬网。

   * *其他实时页面*:选中此选项可确保测试不在前25个热门实时页面之外、但对测试很重要的页面。与“常用”活动页面类似，这些活动页面从访问日志中提取，并且必须也存在在舞台上。

   * *新页面*:选择此选项以测试可能仅部署到舞台且尚未部署到生产但必须测试的新页面。

      **所选页面集之间的流量分布**

      在管线配置（“插入”链接）的“测试”选项卡中，您可以从一组到三组的任意位置进行选择。 流量的分配基于所选集数，即如果全部选择了三个集，则每组将占总页面视图的33%;如果选择了两个，则50%将转至每个集；如果选择了一个，则100%的流量将转到该集。

      例如，假设“常用实时页面”和“新页面”集（在此示例中，不使用其他实时页面）之间存在50% - 50%的拆分，而“新页面”集包含3000页。 页面视图每分钟KPI设置为200。 在30分钟的测试期间：

      * “热门实时页面”集中的25页中的每页将被点击120次 — ((200 * 0.5)/ 25)* 30 = 120

      * “新页面”集中的3000页中的每页将点击一次 — ((200 * 0.5)/ 3000)* 30 = 1

#### 测试和报告{#testing-reporting}

Cloud Manager在30分钟的测试时间内在舞台发布服务器上请求页面（默认情况下为未经过身份验证的用户），并测量（虚拟）用户生成的量度(响应时间、错误率、每分钟视图等)，从而执行AEM Sites项目的性能测试 以及所有实例的各种系统级度量（CPU、内存、网络数据）。\
下表总结了使用三层门控系统的性能测试指标：

下表总结了使用三层门控系统的性能测试矩阵：

| **量度** | **类别** | **失败阈值** |
|---|---|---|
| 页面请求错误率% | 关键 | >= 2% |
| CPU利用率 | 关键 | >= 80% |
| 磁盘IO等待时间 | 关键 | >= 50% |
| 95百分点响应时间 | 重要 | >=项目级KPI |
| 峰值响应时间 | 重要 | >= 18秒 |
| 页面视图每分钟 | 重要 | &lt; Program-level=&quot;&quot; KPI=&quot;&quot;> |
| 磁盘带宽利用 | 重要 | >= 90% |
| 网络带宽利用 | 重要 | >= 90% |
| 每分钟请求数 | 信息 | >= 6000 |

有关使用基本身份验证进行站点和资产性能测试的详细信息，请参阅下面的&#x200B;**已验证的性能测试**&#x200B;部分。

>[!NOTE]
>在测试期间，将监视每个实例，包括发布和作者。 如果未获取任何度量，则该度量将报告为未知，且相应步骤将失败。

#### 已验证的性能测试{#authenticated-performance-testing}

此功能为“站点”可选。
具有已验证站点的AMS客户可以指定Cloud Manager在站点性能测试期间用来访问网站的用户名和密码。
用户名和密码指定为名称为`CM_PERF_TEST_BASIC_USERNAME`和`CM_PERF_TEST_BASIC_PASSWORD`的Pipeline Variables。
尽管并非严格要求，但建议将字符串变量类型用于用户名，将secretString变量类型用于密码。 如果同时指定了这两个凭据，则来自性能测试Crawler和测试虚拟用户的每个请求都将包含这些凭据作为HTTP Basic身份验证。

要使用Cloud Manager CLI设置这些变量，请运行：

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

请参阅[变量](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchPipelineVariables)以了解如何使用API。

### AEM Assets {#aem-assets}

Cloud Manager通过在30分钟的测试时间内重复上传资产，执行AEM Assets项目的性能测试。

1. **入职要求**

   对于Assets性能测试，您的客户成功工程师将在创作到阶段环境的启动过程中创建一个`cloudmanager`用户（和密码）。 性能测试步骤需要名为`cloudmanager`的用户以及由CSE设置的关联密码。 不应从作者中删除，也不应将其更改为权限。 这样做很可能会失败Assets性能测试。

1. **用于测试的图像和资产**

   客户可以上传自己的资产进行测试。 这可以从“管线设置”(Pipeline Setup)或“编辑”(Edit)屏幕中完成。 支持JPEG、PNG、GIF和BMP等常见图像格式以及Photoshop、Illustrator和Postscript文件。 但是，如果未上传图像，Cloud Manager将使用默认图像和PDF文档进行测试。

1. **用于测试的资产分发**

   在“管道设置”或“编辑”屏幕中设置每分钟上传的每种类型资源的分布。
例如，如下图所示，如果使用70/30拆分。 每分钟上传10个资产，每分钟上传7个图像，3个文档。

1. **测试和报告**

   Cloud Manager将使用CSE在上述步骤#1（入门要求）中设置的用户名和密码在作者实例上创建一个文件夹，并使用开放源代码库在文件夹中上传资产。 使用此[开源库](https://github.com/adobe/toughday2)写入Assets测试步骤运行的测试。 每个资产的处理时间以及各种系统级量度都会在30分钟的测试持续时间内进行测量。 此功能可以上传图像和PDF文档。

   >[!NOTE]
   >您可以从[配置CI/CD管道](configuring-pipeline.md)了解有关配置性能测试的更多信息。 请参阅[设置项目](setting-up-program.md)，了解如何设置项目和定义KPI。

### 性能测试结果图表{#performance-testing-results-graphs}

新图形和下载选项已添加到“性能测试结果”对话框。

打开“性能测试”对话框时，可以展开量度面板以显示图表、提供下载链接或同时显示两者。

对于[!UICONTROL Cloud Manager] 2018.7.0版，此功能适用于以下量度：

* **CPU利用率**
   * 测试期间CPU利用率的图表。

* **磁盘I/O等待时间**
   * 测试期间磁盘I/O等待时间图表。

* **页面错误率**
   * 测试期间每分钟的页面错误图。
   * 一个CSV文件，其中列出了在测试过程中生成错误的页面。

* **磁盘带宽利用**
   * 测试期间磁盘带宽利用率图。

* **网络带宽利用**
   * 测试期间的网络带宽利用率图。

* **峰值响应时间**
   * 测试期间每分钟的峰值响应时间图。

* **第95百分点响应时间**
   * 测试期间每分钟第95个百分点响应时间的图。
   * 一个CSV文件，列出其第95百分点响应时间超过定义的KPI的页面。

以下图像显示性能测试图：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

