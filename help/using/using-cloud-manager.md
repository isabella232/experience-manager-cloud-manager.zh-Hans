---
title: 使用Cloud Manager
seo-title: 使用Adobe AEM Cloud Manager
description: AEM Cloud Manager用户界面已解释
seo-description: Adobe AEM Cloud Manager用户界面已解释
page-status-flag: 从未激活
uuid: cef44d35-75ed-44bb-9636-2de2bca5e458
contentOwner: jsyal
discoiquuid: c37566d5-0d1b-4c44-abd7-b271 ea443 c1 a
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 使用Cloud Manager{#using-cloud-manager}

本节介绍了用户界面(UI)， [!UICONTROL Cloud Manager] 并解释了工作流从设置程序到代码部署之后的工作流程，以及质量检查。

## 先决条件 {#prerequisites}

在了解使用情况 [!UICONTROL Cloud Manager]之前，建议执行以下几节：

* [在使用[！UICONTROL Cloud Manager]](understanding-concepts.md)
* [为[！UICONTROL Cloud Manager]](setting-configurations-for-cloud-manager.md)

## 快速入门 [!UICONTROL Cloud Manager]{#getting-started-with-cloud-manager}

设置了常规配置后 [!UICONTROL Cloud Manager]，您便可以使用 [!UICONTROL Cloud Manager]该配置。

1. 登录Adobe [!UICONTROL Experience Cloud] ，您将看到解决方案列表。

   ![](assets/screen_shot_2018-04-22at92951am.png)

1. 选择该程序并单击左上方图标以打开 [!UICONTROL Cloud Manager]。

   ![](assets/screen_shot_2018-04-22at93346am.png)

## 设置程序 {#setting-up-program}

在入职之后，业务所有者需要完成程序的初始设置。这涉及设置程序描述并定义将用于性能测试的KPI。或者，也可以上传缩略图。

定义的KPI用作每次渠道执行时传递的性能测试的基准。

>[!NOTE]
>
>定义的KPI会度量 **在舞台** 环境上运行的测试。通常，这些KPI会缩小以适合舞台环境的功能。
>
>例如，在生产环境中每分钟平均需要1000次页面查看的用户，以及生产环境中有四 `dispatcher/publish` 台服务器的用户应将其缩放为每分钟250页(假定其舞台环境只由 `dispatcher/publish` 一个服务器对组成)。
>
>此外，许多用户在生产环境前将有一个CDN(Akamai，CloudFront)。由于 [!UICONTROL Cloud Manager] 直接针对舞台环境进行测试，KPI应该只反映传递CDN的流量，即缓存错误。通常，这将是总生产流量的相对较小子集。

### 用于 [!UICONTROL Cloud Manager] 定义KPI {#using-cloud-manager-to-define-kpis}

请按照以下步骤设置计划并定义KPI：

1. 单击 **设置程序** 以启动设置过程 [!UICONTROL Cloud Manager]。
1. 此时将显示 **编辑程序信息** 屏幕。

   将缩略图上传到程序。您还可以为程序添加相关描述，然后单击 **“下一步**”。

1. 此时将显示 **配置用户** 屏幕。

   您可以配置团队角色和用户。单击**下一步**。

1. 此时将显示 **配置常规业务KPI** 屏幕。

   您可以定义两个KPI(每个部署的期望)：

   1. 您可以接受的95%的感知响应时间是什么？

      1. 建议的值-秒
   1. 峰值负载下每分钟的页面查看次数是多少？

      1. 建议的值-200pf/m


1. 单击 **提交** 以完成设置向导。

   您将看到主屏幕 [!UICONTROL Cloud Manager] 以更改 **为部署**。

## 可用环境 {#available-environments}

列表中的 **可用环境**[!UICONTROL Cloud Manager] 列出了所有受管AEM环境。

每个列出的环境都将具有与之关联的状态。

## 配置渠道 {#configuring-pipeline}

### 设置渠道 {#setting-up-pipeline}

>[!CAUTION]
>
>只有在Git存储库有至少一个分支的情况下，才能设置该管道。

在开始部署代码之前，必须先配置您的渠道设置 [!UICONTROL Cloud Manager]。

要了解有关管道配置的更多信息，请 **** 参阅** [在使用[！UICONTROL Cloud Manager]](understanding-concepts.md)**。

>[!NOTE]
>
>您可以在初始设置后更改管道设置。

### 通过配置渠道设置 [!UICONTROL Cloud Manager]{#configuring-pipeline-settings-from-the-cloud-manager}

请按照以下步骤 [!UICONTROL Cloud Manager] 进行操作，为您的管道配置先决条件和偏好：

1. 访问 **“分支”** 选项卡以设置应用程序分支。

   选择要设置的git分支。

   >[!NOTE]
   >
   >Git存储库中的分支会链接到您的程序。

   ![](assets/screen_shot_2018-05-06at73604pm.png)

1. 访问 **“环境** ”选项卡以选择 **“舞台** 和 **生产** ”选项。

   您可以定义将启动管道的触发器：

   * **手动** -某人必须在UI中手动单击才能启动管道。
   现在，您可以定义控制生产部署的参数。以下三个可用选项如下所示：

   * **使用转到实时批准**-部署必须由业务所有者、项目经理或部署经理手动批准 [!UICONTROL Cloud Manager] 。
   * **使用CSE监控** - CSE会参与实际开始部署。
   ![](assets/screen_shot_2018-05-06at73715pm.png)

1. 访问 **“测试** ”选项卡以定义您的程序的测试条件。

   现在，您可以配置性能测试参数。

   ![](assets/screen_shot_2018-05-06at73750pm.png)

## 部署代码 {#deploying-code}

配置管道(存储库、环境和测试环境)后，即可部署代码。

### 部署代码从 [!UICONTROL Cloud Manager]{#deploying-code-from-cloud-manager}

请按照以下步骤将代码部署到生产环境：

1. 单击 **从** 中 [!UICONTROL Cloud Manager] 部署以开始部署过程。
1. 此时将显示 **“Stage Deployment** ”屏幕。

   单击 **构建** 以启动进程。

1. 完整的构建过程考虑多个参数以检查和部署代码。

   选中的以下参数如下所示：

   **Stage Deployment**

   * 存储库
   * 单元测试
   * 代码扫描
   * 部署到Stage Environment
   **预生产测试**

   * 安全测试
   * 性能测试
   >[!NOTE]
   >
   >此外，您还可以查看上述测试条件的日志或审核结果。

## 质量检查结果 {#results-from-quality-checks}

管道中有三个入口：代码质量、性能测试和安全测试。

对于每个网关，门户确定的问题有三层结构。

* **关键** -这些是门户确定的问题，导致管道立即失败。
* **重要** -这些是门户识别的问题，它导致管道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，渠道会继续发展，也可以接受问题，在这种情况下，管道会停止失败。
* **信息** -这些是由门户确定的问题，仅用于信息性目的且不影响管道执行。

### 代码扫描 {#code-scanning}

![](assets/screen_shot_2018-04-22at101443am.png)

### 性能测试 {#performance-testing}

*使用测试实现性能测试*[!UICONTROL Cloud Manager] 30分钟。

在管道设置过程中，部署管理器可以决定流向每个桶的流量。他们可以从任意位置到全部三个桶箱进行选择。流量的分布取决于选定的标记数量，即如果全部被选中，则将页面查看总次数的33%放入每个桶；如果选择两项，则50%转至每组；如果选择一个，则100%流量转到该设置。

例如，假设在“常用的实时页面”和“新建页面”之间有50%/50%的分割(本示例中未使用其他实时页面)，而新页面集包含3000页。每分钟KPI的页面查看次数设置为200。在30分钟的测试期内：

* “常用Live Pages”集中的25个页面将点击240次- `((200 &#42; 0.5) / 25) &#42; 30 = 120`
* 新页面集中的3000页每一页都将点击一次- `((200 &#42; 0.5) / 3000) &#42; 30 = 1`

![](assets/image2018-3-14_16-23-56.png)

### 性能测试指标 {#performance-test-metrics}

在测试期间，会捕获许多指标，并与由AMS设置的业务所有者或标准所定义的KPI进行比较。

这些是使用三层分配系统报告的，如下所示：

### 运行管道时三层门 {#three-tier-gates-while-running-a-pipeline}

管道中有三个网关，如代码质量、性能测试和安全测试。

对于每个网关，门户确定的问题有三层结构：

* **关键**：这些问题由门户确定，导致管道立即失败。
* **重要**：这些问题由入口识别，造成管道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，渠道会继续发展，也可以接受问题，在这种情况下，管道会停止失败。
* **信息**：这些问题是由门户确定的，只提供用于信息性目的，不影响管道执行。

下表总结了使用三层分级系统的性能测试矩阵：

| **量度** | **类别** | **失败阈值** |
|---|---|---|
| 页面请求错误率% | 关键 | &gt;= 2% |
| CPU使用率 | 关键 | &gt;= 80% |
| 磁盘IO等待时间 | 关键 | &gt;= 50% |
| 95Perentity响应时间 | 重要事项 | &gt;=程序级KPI |
| 峰值响应时间 | 重要事项 | &gt;=18秒 |
| 每分钟的页面查看次数 | 重要事项 | &lt;计划级别KPI |
| 磁盘带宽利用率 | 重要事项 | &gt;= 90% |
| 网络带宽利用率 | 重要事项 | &gt;= 90% |
| 每分钟请求数 | 信息 | &lt; 6000 |

### 安全测试 {#security-testing}

[!UICONTROL Cloud Manager] 在部署之后运行现有 *AEM Security Heath检查* ，并通过UI报告其状态。结果是从环境中的所有AEM实例聚集的。

如果有任何实例报告给定健康检查失败，整个环境将失败该健康检查。与Code Quality和Performance Testing一样，这些健康检查按类别组织并使用三层分级系统进行报告。唯一的区别是在安全测试方面没有阈值。所有健康检查只能通过或失败。

当前检查包括：

| **健康检查** | **类别** |
|---|---|
| 反序列化防火墙连接 API 已准备就绪 | 关键 |
| 反序列化防火墙运行正常 | 关键 |
| 反序列化防火墙已加载 | 关键 |
| 可授权的节点名称生成 | 关键 |
| 默认登录帐户 | 关键 |
| Sling Get Servlet | 关键 |
| CQ Dispatcher 配置 | 关键 |
| CQ HTML 库管理器配置 | 关键 |
| Sling Java 脚本处理程序 | 关键 |
| Sling Jsp 脚本处理程序 | 关键 |
| Sling 引用过滤器 | 关键 |
| SSL 配置 | 关键 |
| 用户配置文件默认访问 | 关键 |
| CRXDE 支持 | 重要事项 |
| DavEx 运行状况检查 | 重要事项 |
| 示例内容包 | 重要事项 |
| WCM 筛选器配置 | 重要事项 |
| WebDAV 运行状况检查 | 重要事项 |
| Web 服务器配置 | 重要事项 |
| 复制和转移用户 | 信息 |

### SonalQue的质量检查实施 {#quality-check-implementation-by-sonarqube}

作为管道的一部分，如上面所述，扫描代码。目前，它由sonarQube实现。我们有93个规则，这些规则结合了一般Java规则和AEM特定规则(包括来自Kenfix的现有规则集的一些规则)。可在以下位置找到这些规则的列表： [Sonarque规则](assets/sonarqube-rules.xlsx)

根据这些规则，计算各种指标，其中一些指标在允许部署到舞台环境之前用作质量门。

这些是当前阈值：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A=漏洞 <br/>B=至少个次要漏洞<br/> C=至少个主要漏洞 <br/>D=至少个关键漏洞 <br/>E=至少个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A= bug <br/>B=至少个次要错误 <br/>C=至少个严重缺陷 <br/>D=至少个关键缺陷E=至少个阻止程序缺陷 | 重要事项 | &lt; C |
| 可维护性等级 | 代码的优异补习成本是： <br/><ul><li>&lt;=5%的时间已进入应用程序，评级为A </li><li>到10%之间的评级为B </li><li>在11%到20%之间，评级为C </li><li>到50%之间的评级为D</li><li>50%以上的内容是E</li></ul> | 重要事项 | &lt; A |
| 范围 | 使用此公式组合覆盖范围和条件覆盖： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>其中：CT=条件，至少 <br/>在CF= conditions在 <br/>LC=覆盖行= lines_ to_ cover-未覆盖的_ line <br/><br/> B=可执行行B=总数量的情况 <br/>下计算为&#39;true&#39;至少在CF=条件下计算为&#39;false&#39;(线条_ to_ cover) | 重要事项 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | &gt; 1 |
| 开放期刊 | 常见问题类型-漏洞、错误和代码消息 | 信息 | &gt; 1 |
| 重复的线条 | 重复块中涉及的行数。<br/>要将一段代码视为重复的代码块： <ul><li> **非Java项目：**</li><li>至少应该有100个连续的和重复的令牌。</li><li>这些令牌至少应在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP20行代码 </li><li>其他语言的10行代码</li></ul><ul><li>**Java项目：**</li><li> 令牌和行数至少应有10个连续和重复的语句。</li></ul>检测重复项时忽略缩进中以及字符串文本中的差异。 | 信息 | &gt; 1% |

### 虚假位置 {#false-positives}

质量扫描过程并非完美无缺，有时会错误地识别问题。这称为 *false正(* 尽管 *false负值* 可能在语义上更正确)。在这些情况下，可以使用标准Java `@SuppressWarnings` 注释注释源代码，该注释指定规则ID作为注释属性。例如，一个常见的问题是，检测硬编码密码的sonarQue规则对于它认为硬编码的密码非常自由。

要查看特定示例，此代码在AEM项目中比较常见，该项目具有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

SonarQube会将此漏洞提升为阻止漏洞。在这种情况下，客户可以确定这不是漏洞并使用适当的规则ID对此注释添加注释：

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

然而，另一方面，如果代码实际上是这样：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String SERVICE_PASSWORD = "password";
```

然后客户应将SonarQue的警告发送到心脏并删除硬编码密码。但是，他们仍需要添加 `@SuppressWarnings` 注释，因为术语实际上由该术语触发 `password`。

>[!NOTE]
>
>最好尽可能地使 `@SuppressWarnings` 注释变得特定，即只注释特定的语句或块导致问题，可以在类级别添加注释。

