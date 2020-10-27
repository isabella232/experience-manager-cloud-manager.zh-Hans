---
title: 自定义代码质量规则
seo-title: 自定义代码质量规则
description: 可查看本页以了解由云管理器执行的自定义代码质量规则。
seo-description: 可查看本页以了解由Adobe Experience Manager云管理器执行的自定义代码质量规则。
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
translation-type: tm+mt
source-git-commit: 71a760997ec2a0873a7f39d206086a8b4fd6854e
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 6%

---


# 自定义代码质量规则 {#custom-code-quality-rules}

本页介绍由Cloud Manager根据AEM Engineering的最佳实践创建的自定义代码质量规则。

>[!NOTE]
>此处提供的代码示例仅供说明性用途。 请参 [阅概念](https://docs.sonarqube.org/7.4/user-guide/concepts/) ，了解SonarQube概念和质量规则。

## SonarQube Rules {#sonarqube-rules}

以下部分重点介绍SonarQube规则：

### 不要使用潜在的危险功能 {#do-not-use-potentially-dangerous-functions}

**密钥**:CQRules:CWE-676

**类型**:漏洞

**严重性**:Major

**自**:2018.4.0版

Thread. ***stop()和********* Thread.interrupt()方法可能会产生难以重现的问题，并且在某些情况下会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不符合规范的代码 {#non-compliant-code}

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

#### 符合规范的代码 {#compliant-code}

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

### 请勿使用可能由外部控制的格式字符串 {#do-not-use-format-strings-which-may-be-externally-controlled}

**密钥**:CQRules:CWE-134

**类型**:漏洞

**严重性**:Major

**自**:2018.4.0版

使用来自外部源（例如请求参数或用户生成的内容）的格式字符串可以使应用程序暴露于拒绝服务攻击。 在某些情况下，格式字符串可以在外部进行控制，但仅允许从可信源进行。

#### 不符合规范的代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

**密钥**:CQRules:ConnectionTimeoutMechanism

**类型**:错误

**严重性**:关键

**自**:2018.6.0版

在AEM应用程序内执行HTTP请求时，确保配置适当的超时以避免不必要的线程消耗至关重要。 很遗憾，Java的默认HTTP客户端(java.net.HttpUrlConnection)和常用的Apache HTTP组件客户端的默认行为都为从不超时，因此必须显式设置超时。 此外，作为最佳实践，这些超时不应超过60秒。

#### 不符合规范的代码 {#non-compliant-code-2}

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

#### 符合规范的代码 {#compliant-code-1}

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

### 客户不应实施或扩展使用@ProviderType添加注释的产品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**密钥**:CQBP-84、CQBP-84-dependencies

**类型**:错误

**严重性**:关键

**自**:2018.7.0版

AEM API包含Java接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，接口com.day.cq.wcm. *api.Page* ，设计为仅由 ***AEM实现***。

当将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码，因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 ***码实现了*** 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

仅由AEM实现的接口（和类）用org.osgi.annotation. *versoning.ProviderType* (或在某些情况下，类似的旧 *注释aQute.bnd.annotation.ProviderType*)进行注释。 此规则标识通过自定义代码实现（或扩展类）此类接口的情况。

#### 不符合规范的代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver对象应始终关闭 {#resourceresolver-objects-should-always-be-closed}

**密钥**:CQRules:CQBP-72

**类型**:代码气味

**严重性**:Major

**自**:2018.4.0版

从ResourceResolverFactory获取的ResourceResolver对象使用系统资源。 尽管当ResourceResolver不再使用时，已经有可回收这些资源的度量，但通过调用close()方法显式关闭任何已打开的ResourceResolver对象会更有效。

一个比较常见的误解是使用现有JCR会话创建的ResourceResolver对象不应显式关闭，或者这样做将关闭基础JCR会话。 这种情况不存在——无论ResourceResolver如何打开，都应在不再使用时关闭它。 由于ResourceResolver实现了Closeable接口，因此也可以使用try-with-resources语法而不是显式调用close()。

#### 不符合规范的代码 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 符合规范的代码 {#compliant-code-2}

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

### 不使用Sling Servlet路径注册Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**密钥**:CQRules:CQBP-75

**类型**:代码气味

**严重性**:Major

**自**:2018.4.0版

如Sling文档中所 [述](http://sling.apache.org/documentation/the-sling-engine/servlets.html)，不建议使用按路径绑定的Servlet。 路径绑定Servlet不能使用标准JCR访问控制，因此需要额外的安全严格性。 建议在存储库中创建节点并按资源类型注册servlet，而不是使用路径绑定servlet。

#### 不符合规范的代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应记录或引发，但不应同时记录或引发 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密钥**:CQRules:CQBP-44—CatchAndEitherLogOrThrow

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

通常，一个例外应仅记录一次。 多次记录异常可能会造成混淆，因为不清楚异常发生了多少次。 导致这种情况的最常见模式是记录并引发捕获的异常。

#### 不符合规范的代码 {#non-compliant-code-6}

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

#### 符合规范的代码 {#compliant-code-3}

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

### 避免在日志语句后面立即添加throw语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密钥**:CQRules:CQBP-44—ConsentiveLogAndThrow

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

避免的另一种常见模式是记录消息，然后立即引发异常。 这通常表示异常消息将在日志文件中重复。

#### 不符合规范的代码 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 符合规范的代码 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在处理GET或HEAD请求时避免在信息处记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

**密钥**:CQRules:CQBP-44 — LogInfoInGetOrHeadRequests

**类型**:代码气味

**严重性**:次要

通常，应使用INFO日志级别来划分重要操作，默认情况下，AEM配置为在INFO级别或更高级别进行日志记录。 GET和HEAD方法只能是只读操作，因此不构成重要行动。 响应GET或HEAD请求以INFO级别进行记录可能会产生明显的日志噪声，从而使在日志文件中识别有用信息变得更困难。 处理GET或HEAD请求时的日志记录应位于出错时的“警告”或“错误”级别，或者位于“调试”或“TRACE”级别（如果更深入的故障排除信息会有所帮助）。

>[!CAUTION]
>
>这不适用于每个请求的access.log类型日志记录。

#### 不符合规范的代码 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 符合规范的代码 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 不要将Exception.getMessage()用作日志记录语句的第一个参数 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**密钥**:CQRules:CQBP-44 — ExceptionGetMessageIsFirstLogParam

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然上下文也可以通过使用堆栈跟踪来确定，但通常日志消息将更易于阅读和理解。 因此，在记录异常时，将异常消息用作日志消息是一种不好的做法——异常消息将包含出错的内容，而日志消息应用于告诉日志阅读器发生异常时应用程序正在做什么。 异常消息仍将记录；通过指定您自己的消息，日志将更易于理解。

#### 不符合规范的代码 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 符合规范的代码 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登录捕获块应处于WARN或ERROR级别 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密钥**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

正如名称所暗示的，Java例外应始终在特殊情况下 *使用* 。 因此，当捕获到异常时，务必确保日志消息记录在适当的级别- WARN或ERROR。 这可确保这些消息在日志中正确显示。

#### 不符合规范的代码 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 符合规范的代码 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不将堆栈跟踪打印到控制台 {#do-not-print-stack-traces-to-the-console}

**密钥**:CQRules:CQBP-44—ExceptionPrintStackTrace

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

如前所述，了解日志消息时，上下文至关重要。 使用Exception.printStackTrace()只 **导致** 堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在多线程应用程序(如AEM)中，如果使用此方法并行打印多个异常，则其堆栈轨迹可能重叠，从而产生严重混淆。 例外应仅通过记录框架记录。

#### 不符合规范的代码 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 符合规范的代码 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不输出到“标准输出”或“标准错误” {#do-not-output-to-standard-output-or-standard-error}

**密钥**:CQRules:CQBP-44 — LogLevelConsolePrinters

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

应始终通过日志记录框架(SLF4J)登录AEM。 直接输出到标准输出或标准错误流会丢失日志记录框架提供的结构和上下文信息，在某些情况下，可能会导致性能问题。

#### 不符合规范的代码 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 符合规范的代码 {#compliant-code-9}

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

**密钥**:CQRules:CQBP-71

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

通常，使用/libs和/apps开始的路径不应硬编码为它们引用的路径，最常存储为相对于Sling搜索路径的路径（默认情况下设置为/libs,/apps）。 使用绝对路径可能会引入细微缺陷，这些缺陷只会在项目生命周期的后期出现。

#### 不符合规范的代码 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 符合规范的代码 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不应使用Sling调度程序 {#sonarqube-sling-scheduler}

**密钥**:CQRules:AMSCORE-554

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

Sling调度程序不得用于需要有保证执行的任务。 Sling Scheduled Jobs可确保执行，并更适合群集和非群集环境。

请参阅 [Apache Sling Eventing和作业处理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) ，进一步了解如何在群集环境中处理Sling Job。

### AEM不应使用已弃用的API {#sonarqube-aem-deprecated}

**密钥**:AMSCORE-553

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

AEM API表面经常处于修订状态，以标识不建议使用的API，因此被视为已弃用。

在很多情况下，这些API使用标准Java@ *Deprecated* annotation弃用，如由标识 `squid:CallToDeprecatedMethod`。

但是，有时AEM上下文中已弃用API，但其他上下文中可能不弃用。 此规则标识此第二类。

## OakPAL内容规则 {#oakpal-rules}

请在云管理器执行的OakPAL检查下找到。

>[!NOTE]
>
>OakPAL是由AEM合作伙伴(2019年AEM Rockstar北美公司的获胜者)开发的框架，该框架使用独立的Oak存储库验证内容包。

### 客户包不应在/libs下创建或修改节点 {#oakpal-customer-package}

**密钥**:UnbardedPaths

**类型**:错误

**严重性**:阻止程序

**自**:版本2019.6.0

AEM内容存储库中的/libs内容树应被客户视为只读，这是一种长期的最佳实践。 修改/libs下的节点 *和属性* ，会给主要和次要更新带来重大风险。 修改/ *Adobe* ，只应通过官方渠道进行。

### 包不应包含重复OSGi配置 {#oakpal-package-osgi}

**密钥**:DuplicateOsgiConfigurations

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

复杂项目上出现的常见问题是同一OSGi组件多次配置。 这就产生了关于哪个配置可操作的模糊。 此规则是“运行模式识别”的，因为它只识别在同一运行模式（或运行模式组合）中多次配置同一组件的问题。

#### 不符合规范的代码 {#non-compliant-code-osgi}

```
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 符合规范的代码 {#compliant-code-osgi}

```
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安装文件夹应仅包含OSGi节点 {#oakpal-config-install}

**密钥**:ConfigAndInstallShouldOnlyContainOsgiNodes

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

出于安全原因，包含 */config/和/install/* /install/的路径只能由AEM中的管理用户读取，并且只能用于OSGi配置和OSGi捆绑包。 将其他类型的内容放在包含这些区段的路径下会导致应用程序行为在管理用户和非管理用户之间无意中发生变化。

一个常见问题是使用组件对话框中 `config` 命名的节点，或者在指定用于内联编辑的富文本编辑器配置时。 要解决此问题，违规节点应重命名为兼容名称。 对于富文本编辑器配置，请 `configPath` 使用节点上 `cq:inplaceEditing` 的属性指定新位置。

#### 不符合规范的代码 {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 符合规范的代码 {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 包不应重叠 {#oakpal-no-overlap}

**密钥**:包重叠

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

与“包不 *应包含重复OSGi配置* ”类似，这是复杂项目中的常见问题，在这些复杂项目中，同一个节点路径由多个单独的内容包写入。 使用内容包依赖关系可以确保结果一致，但最好避免完全重叠。

### 默认创作模式不应为经典UI {#oakpal-default-authoring}

**密钥**:ClassicUIAuthoringMode

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

OSGi配置定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 义AEM中的默认创作模式。 由于自AEM 6.4起已弃用经典UI，因此现在将默认创作模式配置为经典UI时，会引发问题。

### 具有对话框的组件应具有触屏UI对话框 {#oakpal-components-dialogs}

**密钥**:ComponentWithOnlyClassicUIDialog

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

AEM具有经典UI对话框的组件应始终具有相应的触屏UI对话框，以提供最佳创作体验，并与不支持经典UI的Cloud Service部署模型兼容。 此规则验证以下情况：

* 具有经典UI对话框（即对话框子节点）的组件必须具有相应的触屏UI对话框(即子 `cq:dialog` 节点)。
* 具有经典UI设计对话框（即design_dialog节点）的组件必须具有相应的触屏UI设计对话框(即子 `cq:design_dialog` 节点)。
* 具有经典UI对话框和经典UI设计对话框的组件必须具有相应的触屏UI对话框和相应的触屏UI设计对话框。

AEM现代化工具文档提供了如何将组件从经典UI转换为触屏UI的文档和工具。 有关更 [多详细信息，请参](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) 阅AEM Medurance Tools。

### 包不应混合可变和不可变内容 {#oakpal-packages-immutable}

**密钥**:ImmutableMutableMixedPackage

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

为了与Cloud Service部署模型兼容，单个内容包必须包含存储库不可变区域的内容（即，不应由客户代码修改并将导致单独的违规）或可变区域（即，其他所有内容），但不能同时包含这两者。 `/apps and /libs, although /libs` 例如，包中同时包含这两 `/apps/myco/components/text and /etc/clientlibs/myco` 者的Cloud Service与不兼容，并会导致报告问题。

Refer to [AEM Project Structure](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) for more details.

### 不应使用反向复制代理 {#oakpal-reverse-replication}

**密钥**:反向复制

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

Cloud Service部署中不支持反向复制，如发行说明 [所述：删除复制代理](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents)。

使用反向复制的客户应与Adobe联系以获得其他解决方案。





