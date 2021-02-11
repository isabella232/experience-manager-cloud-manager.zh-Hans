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
source-git-commit: 7cfa7826f851cb55be72211f8e8a980451846f3b
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 4%

---


# 自定义代码质量规则 {#custom-code-quality-rules}

本页介绍由Cloud Manager根据AEM Engineering的最佳实践创建的自定义代码质量规则。

>[!NOTE]
>此处提供的代码示例仅供说明性用途。 请参阅[概念](https://docs.sonarqube.org/7.4/user-guide/concepts/)以了解SonarQube概念和质量规则。

## SonarQube规则{#sonarqube-rules}

以下部分重点介绍SonarQube规则：

### 不要使用可能危险的函数{#do-not-use-potentially-dangerous-functions}

**密钥**:CQRules:CWE-676

**类型**:漏洞

**严重性**:Major

**自**:2018.4.0版

Thread. ***stop()和********* Thread.interrupt()方法可能会产生难以重现的问题，并且在某些情况下会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不兼容代码{#non-compliant-code}

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

### 请勿使用外部可控的格式字符串{#do-not-use-format-strings-which-may-be-externally-controlled}

**密钥**:CQRules:CWE-134

**类型**:漏洞

**严重性**:Major

**自**:2018.4.0版

使用来自外部源（例如请求参数或用户生成的内容）的格式字符串可以使应用程序暴露于拒绝服务攻击。 在某些情况下，格式字符串可以在外部进行控制，但仅允许从可信源进行。

#### 不兼容代码{#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时{#http-requests-should-always-have-socket-and-connect-timeouts}

**密钥**:CQRules:ConnectionTimeoutMechanism

**类型**:错误

**严重性**:关键

**自**:2018.6.0版

在AEM应用程序内执行HTTP请求时，确保配置适当的超时以避免不必要的线程消耗至关重要。 很遗憾，Java的默认HTTP客户端(java.net.HttpUrlConnection)和常用的Apache HTTP组件客户端的默认行为都为从不超时，因此必须显式设置超时。 此外，作为最佳实践，这些超时不应超过60秒。

#### 不兼容代码{#non-compliant-code-2}

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

### 客户{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}不应实施或扩展使用@ProviderType添加注释的产品API

**密钥**:CQBP-84、CQBP-84-dependencies

**类型**:错误

**严重性**:关键

**自**:2018.7.0版

AEM API包含Java接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，接口com.day.cq.wcm. *api.Page* ，设计为仅由 ***AEM实现***。

当将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码，因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 ***码实现了*** 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

仅由AEM实现的接口（和类）用&#x200B;*org.osgi.annotation.versoning.ProviderType*&#x200B;进行注释（或在某些情况下，类似的旧注释&#x200B;*aQuete.bnd.annotation.ProviderType*）。 此规则标识通过自定义代码实现（或扩展类）此类接口的情况。

#### 不兼容代码{#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver对象应始终关闭{#resourceresolver-objects-should-always-be-closed}

**密钥**:CQRules:CQBP-72

**类型**:代码气味

**严重性**:Major

**自**:2018.4.0版

从ResourceResolverFactory获取的ResourceResolver对象使用系统资源。 尽管当ResourceResolver不再使用时，已经有可回收这些资源的度量，但通过调用close()方法显式关闭任何已打开的ResourceResolver对象会更有效。

一个比较常见的误解是使用现有JCR会话创建的ResourceResolver对象不应显式关闭，或者这样做将关闭基础JCR会话。 这种情况不存在——无论ResourceResolver如何打开，都应在不再使用时关闭它。 由于ResourceResolver实现了Closeable接口，因此也可以使用try-with-resources语法而不是显式调用close()。

#### 不兼容代码{#non-compliant-code-4}

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

### 不要使用Sling Servlet路径注册Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**密钥**:CQRules:CQBP-75

**类型**:代码气味

**严重性**:Major

**自**:2018.4.0版

如[Sling文档](http://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，不建议使用按路径绑定servlet。 路径绑定Servlet不能使用标准JCR访问控制，因此需要额外的安全严格性。 建议在存储库中创建节点并按资源类型注册servlet，而不是使用路径绑定servlet。

#### 不兼容代码{#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应记录或引发，但不应同时记录{#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密钥**:CQRules:CQBP-44—CatchAndEitherLogOrThrow

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

通常，一个例外应仅记录一次。 多次记录异常可能会造成混淆，因为不清楚异常发生了多少次。 导致这种情况的最常见模式是记录并引发捕获的异常。

#### 不兼容代码{#non-compliant-code-6}

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

### 避免在日志语句后面紧跟throw语句{#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密钥**:CQRules:CQBP-44—ConsentiveLogAndThrow

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

避免的另一种常见模式是记录消息，然后立即引发异常。 这通常表示异常消息将在日志文件中重复。

#### 不兼容代码{#non-compliant-code-7}

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

### 在处理GET或HEAD请求{#avoid-logging-at-info-when-handling-get-or-head-requests}时避免在INFO处记录

**密钥**:CQRules:CQBP-44 — LogInfoInGetOrHeadRequests

**类型**:代码气味

**严重性**:次要

通常，应使用INFO日志级别来划分重要操作，默认情况下，AEM配置为在INFO级别或更高级别进行日志记录。 GET和HEAD方法只能是只读操作，因此不构成重要行动。 响应GET或HEAD请求以INFO级别进行记录可能会产生明显的日志噪声，从而使在日志文件中识别有用信息变得更困难。 处理GET或HEAD请求时的日志记录应位于出错时的“警告”或“错误”级别，或者位于“调试”或“TRACE”级别（如果更深入的故障排除信息会有所帮助）。

>[!CAUTION]
>
>这不适用于每个请求的access.log类型日志记录。

#### 不兼容代码{#non-compliant-code-8}

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

### 不要将Exception.getMessage()用作日志记录语句{#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}的第一个参数

**密钥**:CQRules:CQBP-44 — ExceptionGetMessageIsFirstLogParam

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然上下文也可以通过使用堆栈跟踪来确定，但通常日志消息将更易于阅读和理解。 因此，在记录异常时，将异常消息用作日志消息是一种不好的做法——异常消息将包含出错的内容，而日志消息应用于告诉日志阅读器发生异常时应用程序正在做什么。 异常消息仍将记录；通过指定您自己的消息，日志将更易于理解。

#### 不兼容代码{#non-compliant-code-9}

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

### 登录捕获块应处于WARN或ERROR级别{#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密钥**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

正如名称所暗示的，Java例外应始终用于&#x200B;*异常*&#x200B;环境。 因此，当捕获到异常时，务必确保日志消息记录在适当的级别- WARN或ERROR。 这可确保这些消息在日志中正确显示。

#### 不兼容代码{#non-compliant-code-10}

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

**密钥**:CQRules:CQBP-44—ExceptionPrintStackTrace

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

如前所述，了解日志消息时，上下文至关重要。 使用Exception.printStackTrace()仅使&#x200B;****&#x200B;堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在多线程应用程序(如AEM)中，如果使用此方法并行打印多个异常，则其堆栈轨迹可能重叠，从而产生严重混淆。 例外应仅通过记录框架记录。

#### 不兼容代码{#non-compliant-code-11}

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

**密钥**:CQRules:CQBP-44 — LogLevelConsolePrinters

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

应始终通过日志记录框架(SLF4J)登录AEM。 直接输出到标准输出或标准错误流会丢失日志记录框架提供的结构和上下文信息，在某些情况下，可能会导致性能问题。

#### 不兼容代码{#non-compliant-code-12}

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

**密钥**:CQRules:CQBP-71

**类型**:代码气味

**严重性**:次要

**自**:2018.4.0版

通常，使用/libs和/apps开始的路径不应硬编码为它们引用的路径，最常存储为相对于Sling搜索路径的路径（默认情况下设置为/libs,/apps）。 使用绝对路径可能会引入细微缺陷，这些缺陷只会在项目生命周期的后期出现。

#### 不兼容代码{#non-compliant-code-13}

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

### 不应使用Sling调度程序{#sonarqube-sling-scheduler}

**密钥**:CQRules:AMSCORE-554

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

Sling调度程序不得用于需要有保证执行的任务。 Sling Scheduled Jobs可确保执行，并更适合群集和非群集环境。

请参阅[Apache Sling Eventing and Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)，进一步了解如何在群集环境中处理Sling Job。

### AEM不应使用已弃用的API {#sonarqube-aem-deprecated}

**密钥**:AMSCORE-553

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

AEM API表面经常处于修订状态，以标识不建议使用的API，因此被视为已弃用。

在很多情况下，使用标准Java *@Deprecated*&#x200B;注释和（如`squid:CallToDeprecatedMethod`所标识）不再使用这些API。

但是，有时AEM上下文中已弃用API，但其他上下文中可能不弃用。 此规则标识此第二类。

## OakPAL内容规则{#oakpal-rules}

请在云管理器执行的OakPAL检查下找到。

>[!NOTE]
>
>OakPAL是由AEM合作伙伴(2019年AEM Rockstar北美公司的获胜者)开发的框架，该框架使用独立的Oak存储库验证内容包。

### 客户包不应在/libs {#oakpal-customer-package}下创建或修改节点

**密钥**:UnbardedPaths

**类型**:错误

**严重性**:阻止程序

**自**:版本2019.6.0

AEM内容存储库中的/libs内容树应被客户视为只读，这是一种长期的最佳实践。 修改&#x200B;*/libs*&#x200B;下的节点和属性会给主要和次要更新带来重大风险。 对&#x200B;*/libs*&#x200B;的修改只应由Adobe通过官方渠道进行。

### 包不应包含重复OSGi配置{#oakpal-package-osgi}

**密钥**:DuplicateOsgiConfigurations

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

复杂项目上出现的常见问题是同一OSGi组件多次配置。 这就产生了关于哪个配置可操作的模糊。 此规则是“运行模式识别”的，因为它只识别在同一运行模式（或运行模式组合）中多次配置同一组件的问题。

#### 不兼容代码{#non-compliant-code-osgi}

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

**密钥**:ConfigAndInstallShouldOnlyContainOsgiNodes

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

出于安全原因，包含&#x200B;*/config/和/install/*&#x200B;的路径只能由AEM中的管理用户读取，并且只能用于OSGi配置和OSGi捆绑包。 将其他类型的内容放在包含这些区段的路径下会导致应用程序行为在管理用户和非管理用户之间无意中发生变化。

一个常见问题是在组件对话框中使用名为`config`的节点，或者在指定用于内联编辑的富文本编辑器配置时。 要解决此问题，违规节点应重命名为兼容名称。 对于富文本编辑器配置，请使用`cq:inplaceEditing`节点上的`configPath`属性指定新位置。

#### 不兼容代码{#non-compliant-code-config-install}

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

### 包不应重叠{#oakpal-no-overlap}

**密钥**:包重叠

**类型**:错误

**严重性**:Major

**自**:版本2019.6.0

与&#x200B;*包不应包含重复OSGi配置*&#x200B;类似，这是复杂项目中的常见问题，在这些复杂项目中，同一节点路径由多个单独的内容包写入。 使用内容包依赖关系可以确保结果一致，但最好避免完全重叠。

### 默认创作模式不应为经典UI {#oakpal-default-authoring}

**密钥**:ClassicUIAuthoringMode

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

OSGi配置`com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl`定义AEM中的默认创作模式。 由于自AEM 6.4起已弃用经典UI，因此现在将默认创作模式配置为经典UI时，会引发问题。

### 具有对话框的组件应具有触屏UI对话框{#oakpal-components-dialogs}

**密钥**:ComponentWithOnlyClassicUIDialog

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

AEM具有经典UI对话框的组件应始终具有相应的触屏UI对话框，以提供最佳创作体验，并与不支持经典UI的Cloud Service部署模型兼容。 此规则验证以下情况：

* 具有经典UI对话框（即对话框子节点）的组件必须具有相应的触屏UI对话框（即`cq:dialog`子节点）。
* 具有经典UI设计对话框（即design_dialog节点）的组件必须具有相应的触屏UI设计对话框（即`cq:design_dialog`子节点）。
* 具有经典UI对话框和经典UI设计对话框的组件必须具有相应的触屏UI对话框和相应的触屏UI设计对话框。

AEM现代化工具文档提供了如何将组件从经典UI转换为触屏UI的文档和工具。 有关更多详细信息，请参阅[AEM Medurance Tools](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html)。

### 包不应混合可变内容和不可变内容{#oakpal-packages-immutable}

**密钥**:ImmutableMutableMixedPackage

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

为了与Cloud Service部署模型兼容，单个内容包必须包含存储库不可变区域的内容（即`/apps and /libs, although /libs`不应由客户代码修改并将导致单独的违规）或可变区域（即其他所有内容），但不能同时包含这两者。 例如，同时包含`/apps/myco/components/text and /etc/clientlibs/myco`的包与Cloud Service不兼容，将导致报告问题。

有关详细信息，请参阅[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)。

### 不应使用反向复制代理{#oakpal-reverse-replication}

**密钥**:反向复制

**类型**:代码气味/Cloud Service兼容性

**严重性**:次要

**自**:版本2020.5.0

反向复制支持在Cloud Service部署中不可用，如[发行说明中所述：删除复制代理](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents)。

使用反向复制的客户应与Adobe联系以获得其他解决方案。

### OakPAL —— 启用代理的客户端库中包含的资源应位于名为resources {#oakpal-resources-proxy}的文件夹中

**密钥**:ClientlibProxyResource

**类型**:错误

**严重性**:次要

**自**:版本2021.2.0

AEM客户端库可能包含静态资源，如图像和字体。 如[使用预处理器](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=en#using-preprocessors)中所述，在使用代理客户端库时，这些静态资源必须包含在名为resources的子文件夹中，才能在发布实例上有效地引用。

#### 不兼容代码{#non-compliant-proxy-enabled}

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

### OakPAL -Cloud Service不兼容工作流进程{#oakpal-usage-cloud-service}的使用

**密钥**:CloudServiceIncompatibleWorkflowProcess

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

随着AEMCloud Service上资产处理转向资产微服务，内部部署和AMS版本AEM中使用的多个工作流进程变得不受支持或不必要。 位于[aem-cloud-migration](https://github.com/adobe/aem-cloud-migration)的迁移工具可用于在AEMCloud Service迁移期间更新工作流模型。

### OakPAL —— 建议使用静态模板，而使用可编辑模板{#oakpal-static-template}

**密钥**:StaticTemplateUsage

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

尽管静态模板在AEM项目中的使用一直很常见，但强烈建议使用可编辑模板，因为它们提供了最灵活的功能，并支持静态模板中不存在的其他功能。 有关详细信息，请参阅[页面模板- Editable](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html?lang=en)。 使用[AEM Moderization Tools](https://opensource.adobe.com/aem-modernize-tools/)可以自动地从静态模板迁移到可编辑模板。

### OakPAL —— 不建议使用旧版基础组件{#oakpal-usage-legacy}

**密钥**:LegacyFoundationComponentUsage

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

旧版基础组件（即`/libs/foundation`下的组件）已弃用于多个AEM发行版，而使用WCM核心组件。 不建议将旧版基础组件用作自定义组件的基础（无论是通过叠加还是继承），并应将其转换为相应的核心组件。 [AEM现代化工具](https://opensource.adobe.com/aem-modernize-tools/)可促进此转换。

### OakPAL —— 只应使用支持的Runmode名称和排序{#oakpal-supported-runmodes}

**密钥**:支持的运行模式

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service对运行模式名称实施严格的命名策略，并对这些运行模式实施严格的排序。 在[运行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)上可以找到受支持运行模式的列表，任何偏离该模式的情况都将被识别为问题。

### OakPAL —— 自定义搜索索引定义节点必须是/oak:index {#oakpal-custom-search}的直接子节点

**密钥**:OakIndexLocation

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）是`/oak:index`的直接子节点。 必须移动其他位置的索引，以与AEMCloud Service兼容。 有关搜索索引的详细信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL —— 自定义搜索索引定义节点必须具有2 {#oakpal-custom-search-compatVersion}的compatVersion

**密钥**:IndexCompatVersion

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）必须将compatVersion属性设置为2。 AEMCloud Service不支持任何其他值。 有关搜索索引的详细信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en)。

### OakPAL —— 自定义搜索索引定义节点的子节点的类型必须为nt:unstructured {#oakpal-descendent-nodes}

**密钥**:IndexDescendantNodeType

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

当自定义搜索索引定义节点具有无序的子节点时，可能会发生难以排除的问题。 为避免出现这些情况，建议`oak:QueryIndexDefinition`节点的所有子节点的类型均为nt:unstructured。

### OakPAL —— 自定义搜索索引定义节点必须包含一个名为indexRules的子节点，该子节点具有子节点{#oakpal-custom-search-index}

**密钥**:IndexRulesNode

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

正确定义的自定义搜索索引定义节点必须包含一个名为indexRules的子节点，而该子节点必须至少具有一个子节点。 有关详细信息，请参阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### OakPAL —— 自定义搜索索引定义节点必须遵循命名约定{#oakpal-custom-search-definitions}

**密钥**:IndexName

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即，类型为`oak:QueryIndexDefinition`的节点）必须按照[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)中描述的特定模式进行命名。

### OakPAL —— 自定义搜索索引定义节点必须使用索引类型lucene {#oakpal-index-type-lucene}

**密钥**:IndexType

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service要求自定义搜索索引定义（即oak:QueryIndexDefinition类型的节点）具有类型属性，并将值设置为&#x200B;**lucene**。 使用旧索引类型进行索引编制必须在迁移到AEMCloud Service之前更新。 有关详细信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL —— 自定义搜索索引定义节点不能包含名为seed {#oakpal-property-name-seed}的属性

**密钥**:IndexSeedProperty

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service禁止自定义搜索索引定义（即`oak:QueryIndexDefinition`类型的节点）包含名为seed的属性。 使用此属性进行索引编制必须在迁移到AEMCloud Service之前更新。 有关详细信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。

### OakPAL —— 自定义搜索索引定义节点不能包含名为reindex {#oakpal-reindex-property}的属性

**密钥**:IndexReindexProperty

**类型**:代码气味

**严重性**:次要

**自**:版本2021.2.0

AEMCloud Service禁止自定义搜索索引定义（即`oak:QueryIndexDefinition`类型的节点）包含名为reindex的属性。 使用此属性进行索引编制必须在迁移到AEMCloud Service之前更新。 有关详细信息，请参阅[内容搜索和索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use)。




