---
title: 管理管道
description: 了解如何管理现有管道，包括编辑、运行和删除它们。
exl-id: e36420d2-57c5-4375-99fb-dd47c1c8bffd
source-git-commit: 28ab641ec85335d8330aeb465c07bf0264218fe4
workflow-type: ht
source-wordcount: '807'
ht-degree: 100%

---


# 管理管道 {#managing-pipelines}

了解如何管理现有管道，包括编辑、运行和删除它们。

## 管道信息卡 {#pipeline-card}

Cloud Manager 中的&#x200B;**项目概述**&#x200B;页面上的&#x200B;**管道**&#x200B;信息卡概述了您的所有管道及其当前状态。

![Cloud Manager 中的管道信息卡](/help/assets/configure-pipelines/pipelines-card.png)

通过单击每个管道旁边的省略号按钮，可以执行以下操作。

* [运行管道](#running-pipelines)
* [编辑管道](#editing-pipelines)
* [删除管道](#deleting-pipelines)
* [查看详细信息](#view-details)

管道列表的底部提供了常规选项。

* **添加** – 用于[添加新的生产管道](/help/using/production-pipelines.md)或[添加新的非生产管道](/help/using/non-production-pipelines.md)
* **全部显示** – 将用户转至&#x200B;**管道**&#x200B;屏幕以在更详细的表中查看所有管道
* **访问存储库信息** – 显示访问 Cloud Manager Git 存储库所需的信息
* **了解详情** – 导航到 CI/CD 管道文档资源。

## 管道窗口 {#pipelines}

**管道**&#x200B;窗口显示所选项目的所有管道的完整列表。此列表很有用，因为它提供的信息比[管道信息卡](#pipeline-card)中的信息更全面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面中，点按或单击&#x200B;**管道**&#x200B;选项卡以切换到&#x200B;**管道**&#x200B;窗口。

1. 在这里，您可以看到项目的所有管道的列表，以及启动和停止管道执行，就像在&#x200B;**管道信息卡**&#x200B;中一样。

如果管道正在执行，则将鼠标悬停在其&#x200B;**状态**&#x200B;列上将显示有关执行的详细信息。

![管道执行详细信息](/help/assets/configure-pipelines/pipeline-status.png)

点按或单击&#x200B;**查看详细信息**&#x200B;将转至[管道执行的详细信息。](#view-details)

## 活动窗口 {#activity}

**活动**&#x200B;窗口显示所选项目的所有管道执行的完整列表。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从&#x200B;**项目概述**&#x200B;页面中，点按或单击&#x200B;**活动**&#x200B;选项卡以切换到&#x200B;**活动**&#x200B;窗口。

1. 在这里，您可以看到项目的所有管道执行的列表，包括当前执行和历史执行。

如果管道正在执行，则将鼠标悬停在其&#x200B;**状态**&#x200B;列上将显示有关执行的详细信息。

![管道执行详细信息](/help/assets/configure-pipelines/pipeline-activity.png)

点按或单击&#x200B;**查看详细信息**&#x200B;将转至[管道执行的详细信息。](#view-details)

## 运行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航到&#x200B;**项目概述**&#x200B;页面中的&#x200B;**管道**&#x200B;信息卡，并单击要运行的管道旁边的省略号按钮，然后从菜单中选择&#x200B;**运行**。

1. 管道将开始运行，并在&#x200B;**状态**&#x200B;栏中显示运行状态。

您可以通过再次单击省略号按钮并选择&#x200B;**[查看详细信息](#view-details)**&#x200B;来查看运行的详细信息。

根据管道类型，您可以通过再次单击省略号按钮并选择&#x200B;**取消**&#x200B;来取消运行。

## 编辑管道 {#editing-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航到&#x200B;**项目概述**&#x200B;页面中的&#x200B;**管道**&#x200B;信息卡，并单击要编辑的管道旁边的省略号按钮，然后从菜单中选择&#x200B;**编辑**。

1. 这将显示&#x200B;**编辑生产管道**&#x200B;或&#x200B;**编辑非生产管道**&#x200B;对话框，您可在其中编辑在创建管道时输入的相同详细信息。

   * 有关对管道可用的所有字段和配置选项的详细信息，请参阅以下页面。
      * [配置生产管道](/help/using/production-pipelines.md)
      * [配置非生产管道](/help/using/non-production-pipelines.md)

1. 在编辑完管道后，单击&#x200B;**更新**。

>[!NOTE]
>
>您无法编辑运行中的管道。

## 删除管道 {#deleting-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航到&#x200B;**项目概述**&#x200B;页面中的&#x200B;**管道**&#x200B;信息卡，并单击要删除的管道旁边的省略号按钮，然后从菜单中选择&#x200B;**删除**。

>[!NOTE]
>
>您无法删除运行中的管道。

## 查看详细信息 {#view-details}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航到&#x200B;**项目概述**&#x200B;页面中的&#x200B;**管道**&#x200B;信息卡，并单击运行的管道旁边的省略号按钮，然后从菜单中选择&#x200B;**查看详细信息**。

1. 您将转到运行中的管道的详细信息页面。

![管道详细信息](/help/assets/configure-pipelines/pipeline-running-details.png)

在此页面中，您可以查看管道各个步骤的状态并检索构建日志以进行诊断。 有关更多信息，请参阅[代码部署](/help/using/code-deployment.md)文档。

管道执行中的所有步骤都将显示，而尚未开始的步骤将灰显。已完成的步骤将显示其持续时间。

管道步骤完成后，将显示摘要。

![步骤摘要](/help/assets/configure-pipelines/pipeline-step.png)

点按或单击&#x200B;**查看详细信息**&#x200B;链接以显示&#x200B;**持续时间**&#x200B;部分。这包括基于该项目的历史趋势的管道的平均持续时间。

![持续时间](/help/assets/configure-pipelines/duration.png)

>[!NOTE]
>
>您只能查看运行中的或已运行至少一次的管道的详细信息。
