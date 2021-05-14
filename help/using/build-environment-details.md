---
title: 了解构建环境
description: 可查看本页以了解有关环境
feature: 环境
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 0a5556729e64c9e8736d13b357db001dd57bc03a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 了解Build环境{#build-environment-details}

Cloud Manager使用专用构建环境构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* Apache Maven 3.6.0已安装。
* 安装的Java版本为Oracle JDK 8u202和11.0.2。
* 还安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * lippng
   * imagick
   * graphicsmagick

* 其他软件包可在构建时安装，如[下面所述。](#installing-additional-system-packages)
* 每栋建筑都建在原始环境上；构建容器不会在执行之间保留任何状态。
* Maven始终使用以下三个命令运行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven在系统级别上配置了settings.xml文件，该文件使用名为`adobe-public`的Adobe自动包括公用用户档案&#x200B;**Artifact**存储库。
有关详细信息，请参阅[Adobe公共主存储库](https://repo.adobe.com/)。

>[!NOTE]
>虽然Cloud Manager未定义`jacoco-maven-plugin`的特定版本，但使用的版本至少必须为`0.7.5.201505241946`。


>[!NOTE]
>请参阅以下其他资源，了解如何使用Cloud Manager API:
> * [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [创建API集成](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## 使用Java 11 {#using-java-11}

Cloud Manager现在支持使用Java 8和Java 11构建客户项目。 默认情况下，项目是使用Java 8构建的。 计划在其项目中使用Java 11的客户可以使用[Apache Maven Toolchains Plugin](https://maven.apache.org/plugins/maven-toolchains-plugin/)执行此操作。

为此，请在pom.xml文件中添加如下`<plugin>`条目：

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

>[!NOTE]
>支持的`vendor`值为`oracle`和`sun`，支持的`version`值为`1.8`、`1.11`和`11`。

>[!NOTE]
>Cloud Manager项目构建仍在使用Java 8调用Maven，因此，通过插件（如[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)）检查或强制工具链插件中配置的Java版本不起作用，因此不得使用此类插件。

## 环境变量{#environment-variables}

### 标准环境变量{#standard-environ-variables}

在某些情况下，客户发现有必要根据有关项目或管道的信息来改变构建流程。

例如，如果正在通过gulp等工具完成构建时JavaScript微型化，则在为开发环境构建时可能希望使用不同的微型化级别，而不是为舞台和生产构建。

为了支持此功能，Cloud Manager将这些标准环境变量添加到每次执行的构建容器中。

| **变量名** | **定义** |
|---|---|
| CM_BUILD | 始终设置为“true” |
| 分支 | 为执行配置的分支 |
| CM_PIPELINE_ID | 数字管线标识符 |
| CM_PIPELINE_NAME | 管线名称 |
| CM_项目_ID | 数字项目标识符 |
| CM_项目_NAME | 项目名称 |
| ARTIFACTS_VERSION | 对于舞台或生产管道，由Cloud Manager生成的合成版本 |

### 管道变量{#pipeline-variables}

在某些情况下，客户的构建过程可能取决于特定的配置变量，这些变量不适于放在Git存储库中，或需要在使用同一分支的管道执行之间有所不同。

Cloud Manager允许通过Cloud Manager API或Cloud Manager CLI按管道配置这些变量。 变量可以存储为纯文本或在静止时加密。 在任一情况下，生成环境内的变量都可用作环境变量，然后可以从`pom.xml`文件或其他生成脚本内引用该变量。

要使用CLI设置变量，请运行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可以列出当前变量：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

变量名称只能包含字母数字和下划线(_)字符。 根据惯例，这些名称应全部为大写。 每个管线限制为200个变量，每个名称必须小于100个字符，对于字符串类型变量，每个值必须小于2048个字符，对于secretString类型变量，每个值必须小于500个字符。

当在`Maven pom.xml`文件中使用时，通常可以使用类似以下语法将这些变量映射到Maven属性：

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


## 安装其他系统包{#installing-additional-system-packages}

某些构建需要安装额外的系统包才能完全运行。 例如，内部版本可能调用Python或ruby脚本，因此需要安装适当的语言解释器。 可通过调用[exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/)调用APT来完成此操作。 此执行通常应包含在特定于Cloud Manager的Maven用户档案中。 例如，要安装python:

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

此技术同样可用于安装语言特定的包，即使用`gem`（对于RubyGems）或`pip`（对于Python包）。

>[!NOTE]
>以这种方式安装系统包时，**不**&#x200B;会在用于运行Adobe Experience Manager的运行时环境中安装它。 如果您需要在AEM环境上安装系统包，请与Adobe代表联系。
