---
title: 创建AEM应用程序项目
seo-title: 创建AEM应用程序项目
description: 'null'
seo-description: 查看本页以了解有关在Cloud Manager入门时设置AEM项目的更多信息。
uuid: 7b976epf-5358-49d8-a58 d-0bae026303 fa
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: 快速入门
discoiquuid: 76c1a8e4-d66 f-4a3 b-8c0 c-b80 c9 e17700 e
translation-type: tm+mt
source-git-commit: 365cd6dfe65059c0c529f774bbcda946d47b0db5

---


# 创建AEM应用程序项目 {#create-an-aem-application-project}

## 使用向导创建AEM应用程序项目 {#using-wizard-to-create-an-aem-application-project}

客户在将客户停放在Cloud Manager上后，将提供一个空的git存储库。当前Adobe Managed Services(AMS)客户(或者迁移到AMS的预制AEM客户)通常已经在Git(或其他版本控制系统)中拥有他们的项目代码，并会将其项目导入Cloud Manager Git存储库。但是，新客户没有现有项目。

为帮助新客户开始工作，Cloud Manger现在能够创建最低的AEM项目作为起点。此过程基于AEM [**Project Architype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T12:52:50.071-0400

2018.8.0: Added this new section

 -->

请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. 登录Cloud Manager并且基本程序设置完成后，如果存储库为空，将在 **概述** 屏幕上显示一个对操作卡的特殊调用。

   ![](assets/image2018-10-3_14-29-44.png)

1. 单击 **创建** 以导航 **到渠道设置** 屏幕。

   ![](assets/image2018-10-3_14-30-22.png)

1. 单击 **创建** 以打开一个对话框，该对话框允许用户提供AEM项目类型所需的参数。在默认表单中，对话框要求有两个值：

   * **标题** -默认情况下，此设置设置为 *计划名称*

   * **新分支名称** -默认情况下此名称 *为主分支*
   ![](assets/screen_shot_2018-10-08at55825am.png)

   对话框中有一个抽屉，可通过单击对话框底部的手柄打开该抽屉。在其展开的表单中，对话框显示了Architype的所有配置参数。其中很多参数都具有根据 **标题生成的默认值**。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如 **，如果标题** 为 ***We. Finance***，则Base Maven Articacic ID参数生成 ***com. webance***。如果需要，可以更改这些值。
   >
   >
   >例如，您可以从生成 ***的value com. webance*** 更改 ***为net. webance***。

1. 在上一步中单击 **创建** ，以使用原型类型创建起动项目，并提交给指定的git分支。完成后，您可以设置渠道。

## 设置项目 {#setting-up-your-project}

### 修改项目设置详细信息 {#modifying-project-setup-details}

为了通过Cloud Manager成功构建和部署，现有AEM项目需要遵守一些基本规则：

* 必须使用Apache Maven构建项目。
* Git存储库的根目录中必须有一 *个pom.xml* 文件。此 *pom.xml* 文件可以引用任意多个子模块(反过来可能有其他子模块等)。如有必要。

* 您可以在 *pom.xml* 文件中添加对其他Maven伪像存储库的引用。但是，不支持访问受密码保护或受网络保护的伪像库。
* 可部署内容包是通过扫描包含在名为目标的目录中的内容包 *zip* 文件来发现的 **。任意数量的子模块都可能生成内容包。

* 可部署调度程序伪像通过扫描 *名为* target的目录(包含在名为 *conf*** 和 *conf. d*&#x200B;的目录中再次扫描)来发现。

* 如果有多个内容包，则不保证包部署的顺序。如果需要特定订单，则可使用内容包依赖关系定义订单。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## 构建环境详细信息 {#build-environment-details}

Cloud Manager使用专用构建环境构建和测试代码。此环境具有以下属性：

* 构建环境基于Linux，源自Ubuntu18.04。
* Apache Maven3.6.0已安装。
* 安装的Java版本为Oracle JDK8u202。
* 安装了一些其他系统包，它们是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphicsmagick

* 其他包可能在构建时安装，如下所述 [](#installing-additional-system-packages)。
* 每个构建都在纯净的环境中完成；构建容器不在执行之间保持任何状态。
* Maven始终使用命令运行： *mvn—批处理模式整洁的org. jacoo：accoco-maven-plugin：prepare-Agent包*
* Maven是在系统级别上配置的，settings.xml文件会自动包含公共Adobe **Artic伪** 存储库。(有关更多详细信息，请参阅 [Adobe Public Maven存储库](https://repo.adobe.com/) )。

## 在Cloud Manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

某些情况下，在Cloud Manager内部运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行时略有改变。在这些情况下 [，Maven配置文件](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义在不同环境中(包括云管理器)的构建方式。

在Cloud Manager内部构建环境中激活Maven配置文件，应考虑是否存在名为环境变量 `CM_BUILD`。此变量始终在Cloud Manager构建环境中设置。相反，只有在Cloud Manager构建环境之外才可以使用该配置文件来查找此变量的缺憾。

例如，如果您希望仅在Cloud Manager中运行该构建时输出简单消息，您将执行以下操作：

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
>要在开发人员工作站上测试此配置文件，您可以在命令行(带有 `-PcmBuild`)或集成开发环境(IDE)中启用该配置文件。

如果您只想输出在Cloud Manager之外运行的简单消息，您应该执行以下操作：

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

在某些情况下，客户的构建流程可能取决于特定配置变量，不适合放在Git存储库中。Cloud Manager允许客户根据客户的成功工程师(CSE)配置这些变量。这些变量存储在安全存储位置，并且仅在为特定客户构建容器中可见。希望使用此功能的客户需要联系他们的CSE来配置变量。

配置后，这些变量将作为环境变量可用。为了将其用作Maven属性，您可以在pom.xml文件中引用这些属性，可能在配置文件中如下所述：

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
>环境变量名称只能包含字母数字和下划线(_)字符。按惯例，这些名称应为大写。

## 安装其他系统包 {#installing-additional-system-packages}

一些构建需要安装其他系统包才能完全正常运行。例如，构建可能调用Python或拼音脚本，因此需要安装相应的语言解释器。可以通过调用 [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) 调用APT来完成此操作。此执行通常应包装在特定于Cloud Manager的Maven配置文件中。例如，要安装python：

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

此相同的技术可用于安装语言特定包，即使用 `gem` RubyGems或 `pip` Python Packages。

>[!NOTE]
>
>以这种方式安装系统包不会将 **其** 安装在运行Adobe Experience Manager的运行时环境中。如果您需要在AEM环境中安装系统包，请与客户成功工程师(CSE)联系。

## 跳过内容包 {#skipping-content-packages}

在Cloud Manager中，构建可能会生成任意数量的内容包。
由于各种原因，可能需要产品包而不是部署内容包。这可能很有用，例如，构建仅用于测试的内容包或将通过构建过程中的另一个步骤重新封装的内容包(即另一个包的子包)。

为了适应这些情况，云管理器将在构建的内容包的属性中查找名为 ***CloudManagerTarget*** 的属性。如果此属性设置为无，则将跳过和未部署包。设置此属性的机制取决于生成内容包的方式。例如，使用filevault-maven-plugin可以配置如下插件：

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

使用content-package-maven-plugin类似于：

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

Adobe工程和咨询团队为AEM开发人员制定了 [一整套最佳实践](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
