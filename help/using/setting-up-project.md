---
title: 设置项目
description: 可查看本页以了解如何设置项目
translation-type: tm+mt
source-git-commit: 2ada697ca21acd0c73dbce2bce3e9481ac50272c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 7%

---


# 设置项目{#setting-up-your-project}

## 修改项目设置详细信息{#modifying-project-setup-details}

为了成功构建和部署Cloud Manager，现有AEM项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* 在Git存储库的根目录中必须有&#x200B;*pom.xml*&#x200B;文件。 此&#x200B;*pom.xml*&#x200B;文件可以引用许多子模块（而这些子模块又可能具有其他子模块等）。 必要时。

* 您可以在&#x200B;*pom.xml*&#x200B;文件中添加对其他Maven对象存储库的引用。 配置后，支持访问[受密码保护的对象存储库](#password-protected-maven-repositories)。 但是，不支持访问受网络保护的对象存储库。
* 通过扫描名为&#x200B;*目标*&#x200B;的目录中包含的内容包&#x200B;*zip*&#x200B;文件，可以发现可部署的内容包。 任何数量的子模块都可以生成内容包。

* 通过扫描&#x200B;*zip*&#x200B;文件(同样，包含在名为&#x200B;*目标*&#x200B;的目录中)来发现可部署的调度程序对象，该目录具有名为&#x200B;*conf*&#x200B;和&#x200B;*conf.d*&#x200B;的目录。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定的订单，可以使用内容包依赖关系定义订单。 从部署中可以跳过[](#skipping-content-packages)包。


## 在云管理器{#activating-maven-profiles-in-cloud-manager}中激活Maven用户档案

在某些有限情况下，在Cloud Manager中运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情况，[Maven用户档案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)可用于定义不同环境（包括Cloud Manager）中构建的不同方式。

在Cloud Manager构建激活中环境Maven用户档案，应通过查找上述CM_BUILD环境变量来完成。 相反，应通过查找此变量的缺失来完成仅在Cloud Manager构建用户档案外使用的环境。

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
>要在开发人员工作站上测试此用户档案，您可以在命令行（带有`-PcmBuild`）或集成开发环境(IDE)中启用它。

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

## 受密码保护的Maven存储库支持{#password-protected-maven-repositories}

>[!NOTE]
>受密码保护的Maven存储库中的对象只应非常谨慎地使用，因为通过此机制部署的代码当前未通过Cloud Manager的质量门运行。 因此，它只应用于极少的情况，以及不绑定到AEM的代码。 建议还部署Java源以及整个项目源代码以及二进制代码。

要从Cloud Manager中使用受密码保护的Maven存储库，请将密码（或者，也可以将用户名）指定为机密[管道变量](/help/using/build-environment-details.md#pipeline-variables)，然后在git存储库中名为`.cloudmanager/maven/settings.xml`的文件中引用该机密。 此文件遵循[ Maven Settings File](https://maven.apache.org/settings.html)模式。 当Cloud Manager构建进程开始时，此文件中的`<servers>`元素将合并到Cloud Manager提供的默认`settings.xml`文件中。 以`adobe`和`cloud-manager`开头的服务器ID被视为保留ID，自定义服务器不应使用它。 Cloud Manager永远不会镜像与这些前缀之一或默认ID `central`匹配的服务器ID **不**。 在此文件就位后，服务器ID将从`pom.xml`文件内的`<repository>`和／或`<pluginRepository>`元素中引用。 通常，这些`<repository>`和／或`<pluginRepository>`元素将包含在特定于[云管理器的用户档案](#activating-maven-profiles-in-cloud-manager)中，尽管这并不是严格必需的。

例如，假设存储库位于https://repository.myco.com/maven2，则Cloud Manager应使用的用户名为`cloudmanager` ，密码为`secretword`。

首先，将密码设置为管道上的机密：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然后从`.cloudmanager/maven/settings.xml`文件中引用它：

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

最后引用`pom.xml`文件中的服务器ID:

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

### 部署源{#deploying-sources}

最好将Java源与二进制一起部署到Maven存储库。

在项目中配置maven-source-plugin:

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

### 部署项目源{#deploying-project-sources}

将整个项目源与二进制文件一起部署到Maven存储库是一个好做法——这样可以重新构建精确的对象。

在项目中配置maven-assembly-plugin:

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

## 正在跳过内容包{#skipping-content-packages}

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

## 根据最佳实践{#develop-your-code-based-on-best-practices}开发代码

Adobe工程和咨询团队为AEM开发人员制定了[一整套最佳做法](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
