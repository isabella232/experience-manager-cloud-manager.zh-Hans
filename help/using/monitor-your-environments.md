---
title: Monitor your Environments
seo-title: Monitor your Environments
description: 'null'
seo-description: Follow this page to learn about System Monitoring in Cloud Manager that is done by observing the individual instances within an environment and tracking a variety of metrics for each instance.
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---


# System Monitoring {#system-monitoring}

System Monitoring in  is done by observing the individual instances within an environment and tracking a variety of metrics for each instance. [!UICONTROL Cloud Manager]Each metric has two defined thresholds – a warning threshold and a critical threshold.****

If a metric is over its critical threshold, it is considered to be in a critical state; if a metric is over its warning threshold (but below its critical threshold), it is considered to be in a warning state. The thresholds are set by Adobe Managed Services and can be visualized in . [!UICONTROL Cloud Manager]In most cases, thresholds are consistent between customers, but there are cases where Adobe Managed Services will modify thresholds to match specific customer requirements. 有关阈值的问题应提交给您的客户成功工程师(CSE)。

## 导航到系统监视 {#navigating-system-monitoring}

导航到“系统监视”功能可通过两种方式完成。

1. Log in to Managed Services - Programs landing page.****

   ![](assets/ProgramLanding.png)

1. 单击程序卡上的第三个图标。

   ![](assets/program-card.png)

   *或者*,

* 通过Reports全局 **导航菜单项** ，导航到 **System Monitoring登录页面**[!UICONTROL Cloud Manager]。


## “系统监视：概述”页 {#system-monitoring-overview-page}

“系统监视概述”页列出了计划中受监视的环境，并报告了四个不同类别的高级别健康状况：

* **主机**
* **存储**
* **网络**
* **应用程序**

每个类别的状态是单个度量的摘要——如果某个类别中的任何度量处于关键状态，则在概述页面中，整个类别都处于关键状态。 可以在环境级别和实例级别查看相同的摘要。

![](assets/Reports.png)

>[!NOTE]
>
>默认情况下，在导航到此页面时，生产环境实例是可见的，但也可以打开其他环境。

## 系统监视详细信息 {#system-monitoring-detail}

要查看特定度量的详细信息，您可以单击左侧导航中的某个类别，或单击特定实例的某个类别指示符。 每个详细信息页面都显示该类别中度量的一系列图形。 您可以查看环境中所有实例的度量或特定实例的度量。 您可以使用右上角的下拉框在环境和实例之间切换。

![](assets/System_Monitoring1.png)

左侧的导航将显示当前选定类别中的可用度量，其中存在当前选定环境和实例的数据。

![](assets/System_Monitoring2.png)

单个图将显示随时间变化的数据状态和图形以及阈值。 如果显示多个实例，则每个实例的数据将位于单独的序列中。

![](assets/Monitoring_Graphs1.png)

单击图例中的系列可在图形上隐藏单个系列。
例如，如果单击警告阈值系列，您将只看到关键阈值。

![](assets/Monitoring_Graphs2.png)

### 度量定义 {#metric-definitions}

**主机**

* 每个核心的负载：由CPU执行或处于等待状态的进程数平均在一个(load1)、五(load5)和十五(load15)分钟周期上。
* 进程计数：当前打开的进程数。
* 用户计数：具有活动Shell会话的用户数。
* 内存使用：当前分配的系统内存百分比。
* JVM内存（堆）:分配的Java堆的大小（以兆字节为单位）。
* 老一代空间：当前分配的JVM旧代内存百分比。

**网络**

* CQ Port Check: The response time in seconds to access the AEM or Dispatcher port. 创作、发布和调度程序有不同的指标。

**存储**

* Disk Space: The used disk space (in Megabytes) for each mount point on the host. There are different metrics for each mount point. At minimum, you will see metrics for "/" and "/mnt", but additional mount point metrics may be available depending on the specific instance configuration.
* Folder Size: AEM Segment Store: The used disk space (in Gigabytes) for the AEM Segment Store.

**应用程序**

* Replication Agent: The time, in seconds, for a test replication event. There are separate metrics for each replication agent.
* Dispatcher Flush: The number of items currently in the dispatcher flush queue.

## SLA Reporting {#sla-reporting}

Customers are able to see the performance of their production AEM environment relative to their contracted Service Level Agreement (SLA). This is available through a sub-menu on the Reports screen.
For example, the graph below shows the monthly SLA attainment for 2018.

![](assets/sla-reporting1.png)

As with the system monitoring graphs, rolling over a data point shows the specific values for that month.

![](assets/sla-reporting2.png)

The Event Analysis section under this graph shows the set of incidents which occurred for the program during the currently selected year. 每个事件都有一个时间范围、一个原因和一组注释。

![](assets/sla-reporting3.png)

## SLA Metrics {#sla-metrics}

* **作者合同**:这是您与Adobe Managed services的合同中为作者层定义的SLA。

* **AMS作者SLA**:这是由Adobe或我们的供应商引起的生产作者层保理事件的可测量正常运行时间。

* **作者SLA**:这是作者层（忽略计划停机时间，如维护窗口）的度量正常运行时间。

* **最终用户合同**:这是您与Adobe Managed services的合同中为发布层定义的SLA。

* **AMS最终用户SLA**:这是由Adobe或我们的供应商引起的生产发布层保理事件的可测量正常运行时间。

* **最终用户SLA**:这是发布层的测量正常运行时间，忽略计划的停机时间（如维护窗口）。