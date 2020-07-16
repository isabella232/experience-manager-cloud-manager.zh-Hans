---
title: 创建 AEM 应用程序项目
seo-title: 创建 AEM 应用程序项目
description: 'null'
seo-description: 可查看本页以了解有关在Cloud Manager入门时设置AEM项目的更多信息。
uuid: 7b976ebf-5358-49d8-a58d-0bae026303fa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 76c1a8e4-d66f-4a3b-8c0c-b80c9e17700e
translation-type: tm+mt
source-git-commit: a4ea83c0b64515915871956c1cd3e53606f1c26b
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 7%

---


# 创建 AEM 应用程序项目 {#create-an-aem-application-project}

## 使用向导创建AEM应用程序项目 {#using-wizard-to-create-an-aem-application-project}

当客户已载入Cloud Manager时，他们将获得一个空的git存储库。 当前Adobe Managed Services(AMS)客户（或迁移到AMS的内部部署AEM客户）通常已将其项目代码放在git（或其他版本控制系统）中，并将其项目导入Cloud Manager Git存储库。 但是，新客户没有现有项目。

为了帮助新客户入门，Cloud Manger现在可以创建最少的AEM项目作为起点。 此过程基于AEM项 [**目原型&#x200B;**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. 登录到Cloud Manager并完成基本程序设置后，如果存储库为空，“ **Overview** ”屏幕上将显示一张特殊的行动动员卡。

   ![](assets/image2018-10-3_14-29-44.png)

1. 单 **击创建** 以打开一个对话框，通过该对话框，用户可以提供AEM项目原型所需的参数。 在默认表单中，对话框要求输入两个值：

   * **标题** -默认情况下，它设置为 *项目名*

   * **新分支名称** -默认情况下，此名称为 *主控*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   该对话框有一个抽屉，可以通过单击对话框底部的手柄来打开该抽屉。 在其扩展形式中，该对话框显示原型的所有配置参数。 这些参数中的许多参数具有根据标题生成的默 **认值**。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果标 **题为** We. ***Finance***，则Base Maven Artifact Id参数将生成为 ***com.wefinance***。 如果需要，可以更改这些值。
   >
   >
   >例如，您可以将生成的 ***值com.wefinance更改******为net.wefinance***。

1. 在上 **一步中** ，单击“创建”，使用原型创建启动项目并提交到指定的git分支。 完成此操作后，可设置管道。

## 设置项目 {#setting-up-your-project}

### 修改项目设置详细信息 {#modifying-project-setup-details}

为了成功构建和部署Cloud Manager，现有AEM项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* 在Git存储 *库的根目录中* ，必须有pom.xml文件。 此 *pom.xml* 文件可以引用多个子模块（这些子模块又可能具有其他子模块等） 必要时。

* 您可以在pom.xml文件中添加对其他Maven *项目存储库的引* 用。 但是，不支持访问受密码保护或受网络保护的对象存储库。
* 可部署的内容包是通过扫描内容包 *zip* 文件来发现的，这些文件包含在名为 *目标的目录中*。 任何数量的子模块都可以生成内容包。

* 通过扫描zip文件(同样，包含在名为 *Dispatcher的目录中* )发现可部署的目标对象，该目录具有名 *为conf**和conf.d***&#x200B;的目录。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定的订单，可以使用内容包依赖关系定义订单。 可以从部署 [中跳](#skipping-content-packages) 过包。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## 构建环境详细信息 {#build-environment-details}

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
* 每栋建筑都建在原始环境上； 构建容器不会在执行之间保持任何状态。
* Maven始终使用以下命令运行： *mvn —batch-mode clean org.jacoco:jaco-maven-plugin:prepare-agent包*
* Maven在系统级别上配置了一个settings.xml文件，该文件自动包括公共Adobe Artifact **存储库** 。 (有关更多详 [细信息，请参阅Adobe](https://repo.adobe.com/) Public Maven Repository)。

>[!NOTE]
>尽管Cloud Manager未定义特定版本，但 `jacoco-maven-plugin`使用的版本至少必须为 `0.7.5.201505241946`。

### 使用Java 11 {#using-java-11}

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

### 自定义环境变量 {#custom-variables}

在某些情况下，客户的构建过程可能取决于特定配置变量，这些变量不适合放置在git存储库中。 云管理器允许客户成功工程师(CSE)按客户配置这些变量。

这些变量存储在安全存储位置，并且仅在特定客户的构建容器中可见。 希望使用此功能的客户需要联系其CSE来配置其变量。
配置后，这些变量将作为环境变量可用。 为了将它们用作Maven属性，您可以在pom.xml文件中引用它们，可能在上述用户档案中引用它们：


```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <properties>
                  <my.custom.property>${env.MY_CUSTOM_PROPERTY}</my.custom.property>  
            </properties>
        </profile>
```

>[!NOTE]
>环境变量名称只能包含字母数字和下划线(_)字符。 按照惯例，这些名称应全部为大写。

## 在Cloud Manager中激活Maven用户档案 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager中运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情 [况，Maven用户档案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义不同环境（包括Cloud Manager）中构建内容的不同方式。

在Cloud Manager构建激活中环境Maven用户档案，应通过查找上述CM_BUILD环境变量来完成。 相反，只有在Cloud Manager构建用户档案之外才能使用的环境应通过查找此变量的基本含义来完成。

例如，如果您希望仅在构建在云管理器中运行时输出简单消息，您可以执行以下操作：

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
>要在开发人员工作站上测试此用户档案，您可以在命令行上（通过）或在集 `-PcmBuild`成开发环境(IDE)中启用它。

如果您希望仅在构建在Cloud Manager外部运行时输出简单消息，您可以执行以下操作：

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
>以这种方式安装系统包不 **会将** 它安装在用于运行Adobe Experience Manager的运行时环境中。 如果您需要在AEM环境上安装系统包，请与客户成功工程师(CSE)联系。

## 跳过内容包 {#skipping-content-packages}

在Cloud Manager中，构建可能生成任意数量的内容包。
由于各种原因，可能希望生成内容包，但不要部署它。 这可能很有用，例如，在构建仅用于测试的内容包时，或者在构建过程中的另一步骤（即作为另一个包的子包）重新打包的内容包时。

为了适应这些情况，Cloud manager将在构建内容包的属性中 ***查找名为cloudManagerTarget*** 的属性。 如果此属性设置为none，则将跳过并且不部署包。 设置此属性的机制取决于构建生成内容包的方式。 例如，使用filevault-maven-plugin可以配置插件，如下所示：

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

使用content-package-maven-plugin时，它类似：

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

## 根据最佳实践开发代码 {#develop-your-code-based-on-best-practices}

Adobe工程和咨询团队为AEM开 [发人员开发了一整套最佳做法](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
