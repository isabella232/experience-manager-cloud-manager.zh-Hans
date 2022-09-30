---
title: 配置非生产管道
description: 了解如何使用 Cloud Manager 创建和配置非生产管道以部署代码。
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 567a16a032bf80451b5e8ba4e3d842cb617a615f
workflow-type: ht
source-wordcount: '598'
ht-degree: 100%

---

# 配置非生产管道 {#configuring-non-production-pipelines}

了解如何使用 Cloud Manager 创建和配置非生产管道以部署代码。如果您首先想从概念上更加深入了解有关管道在 Cloud Manager 中的工作原理，请参阅 [CI/CD 管道](/help/overview/ci-cd-pipelines.md)文档。

## 概述 {#overview}

通过使用 [!UICONTROL Cloud Manager] 中的&#x200B;**管道**&#x200B;图块，**部署经理**&#x200B;可以创建两种不同类型的管道。

* **生产管道** – 生产管道是一个专用管道，它包含一系列精心设计的步骤，可执行这些步骤以将源代码用于生产环境。
* **非生产管道** – 非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境中。

本文档侧重于非生产管道。有关如何配置生产管道的详细信息，请参阅[配置生产管道](/help/using/production-pipelines.md)文档。

有两种类型的非生产管道：

* **代码质量管道** – 这些代码质量管道将扫描 Git 分支中的代码并执行构建和代码质量步骤。
* **部署管道** – 除了执行代码质量管道等构建和代码质量步骤之外，这些管道还将代码部署到非生产环境。

>[!NOTE]
>
>在管道的关联 Git 存储库具有至少一个分支且[项目设置](/help/getting-started/program-setup.md)完成之前，无法设置管道。请参阅 [Cloud Manager 存储库](/help/managing-code/repositories.md)文档，了解如何在 Cloud Manager 中添加和管理存储库。

## 视频教程 {#video-tutorial}

该视频概述了本文档中详述的管道创建过程。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

## 添加非生产管道 {#add-non-production-pipeline}

在设置项目并具有至少一个使用 Cloud Manager UI 的环境后，便可以执行以下步骤来添加非生产管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 中登录 Cloud Manager 并选择适当的组织和项目。

1. 从 Cloud Manager 主屏幕访问管道信息卡。单击&#x200B;**添加**&#x200B;并选择&#x200B;**添加非生产管道**。

   ![添加非生产管道](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**配置**&#x200B;选项卡上，选择要创建的管道类型，即&#x200B;**代码质量管道**&#x200B;或&#x200B;**部署管道**。

   ![选择管道类型](/help/assets/configure-pipelines/add-non-production-pipeline.png)

1. 在&#x200B;**非生产管道名称**&#x200B;字段中提供管道描述。

1. 如果您已选择添加&#x200B;**部署管道**，请从&#x200B;**符合条件的部署环境**&#x200B;下拉列表中选择目标部署环境。

1. 提供管道应从中检索代码的存储库。

   * **存储库** - 此选项定义管道应从中检索代码的 Git 存储库。
   * **Git 分支** – 此选项定义管道应从中检索代码的所选存储库的分支。

1. 定义部署选项。

   1. 在&#x200B;**部署触发器**&#x200B;下，定义将激活管道的事件。

      * **手动** - 使用此选项可手动启动管道。
      * **在 Git 发生更改时** – 只要将承诺添加到配置的 Git 分支，此选项就会启动管道。利用此选项，您仍能根据需要手动启动管道。
   1. 对于部署管道，在&#x200B;**重要量度失败行为**&#x200B;下，定义在任何质量审核出现重要失败时的管道行为。

      * **每次询问** – 这是默认设置，需要对任何重要失败进行手动干预。
      * **立即失败** – 如果选定此选项，则只要发生重要失败，就会取消管道。这实际上是在模拟用户手动拒绝每个失败的情况。
      * **立即继续** – 如果选定此选项，则每当发生重要失败时，管道就会自动继续。这实际上是在模拟用户手动审批每个失败的情况。


1. 单击&#x200B;**保存**&#x200B;以保存管道。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。有关更多详细信息，请参阅[代码部署](/help/using/code-deployment.md)文档。
