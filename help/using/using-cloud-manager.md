---
title: 使用Cloud Manager
seo-title: 使用Adobe AEM Cloud Manager
description: AEM Cloud manager用户界面说明
seo-description: Adobe AEM Cloud manager用户界面说明
page-status-flag: 从未激活
uuid: cef44d35-75ed-44bb-9636-2de2bca5e458
contentOwner: jsyal
discoiquuid: c37566d5-0d1b-4c44-abd7-b271ea443c1a
translation-type: tm+mt
source-git-commit: 4c1c6786db9b8972f9315bd2f12fc1752881492f

---


# 使用Cloud Manager{#using-cloud-manager}

本节介绍的用户界面(UI) [!UICONTROL Cloud Manager] ，并说明从程序设置到代码部署的工作流，然后是质量检查。

## 先决条件 {#prerequisites}

在详细了解使用的信息之 [!UICONTROL Cloud Manager]前，建议先阅读以下几节：

* [在使用[!UICONTROL Cloud Manager]之前了解概念](understanding-concepts.md)
* [为[!UICONTROL Cloud Manager]设置常规配置](setting-configurations-for-cloud-manager.md)

## Getting Started with [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

为设置常规配置后， [!UICONTROL Cloud Manager]您便可以使用 [!UICONTROL Cloud Manager]。

1. 登录到Adobe, [!UICONTROL Experience Cloud] 您将看到解决方案列表。

   ![](assets/screen_shot_2018-04-22at92951am.png)

1. 选择程序并单击左上角的图标以打开 [!UICONTROL Cloud Manager]。

   ![](assets/screen_shot_2018-04-22at93346am.png)

## 设置程序 {#setting-up-program}

入职后，企业所有者需要对计划进行一些初始设置。 这包括设置计划描述和定义用于性能测试的KPI。 （可选）可以上传缩略图。

定义的KPI用作每次管线执行时通过的性能测试的基准。

>[!NOTE]
>
>定义的KPI是在舞台环境中运行的测 **试中** 。 通常，这些KPI会按比例缩小以适合舞台环境的功能。
>
>例如，在生产环境中，平均每分钟需要1000次页面查看，并且生产中有四台服务器的用户应将该时间缩放到每分钟250次页面查看（假定其舞台环境仅包含一个服务器对）。 `dispatcher/publish``dispatcher/publish`
>
>此外，许多用户在其生产环境前面将有一个CDN(Akamai、CloudFront)。 由于 [!UICONTROL Cloud Manager] 直接针对舞台环境进行测试，因此KPI应仅反映通过CDN的预期流量，即缓存未命中。 通常，这是总生产流量中相对较小的子集。

### 使用 [!UICONTROL Cloud Manager] 定义KPI {#using-cloud-manager-to-define-kpis}

请按照以下步骤设置计划并定义KPI:

1. 单击 **“设置程序** ”以在中启动设置过程 [!UICONTROL Cloud Manager]。
1. 此时将 **显示“编辑程序信息** ”屏幕。

   将缩略图上传到您的程序。 您还可以向程序添加相关说明，然后单击“下 **一步”**。

1. 此时将显示 **配置用户** (Configure Users)屏幕。

   您可以配置团队角色和用户。 单击&#x200B;**下一步**。

1. 此时 **会显示配置一般业务** KPI屏幕。

   您可以定义两个KPI（对每个部署的期望）:

   1. 您能接受的第95百分位响应时间是多少？

      1. 推荐值- 3秒
   1. 在高峰负载下，每分钟页面查看次数是多少？

      1. 建议值- 200 pv/m


1. 单击 **提交** ，以完成设置向导。

   您将看到更改为“部署” [!UICONTROL Cloud Manager] 的主 **屏幕**。

## 可用环境 {#available-environments}

中 **的“可用环境** ”列 [!UICONTROL Cloud Manager] 出所有受管AEM环境。

列出的每个环境都将具有与其关联的状态。

## 配置管道 {#configuring-pipeline}

### 设置管道 {#setting-up-pipeline}

>[!CAUTION]
>
>在git存储库至少有一个分支之前，无法设置管道。

在开始部署代码之前，必须先从中配置管道设置 [!UICONTROL Cloud Manager]。

要进一步了解管道配置，请参 **阅使用[!UICONTROL Cloud Manager]**[](understanding-concepts.md)**之前了解概念中的管道概述一节。

>[!NOTE]
>
>可在初始设置后更改管线设置。

### 从Adobe Pipeline Settings [!UICONTROL Cloud Manager]{#configuring-pipeline-settings-from-the-cloud-manager}

请按照以下步骤， [!UICONTROL Cloud Manager] 为管道配置行为和首选项：

1. 访问“ **Branch** ”（分支）选项卡以设置应用程序分支。

   选择要设置的git分支。

   >[!NOTE]
   >
   >在Git存储库中找到的分支会链接到您的程序。

   ![](assets/screen_shot_2018-05-06at73604pm.png)

1. 访问“环 **境** ”选项卡以选 **择“舞台** ”和“ **生产** ”选项。

   您可以定义将启动管线的触发器：

   * **手动** -必须有人在UI中手动单击才能启动管道。
   现在，您可以定义控制生产部署的参数。 三个可用选项如下：

   * **使用实时批准**-部署必须由业务所有者、项目经理或部署经理通过 [!UICONTROL Cloud Manager] UI手动批准。
   * **使用CSE监督** -参与CSE以实际开始部署。
   ![](assets/screen_shot_2018-05-06at73715pm.png)

1. 访问“ **测试** ”选项卡，为程序定义测试条件。

   现在，您可以配置性能测试参数。

   ![](assets/screen_shot_2018-05-06at73750pm.png)

## 部署代码 {#deploying-code}

配置管道（存储库、环境和测试环境）后，即可部署代码。

### 从部署代码 [!UICONTROL Cloud Manager]{#deploying-code-from-cloud-manager}

按照以下步骤将代码部署到生产环境：

1. 单击 **部署** ，开 [!UICONTROL Cloud Manager] 始部署过程。
1. 将显 **示“Stage Deployment** ”屏幕。

   单击 **构建** ，开始该过程。

1. 整个构建过程会考虑多个参数来检查和部署代码。

   检查的以下参数如下：

   **Stage Deployment**

   * 存储库
   * 单元测试
   * 代码扫描
   * 部署到Stage Environment
   **预制作测试**

   * 安全性测试
   * 性能测试
   >[!NOTE]
   >
   >此外，您还可以查看日志或查看上述测试标准的结果。

## 质量检查的结果 {#results-from-quality-checks}

有三扇门在酝酿中：代码质量、性能测试和安全性测试。

对于每个门，门所识别的问题都有三层结构。

* **关键** -这些是由门确定的问题，它们会导致管道立即失败。
* **重要** -这些是由门识别的问题，它们导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下，管道会继续），或者他们可以接受问题（在这种情况下，管道会因故障而停止）。
* **Info** —— 这些是门所识别的问题，仅供参考，对管道执行没有影响。

### 代码扫描 {#code-scanning}

![](assets/screen_shot_2018-04-22at101443am.png)

### 性能测试 {#performance-testing}

*中的性能测试* , [!UICONTROL Cloud Manager] 使用30分钟的测试来实现。

在管道设置过程中，部署管理器可以决定要引导到每个存储段的流量。 他们可以选择从1到3的任意位置。 流量分配基于所选的时段数，即如果全部选择了三个时段，则每个时段将占总页面查看次数的33%;如果选择两个，则每组50%;如果选择了一个，则100%的流量将转到该集。

例如，假设在“常用实时页面”和“新页面”集（在本例中，不使用“其他实时页面”）之间存在50%/50%的拆分，而“新页面”集包含3000页。 页面查看次数／分钟KPI设置为200。 在30分钟的测试期内：

* 热门实时页面集中的25个页面中的每个页面都将点击240次- `((200 &#42; 0.5) / 25) &#42; 30 = 120`
* “新页面”集中的3000个页面中的每个页面都将点击一次- `((200 &#42; 0.5) / 3000) &#42; 30 = 1`

![](assets/image2018-3-14_16-23-56.png)

### 性能测试指标 {#performance-test-metrics}

在测试期间，会捕获许多指标并将其与由业务所有者定义的KPI或AMS设置的标准进行比较。

这些信息使用三层门控系统报告如下：

### 运行管道时的三层门 {#three-tier-gates-while-running-a-pipeline}

有三个门口在管道中：代码质量、性能测试和安全测试。

对于每个门，门所识别的问题都有三层结构：

* **关键**:这些是由门确定的问题，它们会导致管道立即失败。
* **重要说明**:这些是由门识别的问题，导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下，管道会继续），或者他们可以接受问题（在这种情况下，管道会因故障而停止）。
* **信息**:这些是由门所识别的问题，这些问题仅用于信息目的并且对管道执行没有影响。

下表总结了使用三层门控系统的性能测试矩阵：

| **量度** | **类别** | **失败阈值** |
|---|---|---|
| 页面请求错误率% | 关键 | &gt;= 2% |
| CPU利用率 | 关键 | &gt;= 80% |
| 磁盘IO等待时间 | 关键 | &gt;= 50% |
| 95百分点响应时间 | 重要信息 | &gt;=计划级KPI |
| 峰值响应时间 | 重要信息 | &gt;= 18秒 |
| 每分钟的页面查看次数 | 重要信息 | &lt;计划级别KPI |
| 磁盘带宽利用 | 重要信息 | &gt;= 90% |
| 网络带宽利用 | 重要信息 | &gt;= 90% |
| 每分钟请求数 | 信息 | &lt; 6000 |

### 安全性测试 {#security-testing}

[!UICONTROL Cloud Manager] 在部署之后 *，在舞台上运行现有的* AEM安全性健康检查并通过UI报告其状态。 结果会从环境中的所有AEM实例中聚集。

如果任一实例报告给定运行状况检查的失败，则整个环境将失败该运行状况检查。 与“代码质量和性能测试”一样，这些运行状况检查会被组织到类别中，并使用三层门控系统进行报告。 唯一的区别是在安全测试中没有阈值。 所有的健康检查都是通过或失败的。

当前检查包括：

| **运行状况检查** | **类别** |
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
| CRXDE 支持 | 重要信息 |
| DavEx 运行状况检查 | 重要信息 |
| 示例内容包 | 重要信息 |
| WCM 筛选器配置 | 重要信息 |
| WebDAV 运行状况检查 | 重要信息 |
| Web 服务器配置 | 重要信息 |
| 复制和转移用户 | 信息 |

### SonarQube实现质量检查 {#quality-check-implementation-by-sonarqube}

如上图所示，作为管道的一部分，将扫描代码。 目前，这由SonarQube实现。 我们有93个规则，这些规则是通用Java规则和特定于AEM的规则（包括Cognifide现有规则集中的一些规则）的组合。 这些规则的列表可在以下位置找到： [code-quality-rules.xlsx](/help/using/assets/code-quality-rules.xlsx)

根据这些规则，将计算各种度量，其中一些度量在允许部署到舞台环境之前用作质量门。

这些是当前的阈值：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A = 0错误 <br/>B =至少1个次要错误 <br/>C =至少1个主要错误 <br/>D =至少1个关键错误E =至少1个阻止程序错误 | 重要信息 | &lt; C |
| 可维护性等级 | 代码气味的未支付补救成本是： <br/><ul><li>&lt;=5%已进入应用程序的时间，评级为A </li><li>评级在6%到10%之间为B </li><li>在11%到20%的评级是C </li><li>21%到50%的评级是D</li><li>超过50%的东西</li></ul> | 重要信息 | &lt; A |
| 范围 | 使用以下公式的行覆盖率和条件覆盖率的组合：其 <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>中：CT =已被评估为“true”的条件至少一次 <br/>CF =已被评估为“false”的条件至少一次 <br/>LC =覆盖行= lines_to_cover - overaded_lines <br/><br/> B =条件总数 <br/>EL =可执行行(lines_to_cover)的总数 | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | &gt; 1 |
| 未解决问题 | 总体问题类型——漏洞、错误和代码气味 | 信息 | &gt; 1 |
| 复制行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块： <ul><li> **非Java项目：**</li><li>至少应有100个连续的和重复的令牌。</li><li>这些令牌至少应该在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码（适用于其他语言）</li></ul><ul><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续和重复的语句。</li></ul>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | &gt; 1% |

### 误报 {#false-positives}

质量扫描过程并不完美，有时会错误地识别实际没有问题的问题。 这称为假正 *数* (尽管假负 *数* 在语义上可能更正确)。 在这些情况下，可以使用标准Java注释对源代码进行注释， `@SuppressWarnings` 该标准Java注释将规则ID指定为注释属性。 例如，一个常见问题是检测硬编码密码的SonarQube规则在其认为硬编码密码的方面非常自由。

要查看特定示例，此代码在AEM项目中很常见，该项目中有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

SonarQube将将此作为阻止程序漏洞提出。 在这种情况下，客户可以识别这不是漏洞，并使用相应的规则ID对此进行注释：

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代码实际上是这样的：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String SERVICE_PASSWORD = "password";
```

然后，客户应当听从SonarQube的警告，删除硬编码密码。 但是，他们仍需要添加注释， `@SuppressWarnings` 因为SonarQube规则实际上是由术语触发的 `password`。

>[!NOTE]
>
>最好尽可能使注释具体 `@SuppressWarnings` 化，即仅对导致问题的特定语句或块进行注释，可以在类级别进行注释。

