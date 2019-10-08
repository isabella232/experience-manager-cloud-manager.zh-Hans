---
title: 监视环境
seo-title: 监视环境
description: 'null'
seo-description: 可查看本页以了解Cloud Manager中的系统监视，具体方法是观察某个环境中的各个实例并跟踪每个实例的各种指标。
translation-type: tm+mt
source-git-commit: 519f43ff16e0474951f97798a8e070141e5c124b

---


# 系统监控 {#system-monitoring}

在中进行系 [!UICONTROL Cloud Manager] 统监视的方法是，观察环境中的各个实例并跟踪每个实例的各种度量。 每个度量都有两个定义的阈值- *警告阈值* 和严 *重阈值*。

如果一个指标超过其临界阈值，则被视为处于临界状态；如果度量超过其警告阈值（但低于其关键阈值），则被视为处于警告状态。 阈值由Adobe Managed services设置，可在中进行可视化 [!UICONTROL Cloud Manager]。 在大多数情况下，客户之间的阈值是一致的，但在某些情况下，Adobe Managed services将修改阈值以符合特定客户要求。 有关阈值的问题应提交给您的客户成功工程师(CSE)。

## 导航到系统监视 {#navigating-system-monitoring}

导航到“系统监视”功能可通过两种方式完成。

1. 登录到 **Managed Services —— 程序登录页** 。

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

## 概述视频到报表 {#video-reports}

Cloud manager报告通过一组图表提供对计划环境和AEM实例的视图，这些图表报告并跟踪每个AEM实例的各种指标。
有关更多详细信息，请参阅以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/26315/?captions=chi_hans)

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

* CQ端口检查：访问AEM或Dispatcher端口的响应时间（以秒为单位）。 创作、发布和调度程序有不同的指标。

**存储**

* 磁盘空间：主机上每个装载点的已用磁盘空间（以兆字节为单位）。 每个装载点有不同的度量。 您至少会看到“/”和“/mnt”的度量，但根据特定实例配置，可能会有其他装载点度量。
* 文件夹大小：AEM区段商店：AEM区段存储的已用磁盘空间（以GB为单位）。

**应用程序**

* 复制代理：测试复制事件的时间（以秒为单位）。 每个复制代理都有单独的度量。
* 调度程序刷新：调度程序刷新队列中当前的项目数。

## SLA报告 {#sla-reporting}

客户能够查看其生产AEM环境相对于其合同服务级别协议(SLA)的性能。 可通过“报告”屏幕上的子菜单执行此操作。
例如，下图显示了2018年的月度SLA水平。

![](assets/sla-reporting1.png)

与系统监视图一样，滚动数据点会显示该月的特定值。

![](assets/sla-reporting2.png)

此图下的“事件分析”部分显示了在当前选定年份为程序发生的事件集。 每个事件都有一个时间范围、一个原因和一组注释。

![](assets/sla-reporting3.png)

## SLA指标 {#sla-metrics}

* **作者合同**:这是您与Adobe Managed services的合同中为作者层定义的SLA。

* **AMS作者SLA**:这是由Adobe或我们的供应商引起的生产作者层保理事件的可测量正常运行时间。

* **作者SLA**:这是作者层（忽略计划停机时间，如维护窗口）的度量正常运行时间。

* **最终用户合同**:这是您与Adobe Managed services的合同中为发布层定义的SLA。

* **AMS最终用户SLA**:这是由Adobe或我们的供应商引起的生产发布层保理事件的可测量正常运行时间。

* **最终用户SLA**:这是发布层的测量正常运行时间，忽略计划的停机时间（如维护窗口）。