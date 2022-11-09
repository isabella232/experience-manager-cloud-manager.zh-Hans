---
title: 设置项目
description: 了解如何设置项目，以便使用 Cloud Manager 管理和部署该项目。
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---


# 项目设置 {#setting-up-your-project}

了解如何设置项目，以便使用 Cloud Manager 管理和部署该项目。

## 修改现有项目 {#modifying-project-setup-details}

现有 AEM 项目需要遵守一些基本规则才能使用 Cloud Manager 成功地构建和部署。

* 必须使用 Apache Maven 构建项目。
* Git 存储库的根目录中必须有一个 `pom.xml` 文件。
   * 此 `pom.xml` 文件可以根据需要引用尽可能多的子模块（这些子模块又可能包含其他子模块）。
   * 可以将引用添加到您在其他 Maven 工件存储库中拥有的 `pom.xml` 文件中。
   * 配置后，支持访问[受密码保护的构件存储库](#password-protected-maven-repositories)。但是，不支持访问受网络保护的工件存储库。
* 通过扫描包含在名为 `target` 的目录中的内容包 .zip 文件来发现可部署的内容包。
   * 任意数量的子模块都能生成内容包。
* 通过扫描包含了名为 `conf` 和 `conf.d` 的 `target` 子目录的 `zip` 文件来发现可部署的 Dispatcher 工件。
* 如果有多个内容包，则无法保证包部署顺序。
* 如果需要特定顺序，可以使用内容包依赖关系来定义该顺序。
* 可以从部署中[跳过](#skipping-content-packages)包。

## 在 Cloud Manager 中激活 Maven 配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些限定情况下，在 Cloud Manager 中运行而不是在开发人员工作站上运行时，您可能需要略微更改构建过程。在这些情况下，可使用 [Maven 配置文件](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)定义构建在不同环境（包括 Cloud Manager）中应有哪些不同之处。

应通过查找 `CM_BUILD` [环境变量](/help/getting-started/build-environment.md#environment-variables)，在 Cloud Manager 构建环境中激活 Maven 配置文件。相反，应在确认缺少此变量后激活仅在 Cloud Manager 构建环境之外使用的配置文件。

例如，如果您希望仅在 Cloud Manager 中运行构建时输出一条简单消息，则可以这样做：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>要在开发人员工作站上测试此配置文件，您可以在命令行上（带 `-PcmBuild`）或集成开发环境 (IDE) 中启用它。

此外，如果您希望仅在 Cloud Manager 外部运行构建时输出一条简单消息，则可以这样做：

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## 受密码保护的 Maven 存储库支持 {#password-protected-maven-repositories}

应非常谨慎地使用来自受密码保护的 Maven 存储库的工件，因为通过此机制部署的代码不会通过 Cloud Manager 质量审核中实施的所有质量规则运行。此外，还建议将 Java 源以及整个项目源代码和二进制文件一起部署。

>[!TIP]
>
>受密码保护的 Maven 存储库中的工件应仅在极少数情况下用于未与 AEM 绑定的代码。

要使用 Cloud Manager 中受密码保护的 Maven 存储库，请将密码（以及（可选）用户名）指定为机密的[管道变量](/help/getting-started/build-environment.md#pipeline-variables)，然后在 Git 存储库中的名为 `.cloudmanager/maven/settings.xml` 的文件中引用此变量。该文件遵循 [Maven 设置文件](https://maven.apache.org/settings.html)架构。

在 Cloud Manager 构建过程开始时，该文件中的 `<servers>` 元素将并入 Cloud Manager 提供的默认 `settings.xml` 文件中。以 `adobe` 和 `cloud-manager` 开头的服务器 ID 被视为保留项，不应由自定义服务器使用。Cloud Manager 绝不会对不带上述某个前缀的服务器 ID 或默认 ID `central` 进行镜像。

有了此文件，将从 `pom.xml` 文件中的 `<repository>` 和/或 `<pluginRepository>` 元素中引用服务器 ID。通常，`<repository>` 和/或 `<pluginRepository>` 元素将包含在 [Cloud Manager 特定的配置文件](#activating-maven-profiles-in-cloud-manager)中，但这并不是完全必要的。

例如，假设存储库位于 `https://repository.myco.com/maven2`，Cloud Manager 应使用的用户名为 `cloudmanager`，密码为 `secretword`。

首先，在管道上将密码设置为密钥：

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword
```

然后，从 `.cloudmanager/maven/settings.xml` 文件中引用它：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

最后，引用 `pom.xml` 文件中的服务器 ID：

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

### 部署源 {#deploying-sources}

好的做法是将 Java 源与二进制文件一起部署到 Maven 存储库。

在项目中配置 `maven-source-plugin`：

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### 部署项目源 {#deploying-project-sources}

好的做法是将整个项目源与二进制文件一起部署到 Maven 存储库。这将允许重新构建精确的工件。

在项目中配置 `maven-assembly-plugin`：

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## 跳过内容包 {#skipping-content-packages}

在 Cloud Manager 中，构建可以生成任意数量的内容包。出于各种原因，可能需要生成内容包但不部署它。这在构建仅用于测试的内容包或将由构建过程中的另一个步骤重新打包的内容包（即作为另一个包的子包）时可能会很有用。

为了适应这些场景，Cloud Manager 将在构建的内容包的属性中查找名为 `cloudManagerTarget` 的属性。如果此属性设置为 `none`，则将跳过并且不部署包。设置此属性的机制取决于构建生成内容包的方式。例如，使用 `filevault-maven-plugin` 可以配置插件，如下所示：

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

使用 `content-package-maven-plugin` 可以执行类似操作：

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## 生成工件重用 {#build-artifact-reuse}

在许多情况下，会将同一代码部署到多个 AEM 环境中。如果可能，当 Cloud Manager 检测到在多个全栈管道执行中使用了相同的 git 承诺时，它可避免重建代码库。

开始执行时，将提取分支管道的当前 HEAD 承诺。 承诺哈希在 UI 中可见，也可通过 API 查看它。 在构建步骤成功完成时，生成的工件将基于该承诺哈希进行存储，并且可在后续管道执行中重用。

如果包在同一个项目中，则将跨管道重用包。 在查找可重用的包时，AEM 会忽略分支并跨分支重用构件。

在进行重用时，构建和代码质量步骤将有效替换为原始执行所产生的结果。 构建步骤的日志文件将列出构件和最初用于构建构件的执行信息。

以下是此类日志输出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

代码质量步骤的日志将包含类似信息。

### 示例 {#example-reuse}

#### 示例 1 {#example-1}

假定您的项目有两个开发管道：

* 管道 1，位于分支 `foo` 上
* 管道 2，位于分支 `bar` 上

两个分支具有同一承诺 ID。

1. 首先运行管道 1 将正常构建包。
1. 然后，运行管道 2 将重用管道 1 所创建的包。

#### 示例 2 {#example-2}

假定您的项目有两个分支：

* 分支 `foo`
* 分支 `bar`

两个分支具有同一承诺 ID。

1. 开发管道构建和执行 `foo`。
1. 随后，生产管道构建和执行 `bar`。

在此情况下，来自 `foo` 的工件将重用于生产管道，因为已识别同一承诺哈希。

### 选择退出 {#opting-out}

如果需要，可以通过将管道变量 `CM_DISABLE_BUILD_REUSE` 设置为 `true` 来禁止再次使用特定管道。如果设置了此变量，则仍将提取承诺哈希，并且将存储生成的工件以供以后使用，但不会再次使用任何之前存储的工件。为了理解此行为，请考虑以下场景。

1. 创建一个新的管道。
1. 执行此管道（执行 #1），当前 HEAD 承诺为 `becdddb`。 执行成功，并且将存储生成的构件。
1. 设置 `CM_DISABLE_BUILD_REUSE` 变量。
1. 重新执行管道而不更改代码。 尽管存在与 `becdddb` 关联的已存储构件，但由于有 `CM_DISABLE_BUILD_REUSE` 变量而不会重用这些构件。
1. 更改代码并执行管道。 HEAD 承诺现在为 `f6ac5e6`。 执行成功，并且将存储生成的构件。
1. 已删除 `CM_DISABLE_BUILD_REUSE` 变量。
1. 重新执行管道而不更改代码。 由于存在与 `f6ac5e6` 关联的已存储构件，因此将再次使用这些构件。

### 注意事项 {#caveats}

* 无论承诺哈希是否相同，生成工件都不会在不同的项目中再次使用。
* 即使分支和/或管道不同，生成工件也将在同一项目中重用。
* [Maven 版本处理](/help/managing-code/maven-project-version.md)仅在生产管道中替换项目版本。因此，如果在开发部署执行和生产管道执行中使用同一承诺，并且首先执行开发部署管道，则版本将部署到暂存和生产环境中且不会进行更改。不过，在此情况下仍会创建标记。
* 如果无法检索已存储的构件，则将执行构建步骤，就像未存储任何构件一样。
* 当 Cloud Manager 决定重用之前创建的生成工件时，不会考虑 `CM_DISABLE_BUILD_REUSE` 之外的管道变量。

## 根据最佳实践开发代码 {#develop-your-code-based-on-best-practices}

Adobe 工程和咨询团队开发了[一组面向 AEM 开发人员的全面的最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/developing/bestpractices/best-practices.html)。
