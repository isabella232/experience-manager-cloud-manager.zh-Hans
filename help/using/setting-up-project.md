---
title: 设置项目
description: 可查看本页以了解如何设置项目
feature: 入门、生产计划
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 2a253abb98fa096f9f1c07bac94804849fad2ebb
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 8%

---

# 设置项目 {#setting-up-your-project}

## 修改项目设置详细信息 {#modifying-project-setup-details}

要使用Cloud Manager成功构建和部署AEM项目，现有Analytics项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* Git存储库的根中必须有&#x200B;*pom.xml*&#x200B;文件。 此&#x200B;*pom.xml*&#x200B;文件可以引用任意数量的子模块（这些子模块又可能具有其他子模块等） 视需要。

* 您可以在&#x200B;*pom.xml*&#x200B;文件中添加对其他Maven对象存储库的引用。 配置后支持访问受密码保护的对象存储库](#password-protected-maven-repositories)。 [但是，不支持访问受网络保护的对象存储库。
* 通过扫描名为&#x200B;*target*&#x200B;的目录中包含的内容包&#x200B;*zip*&#x200B;文件，可发现可部署的内容包。 任意数量的子模块可以生成内容包。

* 通过扫描名为&#x200B;*conf*&#x200B;和&#x200B;*conf.d*&#x200B;的目录（同样包含在名为&#x200B;*target*&#x200B;的目录中）的&#x200B;*zip*&#x200B;文件，可发现可部署的Dispatcher工件。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定顺序，可以使用内容包依赖关系来定义顺序。 部署中的包可能已跳过[](#skipping-content-packages)。


## 在Cloud Manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager内运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情况，可以使用[Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)定义在包括Cloud Manager在内的不同环境中，内部版本应如何不同。

在Cloud Manager构建环境中激活Maven配置文件时，应通过查找上述CM_BUILD环境变量来完成。 相反，应通过查找此变量的缺失来完成仅在Cloud Manager构建环境之外使用的用户档案。

例如，如果您只想在Cloud Manager中运行内部版本时输出简单消息，则可以执行以下操作：

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
>要在开发人员工作站上测试此配置文件，您可以在命令行（带有`-PcmBuild`）或集成开发环境(IDE)中启用此配置文件。

如果您希望仅在内部版本在Cloud Manager之外运行时才输出简单消息，则可以执行以下操作：

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

## 受密码保护的Maven存储库支持 {#password-protected-maven-repositories}

>[!NOTE]
>受密码保护的Maven存储库中的工件只应非常谨慎地使用，因为通过此机制部署的代码当前未通过Cloud Manager质量门中实施的所有质量规则运行。 因此，它只应用于极少数情况下以及未绑定到AEM的代码。 建议还应将Java源以及整个项目源代码与二进制文件一起部署。

要从Cloud Manager中使用受密码保护的Maven存储库，请将密码（以及可选的用户名）指定为密钥[管道变量](/help/using/build-environment-details.md#pipeline-variables)，然后在git存储库中名为`.cloudmanager/maven/settings.xml`的文件中引用该密钥。 此文件遵循[Maven设置文件](https://maven.apache.org/settings.html)架构。 当Cloud Manager构建过程启动时，此文件中的`<servers>`元素将合并到Cloud Manager提供的默认`settings.xml`文件中。 以`adobe`和`cloud-manager`开头的服务器ID被视为保留ID，自定义服务器不应使用这些ID。 Cloud Manager将永远不会镜像与其中一个前缀或默认ID `central`匹配的服务器ID **不**。 此文件就位后，服务器ID将从`<repository>`和/或`<pluginRepository>`元素内的`pom.xml`文件中引用。 通常，这些`<repository>`和/或`<pluginRepository>`元素将包含在特定于[Cloud Manager的配置文件](#activating-maven-profiles-in-cloud-manager)中，尽管这并非严格必需的。

例如，假设存储库位于https://repository.myco.com/maven2 ,Cloud Manager的用户名应为`cloudmanager` ，密码为`secretword` 。

首先，在管道上将密码设置为密钥：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然后，从`.cloudmanager/maven/settings.xml`文件中引用此内容：

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

最后，引用`pom.xml`文件中的服务器ID:

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

最好将Java源与二进制文件一起部署到Maven存储库。

在项目中配置maven-source-plugin :

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

最好将整个项目源与二进制文件一起部署到Maven存储库，以便重建确切的对象。

在项目中配置maven-assembly-plugin :

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

在Cloud Manager中，内部版本可能会生成任意数量的内容包。
出于各种原因，可能需要生成内容包，但不部署它。 例如，当构建仅用于测试的内容包时，或者当内容包将被构建过程中的其他步骤（即作为其他包的子包）重新打包时，这可能会非常有用。

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

使用content-package-maven-plugin时，类似于：

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

Adobe工程和咨询团队为AEM开发人员开发了一套[全面的最佳实践](https://helpx.adobe.com/cn/experience-manager/6-4/sites/developing/using/best-practices.html)。
