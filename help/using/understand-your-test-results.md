---
title: 了解测试结果
description: 了解管道的代码质量测试的工作原理，以及它如何提高部署质量。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
feature: CI-CD Pipeline, Test Results
exl-id: 6a574858-a30e-4768-bafc-8fe79f928294
source-git-commit: 2179314120911cac8a0dd99a8b57974751959871
workflow-type: tm+mt
source-wordcount: '2897'
ht-degree: 3%

---

# 了解测试结果 {#understand-your-test-results}

了解管道的代码质量测试的工作原理，以及它如何提高部署质量。

## Communications API {#introduction}

在管道执行期间，会捕获许多量度并将其与业务所有者定义的关键绩效指标(KPI)或Adobe Managed Services设置的标准进行比较。

这些报告使用下一节中定义的三层评级系统进行报告

>[!NOTE]
>
>要了解Cloud Manager支持的AEMas a Cloud Service测试，请参阅 [AEMas a Cloud Service文档。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html).


## 三级评级  {#three-tier-gates-while-running-a-pipeline}

管道中有三扇门：

* 代码质量
* 性能测试
* 安全测试

对于每个门，都有一个由门标识的问题的三层结构。

* **关键**  — 这些是导致管道立即失败的问题。
* **重要信息**  — 这些问题导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下管道会继续），也可以接受问题（在这种情况下，管道会因故障而停止）。 重要失败的覆盖受 [超时。](deploying-code.md#timeouts)
* **信息**  — 这些问题仅供参考，对管道执行没有影响。

>[!NOTE]
>
>在仅代码质量管道中，无法覆盖“代码质量”门中的重要故障，因为代码质量测试步骤是管道中的最后一步。

## 代码质量测试 {#code-quality-testing}

此步骤会评估应用程序代码的质量，该代码是仅代码质量管道的主要目的，将立即在所有非生产和生产管道中执行构建步骤。 请参阅该文档 [配置非生产管道](configuring-non-production-pipelines.md) 以了解更多。

### 了解代码质量测试 {#understanding-code-quality-testing}

代码质量测试会扫描源代码，以确保它符合特定质量标准。 这是通过SonarQube分析、使用OakPAL的内容包级别检查以及使用调度程序优化工具进行调度程序验证的组合来实现的。

有100多个规则可组合通用Java规则和特定于AEM的规则。 某些特定于AEM的规则是根据AEM Engineering中的最佳实践创建的，称为 [自定义代码质量规则。](/help/using/custom-code-quality-rules.md)

>[!NOTE]
>
>您可以下载规则的完整列表 [使用此链接。](/help/using/assets/CodeQuality-rules-latest-AMS.xlsx)

代码质量测试的结果将以 **评级**. 下表汇总了各种测试标准的评级。

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全评级 | A =无漏洞<br/>B =至少1个次要漏洞<br/>C =至少1个主要漏洞<br/>D =至少1个关键漏洞<br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性评级 | A =无错误<br/>B =至少1个次要错误 <br/>C =至少1个主要错误<br/>D =至少1个严重错误<br/>E =至少1个阻止程序错误 | 重要信息 | &lt; C |
| 可维护性评级 | 由代码气味的未解决修复成本定义，以已进入应用程序的时间的百分比表示<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = > 50%</li></ul> | 重要信息 | &lt; A |
| 范围 | 由单位测试线覆盖率和条件覆盖率的混合使用公式定义： <br/>`Coverage = (CT + CF + LC) / (2 * B + EL)`  <ul><li>`CT` =已评估为 `true` 运行单元测试时至少一次</li><li>`CF` =已评估为 `false` 运行单元测试时至少一次</li><li>`LC` =覆盖行= lines_to_cover - oncovered_lines</li><li>`B` =条件总数</li><li>`EL` =可执行行的总数(linestocover)</li></ul> | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数 | 信息 | > 1 |
| 未决问题 | 总体问题类型 — 漏洞、错误和代码气味 | 信息 | > 0 |
| 复制的行 | 定义为重复块中涉及的行数。 在以下条件下，代码块会被视为重复的代码块。<br>非Java项目：<ul><li>应至少有100个连续令牌和重复令牌。</li><li>这些令牌应至少分布在以下几个位置： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，用于其他语言</li></ul>Java项目：<ul></li><li> 无论令牌和行的数量如何，都应至少有10个连续的和重复的语句。</li></ul>在检测重复项时，将忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的Cloud Service兼容性问题的数量 | 信息 | > 0 |

>[!NOTE]
>
>请参阅 [SonarQube的度量定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 以了解更多详细信息。

>[!NOTE]
>
>了解有关执行的自定义代码质量规则的更多信息 [!UICONTROL Cloud Manager]，请参阅此文档 [自定义代码质量规则。](custom-code-quality-rules.md)

### 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际上没有问题的问题。 这称为 **误报**.

在这些情况下，可以使用标准Java对源代码进行注释 `@SuppressWarnings` 将规则ID指定为注释属性的注释。 例如，一个常见的误报是，用于检测硬编码密码的SonarQube规则在识别硬编码密码的方式上可能过于激进。

以下代码在AEM项目中相当常见，该项目中有用于连接到某些外部服务的代码。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube随后会引发拦截器漏洞。 但是，在查看代码后，您会发现这不是一个漏洞，并且可以使用相应的规则ID对代码进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，如果代码为：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那么，正确的解决方案就是删除硬编码密码。

>[!NOTE]
>
>虽然最好的做法是 `@SuppressWarnings` 尽可能具体的注释（即仅对导致问题的特定语句或块添加注释）可以在类级别添加注释。

## 安全测试 {#security-testing}

[!UICONTROL Cloud Manager] 运行现有 **AEM安全性健康检查** 部署后在暂存环境中运行，并通过UI报告状态。 结果将从环境中的所有AEM实例进行聚合。

这些运行状况检查可随时通过Web控制台或操作功能板执行。

如果有任何实例报告给定运行状况检查失败，则整个环境将失败该运行状况检查。 与代码质量和性能测试一样，这些运行状况检查按类别组织，并使用三层门控系统报告。 唯一的区别在于在安全测试中没有阈值。 所有运行状况检查均通过或失败。

下表列出了运行状况检查。

| 名称 | 运行状况检查实施 | 类别 |
|---|---|---|
| 反序列化防火墙连接API就绪处于可接受的状态。 | [反序列化防火墙连接 API 已准备就绪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 关键 |
| 反序列化防火墙功能正常。 | [反序列化防火墙运行正常](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 关键 |
| 已加载反序列化防火墙。 | [反序列化防火墙已加载](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 关键 |
| `AuthorizableNodeName` 实施不会在节点名称/路径中显示可授权的ID。 | [可授权的节点名称生成](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#security) | 关键 |
| 默认密码已更改。 | [默认登录帐户](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#users-and-groups-in-aem) | 关键 |
| Sling默认GETServlet受DOS攻击保护。 | Sling Get Servlet | 关键 |
| 已正确配置Sling Java脚本处理程序。 | Sling Java 脚本处理程序 | 关键 |
| 已正确配置Sling JSP脚本处理程序。 | Sling JSP脚本处理程序 | 关键 |
| SSL配置正确。 | SSL 配置 | 关键 |
| 未找到明显不安全的用户配置文件策略。 | 用户配置文件默认访问 | 关键 |
| 配置Sling反向链接过滤器以防止CSRF攻击。 | [Sling 引用过滤器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#security) | 重要信息 |
| 已正确配置AdobeGraniteHTML库管理器。 | CQ HTML 库管理器配置 | 重要信息 |
| 已禁用CRXDE支持包。 | CRXDE 支持 | 重要信息 |
| Sling DavEx包和Servlet被禁用。 | DavEx 运行状况检查 | 重要信息 |
| 未安装示例内容。 | 示例内容包 | 重要信息 |
| WCM请求过滤器和WCM调试过滤器都处于禁用状态。 | [WCM 筛选器配置](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html#configuring) | 重要信息 |
| 已正确配置Sling WebDAV包和Servlet。 | WebDAV 运行状况检查 | 重要信息 |
| Web服务器配置为防止点击劫持。 | Web 服务器配置 | 重要信息 |
| 复制未使用 `admin` 用户。 | 复制和转移用户 | 信息 |

## 性能测试 {#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager可执行AEM Sites程序的性能测试。 性能测试会运行大约30分钟，方法是旋转虚拟用户（容器）以模拟实际用户在暂存环境中访问页面以模拟流量。 这些页面可使用Crawler找到。

#### 虚拟用户 {#virtual-users}

Cloud Manager旋转的虚拟用户或容器数量由用户定义的KPI（响应时间和页面查看次数/分钟）(使用 **业务所有者** 角色 [创建或编辑程序。](setting-up-program.md) 根据定义的KPI，最多将拆分10个可模拟实际用户的容器。 选择进行测试的页面会被拆分并分配给每个虚拟用户。

#### Crawler {#crawler}

在30分钟测试期开始之前，Cloud Manager将使用客户成功工程师配置的一组或多个种子URL来爬网暂存环境。 从这些URL开始，将检查每个页面的HTML，并以宽度优先的方式遍历链接。 此爬网过程最多限制为5000页。 来自Crawler的请求的固定超时为10秒。

#### 要测试的页面集 {#page-sets}

页面由三个页面集选择。 Cloud Manager使用来自生产和暂存环境中AEM实例的访问日志来确定以下存储段。

* **热门实时页面**  — 选中此选项可确保测试实时客户访问的最受欢迎页面。 Cloud Manager将读取访问日志，并确定实时客户最常访问的前25个页面，以生成顶部列表 `Popular Live Pages`. 然后，会在暂存环境中爬网暂存环境中也存在的这些元素的交集。

* **其他实时页面**  — 选择此选项可确保测试不属于前25个受欢迎的实时页面（可能不受欢迎，但对测试很重要）的页面。 与常用的实时页面类似，这些页面是从访问日志中提取的，并且还必须存在于暂存环境中。

* **新页面**  — 选择此选项可测试可能只部署到暂存环境但尚未部署到生产环境但必须进行测试的新页面。

##### 所选页面集之间的流量分布 {#distribution-of-traffic}

您可以在 **测试** 选项卡 [管道配置。](configuring-production-pipelines.md) 流量分配基于所选集数。 即，如果选择所有这三个页面，则每个页面集将占总页面查看次数的33%。 如果选择两个，则50%将转至每个集。 如果选择一个，则100%的流量会转到该集。

让我们考虑这个示例。

* 热50/50的实时页面和新页面集之间存在拆分。
* 不会使用其他实时页面。
* 新页面集包含3000页。
* 页面查看次数/分钟KPI设置为200。

在30分钟的测试期间：

* 热门实时页面集中的25个页面中的每个页面都将被点击120次： `((200 * 0.5) / 25) * 30 = 120`
* 新页面集中的3000个页面中的每个页面都将被点击一次： `((200 * 0.5) / 3000) * 30 = 1`

#### 测试和报告 {#testing-reporting}

Cloud Manager默认情况下会在暂存发布服务器上以未经身份验证的用户身份请求页面，为期30分钟，以执行AEM Sites程序的性能测试。 它测量用户生成的虚拟量度（响应时间、错误率、每分钟查看次数等） 每个页面以及所有实例的各种系统级别量度（CPU、内存、网络数据）。

下表总结了使用三层门控系统的性能测试矩阵。

| 量度 | 类别 | 失败阈值 |
|---|---|---|
| 页面请求错误率 | 关键 | >= 2% |
| CPU利用率 | 关键 | >= 80% |
| 磁盘IO等待时间 | 关键 | >= 50% |
| 第95个百分位数响应时间 | 重要信息 | >=项目级别KPI |
| 峰值响应时间 | 重要信息 | >= 18秒 |
| 每分钟页面查看次数 | 重要信息 | &lt;项目级别KPI |
| 磁盘带宽利用率 | 重要信息 | >= 90% |
| 网络带宽利用 | 重要信息 | >= 90% |
| 每分钟请求数 | 信息 | >= 6000 |

请参阅章节 [已验证的性能测试](#authenticated-performance-testing) 有关使用基本身份验证对站点和资产进行性能测试的更多详细信息。

>[!NOTE]
>
>在测试期间，会监控创作实例和发布实例。 如果未获取某个实例的任何量度，则该量度将报告为未知量度，并且相应步骤将失败。

#### 可选 — 已通过身份验证的性能测试 {#authenticated-performance-testing}

如有必要，具有经过身份验证的站点的AMS客户可以指定一个用户名和密码，Cloud Manager将在站点性能测试期间使用该用户名和密码访问该网站。

用户名和密码被指定为具有名称的管道变量 `CM_PERF_TEST_BASIC_USERNAME` 和 `CM_PERF_TEST_BASIC_PASSWORD`.

用户名应存储在 `string` 变量和密码应存储在 `secretString` 变量。 如果指定了这两个凭据，则性能测试Crawler和测试虚拟用户的每个请求都将包含这些凭据作为HTTP Basic身份验证。

要使用Cloud Manager CLI设置这些变量，请运行：

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

请参阅该文档 [修补用户管道变量](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchPipelineVariables) 了解如何使用API。

### AEM Assets {#aem-assets}

Cloud Manager通过在30分钟的测试期间内反复上传资产，执行AEM Assets程序的性能测试。

#### 入门要求 {#onboarding-requirement}

对于资产性能测试，您的客户成功工程师将创建 `cloudmanager` 将作者载入暂存环境期间的用户和密码。 性能测试步骤需要一个名为 `cloudmanager` 以及由CSE设置的关联密码。 不应从创作实例中删除该内容，也不应更改其权限。 这样做可能会失败Assets性能测试。

#### 用于测试的图像和资产 {#assets-for-testing}

客户可以上传自己的资产以进行测试。 此操作可从 **管道设置** 或 **编辑** 屏幕。 支持常用图像格式(如JPEG、PNG、GIF和BMP)以及Photoshop、Illustrator和Postscript文件。

如果未上传图像，Cloud Manager将使用默认的图像和PDF文档进行测试。

#### 用于测试的资产分发 {#distribution-of-assets}

每分钟上传的每种类型资产的分布情况在 **管道设置** 或 **编辑** 屏幕。

例如，如果使用70/30拆分，并且每分钟上传10个资产，则每分钟将上传7个图像和3个文档。

#### 测试和报告 {#testing-and-reporting}

Cloud Manager将在创作实例上使用CSE在 [入门要求](#onboaring-requirements) 中。 然后，使用开源库将资产上传到文件夹。 由资产测试步骤运行的测试使用 [打开源库。](https://github.com/adobe/toughday2) 在30分钟的测试持续时间内，会测量每个资产的处理时间以及各种系统级别的量度。 此功能可以上传图像和PDF文档。

>[!TIP]
>
>请参阅该文档 [配置生产管道](configuring-production-pipelines.md) 以了解更多。 请参阅文档 [设置程序](setting-up-program.md) 了解如何设置项目并定义KPI。

### 性能测试结果图 {#performance-testing-results-graphs}

在 **性能测试对话框**

![量度列表](assets/understand_test-results-screen1.png)

量度面板可以展开以显示图形，提供下载链接，或同时提供两者。

![以图形形式展开的量度](assets/screen_shot_2018-09-05at83933pm.png)

此功能适用于以下量度。

* **CPU利用率**
   * 测试期间CPU利用率的图表

* **磁盘I/O等待时间**
   * 测试期间磁盘I/O等待时间的图表

* **页面错误率**
   * 测试期间每分钟的页面错误图
   * 一个CSV文件，其中列出了测试期间出错的页面

* **磁盘带宽利用率**
   * 测试期间磁盘带宽利用图

* **网络带宽利用**
   * 测试期网络带宽利用图

* **峰值响应时间**
   * 测试期间每分钟的峰值响应时间图

* **第95个百分位数响应时间**
   * 测试期间每分钟第95个百分位数响应时间的图
   * 一个CSV文件，其中列出了第95个百分位数响应时间超过定义KPI的页面

## 内容包扫描优化 {#content-package-scanning-optimization}

在质量分析流程中，Cloud Manager将对Maven内部版本生成的内容包进行分析。 Cloud Manager提供了优化功能来加快此过程，当发现某些包装约束时，这些功能非常有效。 最重要的是对输出单个内容包（通常称为“全部”包）的项目执行了优化，该包中包含由内部版本生成的许多其他内容包，这些内容包被标记为跳过。 当Cloud Manager检测到此方案时，将直接扫描各个内容包并根据依赖关系对其进行排序，而不是解压缩“所有”包。 例如，请考虑以下内部版本输出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` （跳过的内容包）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` （跳过的内容包）

如果 `myco-all-1.0.0-SNAPSHOT.zip` 是两个跳过的内容包，则将扫描两个嵌入的包，而不是“所有”内容包。

对于生成数十个嵌入式包的项目，显示此优化后，每个管道执行最多可节省10分钟。

当“所有”内容包包含跳过的内容包和OSGi包的组合时，可能会出现特殊情况。 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 包含先前提到的两个嵌入式包以及一个或多个OSGi包，然后仅使用OSGi包构建一个新的、最小的内容包。 此包始终名为 `cloudmanager-synthetic-jar-package` 包装的包装在 `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* 此优化不会影响部署到AEM的包。
>* 由于嵌入的内容包与跳过的内容包之间的匹配基于文件名，因此如果多个跳过的内容包具有相同的文件名，或者在嵌入时更改了文件名，则无法执行此优化。