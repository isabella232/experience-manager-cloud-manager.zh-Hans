---
title: 使用多个Git存储库
description: 了解如何使用您自己的git存储库或多个git存储库，而不是直接使用Cloud Manager的git存储库。
exl-id: 53bf78bb-489a-4a83-8459-c361f532d54a
source-git-commit: da9dff997a277c207e2c48207217cb30325f3c0d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 使用多个源 Git 存储库 {#working-with-multiple-source-git-repos}

了解如何使用您自己的git存储库或多个git存储库，而不是直接使用Cloud Manager的git存储库。

## 同步客户管理的Git存储库 {#syncing-customer-managed-git-repositories}

如果您希望使用自己的存储库或存储库，则应设置自动同步过程，以确保Cloud Manager的git存储库始终保持最新。

根据您的git存储库的托管位置，可以使用GitHub操作或Jenkins等连续集成解决方案来设置自动化。 实施自动化后，每个推送到您自己的存储库的内容都会自动转发到Cloud Manager的git存储库。

虽然单个客户拥有的git存储库的此类自动化过程非常简单，但为多个存储库配置此功能时，需要更多参与的初始设置。 需要将来自多个git存储库的内容映射到单个Cloud Manager的git存储库中的不同目录。 需要使用根Maven配置Cloud Manager的Git存储库 `pom.xml`，在模块部分中列出不同的子项目

以下是一个示例 `pom.xml` 适用于两个客户拥有的git存储库。 第一个项目将放入名为 `project-a`，则第二个项目将放入名为的目录中 `project-b`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
  
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
  
</project>
```

这样的根 `pom.xml` 会推送到Cloud Manager的git存储库中的分支。 然后，需要设置这两个项目以自动将更改转发到Cloud Manager的Git存储库。

例如，GitHub操作可以通过将内容推送到项目A中的分支来触发。该操作将签出项目A和Cloud Manager git存储库，并将项目A中的所有内容复制到目录 `project-a` 在Cloud Manager的git存储库中，然后提交推送更改。

例如， `main` 项目A中的分支会自动推送到 `main` Cloud Manager的git存储库中的分支。 当然，可能存在分支之间的映射，如将消息推送到名为 `dev` 在项目A中，会被推送到名为 `development` 在Cloud Manager的git存储库中。 项目B需要执行类似步骤。

根据分支策略和工作流，可以为不同分支配置同步。 如果使用的git存储库没有提供与GitHub操作类似的概念，则也可以通过Jenkins（或类似）进行集成。 在这种情况下，网络挂钩会触发Jenkins作业，该作业负责工作。

请按照以下步骤添加新的（第三个）源或存储库：

1. 向新存储库添加新的GitHub操作，以将更改从该存储库推送到Cloud Manager的Git存储库。
1. 至少执行一次该操作，以确保项目代码位于Cloud Manager的git存储库中。
1. 在根Maven中添加对新目录的引用 `pom.xml` 在Cloud Manager git存储库中。

## GitHub操作示例 {#sample-github-action}

这是一个由推送到 `main` 分支，然后推送到Cloud Manager的git存储库的子目录中。 GitHub操作需要提供两个密钥， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能够连接并推送到Cloud Manager的git存储库。

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

如上所示，使用GitHub操作非常灵活。 可以执行git存储库分支之间的任何映射，以及将单独的git项目映射到主项目的目录布局中的任何映射。

>[!NOTE]
>
>上述脚本使用 `git add` 更新假定包含删除的存储库。 根据Git的默认配置，可能需要将其替换为 `git add --all`.

## Jenkins作业示例 {#sample-jenkins-job}

这是一个可在Jenkins作业或类似作业中使用的示例脚本。 它由Git存储库中的更改触发。 Jenkins作业会检出该项目或分支的最新状态，然后触发此脚本。

此脚本随后会检出Cloud Manager的git存储库，并将项目代码提交到子目录。

詹金斯的工作需要有两个秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能够连接并推送到Cloud Manager的git存储库。

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

如上所示，使用Jenkins作业非常灵活。 可以执行git存储库分支之间的任何映射，以及将单独的git项目映射到主项目的目录布局中的任何映射。

>[!NOTE]
>
>上述脚本使用 `git add` 要更新假定包含删除的存储库。根据git的默认配置，可能需要将其替换为 `git add --all`.
