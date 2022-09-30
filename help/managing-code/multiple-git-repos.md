---
title: 使用多个 Git 存储库
description: 了解如何使用您自己的 Git 存储库或多个 Git 存储库，而不是直接使用 Cloud Manager 的 Git 存储库。
exl-id: 53bf78bb-489a-4a83-8459-c361f532d54a
source-git-commit: da9dff997a277c207e2c48207217cb30325f3c0d
workflow-type: ht
source-wordcount: '756'
ht-degree: 100%

---

# 使用多个源 Git 存储库 {#working-with-multiple-source-git-repos}

了解如何使用您自己的 Git 存储库或多个 Git 存储库，而不是直接使用 Cloud Manager 的 Git 存储库。

## 同步客户管理的 Git 存储库 {#syncing-customer-managed-git-repositories}

如果您希望使用自己的存储库或多个存储库，则应设置自动同步过程以确保 Cloud Manager 的 Git 存储库始终保持最新。

根据托管 Git 存储库的位置，可以使用 GitHub 操作或 Jenkins 等持续集成解决方案来设置自动化。借助自动化功能，在每次推送到您自己的存储库时，都会自动转发到 Cloud Manager 的 Git 存储库。

虽然为单个客户拥有的 Git 存储库实施此类自动化很简单，但为多个存储库配置此类自动化则需要更复杂的初始设置。来自多个 Git 存储库的内容需映射到单个 Cloud Manager 的 Git 存储库中的不同目录。Cloud Manager 的 Git 存储库需要使用根 Maven `pom.xml` 进行设置，并在模块部分中列出不同的子项目

以下是两个客户拥有的 Git 存储库的示例 `pom.xml`。第一个项目将放置到名为 `project-a` 的目录中，第二个项目将放置到名为 `project-b` 的目录中。

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

此类根 `pom.xml` 将推送到 Cloud Manager 的 Git 存储库中的分支。随后，需要设置这两个项目以自动将更改转发到 Cloud Manager 的 Git 存储库。

例如，可以通过推送到项目 A 中的分支来触发 GitHub 操作。该操作将检查项目 A 和 Cloud Manager Git 存储库，并将所有内容从项目 A 复制到 Cloud Manager Git 存储库中的 `project-a` 目录，然后提交推送更改。

例如，对项目 A 中的 `main` 分支所做的更改将自动推送到 Cloud Manager Git 存储库中的 `main` 分支。当然，分支之间会存在映射，例如在推送到项目 A 中名为 `dev` 的分支时，会推送到 Cloud Manager Git 存储库中名为 `development` 的分支。对于项目 B，需要执行类似的步骤。

根据分支策略和工作流，可以为不同的分支配置同步。如果使用的 Git 存储库未提供类似于 GitHub 操作的概念，则也可以通过 Jenkins（或类似方法）进行集成。在此情况下，一个 webhook 将触发一个 Jenkins 作业来完成这项工作。

执行以下步骤以添加新的（第三个）源或存储库：

1. 将新的 GitHub 操作添加到新存储库，这会将更改从该存储库推送到 Cloud Manager 的 Git 存储库。
1. 至少执行一次该操作，确保项目代码位于 Cloud Manager 的 Git 存储库中。
1. 在 Cloud Manager Git 存储库的根 Maven `pom.xml` 中添加对新目录的引用。

## 示例 GitHub 操作 {#sample-github-action}

这是一个通过以下方式触发的示例 GitHub 操作，推送到 `main` 分支，然后推送到 Cloud Manager Git 存储库的子目录。需提供 `MAIN_USER` 和 `MAIN_PASSWORD` 这两个密钥，GitHub 操作才能连接并推送到 Cloud Manager 的 Git 存储库。

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

如上所示，使用 GitHub 操作是非常灵活的。可以执行 Git 存储库的分支之间的任何映射，以及将单独的 Git 项目映射到主项目的目录布局中。

>[!NOTE]
>
>上述脚本使用 `git add` 更新假定包含移除内容的存储库。根据 Git 的默认配置，这可能需要替换为 `git add --all`。

## 示例 Jenkins 作业 {#sample-jenkins-job}

这是一个示例脚本，可用于 Jenkins 作业或类似作业。它由 Git 存储库中的更改触发。Jenkins 作业将签出该项目或分支的最新状态，然后触发此脚本。

此脚本依次签出 Cloud Manager 的 Git 存储库并将项目代码提交到子目录。

需提供 `MAIN_USER` 和 `MAIN_PASSWORD` 这两个密钥，Jenkins 作业才能连接并推送到 Cloud Manager 的 Git 存储库。

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

如上所示，使用 Jenkins 作业是非常灵活的。可以执行 Git 存储库的分支之间的任何映射，以及将单独的 Git 项目映射到主项目的目录布局中。

>[!NOTE]
>
>上述脚本使用 `git add` 更新假定包含移除内容的存储库。根据 Git 的默认配置，这可能需要替换为 `git add --all`。
