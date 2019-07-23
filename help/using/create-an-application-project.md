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
source-git-commit: b39fc865e3c34052fb94b223d9eebc0fce3495d2

---


# Create an AEM Application Project {#create-an-aem-application-project}

## Using Wizard to Create an AEM Application Project {#using-wizard-to-create-an-aem-application-project}

客户在将客户停放在Cloud Manager上后，将提供一个空的git存储库。当前Adobe Managed Services(AMS)客户(或者迁移到AMS的预制AEM客户)通常已经在Git(或其他版本控制系统)中拥有他们的项目代码，并会将其项目导入Cloud Manager Git存储库。但是，新客户没有现有项目。

为帮助新客户开始工作，Cloud Manger现在能够创建最低的AEM项目作为起点。This process is based on the [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T12:52:50.071-0400

2018.8.0: Added this new section

 -->

请按照以下步骤在Cloud Manager中创建AEM应用程序项目：

1. Once you log in to Cloud Manager and the basic program setup is complete, a special call to action card will be shown on the **Overview** screen, if the repository is empty.

   ![](assets/image2018-10-3_14-29-44.png)

1. Click **Create** to navigate to the **Pipeline Setup** screen.

   ![](assets/image2018-10-3_14-30-22.png)

1. Click **Create to** open a dialog box, which allows the user to provide the parameters required by the AEM Project Archetype. 在默认表单中，对话框要求有两个值：

   * **标题** -默认情况下，此设置设置为 *计划名称*

   * **新分支名称** -默认情况下此名称 *为主分支*
   ![](assets/screen_shot_2018-10-08at55825am.png)

   对话框中有一个抽屉，可通过单击对话框底部的手柄打开该抽屉。在其展开的表单中，对话框显示了Architype的所有配置参数。Many of these parameters have default values which are generated based on the **Title**.

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >For example, if the **Title** is ***We.Finance***, the Base Maven Artifact Id parameter is generated as ***com.wefinance***. 如果需要，可以更改这些值。
   >
   >
   >For example, you can change from the generated ***value com.wefinance*** to ***net.wefinance***.

1. Click **Create** in the preceding step to create the starter project by using the archetype and commit to the named git branch. 完成后，您可以设置渠道。

## Setting up your Project {#setting-up-your-project}

### Modifying Project Setup Details {#modifying-project-setup-details}

为了通过Cloud Manager成功构建和部署，现有AEM项目需要遵守一些基本规则：

* 必须使用Apache Maven构建项目。
* There must be a *pom.xml* file in the root of the Git repository. This *pom.xml* file can refer to as many submodules (which in turn may have other submodules, etc.) 如有必要。

* You can add references to additional Maven artifact repositories in your *pom.xml* files. 但是，不支持访问受密码保护或受网络保护的伪像库。
* Deployable content packages are discovered by scanning for content package *zip* files which are contained in a directory named *target*. 任意数量的子模块都可能生成内容包。

* Deployable Dispatcher artifacts are discovered by scanning for *zip* files (again, contained in a directory named *target*) which have directories named *conf* and *conf.d*.

* 如果有多个内容包，则不保证包部署的顺序。如果需要特定订单，则可使用内容包依赖关系定义订单。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## Build Environment Details {#build-environment-details}

Cloud Manager builds and tests your code using a specialized build runtime **Environment**. 此环境具有以下属性：

* 构建环境基于Linux。
* Apache Maven3.6.0已安装。
* 安装的Java版本为Oracle JDK8u202。
* 安装了一些其他系统包，它们是必需的：

   * bzip2
   * 解压缩
   * libpng
   * imagemagick
   * graphicsmagick
   * 如果您需要其他软件包，则需要通过客户成功工程师(CSE)请求这些包。

* 每个构建都在纯净的环境中完成；构建容器不在执行之间保持任何状态。
* Maven is always run with the command: *mvn --batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent package*
* Maven is configured at a system level with a settings.xml file which automatically includes the public Adobe **Artifact** repository. (Refer to [Adobe Public Maven Repository](https://repo.adobe.com/) for more details).

## Activating Maven Profiles in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

某些情况下，在Cloud Manager内部运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行时略有改变。For these cases, [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) can be used to define how the build should be different in different environments, including Cloud Manager.

Activation of a Maven Profile inside the Cloud Manager build environment should be done by looking for the presence of an environment variable named `CM_BUILD`. 此变量始终在Cloud Manager构建环境中设置。相反，只有在Cloud Manager构建环境之外才可以使用该配置文件来查找此变量的缺憾。

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
>To test this profile on a developer workstation, you can either enable it on the command line (with `-PcmBuild`) or in your Integrated Development Environment (IDE).

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

## Develop your Code Based on Best Practices {#develop-your-code-based-on-best-practices}

Adobe Engineering and Consulting teams have developed a [comprehensive set of best practices for AEM developers](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html).
