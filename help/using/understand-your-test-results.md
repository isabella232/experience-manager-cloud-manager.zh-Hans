---
title: 理解测试结果
seo-title: 理解测试结果
description: 'null'
seo-description: 可查看本页以了解在Cloud Manager中运行管道、代码扫描、性能和安全测试验证项目时的三层门。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
translation-type: tm+mt
source-git-commit: d38b6da61c552a3e9ad03dac49a64553f0cb00b4
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 6%

---


# 理解测试结果 {#understand-your-test-results}

在管道执行过程中，会捕获许多指标并将其与由业务所有者定义的关键绩效指标(KPI)或Adobe Managed Services设置的标准进行比较。

这些信息是使用本节中定义的三层门控系统报告的。

## 运行管道时的三层门  {#three-tier-gates-while-running-a-pipeline}

有三扇门在等待：

* 代码质量
* 性能测试
* 安全测试

对于每个门，都有由门确定的问题的三层结构。

* **关键** -这些问题由门确定，导致管道立即失败。
* **重要** -这些是由门标识的问题，它们导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以改写问题，在这种情况下，管道将继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。
* **Info** —— 这些问题由门确定，仅供参考，对管道执行没有影响。

>[!NOTE]
>
>在仅代码质量管线中，不能覆盖代码质量测试门中的重要故障，因为代码质量测试步骤是管线中的最后一步。

## 代码质量测试 {#code-quality-testing}

此步骤将评估应用程序代码的质量。 它是仅代码质量管道的核心目标，在所有非生产和生产管道中立即执行构建步骤。 请参阅 [配置CI-CD管道](/help/using/configuring-pipeline.md) ，进一步了解不同类型的管道。

### 了解代码质量测试 {#understanding-code-quality-testing}

在“代码质量测试”中，将扫描源代码，确保它满足某些质量标准。 目前，这是通过SonarQube和使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则，这些规则结合了通用Java规则和AEM特定规则。 某些AEM特定规则是根据AEM工程部门的最佳实践创建的，称为“自定 [义代码质量规则](/help/using/custom-code-quality-rules.md)”。

>[!NOTE]
>您可以在此处下载规则的完整 [列表](/help/using/assets/CodeQuality-rules-latest.xlsx)。

此步骤的结果将作为评 *级*。 下表总结了各种测试标准的评级：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A = 0错误 <br/>B =至少1个次要错误 <br/>C =至少1个主要错误 <br/>D =至少1个关键错误<br/>E =至少1个阻止程序错误 | 重要信息 | &lt; C |
| 可维护性等级 | 代码气味的未平仓修复成本为： <br/><ul><li>&lt;=5%已进入应用程序的时间，评级为A </li><li>评级在6%到10%之间是B </li><li>11%到20%的评级是C </li><li>21%到50%的评级是D</li><li>超过50%的东西</li></ul> | 重要信息 | &lt; A |
| 范围 | 单位测试线覆盖和条件覆盖的混合使用以下公式： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>其中：CT =运行单元测试时已至少评估为“true”的条件 <br/>CF =运行单元测试时已至少评估为“false”的条件 <br/>LC =覆盖行=行=到覆盖——未覆盖行 <br/><br/> B =条件总数 <br/>EL =可执行行（lines到覆盖）总数 | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | > 1 |
| 未解决问题 | 总体问题类型——漏洞、错误和代码气味 | 信息 | > 0 |
| 复制行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块： <br/><ul><li>**非Java项目：**</li><li>至少应有100个连续令牌和重复令牌。</li><li>这些令牌至少应在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，适用于其他语言</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续和重复的语句。</li></ul> <br/>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的Cloud Service兼容性问题数。 | 信息 | > 0 |


>[!NOTE]
>
>有关更 [详细的定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，请参阅度量定义。

>[!NOTE]
>
>要进一步了解执行的自定义代码质量规 [!UICONTROL Cloud Manager]则，请参阅自 [定义代码质量规则](custom-code-quality-rules.md)。

### 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际上没有问题的问题。 这称为“假阳性”。

在这些情况下，可以使用标准Java注释对源代 `@SuppressWarnings` 码进行注释，该注释将规则ID指定为注释属性。 例如，一个常见问题是，用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能具有攻击性。

要查看特定示例，此代码在AEM项目中很常见，该项目具有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，SonarQube将引发阻止程序漏洞。 查看代码后，您会发现这不是漏洞，并可以使用相应的规则ID对此进行注释。

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
>尽管最好尽量使注释具 `@SuppressWarnings` 体，即仅注释导致问题的特定语句或块，但也可以在类级别添加注释。

## 安全测试 {#security-testing}

[!UICONTROL Cloud Manager] 在部署后 ***在舞台上运行现有*** “AEM安全健康检查”，并通过UI报告状态。 结果从环境中的所有AEM实例进行聚集。

如果任何实例 **报告** ，给定运行状况检查失败，则整个 **环境** 将失败该运行状况检查。 与代码质量和性能测试一样，这些运行状况检查会组织成类别，并使用三层选通系统进行报告。 唯一的区别是在安全测试中没有阈值。 所有运行状况检查都只是通过或失败。

下表列表了当前检查：

| **名称** | **运行状况检查实施** | **类别** |
|---|---|---|
| 反序列化防火墙连接API就绪状态为可接受状态 | 反序列化防火墙连接 API 已准备就绪 | 关键 |
| 反序列化防火墙功能正常 | 反序列化防火墙运行正常 | 关键 |
| 反序列化防火墙已加载 | 反序列化防火墙已加载 | 关键 |
| AuthorizableNodeName实现不会在节点名称／路径中显示可授权的ID。 | 可授权的节点名称生成 | 关键 |
| 默认密码已更改 | 默认登录帐户 | 关键 |
| Sling默认GETservlet受DOS攻击保护。 | Sling Get Servlet | 关键 |
| Sling Java脚本处理程序已正确配置 | Sling Java 脚本处理程序 | 关键 |
| Sling JSP脚本处理程序已正确配置 | Sling JSP脚本处理程序 | 关键 |
| 正确配置了SSL | SSL 配置 | 关键 |
| 未发现明显不安全的用户用户档案策略 | 用户配置文件默认访问 | 关键 |
| 配置Sling推荐人过滤器以防止CSRF攻击 | Sling 引用过滤器 | 重要信息 |
| AdobeGranite HTML库管理器已正确配置 | CQ HTML 库管理器配置 | 重要信息 |
| 已禁用CRXDE支持包 | CRXDE 支持 | 重要信息 |
| 已禁用Sling DavEx捆绑和servlet | DavEx 运行状况检查 | 重要信息 |
| 未安装示例内容 | 示例内容包 | 重要信息 |
| WCM请求过滤器和WCM调试过滤器均被禁用 | WCM 筛选器配置 | 重要信息 |
| Sling WebDAV捆绑和servlet已正确配置 | WebDAV 运行状况检查 | 重要信息 |
| Web服务器配置为防止点击劫持 | Web 服务器配置 | 重要信息 |
| 复制未使用“admin”用户 | 复制和转移用户 | 信息 |

## 性能测试 {#performance-testing}

*中的性能* 测试 [!UICONTROL Cloud Manager] 是使用30分钟的测试实现的。

在管道设置过程中，部署管理器可以决定要将多少流量引导到每个存储段。

您可以通过配置CI/CD管道 [进一步了解存储段控件](configuring-pipeline.md)。

>[!NOTE]
>
>要设置项目并定义KPI，请参阅 [设置项目](setting-up-program.md)。

下表总结了使用三层选通系统的性能测试矩阵：

| **量度** | **类别** | **失败阈值** |
|---|---|---|
| 页面请求错误率% | 关键 | >= 2% |
| CPU利用率 | 关键 | >= 80% |
| 磁盘IO等待时间 | 关键 | >= 50% |
| 95百分点响应时间 | 重要信息 | >=项目级KPI |
| 峰值响应时间 | 重要信息 | >= 18秒 |
| 页面视图每分钟 | 重要信息 | &lt;项目级KPI |
| 磁盘带宽利用 | 重要信息 | >= 90% |
| 网络带宽利用 | 重要信息 | >= 90% |
| 每分钟请求数 | 信息 | &lt; 6000 |

### 性能测试结果图表 {#performance-testing-results-graphs}

新的图形和下载选项已添加到性能测试结果对话框中。

打开“性能测试”对话框时，可以展开度量面板以显示图形、提供下载链接或同时显示两者。

对 [!UICONTROL Cloud Manager] 于版本2018.7.0，此功能可用于以下指标：

* **CPU利用率**
   * 测试期间的CPU利用率图。

* **磁盘I/O等待时间**
   * 测试期间磁盘I/O等待时间的图表。

* **页面错误率**
   * 测试期间每分钟的页面错误图。
   * 一个CSV文件，其中列出了测试过程中出错的页面。

* **磁盘带宽利用**
   * 测试期间磁盘带宽利用率的图表。

* **网络带宽利用**
   * 测试期间的网络带宽利用图。

* **峰值响应时间**
   * 测试期间每分钟的峰值响应时间图。

* **第95百分点响应时间**
   * 测试期间每分钟第95个百分点响应时间的图。
   * 一个CSV文件，列出其第95百分点响应时间超过定义的KPI的页面。

以下图像显示性能测试图：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

