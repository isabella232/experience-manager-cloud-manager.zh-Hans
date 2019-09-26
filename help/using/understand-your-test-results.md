---
title: 了解测试结果
seo-title: 了解测试结果
description: 'null'
seo-description: 可查看本页，了解在Cloud manager中运行管道、代码扫描、性能和安全测试时三层门以验证您的程序。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
translation-type: tm+mt
source-git-commit: 26014cfabfee6226033ba2fc1167d8f5509e17c6

---


# 了解测试结果 {#understand-your-test-results}

在管道 **流程中** ，会捕获许多指标并将其与由业务所有者定义的关键绩效指标(KPI)或Adobe Managed services设置的标准进行比较。

这些参数使用本节中定义的三层门控系统报告。

## 运行管道时的三层门 {#three-tier-gates-while-running-a-pipeline}

有三扇门在酝酿中：

* 代码质量
* 性能测试
* 安全性测试

对于每个门，门所识别的问题都有三层结构。

* **关键** -这些是由门确定的问题，它们会导致管道立即失败。
* **重要** -这些是由门识别的问题，它们导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下，管道会继续），或者他们可以接受问题（在这种情况下，管道会因故障而停止）。
* **Info** —— 这些是门所识别的问题，仅供参考，对管道执行没有影响。

>[!NOTE]
>
>在“仅代码质量”管道中，“代码质量测试”门中的重要故障不能被覆盖，因为“代码质量测试”步骤是该管道中的最后一步。

## 代码质量测试 {#code-quality-testing}

作为管道的一部分，将扫描源代码以确保部署符合特定质量标准。 目前，这是通过SonarQube和使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则，这些规则结合了通用Java规则和特定于AEM的规则。 下表总结了测试标准的等级：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | Critical | &lt; B |
| Reliability Rating | A = 0 Bug <br/>B = at least 1 Minor Bug <br/>C = at least 1 Major Bug <br/>D = at least 1 Critical Bug E = at least 1 Blocker Bug | 重要信息 | &lt; C |
| Maintainability Rating | Outstanding remediation cost for code smells is: <br/><ul><li>&lt;=5% of the time that has already gone into the application, the rating is A </li><li>between 6 to 10% the rating is a B </li><li>between 11 to 20% the rating is a C </li><li>between 21 to 50% the rating is a D</li><li>anything over 50% is an E</li></ul> | 重要信息 | &lt; A |
| 范围 | 单位测试线覆盖率和条件覆盖率的组合，使用以下公式：其 <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>中：CT =在运行单元测试时已至少评估为“true”的条件，而运行单元测试时 <br/>CF =已评估为“false”的条件至少评估一次， <br/>LC =覆盖行= lines_to_cover - unvered_lines <br/><br/> B =条件 <br/>EL =可执行行的总数(lines_to_cover) | 重要信息 | &lt; 50% |
| Skipped Unit Tests | Number of skipped unit tests. | 信息 | &gt; 1 |
| Open Issues | Overall issue types - Vulnerabilities, Bugs, and Code Smells | 信息 | &gt; 1 |
| Duplicated Lines | 重复块中涉及的行数。 <br/>对于要视为重复的代码块： <br/><ul><li>**非Java项目：**</li><li>至少应有100个连续的和重复的令牌。</li><li>这些令牌至少应该在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码（适用于其他语言）</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续和重复的语句。</li></ul> <br/>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | &gt; 1% |


>[!NOTE]
>
>有关更详细 [的定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，请参阅度量定义。

您可以在此处下载 [规则列表code-quality-rules.xlsx](/help/using/assets/CodeQuality-Rules-new.xlsx)

>[!NOTE]
>
>要进一步了解由执行的自定义代码质量规则， [!UICONTROL Cloud Manager]请参阅自定义 [代码质量规则](custom-code-quality-rules.md)。

### 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际没有问题的问题。 这称为"假阳性"。

在这些情况下，可以使用标准Java注释对源代码进行注释， `@SuppressWarnings` 该标准Java注释将规则ID指定为注释属性。 例如，一个常见问题是用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能具有攻击性。

要查看特定示例，此代码在AEM项目中很常见，该项目中有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，SonarQube将引发一个阻止程序漏洞。 查看代码后，您会发现这不是一个漏洞，并可以使用相应的规则ID对此进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代码实际上是这样的：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，正确的解决方案是删除硬编码密码。

>[!NOTE]
>
>尽管最佳做法是尽可能使注释具体 `@SuppressWarnings` （即仅对导致问题的特定语句或块进行注释），但可以在类级别进行注释。

## 安全性测试 {#security-testing}

[!UICONTROL Cloud Manager] 在部署之后 ***，在舞台上运行现有的*** AEM安全性健康检查并通过UI报告状态。 结果会从环境中的所有AEM实例中聚集。

如果任何实例 **报告给定的运行状况检查** ，则整个环境将 **** 失败该运行状况检查。 As with Code Quality and Performance Testing, these health checks are organized into categories and reported using the three-tier gating system. The only distinction is that there is no threshold in the case of security testing. All the health checks are simply pass or fail.

The following table lists the current checks:

| **名称** | **Health Check Implementation** | **类别** |
|---|---|---|
| Deserialization firewall Attach API Readiness is in an acceptable state | 反序列化防火墙连接 API 已准备就绪 | Critical |
| Deserialization firewall is functional | 反序列化防火墙运行正常 | Critical |
| Deserialization firewall is loaded | 反序列化防火墙已加载 | Critical |
| AuthorizableNodeName implementation does not expose authorizable ID in the node name/path. | 可授权的节点名称生成 | Critical |
| 默认密码已更改 | 默认登录帐户 | Critical |
| Sling default GET servlet is protected from DOS attacks. | Sling Get Servlet | 关键 |
| 调度程序正确筛选请求 | CQ Dispatcher 配置 | 关键 |
| Sling java脚本处理程序已正确配置 | Sling Java 脚本处理程序 | 关键 |
| Sling JSP脚本处理程序已正确配置 | Sling JSP脚本处理程序 | 关键 |
| SSL配置正确 | SSL 配置 | 关键 |
| 未发现明显不安全的用户配置文件策略 | 用户配置文件默认访问 | 关键 |
| 配置Sling Referrer过滤器以防止CSRF攻击 | Sling 引用过滤器 | Important |
| Adobe Granite HTML Library manager已正确配置 | CQ HTML 库管理器配置 | Important |
| CRXDE支持包被禁用 | CRXDE 支持 | Important |
| Sling DavEx捆绑和servlet被禁用 | DavEx 运行状况检查 | Important |
| 未安装示例内容 | 示例内容包 | Important |
| WCM请求过滤器和WCM调试过滤器都被禁用 | WCM 筛选器配置 | Important |
| Sling webDAV包和Servlet已正确配置 | WebDAV 运行状况检查 | Important |
| Web服务器配置为防止点击劫持 | Web 服务器配置 | 重要信息 |
| 复制未使用“admin”用户 | 复制和转移用户 | 信息 |

## 性能测试 {#performance-testing}

*中的性能测试* , [!UICONTROL Cloud Manager] 使用30分钟的测试来实现。

在管道设置过程中，部署管理器可以决定要引导到每个存储段的流量。

您可以从配置CI/CD管道中进一步 [了解存储段控件](configuring-pipeline.md)。

>[!NOTE]
>
>要设置计划并定义KPI，请参阅设 [置计划](setting-up-program.md)。

下表总结了使用三层门控系统的性能测试矩阵：

| **量度** | **类别** | **失败阈值** |
|---|---|---|
| 页面请求错误率% | Critical | &gt;= 2% |
| CPU利用率 | Critical | &gt;= 80% |
| Disk IO Wait Time | Critical | &gt;= 50% |
| 95 Percentile Response Time | 重要信息 | &gt;= Program-level KPI |
| Peak Response Time | 重要信息 | &gt;= 18秒 |
| Page Views Per Minute | 重要信息 | &lt; Program-level KPI |
| Disk Bandwidth Utilization | 重要信息 | &gt;= 90% |
| Network Bandwidth Utilization | 重要信息 | &gt;= 90% |
| Requests Per Minute | 信息 | &lt; 6000 |

### 性能测试结果图 {#performance-testing-results-graphs}

New graphs and download options have been added to the Performance Test Results dialog.

打开“性能测试”对话框时，可以展开度量面板以显示图形、提供下载链接或同时显示两者。

For  Release 2018.7.0, this functionality is available for the following metrics:[!UICONTROL Cloud Manager]

* **CPU利用率**
   * 测试期间的CPU使用率图。

* **磁盘I/O等待时间**
   * 测试期间磁盘I/O等待时间的图表。

* **页面错误率**
   * 测试期间每分钟的页面错误图。
   * 一个CSV文件，其中列出了在测试过程中产生错误的页面。

* **磁盘带宽利用**
   * 测试期间磁盘带宽利用率图。

* **网络带宽利用**
   * 测试期间网络带宽利用率图。

* **峰值响应时间**
   * 测试期间每分钟的峰值响应时间图。

* **第95百分点响应时间**
   * 在测试期间每分钟95个百分点的响应时间的图。
   * 一个CSV文件，列出其第95百分点响应时间超过定义的KPI的页面。

以下图像显示性能测试图：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

