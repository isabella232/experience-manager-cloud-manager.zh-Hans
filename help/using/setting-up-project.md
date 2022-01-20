---
title: 设置项目
description: 可查看本页以了解如何设置项目
feature: Getting Started, Production Programs
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 8861b5e48b8e1d081b4c8653000a8f2cf16dd11f
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 5%

---

# 设置项目 {#setting-up-your-project}

## 修改项目设置详细信息 {#modifying-project-setup-details}

要使用Cloud Manager成功构建和部署AEM项目，现有Analytics项目需要遵守一些基本规则：

* 项目必须使用Apache Maven构建。
* 一定有 *pom.xml* 文件。 此 *pom.xml* 文件可以引用任意数量的子模块（这些子模块又可能具有其他子模块等） 视需要。

* 您可以在 *pom.xml* 文件。 访问 [受密码保护的项目存储库](#password-protected-maven-repositories) 配置时支持。 但是，不支持访问受网络保护的对象存储库。
* 通过扫描内容包来发现可部署的内容包 *zip* 包含在名为 *目标*. 任意数量的子模块可以生成内容包。

* 通过扫描发现可部署的调度程序工件 *zip* 文件(同样，包含在名为 *目标*)的目录名为 *conf* 和 *conf.d*.

* 如果有多个内容包，则无法保证包部署的顺序。 如果需要特定顺序，可以使用内容包依赖关系来定义顺序。 包可以 [跳过](#skipping-content-packages) 从部署。


## 在Cloud Manager中激活Maven配置文件 {#activating-maven-profiles-in-cloud-manager}

在某些有限情况下，在Cloud Manager内运行时，您可能需要稍微改变构建过程，而不是在开发人员工作站上运行。 对于这些情况， [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用于定义在包括Cloud Manager在内的不同环境中，内部版本应有何不同。

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
>要在开发人员工作站上测试此配置文件，您可以在命令行中启用它(使用 `-PcmBuild`)或集成开发环境(IDE)中。

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

要从Cloud Manager中使用受密码保护的Maven存储库，请将密码（和可选用户名）指定为密钥 [管道变量](/help/using/build-environment-details.md#pipeline-variables) 然后在名为 `.cloudmanager/maven/settings.xml` 在git存储库中。 此文件遵循 [Maven设置文件](https://maven.apache.org/settings.html) 架构。 当Cloud Manager构建过程开始时， `<servers>` 此文件中的元素将合并到默认 `settings.xml` 文件。 服务器ID以 `adobe` 和 `cloud-manager` 视为保留，不应被自定义服务器使用。 服务器ID **not** 匹配这些前缀之一或默认ID `central` 将永远不会被Cloud Manager镜像。 此文件就位后，将从内部引用服务器ID `<repository>` 和/或 `<pluginRepository>` 元素内部 `pom.xml` 文件。 通常， `<repository>` 和/或 `<pluginRepository>` 元素将包含在 [特定于Cloud Manager的配置文件](#activating-maven-profiles-in-cloud-manager)，尽管这并非严格必要。

例如，假定存储库位于https://repository.myco.com/maven2 ，则Cloud Manager应使用的用户名为 `cloudmanager` 密码是 `secretword`.

首先，在管道上将密码设置为密钥：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然后，在 `.cloudmanager/maven/settings.xml` 文件：

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

最后引用 `pom.xml` 文件：

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

## 构建对象重用 {#build-artifact-reuse}

在许多情况下，会将相同的代码部署到多个AEM环境。 如果Cloud Manager检测到在多个全堆栈管道执行中使用相同的git提交，则将尽可能避免重建代码库。

启动执行时，将提取分支管道的当前HEAD提交。 提交哈希在UI中和通过API可见。 成功完成构建步骤后，将基于提交哈希存储生成的工件，并可在后续管道执行中重复使用。 当重复使用时，构建和代码质量步骤会被有效地替换为原始执行的结果。 生成步骤的日志文件将列出最初用于生成对象的工件和执行信息。

以下是此类日志输出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

代码质量步骤的日志将包含类似信息。

### 选择退出 {#opting-out}

如果需要，可以通过设置管道变量来禁用特定管道的重复使用行为 `CM_DISABLE_BUILD_REUSE` to `true`. 如果设置了此变量，则仍会提取提交哈希，并且将存储所生成的工件以供日后使用，但之前存储的任何工件将不会重复使用。 要了解此行为，请考虑以下情景。

1. 将创建新管道。
1. 将执行(执行#1)并且当前HEAD提交为 `becdddb`. 执行成功，并且会存储所生成的工件。
1. 的 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将在不更改代码的情况下重新执行管道。 尽管存储了与 `becdddb`，由于 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将更改代码并执行管道。 HEAD提交现在为 `f6ac5e6`. 执行成功，并且会存储所生成的工件。
1. 的 `CM_DISABLE_BUILD_REUSE` 变量。
1. 将在不更改代码的情况下重新执行管道。 由于存储了与 `f6ac5e6`，则这些工件将被重复使用。

### 注意事项 {#caveats}

* [Maven版本处理](/help/using/activating-maven-project.md) 仅在生产管道中替换项目版本。 因此，如果开发部署执行和生产管道执行都使用相同的提交，并且首先执行开发部署管道，则这些版本将部署到暂存和生产环境，而不会发生更改。 但是，在这种情况下仍将创建标记。
* 如果存储的工件检索失败，则执行生成步骤，如同尚未存储任何工件一样。
* 管道变量(而非 `CM_DISABLE_BUILD_REUSE` 当Cloud Manager决定重复使用之前创建的内部版本对象时，不会考虑使用该对象。

## 根据最佳实践开发代码 {#develop-your-code-based-on-best-practices}

Adobe工程和咨询团队已开发了 [面向AEM开发人员的一整套最佳实践。](https://helpx.adobe.com/cn/experience-manager/6-4/sites/developing/using/best-practices.html)
