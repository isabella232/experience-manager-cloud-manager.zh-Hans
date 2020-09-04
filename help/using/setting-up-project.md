---
title: 设置项目
description: 可查看本页以了解如何设置项目
translation-type: tm+mt
source-git-commit: 2ada697ca21acd0c73dbce2bce3e9481ac50272c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 7%

---


# 设置项目 {#setting-up-your-project}

## 修改项目设置详细信息 {#modifying-project-setup-details}

为了成功构建和部署Cloud Manager，现有AEM项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* 在Git存储 *库的根目录中* ，必须有pom.xml文件。 此 *pom.xml* 文件可以引用许多子模块（这些子模块又可能具有其他子模块等） 必要时。

* 您可以在pom.xml文件中添加对其他Maven *项目存储库的引* 用。 配置时 [支持访问受密码保护](#password-protected-maven-repositories) 的对象存储库。 但是，不支持访问受网络保护的对象存储库。
* 可部署的内容包是通过扫描内容包 *zip* 文件来发现的，这些文件包含在名为 *目标的目录中*。 任何数量的子模块都可以生成内容包。

* 通过扫描zip文件(同样，包含在名为 *目标的目录中* )发现可部署的调度程序对象，该目录具有名 *为conf**和conf.d***&#x200B;的目录。

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定的订单，可以使用内容包依赖关系定义订单。 可以从部署 [中跳](#skipping-content-packages) 过包。


## 在Cloud Manager中激活Maven用户档案 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager中运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情 [况，Maven用户档案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义不同环境（包括Cloud Manager）中构建内容的不同方式。

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

## 受密码保护的Maven存储库支持 {#password-protected-maven-repositories}

>[!NOTE]
>受密码保护的Maven存储库中的对象只应非常谨慎地使用，因为通过此机制部署的代码当前未通过Cloud Manager的质量门运行。 因此，它只应用于极少的情况，以及不绑定到AEM的代码。 建议还部署Java源以及整个项目源代码以及二进制代码。

要从Cloud Manager中使用受密码保护的Maven存储库，请将密码（以及用户名）指定为机密管 [线变量](/help/using/build-environment-details.md#pipeline-variables) ，然后在git存储库中名为的文件中引 `.cloudmanager/maven/settings.xml` 用该机密。 此文件遵循“主设 [置文件”模式](https://maven.apache.org/settings.html) 。 当Cloud Manager构建流程开始时， `<servers>` 此文件中的元素将合并到Cloud Manager提 `settings.xml` 供的默认文件中。 服务器ID从开 `adobe` 始 `cloud-manager` ，被视为保留ID，不应由自定义服务器使用。 Cloud Manager **将** 永远不会镜像与这些前缀之 `central` 一不匹配的服务器ID或默认ID。 在此文件就位后，服务器ID将从文件内的 `<repository>` 和／或 `<pluginRepository>` 元素中引 `pom.xml` 用。 通常，这 `<repository>` 些和/ `<pluginRepository>` 或元素将包含在特 [定于Cloud Manager的用户档案中](#activating-maven-profiles-in-cloud-manager)，尽管这并不是严格必需的。

例如，假设存储库位于https://repository.myco.com/maven2，则Cloud Manager应使用的用户名为， `cloudmanager` 密码为 `secretword`。

首先，将密码设置为管道上的机密：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然后从文件中引 `.cloudmanager/maven/settings.xml` 用它：

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

最后引用文件中的服务 `pom.xml` 器ID:

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

### 部署项目源 {#deploying-project-sources}

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
