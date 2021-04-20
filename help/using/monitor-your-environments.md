---
title: 监视环境
seo-title: 监视环境
description: 了解如何在Cloud Manager中监控环境
seo-description: 可查看本页以了解有关Cloud Manager中的系统监视的信息，具体方法是观察某个环境中的各个实例并跟踪每个实例的各种量度。
feature: Environments
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# 系统监视{#system-monitoring}

[!UICONTROL Cloud Manager]中的系统监视是通过观察环境中的单个实例并跟踪每个实例的各种度量来完成的。 每个量度具有两个定义的阈值 — *警告阈值*&#x200B;和&#x200B;*严重阈值*。

如果某个量度超过其临界阈值，则被视为处于临界状态；如果量度超过其警告阈值（但低于其严重阈值），则它被视为处于警告状态。 阈值由Adobe Managed Services设置，可在[!UICONTROL Cloud Manager]中进行可视化。 在大多数情况下，客户之间的阈值是一致的，但在某些情况下，Adobe Managed Services将修改阈值以符合特定客户要求。 有关阈值的问题应提交给您的客户成功工程师(CSE)。

## 导航到系统监视{#navigating-system-monitoring}

导航到“系统监视”功能可通过两种方式完成。

1. 登录到&#x200B;**Managed Services -项目**&#x200B;登陆页。

   ![](assets/ProgramLanding.png)

1. 单击项目卡上的第四个图标。

   ![](assets/first-timea1.png)

   *或者*,

* 通过[!UICONTROL Cloud Manager]中的&#x200B;**报告**&#x200B;全局导航菜单项，导航到&#x200B;**系统监视**&#x200B;登陆页。


## “系统监视概述”页{#system-monitoring-overview-page}

“系统监视概述”页列表项目中被监视的环境，并在四个不同的类别中报告其高级运行状况：

* **主机**
* **存储**
* **网络**
* **应用程序**

每个类别的状态是单个量度的摘要 — 如果某个类别中的任何量度处于关键状态，则整个类别处于关键状态，以用于概述页面。 可以在环境级和实例级查看相同的摘要。

![](assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>默认情况下，当导航到此页时，生产环境实例是可见的，但也可以打开其他环境。

## 视频教程{#video-tutorial}

### Cloud Manager报表概述{#reports-video}

Cloud Manager报表通过一组图表向项目的环境和AEM实例提供视图，这些图表报告并跟踪每个AEM实例的各种量度。
有关更多详细信息，请参阅以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)

## 系统监视详细信息{#system-monitoring-detail}

要视图特定量度的详细信息，您可以单击左侧导航中的某个类别，或单击特定实例的某个类别指示器。 每个详细信息页面都显示该类别中量度的一系列图表。 您可以视图环境中所有实例的量度，也可以对特定实例进行量度。 您可以使用右上角的下拉框在环境和实例之间切换。

![](assets/System_Monitoring1.png)

左侧的导航将显示当前选定类别中的可用量度，其中有当前选定环境和实例的数据。

![](assets/System_Monitoring2.png)

单个图表将显示随时间变化的数据状态和图表以及阈值。 如果显示多个实例，则每个实例的数据将位于一个单独的系列中。

![](assets/Monitoring_Graphs1.png)

单击图例中的系列可在图形上隐藏单个系列。
例如，如果单击警告阈值系列，则只会看到严重阈值。

![](assets/Monitoring_Graphs2.png)

### 量度定义{#metric-definitions}

**主机**

* 每个核心的加载：由CPU执行或处于等待状态的进程数，平均在1(load1)、5(load5)和15(load15)分钟时间内。
* 进程计数：当前打开的进程数。
* 用户计数：具有活动shell会话的用户数。
* 内存使用：当前分配的系统内存百分比。
* JVM内存（堆）：分配的Java堆的大小（以兆字节为单位）。
* 老一代空间：当前分配的JVM旧代内存百分比。

**网络**

* CQ端口检查：访问AEM或调度程序端口的响应时间（秒）。 创作、发布和调度程序有不同的量度。

**存储**

* 磁盘空间：主机上每个装载点的已用磁盘空间（以MB为单位）。 每个装入点有不同的量度。 您至少会看到“/”和“/mnt”的量度，但根据特定实例配置，可能会有其他装入点量度可用。
* 文件夹大小：AEM区段商店：AEM区段存储的已用磁盘空间(GB)。

**应用程序**

* 复制代理：测试复制事件的时间（以秒为单位）。 每个复制代理都有单独的量度。
* 调度程序刷新：调度程序刷新队列中当前的项目数。

## SLA报告{#sla-reporting}

客户能够看到其生产AEM环境相对于其合同服务水平协议(SLA)的性能。 可通过“报告”屏幕上的子菜单执行此操作。
例如，下图显示了2018年的月度SLA达到情况。

![](assets/SLA-Reports-one.png)

与系统监视图一样，滚动数据点可显示该月的特定值。

![](assets/SLA-Reports-two.png)

此图表下的事件分析部分显示在当前选定年份内为项目发生的事件集。 每个事件都有一个时间范围、原因和一组注释。

![](assets/sla-reporting3.png)

## SLA量度{#sla-metrics}

* **作者合同**:这是您与Adobe Managed Services的合同中为创作层定义的SLA。

* **AMS作者SLA**:这是由Adobe或我们的供应商造成的生产作者层保理事件的可衡量正常运行时间。

* **作者SLA**:这是作者层的可测量正常运行时间，忽略计划停机时间（如维护窗口）。

* **最终用户合同**:这是您与Adobe Managed Services的合同中为发布层定义的SLA。

* **AMS最终用户SLA**:这是由Adobe或我们的供应商引起的生产发布层保理事件的可衡量正常运行时间。

* **最终用户SLA**:这是发布层的可测量正常运行时间，忽略计划停机（如维护窗口）。