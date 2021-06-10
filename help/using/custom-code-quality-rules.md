---
title: 自定义代码质量规则
seo-title: 自定义代码质量规则
description: 可阅读本页，了解Cloud Manager执行的自定义代码质量规则。
seo-description: 可阅读本页内容，了解由Adobe Experience Manager Cloud Manager执行的自定义代码质量规则。
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
feature: 代码质量规则
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 5111a918b8063ab576ef587dc3c8d66ad976fc1a
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 4%

---

# 自定义代码质量规则 {#custom-code-quality-rules}

>[!NOTE]
>要了解AEM as a Cloud Service中Cloud Manager的自定义代码质量规则，请参阅[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/custom-code-quality-rules.html?lang=en#using-cloud-manager)。

本页介绍由Cloud Manager根据AEM Engineering中的最佳实践创建的自定义代码质量规则。

>[!NOTE]
>此处提供的代码示例仅供说明性用途。 请参阅[概念](https://docs.sonarqube.org/7.4/user-guide/concepts/) ，了解SonarQube概念和质量规则。

## SonarQube规则{#sonarqube-rules}

以下部分重点介绍SonarQube规则：

### 请勿使用潜在危险的函数{#do-not-use-potentially-dangerous-functions}

**键**:CQRules:CWE-676

**类型**:漏洞

**严重性**:主要

**自**:版本2018.4.0

Thread. ***stop()和********* Thread.interrupt()方法可能会产生难以重现的问题，并且在某些情况下会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不符合代码{#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### 兼容代码{#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### 请勿使用可能由外部控制的格式字符串{#do-not-use-format-strings-which-may-be-externally-controlled}

**键**:CQRules:CWE-134

**类型**:漏洞

**严重性**:主要

**自**:版本2018.4.0

使用来自外部源（如请求参数或用户生成的内容）的格式字符串可以使应用程序暴露于拒绝服务攻击。 在某些情况下，格式字符串可能受外部控制，但仅允许来自受信任源。

#### 不符合代码{#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时{#http-requests-should-always-have-socket-and-connect-timeouts}

**键**:CQRules:ConnectionTimeoutMechanism

**类型**:错误

**严重性**:关键

**自**:版本2018.6.0

在从AEM应用程序内执行HTTP请求时，必须确保配置正确的超时，以避免不必要的线程消耗。 遗憾的是，Java的默认HTTP客户端(java.net.HttpUrlConnection)和常用的Apache HTTP组件客户端的默认行为是从不超时，因此必须明确设置超时。 此外，作为最佳实践，这些超时不应超过60秒。

#### 不符合代码{#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### 兼容代码{#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### ResourceResolver对象应始终关闭{#resourceresolver-objects-should-always-be-closed}

**键**:CQRules:CQBP-72

**类型**:代码气味

**严重性**:主要

**自**:版本2018.4.0

从ResourceResolverFactory获取的ResourceResolver对象会消耗系统资源。 尽管在ResourceResolver不再使用时，已经制定了回收这些资源的措施，但通过调用close()方法来显式关闭任何打开的ResourceResolver对象会更为有效。

一个相对常见的误解是，使用现有JCR会话创建的ResourceResolver对象不应显式关闭，或者这样做将关闭基础JCR会话。 但情况并非如此 — 无论ResourceResolver是如何打开的，都应在不再使用时关闭它。 由于ResourceResolver实现了可关闭接口，因此也可以使用try-with-resources语法，而不是显式调用close()。

#### 不符合代码{#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 兼容代码{#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### 请勿使用Sling Servlet路径注册Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**键**:CQRules:CQBP-75

**类型**:代码气味

**严重性**:主要

**自**:版本2018.4.0

如[Sling文档](http://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，不建议使用按路径划分的绑定Servlet。 路径绑定的Servlet无法使用标准JCR访问控制，因此需要额外的安全严格性。 建议在存储库中创建节点并按资源类型注册Servlet，而不是使用路径绑定Servlet。

#### 不符合代码{#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 应记录或引发捕获的异常，但不应同时记录或引发{#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**键**:CQRules:CQBP-44—CatchAndEitherLogOrThrow

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

通常，例外应只记录一次。 多次记录异常可能会造成混淆，因为不清楚异常发生的次数。 导致这种情况的最常见模式是记录并引发捕获异常。

#### 不符合代码{#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### 兼容代码{#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### 避免在日志语句后面紧接着引发语句{#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**键**:CQRules:CQBP-44—ConcentiveLogAndThrow

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

要避免的另一种常见模式是，记录消息，然后立即引发异常。 这通常表示异常消息将在日志文件中重复出现。

#### 不符合代码{#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 兼容代码{#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在处理GET或HEAD请求{#avoid-logging-at-info-when-handling-get-or-head-requests}时，避免在“信息”处记录

**键**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**类型**:代码气味

**严重性**:次要

通常，应使用“信息”日志级别来标定重要操作，并且默认情况下，AEM配置为在“信息”级别或更高级别登录。 GET和HEAD方法只应是只读操作，因此不构成重要操作。 响应GET或HEAD请求在“信息”级别进行日志记录可能会产生严重的日志噪声，从而更难识别日志文件中的有用信息。 处理GET或HEAD请求时的日志记录应位于出现问题时的“警告”或“错误”级别，或者位于“调试”或“TRACE”级别（如果更深入的故障诊断信息会有所帮助）。

>[!CAUTION]
>
>这不适用于每个请求的access.log类型日志记录。

#### 不符合代码{#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 兼容代码{#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 请勿将Exception.getMessage()用作日志记录语句{#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}的第一个参数

**键**:CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然上下文也可以通过使用堆栈跟踪来确定，但一般来说，日志消息将更易于阅读和理解。 因此，在记录异常时，将异常的消息用作日志消息是一种不好的做法，因为异常消息将包含错误内容，而日志消息应用于告知日志阅读器应用程序在异常发生时正在执行的操作。 例外消息仍将被记录；通过指定您自己的消息，日志将更便于理解。

#### 不符合代码{#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 兼容代码{#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 在捕获块中登录应位于“警告”或“错误”级别{#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**键**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

如名称所示，在&#x200B;*例外*&#x200B;情况下应始终使用Java例外。 因此，当捕获到异常时，务必确保日志消息记录在适当的级别（警告或错误）。 这可确保这些消息在日志中正确显示。

#### 不符合代码{#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 兼容代码{#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿将堆栈跟踪打印到控制台{#do-not-print-stack-traces-to-the-console}

**键**:CQRules:CQBP-44—ExceptionPrintStackTrace

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

如上所述，了解日志消息时，上下文至关重要。 使用Exception.printStackTrace()会导致&#x200B;**仅**&#x200B;堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在诸如AEM的多线程应用中，如果使用此方法并行打印多个例外，则其堆栈轨迹可能会重叠，从而产生明显混淆。 应仅通过日志记录框架记录例外。

#### 不符合代码{#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 兼容代码{#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不输出到标准输出或标准错误{#do-not-output-to-standard-output-or-standard-error}

**键**:CQRules:CQBP-44—LogLevelConsolePrinters

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

登录AEM应始终通过日志记录框架(SLF4J)完成。 直接输出到标准输出或标准错误流会丢失由日志记录框架提供的结构和上下文信息，并且在某些情况下可能导致性能问题。

#### 不符合代码{#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 兼容代码{#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬编码/apps和/libs路径{#avoid-hardcoded-apps-and-libs-paths}

**键**:CQRules:CQBP-71

**类型**:代码气味

**严重性**:次要

**自**:版本2018.4.0

通常，以/libs和/apps开头的路径不应进行硬编码，因为它们引用的路径通常存储为相对于Sling搜索路径（默认情况下设置为/libs和/apps）的路径。 使用绝对路径可能会引入一些细微的缺陷，这些缺陷仅在项目生命周期的后期才会出现。

#### 不符合代码{#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 兼容代码{#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不应使用{#sonarqube-sling-scheduler} Sling调度程序

**键**:CQRules:AMSCORE-554

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

Sling调度程序不得用于需要保证执行的任务。 Sling计划作业可确保执行，并且更适合群集和非群集环境。

请参阅[Apache Sling事件和作业处理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) ，了解有关如何在群集环境中处理Sling作业的更多信息。

### AEM已弃用的API不应使用{#sonarqube-aem-deprecated}

**键**:AMSCORE-553

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

AEM API表面处于不断修订的状态，可识别不鼓励使用并因此被视为弃用的API。

在很多情况下，这些API会使用标准Java *@Deprecated*&#x200B;注释并且因此由`squid:CallToDeprecatedMethod`标识而被弃用。

但是，在某些情况下，AEM上下文中已弃用API，但在其他上下文中可能不会弃用API。 此规则标识此第二类。

## OakPAL内容规则{#oakpal-rules}

请在下面找到Cloud Manager执行的OakPAL检查。

>[!NOTE]
>
>OakPAL是由AEM合作伙伴(2019年AEM Rockstar北美地区入选者)开发的框架，该合作伙伴使用独立的Oak存储库来验证内容包。

### 客户{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}不应实施或扩展带有@ProviderType的产品API

**键**:CQBP-84

**类型**:错误

**严重性**:关键

**自**:版本2018.7.0

AEM API包含Java接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，接口com.day.cq.wcm. *api.Page* ，设计为仅由 ***AEM实现***。

当将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码，因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 ***码实现了*** 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

仅打算由AEM实现的接口（和类）使用&#x200B;*org.osgi.annotation.versioning.ProviderType*（或者，在某些情况下，使用类似的旧版注释&#x200B;*aQute.bnd.annotation.ProviderType*）进行注释。 此规则标识通过自定义代码实现此类接口（或扩展类）的情况。

#### 不符合代码{#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 客户包不应在/libs {#oakpal-customer-package}下创建或修改节点

**键**:UnbandedPaths

**类型**:错误

**严重性**:阻止程序

**自**:版本2019.6.0

客户应将AEM内容存储库中的/libs内容树视为只读，这是一种长期存在的最佳实践。 修改&#x200B;*/libs*&#x200B;下的节点和属性会对主要和次要更新造成重大风险。 对&#x200B;*/libs*&#x200B;的修改只应通过官方渠道进行Adobe。

### 包不应包含重复的OSGi配置{#oakpal-package-osgi}

**键**:DuplicateOsgiConfigurations

**类型**:错误

**严重性**:主要

**自**:版本2019.6.0

复杂项目中出现的常见问题是多次配置同一OSGi组件。 这就产生了关于哪种配置可操作的模糊性。 此规则“支持运行模式”，因为它将仅识别在同一运行模式（或运行模式的组合）中多次配置同一组件的问题。

#### 不符合代码{#non-compliant-code-osgi}

```
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 兼容代码{#compliant-code-osgi}

```
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安装文件夹应仅包含OSGi节点{#oakpal-config-install}

**键**:ConfigAndInstallShouldOnlyContainOsgiNodes

**类型**:错误

**严重性**:主要

**自**:版本2019.6.0

出于安全考虑，包含&#x200B;*/config/和/install/*&#x200B;的路径只能由AEM中的管理用户读取，且只能用于OSGi配置和OSGi包。 将其他类型的内容放在包含这些区段的路径下会导致应用程序行为，这些行为在管理用户和非管理用户之间会无意中发生变化。

一个常见问题是：在组件对话框中或指定用于内联编辑的富文本编辑器配置时，使用名为`config`的节点。 要解决此问题，应将违规节点重命名为兼容名称。 对于富文本编辑器配置，请使用`cq:inplaceEditing`节点上的`configPath`属性指定新位置。

#### 不符合代码{#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 兼容代码{#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 包不应与{#oakpal-no-overlap}重叠

**键**:包重叠

**类型**:错误

**严重性**:主要

**自**:版本2019.6.0

与&#x200B;*包不应包含重复的OSGi配置*&#x200B;类似，这是复杂项目中常见的问题，在这些复杂项目中，同一节点路径由多个单独的内容包写入。 虽然可以使用内容包依赖关系确保结果一致，但最好避免完全重叠。

### 默认创作模式不应为经典UI {#oakpal-default-authoring}

**键**:ClassicUIAuthoringMode

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

OSGi配置`com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl`定义了AEM中的默认创作模式。 由于自AEM 6.4起已弃用经典UI，因此现在将默认创作模式配置为经典UI时，将会引发问题。

### 具有对话框的组件应具有触屏UI对话框{#oakpal-components-dialogs}

**键**:ComponentWithOnlyClassicUIDialog

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

具有经典UI对话框的AEM组件应始终具有相应的触屏UI对话框，以便提供最佳创作体验，并与不支持经典UI的Cloud Service部署模型兼容。 此规则验证以下情况：

* 具有经典UI对话框的组件（即对话框子节点）必须具有相应的触屏UI对话框（即`cq:dialog`子节点）。
* 具有经典UI设计对话框的组件（即design_dialog节点）必须具有相应的触屏UI设计对话框（即`cq:design_dialog`子节点）。
* 同时具有经典UI对话框和经典UI设计对话框的组件必须同时具有相应的触屏UI对话框和相应的触屏UI设计对话框。

AEM现代化工具文档提供了有关如何将组件从经典UI转换为触屏UI的文档和工具。 有关更多详细信息，请参阅[AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html)。

### 包不应混合使用可变和不可变内容{#oakpal-packages-immutable}

**键**:ImmutableMutableMixedPackage

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

为了与Cloud Service部署模型兼容，单个内容包必须包含存储库不可变区域的内容（即`/apps and /libs, although /libs`不应被客户代码修改，并将导致单独的违规）或可变区域（即其他所有内容），但不能同时包含这两者。 例如，包含`/apps/myco/components/text and /etc/clientlibs/myco`的包与Cloud Service不兼容，并且会导致报告问题。

有关更多详细信息，请参阅[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)。

### 不应使用反向复制代理{#oakpal-reverse-replication}

**键**:反向复制

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

如[发行说明中所述，在Cloud Service部署中不提供对反向复制的支持：删除了复制代理](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents)。

使用反向复制的客户应与Adobe联系以获取其他解决方案。

### OakPAL — 启用代理的客户端库中包含的资源应位于名为“resources {#oakpal-resources-proxy}”的文件夹中

**键**:ClientlibProxyResource

**类型**:错误

**严重性**:次要

**自**:版本2021.2.0

AEM客户端库可能包含静态资源，如图像和字体。 如[使用预处理器](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=en#using-preprocessors)中所述，在使用代理客户端库时，这些静态资源必须包含在名为资源的子文件夹中，才能在发布实例上有效引用。

#### 不符合代码{#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 兼容代码{#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL — 使用Cloud Service不兼容的工作流进程{#oakpal-usage-cloud-service}

**键**:CloudServiceIncomplatibleWorkflowProcess

**类型**:代码气味

**严重性**:阻止程序

**自**:版本2021.2.0

随着在AEMCloud Service上转到资产微服务以进行资产处理，在AEM的内部部署版本和AMS版本中使用的多个工作流流程变得不支持或不必要。 位于[aem-cloud-migration](https://github.com/adobe/aem-cloud-migration)的迁移工具可用于在AEMCloud Service迁移期间更新工作流模型。

### OakPAL — 不鼓励使用静态模板，而应使用可编辑的模板{#oakpal-static-template}

**键**:StaticTemplateUsage

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

尽管静态模板的使用在AEM项目中一直非常常见，但是强烈建议使用可编辑的模板，因为它们提供了最大的灵活性，并支持静态模板中不存在的其他功能。 有关更多信息，请参阅[页面模板 — 可编辑](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html?lang=en)。 使用[AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/)，可以在很大程度上自动从静态模板迁移到可编辑的模板。

### OakPAL — 不建议使用旧版基础组件{#oakpal-usage-legacy}

**键**:旧版FoundationComponentUsage

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

多个AEM版本已弃用旧版基础组件（即`/libs/foundation`下的组件），转而使用WCM核心组件。 不建议将旧版基础组件用作自定义组件的基础（无论是通过叠加还是继承），并且应将其转换为相应的核心组件。 [AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/)可促进此转换。

### OakPAL — 应仅使用支持的Runmode名称和排序{#oakpal-supported-runmodes}

**键**:受支持的运行模式

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service对运行模式名称强制实施严格的命名策略，并对这些运行模式实施严格的排序。 在[Runmodes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)上可以找到支持的运行模式列表，与此相关的任何偏差都将被标识为问题。

### OakPAL — 自定义搜索索引定义节点必须是/oak:index {#oakpal-custom-search}的直接子节点

**键**:OakIndexLocation

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）是`/oak:index`的直接子节点。 必须移动其他位置的索引才能与AEMCloud Service兼容。 有关搜索索引的更多信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL — 自定义搜索索引定义节点必须具有2 {#oakpal-custom-search-compatVersion}的compatVersion

**键**:IndexCompatVersion

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）必须将compatVersion属性设置为2。 AEMCloud Service不支持任何其他值。 有关搜索索引的更多信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL — 自定义搜索索引定义节点的子节点类型必须为nt:unstructured {#oakpal-descendent-nodes}

**键**:IndexDescendantNodeType

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

如果自定义搜索索引定义节点具有无序的子节点，则可能会发生难以排除的问题。 为避免出现这些情况，建议`oak:QueryIndexDefinition`节点的所有子节点类型均为nt:unstructured。

### OakPAL — 自定义搜索索引定义节点必须包含名为indexRules的子节点，该子节点具有子节点{#oakpal-custom-search-index}

**键**:IndexRulesNode

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

正确定义的自定义搜索索引定义节点必须包含一个名为indexRules的子节点，而该子节点又必须至少有一个子节点。 有关更多信息，请参阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### OakPAL — 自定义搜索索引定义节点必须遵循命名约定{#oakpal-custom-search-definitions}

**键**:IndexName

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即`oak:QueryIndexDefinition`类型的节点）必须按照[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)中描述的特定模式命名。

### OakPAL — 自定义搜索索引定义节点必须使用索引类型lucene {#oakpal-index-type-lucene}

**键**:IndexType

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）具有类型属性，并将值设置为&#x200B;**lucene**。 在迁移到AEMCloud Service之前，必须更新使用旧索引类型的索引。 有关更多信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL — 自定义搜索索引定义节点不得包含名为seed {#oakpal-property-name-seed}的属性

**键**:IndexSeedProperty

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service禁止自定义搜索索引定义（即`oak:QueryIndexDefinition`类型的节点）包含名为seed的属性。 在迁移到AEMCloud Service之前，必须更新使用此属性的索引。 有关更多信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL — 自定义搜索索引定义节点不得包含名为reindex {#oakpal-reindex-property}的属性

**键**:IndexReindexProperty

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service禁止自定义搜索索引定义（即`oak:QueryIndexDefinition`类型的节点）包含名为reindex的属性。 在迁移到AEMCloud Service之前，必须更新使用此属性的索引。 有关更多信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

## Dispatcher优化工具{#dispatcher-optimization-tool-rules}

以下部分重点介绍Cloud Manager执行的DOT检查：

* [DOT — 解析冲突 — 调度程序配置意外令牌](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [DOT — 解析冲突 — 调度程序配置不匹配引号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [DOT — 解析冲突 — 调度程序配置缺少大括号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [DOT — 解析冲突 — 调度程序配置额外大括号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [DOT — 解析冲突 — Dispatcher配置缺少必需属性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [DOT — 解析冲突 — Dispatcher配置已弃用属性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [DOT — 解析冲突 — 未找到调度程序配置](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [DOT — 解析冲突 — 未找到Httpd配置包含文件](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [DOT — 解析冲突 — 调度程序配置常规](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [DOT - Dispatcher发布场缓存应启用serveStaleOnError](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [DOT - Dispatcher发布场筛选器应包含6.x.x版本的AEM原型中的默认拒绝规则](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [DOT - Dispatcher发布场缓存状态文件级别属性应>= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [DOT - Dispatcher发布场gracePeriod属性应为>= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [DOT — 每个Dispatcher场应具有唯一的名称](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [DOT - Dispatcher发布场缓存应当以允许列表方式配置其ignoreUrlParams规则](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [DOT - Dispatcher发布场过滤器应以允许列表方式指定允许的Sling选择器](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [DOT - Dispatcher发布场过滤器应以允许列表方式指定允许的Sling后缀模式](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [DOT — 在具有根目录路径的VirtualHost Directory部分中，不应使用“要求所有已授予”指令](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
