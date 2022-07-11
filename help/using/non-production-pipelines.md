---
title: 配置非生产管道
description: 了解如何使用Cloud Manager创建和配置非生产管道以部署您的代码。
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 567a16a032bf80451b5e8ba4e3d842cb617a615f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# 配置非生产管道 {#configuring-non-production-pipelines}

了解如何使用Cloud Manager创建和配置非生产管道以部署您的代码。 如果您首先想要更概念地概述Cloud Manager中管道的工作方式，请参阅此文档 [CI/CD管道。](/help/overview/ci-cd-pipelines.md)

## 概述 {#overview}

使用 **管道** 拼贴 [!UICONTROL Cloud Manager], **部署管理器** 可以创建两种不同类型的管线。

* **生产管道**  — 生产管道是由一系列精心策划的步骤组成的专门构建的管道，从始至终将源代码引入生产。
* **非生产管道**  — 非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境。

本文档重点介绍非生产管道。 有关如何配置生产管道的详细信息，请参阅此文档 [配置生产管道。](/help/using/production-pipelines.md)

非生产管道有两种类型：

* **代码质量管道**  — 这些操作会在git分支中扫描代码，并执行生成和代码质量步骤。
* **部署管道**  — 除了执行构建和代码质量步骤（如代码质量管道）之外，这些管道还会将代码部署到非生产环境。

>[!NOTE]
>
>只有在其关联的git存储库具有至少一个分支和 [程序设置](/help/getting-started/program-setup.md) 完成。 查看文档 [Cloud Manager存储库](/help/managing-code/repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

## 视频教程 {#video-tutorial}

此视频提供了管道创建过程的概述，本文档对该过程进行了详细介绍。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

## 添加非生产管道 {#add-non-production-pipeline}

在您设置了程序并且使用Cloud Manager UI至少拥有一个环境后，便可以按照以下步骤添加非生产管道。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 并选择相应的组织和程序。

1. 从Cloud Manager主屏幕访问管道卡。 单击 **添加** 选择 **添加非生产管道**.

   ![添加非生产管道](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. 在 **配置** 选项卡 **添加非生产管道** 对话框中，选择要创建的管线类型， **代码质量管道** 或 **部署管道**.

   ![选择管道类型](/help/assets/configure-pipelines/add-non-production-pipeline.png)

1. 为 **非生产管道名称** 字段。

1. 如果您选择添加 **部署管道**，从 **符合条件的部署环境** 下拉列表。

1. 提供管道应在其中检索代码的存储库。

   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
   * **Git分支**  — 此选项定义所选管道中应从哪个分支检索代码。

1. 定义部署选项。

   1. 在 **部署触发器**，定义激活管道的事件。

      * **手动**  — 使用此选项手动启动管道。
      * **在Git更改时**  — 每当将提交添加到配置的git分支时，此选项都会启动管道。 通过此选项，您仍可以根据需要手动启动管道。
   1. 对于部署管道，在 **重要量度失败行为**，定义在任何质量门中遇到重要故障时管道的行为。

      * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
      * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
      * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。


1. 单击 **保存** 来保存管道。

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。 请查看文档 [代码部署](/help/using/code-deployment.md) 以了解更多详细信息。
