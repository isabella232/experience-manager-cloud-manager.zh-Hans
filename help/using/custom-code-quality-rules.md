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
source-git-commit: f8cea9d52ebb01d7f5291d4dfcd82011da8dacc2

---


# 自定义代码质量规则 {#custom-code-quality-rules}

本页描述了Cloud Manager执行的自定义代码质量规则，这些规则基于AEM工程的最佳实践创建。

>[!NOTE]
>
>此处提供的代码示例仅用于说明性目的。

## Sonarque规则 {#sonarqube-rules}

下节突出显示了SonarQue规则：

### 不要使用可能危险的函数 {#do-not-use-potentially-dangerous-functions}

**密钥**：CQ规则：CWE-676

**类型**：漏洞

**严重性**：Major

**** 因为：版本2018.4.0

***String. stop()*** 和 ***线程. interbrounch()的方法*** 可能会生成难以重现的问题，在某些情况下会出现安全漏洞。应严格监控和验证其使用情况。通常，消息传递是实现类似目标的更安全方法。

#### 不兼容的代码 {#non-compliant-code}

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

#### 兼容代码 {#compliant-code}

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

### 不要使用可能是外部控制的格式字符串 {#do-not-use-format-strings-which-may-be-externally-controlled}

**密钥**：CQ规则：CWE-134

**类型**：漏洞

**严重性**：Major

**** 因为：版本2018.4.0

使用外部源(此请求参数或用户生成的内容)的格式字符串可以使应用程序暴露应用程序拒绝服务攻击。某些情况下，格式字符串可能是外部控制的，但只允许受信任的源。

#### 不兼容的代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

**密钥**：CQ规则：ConnectionTimeout机制

**类型**：Bug

**严重性**：关键

**** 因为：版本2018.6.0

在AEM应用程序中执行HTTP请求时，务必确保配置正确的超时以避免不必要的线程消耗。不幸的是，Java的默认HTTP Client(InstantPurlConnection)和常用Apache HTTP Components客户端的默认行为是永不超时，因此必须显式设置超时。此外，作为最佳实践，这些超时不应超过60秒。

#### 不兼容的代码 {#non-compliant-code-2}

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

#### 兼容代码 {#compliant-code-1}

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

### 使用@ ProviderType注释的产品API不应由客户实施或扩展 {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**密钥**：CQBP-84，CQBP-84-附属

**类型**：Bug

**严重性**：关键

**** 因为：版本2018.7.0

AEM API包含仅供自定义代码使用但未实现的Java接口和类。例如，界面 *com.day.cq.wcm. api只* 设计为 ***由AEM实现***。

当新方法添加到这些接口时，这些附加的方法不会影响使用这些接口的现有代码，因此，将新方法添加到这些接口会被视为向后兼容。但是，如果自定义代码 ***实现*** 了其中一个接口，则自定义代码为客户引入了向后兼容性风险。

只能由AEM实现的接口(和类)使用 *org. osgi. annotation. vertirecting. providerType* (或在某些情况下，类似旧的注释 *Aquote. bnd. annotation. providerType*)添加注释。此规则用于标识通过自定义代码实现(或扩展类)此类接口的情况。

#### 不兼容的代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### resourceSolver对象应始终关闭 {#resourceresolver-objects-should-always-be-closed}

**密钥**：CQ规则：CQBP-72

**类型**：代码嗅觉

**严重性**：Major

**** 因为：版本2018.4.0

resourceSolver从resourceSolverFactory获得的对象消耗系统资源。尽管在ResourceSolver不再使用时有相应的措施可重新调用这些资源，但通过调用close()方法显式关闭任何打开的resourceSolver对象更加有效。

一个相对常见的误解是，使用现有JCR Session创建的ResourceSolver对象不应明确关闭，也不应关闭基础JCR会话。不是这种情况-无论resourceSolver是如何打开的，它在不再使用时都应关闭。由于resourceSolver实现了可关闭的接口，因此还可以使用尝试资源的语法而不是显式调用close()。

#### 不兼容的代码 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 兼容代码 {#compliant-code-2}

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

### 不要使用sling servlet路径注册servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**密钥**：CQ规则：CQBP-75

**类型**：代码嗅觉

**严重性**：Major

**** 因为：版本2018.4.0

如 [sling文档](http://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，按路径绑定servings servlet。路径绑定servlet无法使用标准JCR访问控制，因此需要额外的安全性控制。建议在存储库中创建节点并按资源类型注册servlet，而不是使用路径绑定servlet。

#### 不兼容的代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的例外情形应被记录或引发，但不会同时引发 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密钥**：CQ规则：CQBP-44—catChandIderLogOverline

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

通常情况下，应只记录一次异常。多次记录异常可能会引起混淆，因为不清楚出现异常的次数。导致这种情况的最常见的模式是记录并引发捕获的异常。

#### 不兼容的代码 {#non-compliant-code-6}

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

#### 兼容代码 {#compliant-code-3}

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

### 避免出现日志语句后紧接着出现throw语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密钥**：CQ规则：CQBP-44—consectUvelogAndRandthrow

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

另一个避免的常见模式是记录一条消息，然后立即引发异常。这通常表示在日志文件中会重复出现异常消息。

#### 不兼容的代码 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 兼容代码 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 处理GET或HEAD请求时避免在信息中记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

**密钥**：CQ规则：CQBP-44—LoginFointorHeadRequest

**类型**：代码嗅觉

**严重性**：未成年人

通常，应使用Info日志级别来划定重要操作，默认情况下，AEM配置为在信息级别或以上日志。GET和HEAD方法只应是只读操作，因此不构成重要操作。在POINT级别进行记录以响应GET或HEAD请求可能会造成大量日志噪声，从而使得难以在日志文件中识别有用信息。当处理GET或HEAD请求时，如果有错误，或者如果有更深入的故障排除信息，处理GET或HEAD请求应处于WARN或ERROR级别。

>[!CAUTION]
>
>这不适用于每个请求的access. log-type记录。

#### 不兼容的代码 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 兼容代码 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 请勿使用Exception. getMessage()作为日志记录语句的第一个参数 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**密钥**：CQ规则：CQBP-44—exceptiongetMessagesFirstLogParam

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

作为最佳实践，日志消息应提供有关应用程序中的位置的上下文信息。尽管上下文也可以通过使用堆栈跟踪来确定，但通常日志消息更易于阅读和理解。因此，在记录异常时，使用例外消息将使用异常消息作为日志消息-例外消息将包含错误的消息，而日志消息应用于告知日志阅读器在异常发生时应用程序所做的操作。例外消息仍将记录；通过指定自己的消息，即可更轻松地理解日志。

#### 不兼容的代码 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 兼容代码 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 在catch块中记录应处于WARN或ERROR级别 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密钥**：CQ规则：CQBP-44—WRonGlogRecoinIncatBlock

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

顾名思义，Java异常应始终在 *特殊* 情况下使用。因此，在捕获异常时，务必确保日志消息在适当级别记录- WARN或ERROR。这可以确保这些消息在日志中正确显示。

#### 不兼容的代码 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 兼容代码 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不要将堆栈跟踪打印到控制台 {#do-not-print-stack-traces-to-the-console}

**密钥**：CQ规则：CQBP-44—ExceptionPrintStackTrace

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

如前所述，在理解日志消息时，上下文至关重要。使用Exception. printStackTrace() **仅** 导致堆栈跟踪输出到标准错误流，从而失去所有上下文。此外，在AEM等多线程应用程序中，如果同时使用此方法打印多个例外，它们的堆栈跟踪可能会重叠，从而产生明显混淆。例外情况应只通过日志记录框架记录。

#### 不兼容的代码 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 兼容代码 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不输出至标准输出或标准错误 {#do-not-output-to-standard-output-or-standard-error}

**密钥**：CQ规则：CQBP-44- LogogConsole打印机

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

登录AEM应始终通过日志记录框架(SLF4J)完成。直接输出到标准输出或标准错误流会丢失日志记录框架提供的结构和上下文信息，某些情况下可能会导致性能问题。

#### 不兼容的代码 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 兼容代码 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬编码/apps和/libs路径 {#avoid-hardcoded-apps-and-libs-paths}

**密钥**：CQ规则：CQBP-71

**类型**：代码嗅觉

**严重性**：未成年人

**** 因为：版本2018.4.0

通常，以/libs和/apps开头的路径不应被硬编码为路径，因为这些路径最常被存储为相对于Sling搜索路径的路径(默认情况下设置为/libs或应用程序)。使用绝对路径可能会引入细微的瑕疵，这些瑕疵只会在项目生命周期后出现。

#### 不兼容的代码 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 兼容代码 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```
