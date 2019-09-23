---
title: 创建AEM应用程序项目
seo-title: 创建AEM应用程序项目
description: 'null'
seo-description: 可查看本页以了解有关在Cloud manager入门时设置AEM项目的更多信息。
uuid: 7b976ebf-5358-49d8-a58d-0bae026303fa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 入门
discoiquuid: 76c1a8e4-d66f-4a3b-8c0c-b80c9e17700e
translation-type: tm+mt
source-git-commit: 365cd6dfe65059c0c529f774bbcda946d47b0db5

---


# 创建AEM应用程序项目 {#create-an-aem-application-project}

## 使用向导创建AEM应用程序项目 {#using-wizard-to-create-an-aem-application-project}

当客户已登记到Cloud Manager时，他们会获得一个空git存储库。 当前Adobe Managed Services(AMS)客户（或迁移到AMS的内部部署AEM客户）通常已在git（或其他版本控制系统）中包含其项目代码，并将其项目导入Cloud manager存储库。 但是，新客户没有现有项目。

为了帮助新客户入门，Cloud Manger现在可以创建最少的AEM项目作为起点。 此过程基于 [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T12:52:50.071-0400

2018.8.0: Added this new section

 -->

请按照以下步骤在Cloud manager中创建AEM应用程序项目：

1. 登录到Cloud Manager并完成基本程序设置后，如果存储库为空，“ **Overview** ”屏幕上将显示一张特殊的行动动员卡。

   ![](assets/image2018-10-3_14-29-44.png)

1. 单击 **创建** ，导航到“管线设 **置”屏幕** 。

   ![](assets/image2018-10-3_14-30-22.png)

1. 单 **击创建** ，打开一个对话框，用户可通过该对话框提供AEM项目原型所需的参数。 在默认表单中，对话框要求输入两个值：

   * **标题** -默认情况下，它设置为程序 *名称*

   * **新分支名称** -默认情况下，此名称为主 *页*
   ![](assets/screen_shot_2018-10-08at55825am.png)

   该对话框有一个抽屉，可以通过单击对话框底部的手柄打开该抽屉。 该对话框在其展开形式中显示Archetype的所有配置参数。 其中许多参数都具有默认值，这些默认值是根据“标题” **生成的**。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果标 **题为** We.Finance ***，则Base Maven Artifact id参数将生成为*** com.wefinance ******。 如果需要，可以更改这些值。
   >
   >
   >例如，您可以将生成的 ***值com.wefinance更改为*** net.wefinance ******。

1. 在上 **一步中** ，单击创建，使用原型创建启动项目并提交到指定的git分支。 完成此操作后，您可以设置管道。

## 设置项目 {#setting-up-your-project}

### 修改项目设置详细信息 {#modifying-project-setup-details}

为了使用Cloud manager成功构建和部署AEM项目，现有AEM项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* Git存储库 *的根中必须有pom.xml* 文件。 此 ** pom.xml文件可以引用多个子模块（这些子模块又可能具有其他子模块等）必要时。

* 您可以在 *pom.xml文件中添加对其他Maven对象存储库的引用* 。 但是，不支持访问受口令保护或受网络保护的对象存储库。
* 通过扫描名为target的目录中包含的内容包 *zip* ，可以发现可部署的内容包 **。 任意数量的子模块可以生成内容包。

* 可部署的调度程序对象是通过扫描 *zip* 文件(同样，包含在名为 *target*&#x200B;的目录中)来发现的，这些文件的目录名 *为conf* 和 ** conf.d。

* 如果有多个内容包，则不保证包部署的排序。 如果需要特定的顺序，可以使用内容包依赖关系来定义顺序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## 构建环境详细信息 {#build-environment-details}

Cloud manager使用专用构建环境构建和测试您的代码。 此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu 18.04。
* 已安装Apache Maven 3.6.0。
* 安装的Java版本为Oracle JDK 8u202。
* 还安装了一些其他系统包，这是必需的：

   * bzip2
   * unzip
   * libpng
   * imagemagick
   * graphicsmagick

* 其他包可能会在构建时安装，如下 [所述](#installing-additional-system-packages)。
* 每栋建筑都建在原始环境中；构建容器不会在执行之间保留任何状态。
* Maven始终使用以下命令运行：mvn *—batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent包*
* Maven在系统级别上配置了settings.xml文件，该文件自动包括公共Adobe **Artifact存储库** 。 (有关更多详细 [信息，请参阅Adobe Public Maven Repository](https://repo.adobe.com/) )。

## 在Cloud manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些有限的情况下，在Cloud manager中运行时，与在开发人员工作站上运行时相比，您可能需要稍微改变构建过程。 对于这些情况， [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) （Maven配置文件）可用于定义构建在包括Cloud manager在内的不同环境中的不同之处。

在Cloud manager构建环境中激活Maven配置文件时，应通过查找名为的环境变量来完成 `CM_BUILD`。 此变量将始终设置在Cloud manager构建环境中。 相反，只有在Cloud manager构建环境之外才能使用的配置文件，应通过查找此变量的大小来完成。

例如，如果您希望仅在构建在Cloud manager中运行时输出简单消息，您可以执行以下操作：

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
>要在开发人员工作站上测试此配置文件，您可以在命令行(随 `-PcmBuild`)或集成开发环境(IDE)中启用它。

如果您希望仅在构建在Cloud manager之外运行时输出简单消息，您可以执行以下操作：

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

## 自定义环境变量

在某些情况下，客户的构建过程可能取决于特定配置变量，这些变量不适合放在git存储库中。 Cloud manager允许客户成功工程师(CSE)按客户配置这些变量。 这些变量存储在安全的存储位置中，并且仅在特定客户的构建容器中可见。 希望使用此功能的客户需要联系其CSE以配置其变量。

配置后，这些变量将作为环境变量可用。 要将它们用作Maven属性，您可以在pom.xml文件中引用它们，可能在上述配置文件中引用它们：

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
>
>环境变量名称只能包含字母数字和下划线(_)字符。 按照惯例，这些名称应全部为大写。

## 安装其他系统包 {#installing-additional-system-packages}

某些构建需要安装额外的系统包才能完全运行。 例如，内部版本可能调用Python或ruby脚本，因此需要安装相应的语言解释器。 这可以通过调用exec- [maven-plugin来调用](https://www.mojohaus.org/exec-maven-plugin/) APT来完成。 此执行通常应包含在特定于Cloud manager的Maven配置文件中。 例如，安装python:

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

此技术同样可用于安装特定于语言的包，即使用RubyGems或 `gem` Python包 `pip` 安装这些包。

>[!NOTE]
>
>以这种方式安装系统包 **不会** ，而是将它安装在用于运行Adobe Experience Manager的运行时环境中。 如果您需要在AEM环境中安装系统包，请与您的客户成功工程师(CSE)联系。

## 跳过内容包 {#skipping-content-packages}

在Cloud manager中，构建可能生成任意数量的内容包。
出于各种原因，可能需要制作内容包，但不要部署它。 这可能很有用，例如，在构建仅用于测试的内容包时，或者在构建过程中将通过另一个步骤重新打包的内容包（即，作为另一个包的子包）时。

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

Adobe工程和咨询团队为AEM开发 [人员开发了一整套最佳做法](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
