---
title: 了解测试结果
seo-title: 了解测试结果
description: 'null'
seo-description: 查看本页可在运行管道、代码扫描、性能和安全测试的同时在Cloud Manager中了解三层网关。
uuid: 93ca01f-0df2-4a6f-81dc-23dfise24dc93
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7 e7318 d4
translation-type: tm+mt
source-git-commit: 26014cfabfee6226033ba2fc1167d8f5509e17c6

---


# 了解测试结果 {#understand-your-test-results}

**在渠道** 流程中，会捕获许多指标，并与由业务所有者定义的主要性能指标(KPI)或Adobe Managed Services设置的标准进行比较。

它们使用本节中定义的三层分组系统进行报告。

## 运行管道时三层门 {#three-tier-gates-while-running-a-pipeline}

管道中有三个入口：

* 代码质量
* 性能测试
* 安全测试

对于每个网关，门户确定的问题有三层结构。

* **关键** -这些是门户确定的问题，导致管道立即失败。
* **重要** -这些是门户识别的问题，它导致管道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题，在这种情况下，渠道会继续发展，也可以接受问题，在这种情况下，管道会停止失败。
* **信息** -这些是由门户确定的问题，仅用于信息性目的且不影响管道执行。

>[!NOTE]
>
>在“仅代码质量管道”中，代码质量测试门中的重要故障无法覆盖，因为“代码质量测试”步骤是管道的最后一步。

## 代码质量测试 {#code-quality-testing}

作为管道的一部分，扫描源代码以确保部署符合特定质量条件。目前，这是通过使用OAKPAL的SonarQue和内容包级检查实现的。有超过100个规则结合了一般的Java规则和AEM特定规则。下表总结了测试标准的等级：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A=漏洞 <br/>B=至少个次要漏洞<br/> C=至少个主要漏洞 <br/>D=至少个关键漏洞 <br/>E=至少个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A= bug <br/>B=至少个次要错误 <br/>C=至少个严重缺陷 <br/>D=至少个关键缺陷E=至少个阻止程序缺陷 | 重要事项 | &lt; C |
| 可维护性等级 | 代码的优异补习成本是： <br/><ul><li>&lt;=5%的时间已进入应用程序，评级为A </li><li>到10%之间的评级为B </li><li>在11%到20%之间，评级为C </li><li>到50%之间的评级为D</li><li>50%以上的内容是E</li></ul> | 重要事项 | &lt; A |
| 范围 | 使用以下公式组合单元测试线覆盖和条件覆盖： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>其中：CT=条件，在运行单元测试CF=条件至少在运行单元测试 <br/>CF=的条件下达到“false”至少一次，运行单元测试 <br/>LC= winds_ to_ cover-未覆盖的_ line <br/><br/> B=可执行行的总数量 <br/>(直线_ to_ cover) | 重要事项 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | &gt; 1 |
| 开放期刊 | 常见问题类型-漏洞、错误和代码消息 | 信息 | &gt; 1 |
| 重复的线条 | 重复块中涉及的行数。<br/>要将一段代码视为重复的代码块： <br/><ul><li>**非Java项目：**</li><li>至少应该有100个连续的和重复的令牌。</li><li>这些令牌至少应在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP20行代码 </li><li>其他语言的10行代码</li><li>**Java项目：**</li><li> 令牌和行数至少应有10个连续和重复的语句。</li></ul> <br/>检测重复项时忽略缩进中以及字符串文本中的差异。 | 信息 | &gt; 1% |


>[!NOTE]
>
>有关更多详细定义，请参阅 [量度定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 。

您可以在此处 [下载规则列表](/help/using/assets/CodeQuality-Rules-new.xlsx)

>[!NOTE]
>
>要进一步了解执行的自定义代码质量规则， [!UICONTROL Cloud Manager]请参阅 [自定义代码质量规则](custom-code-quality-rules.md)。

### 处理虚假位置 {#dealing-with-false-positives}

质量扫描过程并非完美无缺，有时会错误地识别问题。这称为“false active”。

在这些情况下，可以使用标准Java `@SuppressWarnings` 注释注释源代码，该注释指定规则ID作为注释属性。例如，一个常见的问题是，sonarQue规则检测硬编码密码会对如何识别硬编码密码很有挑战性。

要查看特定示例，此代码在AEM项目中比较常见，该项目具有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube随后将引发阻止漏洞。查看代码后，您会发现这不是漏洞，并且可以用适当的规则ID对此漏洞进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然而，另一方面，如果代码实际上是这样：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那么正确的解决方案就是删除硬编码的密码。

>[!NOTE]
>
>尽管最佳实践是尽可能地使 `@SuppressWarnings` 注释变得特定，但只需注释特定的语句或块就可以在类级别添加注释。

## 安全测试 {#security-testing}

[!UICONTROL Cloud Manager] 在部署之后运行现有 ***AEM Security Heath检查*** ，并通过UI报告状态。结果是从环境中的所有AEM实例聚集的。

如果任何 **实例** 报告给定健康检查失败， **整个环境** 将失败该健康检查。与Code Quality和Performance Testing一样，这些健康检查按类别组织并使用三层分级系统进行报告。唯一的区别是在安全测试方面没有阈值。所有健康检查只能通过或失败。

下表列出了当前检查：

| **名称** | **健康检查实施** | **类别** |
|---|---|---|
| 反序列化防火墙附加API就绪状态处于可接受状态 | 反序列化防火墙连接 API 已准备就绪 | 关键 |
| 反序列化防火墙功能 | 反序列化防火墙运行正常 | 关键 |
| 已加载反序列化防火墙 | 反序列化防火墙已加载 | 关键 |
| authorizableNoteName实现不在节点名称/路径中暴露可授权的ID。 | 可授权的节点名称生成 | 关键 |
| 默认口令已更改 | 默认登录帐户 | 关键 |
| Sling default GET servlet受DOS攻击保护。 | Sling Get Servlet | 关键 |
| Dispatcher正确过滤请求 | CQ Dispatcher 配置 | 关键 |
| 正确配置Sling Java Script处理程序 | Sling Java 脚本处理程序 | 关键 |
| 正确配置Sling JSP脚本处理程序 | Sling JSP脚本处理程序 | 关键 |
| SSL配置正确 | SSL 配置 | 关键 |
| 找不到明显安全的用户配置文件策略 | 用户配置文件默认访问 | 关键 |
| 为防止CSRF攻击，配置了sling引介过滤器 | Sling 引用过滤器 | 重要事项 |
| Adobe Granite HTML库管理器正确配置 | CQ HTML 库管理器配置 | 重要事项 |
| 禁用CRXDE支持包 | CRXDE 支持 | 重要事项 |
| 禁用了Sling Davex捆绑和servlet | DavEx 运行状况检查 | 重要事项 |
| 未安装示例内容 | 示例内容包 | 重要事项 |
| WCM请求过滤器和WCM调试过滤器都被禁用 | WCM 筛选器配置 | 重要事项 |
| Sling WebDAV捆绑包和servlet正确配置 | WebDAV 运行状况检查 | 重要事项 |
| Web服务器配置为防止点击劫持 | Web 服务器配置 | 重要事项 |
| 复制未使用“管理员”用户 | 复制和转移用户 | 信息 |

## 性能测试 {#performance-testing}

*通过30分钟*[!UICONTROL Cloud Manager] 测试实现性能测试。

在管道设置过程中，部署管理器可以决定流向每个桶的流量。

您可以从 [配置CI/CD管线中了解有关桶控件的更多信息](configuring-pipeline.md)。

>[!NOTE]
>
>要设置程序并定义KPI，请参阅 [设置程序](setting-up-program.md)。

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

### 性能测试结果图表 {#performance-testing-results-graphs}

新的图形和下载选项已添加到“性能测试结果”对话框中。

打开“性能测试”对话框时，可展开量度面板以显示图形、提供指向下载的链接或同时提供两者。

[!UICONTROL Cloud Manager] 对于2018.7.0版，此功能可用于以下指标：

* **CPU利用率**
   * 测试期间的CPU使用情况图形。

* **磁盘I/等待时间**
   * 测试期间的Disk I/等待时间图形。

* **页面错误率**
   * 测试期间每分钟的页面错误图表。
   * 在测试过程中生成错误的CSV文件列表页面。

* **磁盘带宽利用率**
   * 测试期间的磁盘带宽使用率图形。

* **网络带宽利用率**
   * 测试期间的网络带宽使用图。

* **峰值响应时间**
   * 测试期内每分钟峰值响应时间的图形。

* **95th Percentile响应时间**
   * 测试期内每分钟995个百分点的图形。
   * 一个CSV文件列表页面，其95th perspentitive响应时间已超过定义的KPI。

以下图像显示性能测试图：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

