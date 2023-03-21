---
title: 自定义代码质量规则
description: 了解 Cloud Manager 在基于来自 AEM 工程的最佳实践的代码质量测试过程中执行的自定义代码质量规则的详细信息。
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: ef87e13eb81faf5605cdd16c6fd46d5f7b3233a9
workflow-type: tm+mt
source-wordcount: '3531'
ht-degree: 100%

---


# 自定义代码质量规则 {#custom-code-quality-rules}

了解 Cloud Manager 在基于来自 AEM 工程的最佳实践的[代码质量测试](/help/using/code-quality-testing.md)过程中执行的自定义代码质量规则的详细信息。

>[!NOTE]
>
>此处提供的代码示例仅用于说明目的。请参阅 [SonarQube 的概念](https://docs.sonarqube.org/latest/)文档，了解其概念和质量规则。

## SonarQube 规则 {#sonarqube-rules}

以下部分详细介绍了 Cloud Manager 执行的 SonarQube 规则。

### 请勿使用有潜在危险的功能 {#do-not-use-potentially-dangerous-functions}

* **密钥**：CQRules:CWE-676
* **类型**：漏洞
* **严重性**：主要
* **开始版本**：版本 2018.4.0

`Thread.stop()` 和 `Thread.interrupt()` 方法可能会产生难以重现的问题，并且有时会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不合规的代码 {#non-compliant-code}

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

#### 合规的代码 {#compliant-code}

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

### 请勿使用可能受外部控制的格式字符串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **密钥**：CQRules:CWE-134
* **类型**：漏洞
* **严重性**：主要
* **从以下版本开始**：版本 2018.4.0

使用来自外部源的格式字符串（例如，请求参数或用户生成的内容）可能会使应用程序遭受拒绝服务攻击。在某些情况下，虽然格式字符串可能会受到外部控制，但仅允许来自受信任源。

#### 不合规的代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP 请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **密钥**：CQRules:ConnectionTimeoutMechanism
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.6.0

从 AEM 应用程序内部执行 HTTP 请求时，请务必确保配置适当的超时以避免不必要的线程消耗。 不幸的是，Java™ 的默认 HTTP 客户端 (`java.net.HttpUrlConnection`) 和常用的 Apache HTTP 组件客户端的默认行为都是永不超时，因此必须明确设置超时。作为最佳实践，这些超时不应超过 60 秒。

#### 不合规的代码 {#non-compliant-code-2}

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

#### 合规的代码 {#compliant-code-1}

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

### ResourceResolver 对象应始终关闭 {#resourceresolver-objects-should-always-be-closed}

* **密钥**：CQRules:CQBP-72
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

从 `ResourceResolverFactory` 获取的 `ResourceResolver` 对象占用系统资源。 虽然可以采取一些措施以在不再使用 `ResourceResolver` 时回收这些资源，但通过调用 `close()` 方法显式关闭任何打开的 `ResourceResolver` 对象会更有效。

一个常见的误解是，使用现有 JCR 会话创建的 `ResourceResolver` 对象不应明确关闭，否则会关闭底层 JCR 会话。情况并非如此。 无论 `ResourceResolver` 的打开方式如何，只要不再使用它，就应将它关闭。 由于 `ResourceResolver` 实施 `Closeable` 接口，也可以使用 `try-with-resources` 语法，而不是显式调用 `close()`。

#### 不合规的代码 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 合规的代码 {#compliant-code-2}

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

### 请勿使用 Sling Servlet 路径来注册 Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **密钥**：CQRules:CQBP-75
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

如 [Sling 文档](https://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，建议不要通过路径绑定 servlet。 路径绑定的 servlet 不能使用标准 JCR 访问控制，因此，需要额外的安全严密性。 建议在存储库中创建节点并按资源类型注册 servlet，而不是使用路径绑定的 servlet。

#### 不合规的代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应被记录或引发，而不是同时记录和引发 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **密钥**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

通常，一个异常应只记录一次。 将一个异常记录多次可能会导致混淆，因为不清楚该异常发生了几次。 导致出现此情况的最常见模式是记录并引发捕获的异常。

#### 不合规的代码 {#non-compliant-code-6}

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

#### 合规的代码 {#compliant-code-3}

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

### 避免 Log 语句后面紧跟 Throw 语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **密钥**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

另一个要避免的常见模式是记录一条消息，然后立即引发异常。 这通常表明异常消息最终会在日志文件中重复。

#### 不合规的代码 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 合规的代码 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在处理 GET 或 HEAD 请求时，避免在 INFO 级别进行记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **密钥**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **类型**：代码异味
* **严重性**：轻微

通常，应使用 INFO 日志级别来划分重要操作，默认情况下，AEM 配置为在 INFO 级别或更高级别进行记录。 GET 和 HEAD 方法只能为只读操作，因此，不会构成重要操作。 在 INFO 级别进行记录来响应 GET 或 HEAD 请求可能会产生大量日志噪音，导致更难以识别日志文件中的有用信息。 处理 GET 或 HEAD 请求时，应在 WARN 或 ERROR 级别进行记录（如果出现问题），或在 DEBUG 或 TRACE 级别进行记录（如果更深入的故障排除信息会很有用）。

>[!NOTE]
>
>这不适用于每个请求的 access.log-type 记录。

#### 不合规的代码 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 合规的代码 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 请勿使用 Exception.getMessage() 作为 Logging 语句的第一个参数 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **密钥**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然也可以使用堆栈跟踪来确定上下文，但通常日志消息将更易于阅读和理解。 因此，在记录异常时，将异常消息用作日志消息是一种不好的做法。 异常消息将包含所发生的问题，而日志消息应让日志读者知道，当发生异常时，应用程序正在做什么。 仍会记录异常消息。 通过指定您自己的消息，可使日志更易于理解。

#### 不合规的代码 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 合规的代码 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 应在 WARN 或 ERROR 级别记录 Catch 块 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **密钥**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

顾名思义，Java™ 异常应始终在异常情况下使用。 因此，当捕获到异常时，请务必确保在适当的级别记录日志消息：WARN 或 ERROR。这将确保这些消息正确显示在日志中。

#### 不合规的代码 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 合规的代码 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿将堆栈跟踪打印到控制台 {#do-not-print-stack-traces-to-the-console}

* **密钥**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2018.4.0

上下文对于理解日志消息是至关重要的。使用 `Exception.printStackTrace()` 会导致仅将堆栈跟踪输出到标准错误流，从而丢失所有上下文。此外，在像 AEM 这样的多线程应用程序中，如果使用此方法并行打印多个异常，则其堆栈跟踪可能会发生重叠，从而导致产生严重混淆。应仅通过记录框架来记录异常。

#### 不合规的代码 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 合规的代码 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿输出到标准输出或标准错误 {#do-not-output-to-standard-output-or-standard-error}

* **密钥**：CQRules:CQBP-44—LogLevelConsolePrinters
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2018.4.0

AEM 中的记录应始终通过记录框架 SLF4J 完成。直接输出到标准输出或标准错误流将丢失记录框架提供的结构和上下文信息，并且有时可能会导致出现性能问题。

#### 不合规的代码 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 合规的代码 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬编码的 /apps 和 /libs 路径 {#avoid-hardcoded-apps-and-libs-paths}

* **密钥**：CQRules:CQBP-71
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2018.4.0

通常，以 `/libs` 和 `/apps` 开头的路径不应进行硬编码，因为它们引用的路径最常存储为 Sling 搜索路径（默认情况下，设置为 `/libs,/apps`）的相对路径。使用绝对路径可能会引入小缺陷，这些缺陷仅在项目生命周期的后期出现。

#### 不合规的代码 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 合规的代码 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不应使用 Sling 调度程序 {#sonarqube-sling-scheduler}

* **密钥**：CQRules:AMSCORE-554
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

Sling 调度程序不得用于需要保证执行的任务。 Sling 计划作业可保证执行，并且更适合集群和非集群环境。

请参阅 [Apache Sling 事件和作业处理文档](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)，详细了解如何在集群环境中处理 Sling 作业。

### 不应使用 AEM 弃用的 API {#sonarqube-aem-deprecated}

* **密钥**：AMSCORE-553
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

AEM API 接口正在不断修订，以识别建议不要使用的 API，从而将其弃用。

通常情况下，使用标准 Java™ *@Deprecated* 注释来弃用这些 API，如 `squid:CallToDeprecatedMethod` 所标识。

但在某些情况下，API 会在 AEM 上下文中被弃用，但在其他上下文中可能不会被弃用。此规则标识第二个类。

## OakPAL 内容规则 {#oakpal-rules}

以下部分详细介绍了 Cloud Manager 执行的 OakPAL 检查。

>[!NOTE]
>
>OakPAL 是一个框架，它使用独立的 Oak 存储库来验证内容包。 它由一个 AEM 合作伙伴开发，并获得了 2019 年的 AEM Rockstar 北美区大奖。

### 客户不应实施或扩展用 @ProviderType 注释的产品 API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **密钥**：CQBP-84
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.7.0

AEM API 包含 Java™ 接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。例如，接口 `com.day.cq.wcm.api.Page` 仅由 AEM 实现。

当将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码，因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 码实现了 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

仅由 AEM 实现的接口和类通过 `org.osgi.annotation.versioning.ProviderType` 进行注释，有时通过类似的旧批注 `aQute.bnd.annotation.ProviderType` 进行注释。此规则标识实现此类接口或自定义代码扩展类的情况。

#### 不合规的代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 客户包不应在 /libs 下创建或修改节点 {#oakpal-customer-package}

* **密钥**：BannedPath
* **类型**：错误
* **严重性**：阻断
* **从以下版本开始**：版本 2019.6.0

客户应将 AEM 内容存储库中的 `/libs` 内容树视为只读，这是一个长期存在的最佳实践。修改 `/libs` 下的节点和属性会给主要和次要更新带来重大风险。 对 `/libs` 的修改只能由 Adobe 通过正式渠道进行。

### 包不应包含重复的 OSGi 配置 {#oakpal-package-osgi}

* **密钥**：DuplicateOsgiConfigurations
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

复杂项目中出现的一个常见问题是，将同一个 OSGi 组件配置多次。 这会导致无法明确哪种配置将是可操作的。此规则是“运行模式感知型”的，因为它只会识别在同一运行模式或运行模式组合中多次配置同一组件的问题。

#### 不合规的代码 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 合规的代码 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Config 和 Install 文件夹应只包含 OSGi 节点 {#oakpal-config-install}

* **密钥**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

出于安全原因，包含 `/config/` 和 `/install/` 的路径只能由 AEM 中的管理用户读取，并且只能用于 OSGi 配置和 OSGi 捆绑包。 如果将其他类型的内容放在包含这些区段的路径下，则会导致应用程序行为在管理用户和非管理用户之间无意中发生变化。

一个常见问题是，在组件对话框中或在为内联编辑指定富文本编辑器配置时使用名为 `config` 的节点。 要解决此问题，应将违规节点重命名为合规的名称。对于富文本编辑器配置，使用 `cq:inplaceEditing` 节点上的 `configPath` 属性指定新位置。

#### 不合规的代码 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 合规的代码 {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 包不应重叠 {#oakpal-no-overlap}

* **密钥**：PackageOverlaps
* **类型**：错误
* **严重性**：主要
* **从以下版本开始**：版本 2019.6.0

与[“包不应包含重复的 OSGi 配置”规则](#oakpal-package-osgi)类似，这是复杂项目中的一个常见问题，其中同一节点路径被多个单独的内容包写入。虽然可使用内容包依赖项来确保获得一致的结果，但最好是完全避免重叠。

### 默认创作模式不应是经典 UI {#oakpal-default-authoring}

* **密钥**：ClassicUIAuthoringMode
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

OSGi 配置 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 定义 AEM 中的默认创作模式。 由于经典 UI 自 AEM 6.4 之后已被弃用，因此，在将默认创作模式配置为经典 UI 时，现在将引发问题。

### 带对话框的组件应具有 Touch UI 对话框 {#oakpal-components-dialogs}

* **密钥**：ComponentWithOnlyClassicUIDialog
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **从以下版本开始**：版本 2020.5.0

具有经典 UI 对话框的 AEM 组件应始终具有对应的 Touch UI 对话框，以提供最佳创作体验并与不支持经典 UI 的 Cloud Service 部署模型兼容。此规则验证以下场景：

* 具有经典 UI 对话框（即 `dialog` 子节点）的组件必须具有相应的 Touch UI 对话框（即 `cq:dialog` 子节点）。
* 具有经典 UI 设计对话框（即 `design_dialog` 节点）的组件必须具有相应的 Touch UI 设计对话框（即 `cq:design_dialog` 子节点）。
* 具有经典 UI 对话框和经典 UI 设计对话框的组件必须具有对应的 Touch UI 对话框和 Touch UI 设计对话框。

“AEM 现代化工具”文档提供了有关如何将组件从经典 UI 转换为 Touch UI 的详细信息以及使用的工具。有关更多详细信息，请参阅[“AEM 现代化工具”文档](https://opensource.adobe.com/aem-modernize-tools/)。

### 包不应混合可变和不可变的内容 {#oakpal-packages-immutable}

* **密钥**：ImmutableMutableMixedPackage
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

要与 Cloud Service 部署模型兼容，各个内容包必须包含存储库的不可变区域（即 `/apps` 和 `/libs`）的内容或可变区域的内容（即未在 `/apps` 或 `/libs` 中的内容），但不能同时包含这两个区域的内容。 例如，同时包含 `/apps/myco/components/text and /etc/clientlibs/myco` 的包不与 Cloud Service 兼容，并且将导致报告问题。

有关更多详细信息，请参阅[“AEM 项目结构”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)。

>[!NOTE]
>
>[客户包不应在 /libs 下创建或修改节点](#oakpal-customer-package)规则始终适用。

### 不应使用反向复制代理 {#oakpal-reverse-replication}

* **密钥**：ReverseReplication
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **从以下版本开始**：版本 2020.5.0

Cloud Service 部署中不支持反向复制，如[发行说明：移除复制代理](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html#replication-agents)中所述。

使用反向复制的客户应联系 Adobe 以获取替代解决方案。

### 启用代理的客户端库中包含的资源应位于名为 resources 的文件夹中 {#oakpal-resources-proxy}

* **密钥**：ClientlibProxyResource
* **类型**：错误
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

AEM 客户端库可能包含静态资源，如图像和字体。如[“使用客户端库”文档](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html#using-preprocessors)中所述，在使用代理的客户端库时，这些静态资源必须包含在名为 `resources` 的子文件夹中，才能在发布实例上有效引用这些资源。

#### 不合规的代码 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 合规的代码 {#compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### 与 Cloud Service 不兼容的工作流的使用 {#oakpal-usage-cloud-service}

* **密钥**：CloudServiceIncompatibleWorkflowProcess
* **类型**：代码异味
* **严重性**：阻断
* **从以下版本开始**：版本 2021.2.0

迁移到 Asset 微服务以便在 AEM Cloud Service 上进行资产处理后，在 AEM 的内部部署和 AMS 版本中使用的多个工作流已变得不受支持或不必要。

[AEM Assets as a Cloud Service GitHub 存储库](https://github.com/adobe/aem-cloud-migration)中的迁移工具可在迁移到 AEM as a Cloud Service 的过程中用于更新工作流模型。

### 建议不要使用静态模板来支持可编辑的模板 {#oakpal-static-template}

* **密钥**：StaticTemplateUsage
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

虽然静态模板的使用历来在 AEM 项目中很普遍，但强烈建议使用可编辑的模板，因为它们提供了最大的灵活性，并支持静态模板中不存在的附加功能。要获取更多信息，请参阅[“页面模板 - 可编辑”文档](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html)。

可以使用 [AEM 现代化工具](https://opensource.adobe.com/aem-modernize-tools/)在很大程度上实现从静态模板到可编辑模板的迁移的自动化。

### 建议不要使用旧的基础组件 {#oakpal-usage-legacy}

* **密钥**：LegacyFoundationComponentUsage
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

旧的基础组件（即 `/libs/foundation` 下的组件）已在多个 AEM 版本中被弃用以便支持[核心组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)建议不要使用旧的基础组件作为自定义组件的基础（无论是通过叠加还是继承），并且应将这些基础组件转换为对应的核心组件。

可以通过 [AEM 现代化工具](https://opensource.adobe.com/aem-modernize-tools/)促进此转换。

### 仅应使用受支持的运行模式名称和排序 {#oakpal-supported-runmodes}

* **密钥**：SupportedRunmode
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

AEM Cloud Service 对运行模式名称实施严格的命名策略，并对这些运行模式进行严格的排序。可以在[“部署到 AEM as a Cloud Service”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)中找到受支持的运行模式列表，任何偏离该列表的情况都将被视为存在问题。

### 自定义搜索索引定义节点必须是 /oak:index 的直接子节点 {#oakpal-custom-search}

* **密钥**：OakIndexLocation
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）是 `/oak:index` 的直接子节点。必须移动其他位置的索引才能与 AEM Cloud Service 兼容。有关搜索索引的更多信息，请参阅[“内容搜索和索引编制”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)。

### 自定义搜索索引定义节点的 compatVersion 必须为 2 {#oakpal-custom-search-compatVersion}

* **密钥**：IndexCompatVersion
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）必须将 `compatVersion` 属性设置为 `2`。AEM Cloud Service 不支持任何其他值。有关搜索索引的更多信息，请参阅[“内容搜索和索引编制”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)。

### 自定义搜索索引定义节点的后代节点的类型必须是 nt:unstructured {#oakpal-descendent-nodes}

* **密钥**：IndexDescendantNodeType
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

当自定义搜索索引定义节点具有无序子节点时，可能会出现难以解决的问题。为了避免出现此情况，建议 `oak:QueryIndexDefinition` 节点的所有后代节点的类型为 `nt:unstructured`。

### 自定义搜索索引定义节点必须包含一个名为 indexRules 的具有子节点的子节点 {#oakpal-custom-search-index}

* **密钥**：IndexRulesNode
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

正确定义的自定义搜索索引定义节点必须包含一个名为 `indexRules` 的子节点，而该子节点必须具有至少一个子节点。有关更多信息，请参阅 [Oak 文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### 自定义搜索索引定义节点必须遵循命名惯例 {#oakpal-custom-search-definitions}

* **密钥**：IndexName
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）必须按照[内容搜索和索引编制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)中所述的特定模式进行命名。

### 自定义搜索索引定义节点必须使用索引类型 lucene  {#oakpal-index-type-lucene}

* **密钥**：IndexType
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）必须将 `type` 属性的值设置为 `lucene`。在迁移到 AEM Cloud Service 之前，必须更新使用旧索引类型的索引编制。有关更多信息，请参阅[“内容搜索和索引编制”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

### 自定义搜索索引定义节点不得包含名为 seed 的属性 {#oakpal-property-name-seed}

* **密钥**：IndexSeedProperty
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 禁止自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）包含名为 `seed` 的属性。在迁移到 AEM Cloud Service 之前，必须更新使用此属性的索引编制。有关更多信息，请参阅[“内容搜索和索引编制”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

### 自定义搜索索引定义节点不得包含名为 reindex 的属性 {#oakpal-reindex-property}

* **密钥**：IndexReindexProperty
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

AEM Cloud Service 禁止自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）包含名为 `reindex` 的属性。在迁移到 AEM Cloud Service 之前，必须更新使用此属性的索引编制。有关更多信息，请参阅[“内容搜索和索引编制”文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

## Dispatcher 优化工具 {#dispatcher-optimization-tool-rules}

以下部分列出了 Cloud Manager 执行的 Dispatcher 优化工具 (DOT) 检查。访问每个检查的链接以查看其 GitHub 定义和详细信息。

* [Dispatcher 配置意外令牌](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [Dispatcher 配置不匹配引号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [Dispatcher 配置缺少大括号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [Dispatcher 配置额外大括号](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [Dispatcher 配置缺少强制属性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [Dispatcher 配置已弃用的属性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [Dispatcher 配置未找到](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [Httpd 配置包含文件未找到](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [Dispatcher 配置常规](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [Dispatcher 发布场缓存应已启用 serveStaleOnError](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [Dispatcher 发布场过滤器应包含来自 AEM 原型的 6.x.x 版本的默认拒绝规则](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [Dispatcher 发布场缓存 statfileslevel 属性应大于等于 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [Dispatcher 发布场缓存 gracePeriod 属性应大于等于 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [每个 Dispatcher 场都应该有一个唯一的名称](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [Dispatcher 发布场缓存应以允许列表方式配置其 ignoreUrlParams 规则](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [Dispatcher 发布场过滤器应以允许列表方式指定允许的 Sling 选择器](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [Dispatcher 发布场过滤器应以允许列表方式指定允许的 Sling 后缀模式](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [不要在具有根目录路径的“VirtualHost 目录”部分中使用“Require all granted”指令](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
