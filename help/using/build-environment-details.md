---
title: 了解构建环境
description: 可查看本页以了解有关环境
translation-type: tm+mt
source-git-commit: 57a99792e151bd5fe69c8372b6a9d3b100036a51
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# 了解构建环境 {#build-environment-details}

Cloud Manager使用专用构建环境构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* Apache Maven 3.6.0已安装。
* 安装的Java版本为Oracle JDK 8u202和11.0.2。
* 还安装了一些其他系统包，这是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphicsmagick

* 其他软件包可以在构建时安装，如 [下所述](#installing-additional-system-packages)。
* 每栋建筑都建在原始环境上；构建容器不会在执行之间保持任何状态。
* Maven始终使用以下三个命令运行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven在系统级别上配置了settings.xml文件，该文件自动包括公共Adobe **项库** 。 (有关更多详 [细信息，请参阅Adobe](https://repo.adobe.com/) 公共Maven存储库。)

>[!NOTE]
>尽管Cloud Manager未定义特定版本，但 `jacoco-maven-plugin`使用的版本至少必须为 `0.7.5.201505241946`。

## 使用Java 11 {#using-java-11}

Cloud Manager现在支持使用Java 8和Java 11构建客户项目。 默认情况下，项目是使用Java 8构建的。 计划在其项目中使用Java 11的客户可以使用Apache Maven Toolchains [插件进行此操作](https://maven.apache.org/plugins/maven-toolchains-plugin/)。

为此，请在pom.xml文件中添加一个 `<plugin>` 如下的条目：

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
>支持 `vendor` 的值 `oracle` 为，支 `sun` 持的值为 `version` 、 `1.8`和 `1.11``11`。

>[!NOTE]
>Cloud Manager项目构建仍在使用Java 8调用Maven，因此检查或强制工具链插件中通过插件(如 [Apache Maven Enforcer插件)配置的Java版本不起作用](https://maven.apache.org/enforcer/maven-enforcer-plugin/) ，且此类插件不得使用。

## 环境变量 {#environment-variables}

### 标准环境变量 {#standard-environ-variables}

在某些情况下，客户发现有必要根据有关项目或管道的信息改变构建流程。

例如，如果正在通过gulp等工具完成构建时间JavaScript微型化，则在为开发环境构建时可能希望使用不同的微型化级别，而不是为舞台和生产构建。

为了支持此功能，Cloud Manager会将这些标准环境变量添加到每次执行的构建容器中。

| **变量名称** | **定义** |
|---|---|
| CM_BUILD | 始终设置为“true” |
| 分支 | 为执行配置的分支 |
| CM_PIPELINE_ID | 数字管线标识符 |
| CM_PIPELINE_NAME | 管道名称 |
| CM_项目_ID | 数字项目标识符 |
| CM_项目_NAME | 项目名称 |
| AFTRACTS_VERSION | 对于舞台或生产管道，由Cloud Manager生成的合成版本 |

### 管道变量 {#pipeline-variables}

在某些情况下，客户的构建过程可能取决于特定配置变量，这些变量不适合放置在Git存储库中，或者需要在使用同一分支的管道执行之间有所不同。

Cloud Manager允许通过Cloud Manager API或Cloud Manager CLI按管道配置这些变量。 变量可以以纯文本形式存储，也可以在静态时加密。 在任何一种情况下，生成环境中的变量都作为环境变量可用，然后可以从文件或其他生成脚本 `pom.xml` 中引用该变量。

要使用CLI设置变量，请运行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可以列出当前变量：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

变量名称只能包含字母数字和下划线(_)字符。 按照惯例，这些名称应全部为大写。 每个管道限制为200个变量，每个名称必须少于100个字符，每个值必须少于2048个字符。

在文件内使 `Maven pom.xml` 用时，通常可以使用类似于下面的语法将这些变量映射到Maven属性：

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

某些构建需要安装额外的系统包才能完全运行。 例如，生成可能调用Python或ruby脚本，因此需要安装相应的语言解释器。 这可以通过调用exec- [maven-plugin来调用](https://www.mojohaus.org/exec-maven-plugin/) APT来完成。 此执行通常应包含在特定于Cloud Manager的Maven用户档案中。 例如，安装python:

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

此技术同样可用于安装语言特定的软件包，即用于 `gem` RubyGems或 `pip` Python软件包。

>[!NOTE]
>
>以这种方式安装系统包不 **会将** 它安装在用于运行Adobe Experience Manager的运行时环境中。 如果您需要AEM环境上安装系统包，请与客户成功工程师(CSE)联系。
