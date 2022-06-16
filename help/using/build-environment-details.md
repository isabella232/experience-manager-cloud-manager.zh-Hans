---
title: 了解生成环境
description: 可查看本页以了解相关环境
feature: Environments
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 9959f649e553d0ff6d41a70a468bec3e2e854d75
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 1%

---

# 了解生成环境 {#build-environment-details}

Cloud Manager使用专门的构建环境来构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* 已安装Apache Maven 3.6.0。
* 安装的Java版本包括OracleJDK 8u202、Azul Zulu 8u292、OracleJDK 11.0.2和Azul Zulu 11.0.11。
* 默认情况下， JAVA_HOME环境变量设置为 `/usr/lib/jvm/jdk1.8.0_202` 其中包含OracleJDK 8u202。 请参阅 [备用Maven执行JDK版本](#alternate-maven) 部分以了解更多详细信息。
* 安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphsmagick

* 其他包可能在生成时安装，如所述 [下面](#installing-additional-system-packages).
* 每栋建筑都是在原始环境下完成的；执行两次时，生成容器不会保留任何状态。
* Maven始终使用以下三个命令运行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven在系统级别使用settings.xml文件进行配置，该文件会自动包含公共Adobe **藏物** 使用名为 `adobe-public`.
请参阅 [Adobe公共Maven存储库](https://repo1.maven.org/) 以了解更多详细信息。

>[!NOTE]
>尽管Cloud Manager未定义 `jacoco-maven-plugin`，则使用的版本必须至少为 `0.7.5.201505241946`.


>[!NOTE]
>请参阅以下其他资源，了解如何使用Cloud Manager API:
> * [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [创建API集成](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## 使用特定Java版本 {#using-java-version}

默认情况下，项目由Cloud Manager构建过程使用Oracle8 JDK构建。 希望使用备用JDK的客户有两种选项：Maven工具链，并为整个Maven执行过程选择备用JDK版本。

### Maven工具链 {#maven-toolchains}

的 [Maven工具链插件](https://maven.apache.org/plugins/maven-toolchains-plugin/) 允许项目选择特定的JDK(或 *刀具链*)，以用于工具链感知型Maven插件的上下文。 此操作将在项目的 `pom.xml` 文件，方法是指定供应商和版本值。 中的示例部分 `pom.xml` 文件为：

```xml
        <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

这将导致所有具有工具链感知的Maven插件都使用OracleJDK版本11。

使用此方法时，Maven本身仍使用默认的JDK(Oracle8)和 `JAVA_HOME` 环境变量未更改。 因此，可通过诸如 [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 不起作用，因此不得使用此类插件。

当前可用的供应商/版本组合包括：

* oracle1.8
* oracle1.11
* oracle11
* sun 1.8
* sun 1.11
* 星期日11
* azul 1.8
* azul 1.11
* azul 8

### 备用Maven执行JDK版本 {#alternate-maven}

还可以选择Azul 8或Azul 11作为整个Maven执行的JDK。 与工具链选项不同，这会更改所有插件所使用的JDK，除非还设置了工具链配置，在这种情况下，仍然会将工具链配置应用于具有工具链感知功能的Maven插件。 因此，请使用 [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 都行。

为此，请创建一个名为 `.cloudmanager/java-version` 在管道使用的git存储库分支中。 此文件可以包含内容11或8。 任何其他值都将被忽略。 如果指定了11，则使用Azul 11，并将JAVA_HOME环境变量设置为 `/usr/lib/jvm/jdk-11.0.11`. 如果指定8，则使用Azul 8，并将JAVA_HOME环境变量设置为 `/usr/lib/jvm/jdk-8.0.292`.

## 环境变量 {#environment-variables}

### 标准环境变量 {#standard-environ-variables}

在某些情况下，客户会发现有必要根据有关项目或管道的信息来更改构建流程。

例如，如果正在通过gulp之类的工具完成构建时的JavaScript缩小，则在构建开发环境时可能希望使用不同的缩小级别，而不是构建舞台和生产环境。

为了支持此功能，Cloud Manager会将这些标准环境变量添加到每次执行的生成容器中。

| **变量名称** | **定义** |
|---|---|
| CM_BUILD | 始终设置为“true” |
| 分支 | 为执行配置的分支 |
| CM_PIPELINE_ID | 数值管道标识符 |
| CM_PIPELINE_NAME | 管道名称 |
| CM_PROGRAM_ID | 数字程序标识符 |
| CM_PROGRAM_NAME | 项目名称 |
| ANTRACTS_VERSION | 对于暂存或生产管道，由Cloud Manager生成的合成版本 |

### 管道变量 {#pipeline-variables}

在某些情况下，客户的构建过程可能取决于特定的配置变量，这些变量不适合放置在Git存储库中，或者需要在使用同一分支的管道执行之间进行更改。

Cloud Manager允许在每个管道基础上通过Cloud Manager API或Cloud Manager CLI配置这些变量。 变量可以存储为纯文本，也可以在静态时加密。 无论哪种情况，变量都会在生成环境中作为环境变量提供，随后可以在 `pom.xml` 文件或其他生成脚本。

要使用CLI设置变量，请运行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可列出当前变量：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

变量名称只能包含字母数字和下划线(_)字符。 按照惯例，名字应全部为大写。 每个管道限制为200个变量，在字符串类型变量中，每个名称必须少于100个字符，在secretString类型变量中，每个值必须少于2048个字符，在secretString类型变量中，每个值必须少于500个字符。

在 `Maven pom.xml` 文件中，使用类似于下面的语法将这些变量映射到Maven属性通常会很有帮助：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```


## 安装其他系统包 {#installing-additional-system-packages}

某些内部版本需要安装其他系统包才能完全正常运行。 例如，内部版本可能会调用Python或ruby脚本，因此需要安装适当的语言解释器。 这可以通过调用 [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) 调用APT。 此执行通常应包含在特定于Cloud Manager的Maven配置文件中。 例如，要安装python:

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

此相同技术可用于安装语言特定的软件包，即使用 `gem` 用于RubyGems或 `pip` 用于Python包。

>[!NOTE]
>以这种方式安装系统包确实可以 **not** 在用于运行Adobe Experience Manager的运行时环境中安装它。 如果您需要在AEM环境中安装系统包，请联系您的Adobe代表。
