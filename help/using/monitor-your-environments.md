---
title: 监控您的环境
seo-title: 监控您的环境
description: 'null'
seo-description: 可查看本页，了解Cloud Manager中的系统监控，这是通过观察环境中的各个实例并跟踪每个实例的各种指标来完成的。
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 系统监控 {#system-monitoring}

通过观察 [!UICONTROL Cloud Manager] 环境中的各个实例并跟踪每个实例的各种指标，进行系统监视。每个指标都有两个定义的阈值-一个 *警告阈值* 和一个 *关键阈值*。

如果某个指标超出关键阈值，则将其视为关键状态；如果某个指标超过其警告阈值(但低于其关键阈值)，则视为处于警告状态。阈值由Adobe Managed Services设置，并可进行可视化 [!UICONTROL Cloud Manager]。在大多数情况下，客户之间的阈值是一致的，但有时Adobe Managed Services会修改阈值以符合特定客户要求。应向您的客户成功工程师(CSE)提出有关阈值的问题。

## 导航到System Monitoring {#navigating-system-monitoring}

导航到System Monitoring功能可通过两种方式完成。

1. 登录 **Managed Services-程序** 登录页面。

   ![](assets/ProgramLanding.png)

1. 单击程序卡上的第三个图标。

   ![](assets/program-card.png)

   *或者*,

* 通过 ******报告** 全局导航菜单项导航到系统监视登陆页面 [!UICONTROL Cloud Manager]。


## 系统监视概述页面 {#system-monitoring-overview-page}

“系统监视概述”页面列出了该计划中监控的环境以及跨四个不同类别的关于其高级健康状况的报告：

* **主机**
* **存储**
* **网络**
* **应用程序**

每个类别中的状态是单个指标的摘要-如果某个类别中的任何指标处于关键状态，则整个类别在概述页面的目的下处于关键状态。可以在环境级别和实例级别查看相同的摘要。

![](assets/Reports.png)

>[!NOTE]
>
>默认情况下，导航到此页面时，生产环境实例会可见，但也可以打开其他环境。

## 系统监视详细信息 {#system-monitoring-detail}

要查看特定指标的详细信息，您可以单击左侧导航中的某个类别，或单击某个特定实例的某个类别指示符。每个详细信息页面都会显示该类别中量度的一系列图表。您可以在环境中或特定实例中查看所有实例的量度。您可以使用右上角的下拉框在环境和实例之间切换。

![](assets/System_Monitoring1.png)

左侧的导航将显示当前选定的类别中的可用指标，该类别中有当前选定的环境和实例的数据。

![](assets/System_Monitoring2.png)

单个图将显示数据随时间的状态和图表以及阈值。如果显示多个实例，则每个实例的数据将位于单独的系列上。

![](assets/System-Monitoring3.png)

通过单击图例中的系列，可以在图形上隐藏单个系列。
例如，如果单击警告阈值序列，则只会看到关键阈值。

![](assets/System_Monitoring4.png)

### 指标定义 {#metric-definitions}

**主机**

* 每核心加载：CPU执行的进程的数量，或者正在等待状态(加载1)、五个(load5)和15个(load15)分钟期间。
* 流程计数：当前打开的进程数。
* 用户计数：处于活动状态的Shell会话的用户数。
* 内存使用情况：当前分配的系统内存百分比。
* JVM内存(堆)：分配的Java Heap的大小(在1000000字节中)。
* 旧世代空间：当前分配的JVM旧代内存百分比。

**网络**

* CQ端口检查：以秒为单位访问AEM或调度程序端口的响应时间。创作、发布和调度程序有不同的指标。

**存储**

* 磁盘空间：主机上每个安装点使用的磁盘空间(在Megytes中)。每个安装点都有不同的度量。您至少会看到“/”和“/mnt”的指标，但可能会根据特定的实例配置提供额外的安装点指标。
* 文件夹大小：AEM区段商店：AEM区段商店使用的磁盘空间(以千兆字节为单位)。

**应用程序**

* 复制代理：测试复制事件的时间(以秒为单位)。每个复制代理都有单独的指标。
* 调度程序刷新：调度程序刷新队列中当前的项目数。

## SLA报表 {#sla-reporting}

客户可以看到其生产AEM环境相对于合同服务水平协议(SLA)的性能。此操作可通过“报告”屏幕上的子菜单获得。
例如，下图显示了2018年SLA的月度获取情况。

![](assets/sla-reporting1.png)

与系统监视图一样，滚动数据点会显示该月的特定值。

![](assets/sla-reporting2.png)

此图下的“活动分析”部分显示了在当前选定年份内该计划发生的事件集。每个事件都有一个时间范围、一个原因和一组注释。

![](assets/sla-reporting3.png)

## SLA指标 {#sla-metrics}

* **作者合同**：这是您在与Adobe Managed Services订立合同时为作者层定义的SLA。

* **AMS作者SLA**：这是由Adobe或我们的供应商造成的生产创作层因数事件的评估时间。

* **作者SLA**：这是作者层忽略预定停机时间的测量时间，如维护窗口。

* **最终用户合同**：这是您与Adobe Managed Services订立的发布层合同中定义的SLA。

* **AMS最终用户SLA**：这是由Adobe或我们的供应商造成的生产发布层因数事件的测量正常运行时间。

* **最终用户SLA**：这是发布层忽略预定停机时间的测量时间，如维护窗口。