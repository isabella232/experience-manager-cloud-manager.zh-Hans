---
title: 管理管道
description: 了解如何管理现有管道，包括编辑、运行和删除这些管道。
index: true
source-git-commit: 099a4490e3a8578b9f3485fd1514d1e97db977ab
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 管理管道 {#managing-pipelines}

了解如何管理现有管道，包括编辑、运行和删除这些管道。

## 管道卡 {#pipeline-card}

的 **管道** 卡 **计划概述** Cloud Manager中的页面概述了所有管道及其当前状态。

![Cloud Manager中的管道卡](/help/using/assets/configure-pipelines/pipelines-card.png)

通过单击每个管道旁边的省略号按钮，您可以执行以下操作。

* [运行管道](#running-pipelines)
* [编辑管道](#editing-pipelines)
* [删除管道](#deleting-pipelines)
* [查看详细信息](#view-details)

在管道列表的底部，有常规选项。

* **添加**  — 至 [添加新的生产管道](configuring-production-pipelines.md) 或 [添加新的非生产管道](configuring-non-production-pipelines.md)
* **显示全部**  — 将用户转到 **管道** 屏幕可查看更详细的表中的所有管线。
* **访问存储库信息**  — 显示访问Cloud Manager git存储库所需的信息
* **了解更多**  — 导航到CI/CD管道文档资源。

## 运行管道 {#running-pipelines}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，然后单击您运行的管道旁边的省略号按钮，选择 **运行** 中。

1. 管道运行开始，并由 **状态** 列。

您可以通过再次单击省略号按钮并选择来查看运行的详细信息 **[查看详细信息。](#view-details)**

根据管道类型，您可能可以通过再次单击省略号按钮并选择来取消运行 **取消**.

## 编辑管道 {#editing-pipelines}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面上，单击您要编辑的管道旁边的省略号按钮，然后选择 **编辑** 中。

1. 的 **编辑生产管道** 或 **编辑非生产管道** 对话框，允许您编辑创建管线时输入的相同详细信息。

   * 有关管道可用的所有字段和配置选项的详细信息，请参阅以下页面。
      * [配置生产管道](configuring-production-pipelines.md)
      * [配置非生产管道](configuring-non-production-pipelines.md)

1. 单击 **更新** 编辑管道后。

>[!NOTE]
>
>无法编辑正在运行的管道。

## 删除管道 {#deleting-pipelines}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，然后单击您运行的管道旁边的省略号按钮，选择 **删除** 中。

>[!NOTE]
>
>无法删除正在运行的管道。

## 查看详细信息 {#view-details}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，然后单击您运行的管道旁边的省略号按钮，选择 **查看详细信息** 中。

1. 您将转到正在运行的管道的详细信息页面。

![管道详细信息](/help/using/assets/configure-pipelines/pipeline-running-details.png)

从此处，您可以查看管道各个步骤的状态，并检索生成日志以用于诊断目的。 查看文档 [部署代码](deploying-code.md) 以了解更多信息。

>[!NOTE]
>
>您只能查看正在运行或至少已运行一次的管道的详细信息。
