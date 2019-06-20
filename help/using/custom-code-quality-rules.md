---
title: 自定义代码质量规则
seo-title: 自定义代码质量规则
description: 请阅读本页，了解Cloud Manager执行的自定义代码质量规则。
seo-description: 请阅读本页，了解Adobe Experience Manager Cloud Manager执行的自定义代码质量规则。
uuid: a7cb465-1982-46be-9e57-e67 b5984979
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a 1866-ef62362509 f
translation-type: tm+mt
source-git-commit: f76b8e6a036ab920f11fb913d3ad29818f1e153f

---


# Custom Code Quality Rules {#custom-code-quality-rules}

本页描述了Cloud Manager执行的自定义代码质量规则，这些规则基于AEM工程的最佳实践创建。

>[!NOTE]
>
>此处提供的代码示例仅用于说明性目的。

## SonarQube Rules {#sonarqube-rules}

下节突出显示了SonarQue规则：

### Do not use potentially dangerous functions {#do-not-use-potentially-dangerous-functions}

**密钥**：CQ规则：CWE-676

**类型**：漏洞

**严重性**：Major

**** 因为：版本2018.4.0

***String. stop()*** 和 ***线程. interbrounch()的方法*** 可能会生成难以重现的问题，在某些情况下会出现安全漏洞。应严格监控和验证其使用情况。通常，消息传递是实现类似目标的更安全方法。

#### Non-Compliant Code {#non-compliant-code}

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

#### Compliant Code {#compliant-code}

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

### Do not use format strings which may be externally controlled {#do-not-use-format-strings-which-may-be-externally-controlled}

**密钥**：CQ规则：CWE-134

**类型**：漏洞

**严重性**：Major

**** 因为：版本2018.4.0

使用外部源(此请求参数或用户生成的内容)的格式字符串可以使应用程序暴露应用程序拒绝服务攻击。某些情况下，格式字符串可能是外部控制的，但只允许受信任的源。

#### Non-Compliant Code {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP requests should always have socket and connect timeouts {#http-requests-should-always-have-socket-and-connect-timeouts}

**密钥**：CQ规则：ConnectionTimeout机制

**类型**：Bug

**严重性**：关键

**** 因为：版本2018.6.0

在AEM应用程序中执行HTTP请求时，务必确保配置正确的超时以避免不必要的线程消耗。不幸的是，Java的默认HTTP Client(InstantPurlConnection)和常用Apache HTTP Components客户端的默认行为是永不超时，因此必须显式设置超时。此外，作为最佳实践，这些超时不应超过60秒。

#### Non-Compliant Code {#non-compliant-code-2}

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

#### Compliant Code {#compliant-code-1}

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

### Product APIs annotated with @ProviderType should not be implemented or extended by customers {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**密钥**：CQBP-84，CQBP-84-附属

**类型**：Bug

**严重性**：关键

**** 因为：版本2018.7.0

AEM API包含仅供自定义代码使用但未实现的Java接口和类。For example, the interface *com.day.cq.wcm.api.Page* is designed to be implemented by ***AEM only***.

当新方法添加到这些接口时，这些附加的方法不会影响使用这些接口的现有代码，因此，将新方法添加到这些接口会被视为向后兼容。However, if custom code ***implements*** one of these interfaces, that custom code has introduced a backwards-compatibility risk for the customer.

Interfaces (and classes) which are only intended to be implemented by AEM are annotated with *org.osgi.annotation.versioning.ProviderType* (or, in some cases, a similar legacy annotation *aQute.bnd.annotation.ProviderType*). 此规则用于标识通过自定义代码实现(或扩展类)此类接口的情况。

#### Non-Compliant Code {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver objects should always be closed {#resourceresolver-objects-should-always-be-closed}

**密钥**：CQ规则：CQBP-72

**类型**：代码嗅觉

**严重性**：Major

**** 因为：版本2018.4.0

resourceSolver从resourceSolverFactory获得的对象消耗系统资源。尽管在ResourceSolver不再使用时有相应的措施可重新调用这些资源，但通过调用close()方法显式关闭任何打开的resourceSolver对象更加有效。

一个相对常见的误解是，使用现有JCR Session创建的ResourceSolver对象不应明确关闭，也不应关闭基础JCR会话。不是这种情况-无论resourceSolver是如何打开的，它在不再使用时都应关闭。由于resourceSolver实现了可关闭的接口，因此还可以使用尝试资源的语法而不是显式调用close()。

#### Non-Compliant Code {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Compliant Code {#compliant-code-2}

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

### Do not use Sling servlet paths to register servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

**密钥**：CQ规则：CQBP-75

**类型**：代码嗅觉

**严重性**：Major

**** 因为：版本2018.4.0

As described in the [Sling documentation](http://sling.apache.org/documentation/the-sling-engine/servlets.html), bindings servlets by paths is discouraged. 路径绑定servlet无法使用标准JCR访问控制，因此需要额外的安全性控制。建议在存储库中创建节点并按资源类型注册servlet，而不是使用路径绑定servlet。

#### Non-Compliant Code {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Caught Exceptions should be logged or thrown, but not both {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密钥**：CQ规则：CQBP-44—catChandIderLogOverline

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

通常情况下，应只记录一次异常。多次记录异常可能会引起混淆，因为不清楚出现异常的次数。导致这种情况的最常见的模式是记录并引发捕获的异常。

#### Non-Compliant Code {#non-compliant-code-6}

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

#### Compliant Code {#compliant-code-3}

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

### Avoid having a log statement immediately followed by a throw statement {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密钥**：CQ规则：CQBP-44—consectUvelogAndRandthrow

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

另一个避免的常见模式是记录一条消息，然后立即引发异常。这通常表示在日志文件中会重复出现异常消息。

#### Non-Compliant Code {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Compliant Code {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Avoid logging at INFO when handling GET or HEAD requests {#avoid-logging-at-info-when-handling-get-or-head-requests}

**密钥**：CQ规则：CQBP-44—LoginFointorHeadRequest

**类型**：代码嗅觉

**严重性**：未成年人

通常，应使用Info日志级别来划定重要操作，默认情况下，AEM配置为在信息级别或以上日志。GET和HEAD方法只应是只读操作，因此不构成重要操作。在POINT级别进行记录以响应GET或HEAD请求可能会造成大量日志噪声，从而使得难以在日志文件中识别有用信息。当处理GET或HEAD请求时，如果有错误，或者如果有更深入的故障排除信息，处理GET或HEAD请求应处于WARN或ERROR级别。

>[!CAUTION]
>
>这不适用于每个请求的access. log-type记录。

#### Non-Compliant Code {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Compliant Code {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Do not use Exception.getMessage() as the first parameter of a logging statement {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**密钥**：CQ规则：CQBP-44—exceptiongetMessagesFirstLogParam

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

作为最佳实践，日志消息应提供有关应用程序中的位置的上下文信息。尽管上下文也可以通过使用堆栈跟踪来确定，但通常日志消息更易于阅读和理解。因此，在记录异常时，使用例外消息将使用异常消息作为日志消息-例外消息将包含错误的消息，而日志消息应用于告知日志阅读器在异常发生时应用程序所做的操作。例外消息仍将记录；通过指定自己的消息，即可更轻松地理解日志。

#### Non-Compliant Code {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Compliant Code {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Logging in catch blocks should be at the WARN or ERROR level {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密钥**：CQ规则：CQBP-44—WRonGlogRecoinIncatBlock

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

As the name suggests, Java exceptions should always be used in *exceptional* circumstances. 因此，在捕获异常时，务必确保日志消息在适当级别记录- WARN或ERROR。这可以确保这些消息在日志中正确显示。

#### Non-Compliant Code {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Compliant Code {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Do not print stack traces to the console {#do-not-print-stack-traces-to-the-console}

**密钥**：CQ规则：CQBP-44—ExceptionPrintStackTrace

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

如前所述，在理解日志消息时，上下文至关重要。Using Exception.printStackTrace() causes **only** the stack trace to be output to the standard error stream thereby losing all context. 此外，在AEM等多线程应用程序中，如果同时使用此方法打印多个例外，它们的堆栈跟踪可能会重叠，从而产生明显混淆。例外情况应只通过日志记录框架记录。

#### Non-Compliant Code {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Compliant Code {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Do not output to Standard Output or Standard Error {#do-not-output-to-standard-output-or-standard-error}

**密钥**：CQ规则：CQBP-44- LogogConsole打印机

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

登录AEM应始终通过日志记录框架(SLF4J)完成。直接输出到标准输出或标准错误流会丢失日志记录框架提供的结构和上下文信息，某些情况下可能会导致性能问题。

#### Non-Compliant Code {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Compliant Code {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Avoid Hardcoded /apps and /libs Paths {#avoid-hardcoded-apps-and-libs-paths}

**密钥**：CQ规则：CQBP-71

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

通常，以/libs和/apps开头的路径不应被硬编码为路径，因为这些路径最常被存储为相对于Sling搜索路径的路径(默认情况下设置为/libs或应用程序)。使用绝对路径可能会引入细微的瑕疵，这些瑕疵只会在项目生命周期后出现。

#### Non-Compliant Code {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Compliant Code {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```


## OakPAL Content Rules {#oakpal-rules}

请查找云管理器执行的OAKPAL检查。

>[!NOTE]
>OkPAL是由AEM合作伙伴开发的一个框架(和2019AEM Rockstar北美语言优胜者)，该框架使用独立的Oak存储库验证内容包。

### Customer Packages Should Not Create or Modify Nodes Under /libs {#oakpal-customer-package}

**密钥**：bannetPath

**类型**：Bug

**严重性**：阻止程序

**** 因为：版本2019.6.0

一直以来，AEM内容存储库中的/libs内容树都应该被客户视为只读。Modifying nodes and properties under */libs* creates significant risk for major and minor updates. Modifications to */libs* should only be made by Adobe through official channels.

### Packages Should Not Contain Duplicate OSGi Configurations {#oakpal-package-osgi}

**密钥**：复制操作图标

**类型**：Bug

**严重性**：Major

**** 因为：版本2019.6.0

在复杂项目上发生的常见问题是多次配置同一OSGi组件。这会导致将哪些配置设置为可操作。此规则为“runode-aware”，因为它只识别同一组件在同一运行模式下多次配置(或运行模式组合)。

#### Non Compliant Code {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Compliant Code {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Config and Install Folders Should Only Contain OSGi Nodes {#oakpal-config-install}

**密钥**：configandInstallShordonlyContainosgiNote

**类型**：Bug

**严重性**：Major

**** 因为：版本2019.6.0

For security reasons, paths containing */config/ and /install/* are only readable by administrative users in AEM and should be used only for OSGi configuration and OSGi bundles. 在包含这些区段的路径下放置其他类型的内容会导致在管理和非管理用户之间有意发生变化。

### Packages Should Not Overlap {#oakpal-no-overlap}

**密钥**：PackageWorks

**类型**：Bug

**严重性**：Major

**** 因为：版本2019.6.0

Similar to the *Packages Should Not Contain Duplicate OSGi Configurations* this is a common problem on complex projects where the same node path is written to by multiple separate content packages. 使用内容包依赖关系可确保得到一致的结果，最好避免完全避免重叠。
