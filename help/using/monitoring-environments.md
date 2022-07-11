---
title: 监控环境
description: 了解如何在Cloud Manager中监控环境。
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# 监控环境 {#monitoring-environments}

了解如何在Cloud Manager中监控环境。

## 量度阈值 {#thresholds}

中的系统监控 [!UICONTROL Cloud Manager] 可通过观察环境中的各个实例并跟踪每个实例的各种量度来完成。 每个量度具有两个定义的阈值：警告阈值和严重阈值。

如果量度超过其临界阈值，则会认为该量度处于临界状态。 如果量度超过其警告阈值（但低于其关键阈值），则会认为该量度处于警告状态。 阈值由Adobe Managed Services设置，可在 [!UICONTROL Cloud Manager]. 在大多数情况下，阈值在客户之间是一致的，但在某些情况下，Adobe Managed Services将修改阈值以符合特定客户要求。 有关阈值的问题应当发送给您的客户成功工程师(CSE)。

## 访问系统监控 {#accessing-system-monitoring}

按照以下步骤访问“System Monitoring（系统监控）”。

1. 登录到 **Managed Services — 计划** 登陆页面。

   ![托管服务方案](/help/assets/ProgramLanding.png)

1. 单击项目卡上的第四个图标。

   ![设置](/help/assets/first-timea1.png)


或者，您也可以导航到 **系统监控** 登陆页面 **报表** 全局导航菜单项 [!UICONTROL Cloud Manager].

## 系统监控概述 {#system-monitoring-overview}

“系统监控概述”页列出了计划中受监控的环境，并报告了这四个不同类别的高级运行状况：

* 主机
* 存储
* 网络
* 应用程序

每个类别中的状态都是单个量度的摘要。 如果某个类别中的任何量度处于关键状态，则对于概述页面而言，整个类别都处于关键状态。 可以在环境级别和实例级别查看相同的总结。

![系统监控概述](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>默认情况下，在导航到此页面时，生产环境实例是可见的，但也可以查看其他环境。

## 系统监控详细信息 {#system-monitoring-detail}

要查看特定量度的详细信息，您可以单击左侧导航中的某个类别，或单击特定实例的某个类别指示器。 每个详细信息页面都会显示该类别中量度的一系列图表。 您可以查看环境中所有实例的量度，也可以查看特定实例的量度。 您可以使用右上角的下拉框在环境和实例之间切换。

![选择环境](/help/assets/System_Monitoring1.png)

左侧的导航将显示当前选定类别中的可用量度，其中包含当前选定环境和实例的数据。

![监控量度](/help/assets/System_Monitoring2.png)

单个图表将显示一段时间内的数据状态和图表以及阈值。 如果显示多个实例，则每个实例的数据将位于单独的系列中。

![量度图](/help/assets/Monitoring_Graphs1.png)

通过单击图例中的系列，可以在图表上隐藏单个系列。
例如，如果单击警告阈值系列，您将只看到严重阈值。

![修改图表](/help/assets/Monitoring_Graphs2.png)

### 量度定义 {#metric-definitions}

#### 主机 {#host}

* **每个核心的负载**:CPU正在执行或处于等待状态的进程数，平均在1（负载1）、5（负载5）和15（负载15）分钟时段内
* **进程计数**:当前打开的进程数
* **用户计数**:具有活动Shell会话的用户数
* **内存使用率**:当前分配的系统内存百分比
* **JVM内存**:分配的Java堆的大小(MB)
* **老一代空间**:当前分配的JVM旧代内存的百分比

#### 网络 {#network}

* **CQ端口检查**:访问AEM或Dispatcher端口的响应时间（以秒为单位）
   * 创作、发布和调度程序有不同的量度。

#### 存储 {#storage}

* **磁盘空间**:主机上每个装载点的已用磁盘空间（以MB为单位）
   * 每个装入点有不同的量度。
   * 至少有 `/` 和 `/mnt`，但其他装入点量度可能会根据特定实例配置而可用。
* **文件夹大小**
* **AEM区段存储**:AEM区段存储的已用磁盘空间（以GB为单位）

#### 应用程序 {#application}

* **复制代理**:测试复制事件的时间（以秒为单位）
   * 每个复制代理都有不同的量度。
* **调度程序刷新**:调度程序刷新队列中的当前项目数

## SLA 报告 {#sla-reporting}

客户能够看到其生产AEM环境相对于其合同服务级别协议(SLA)的性能。 可通过 **报表** 屏幕。

下图显示了2018年的月度SLA达到情况。

![SLA 2018图](/help/assets/SLA-Reports-one.png)

与系统监控图一样，滚动数据点会显示当月的特定值。

![数据点滚动](/help/assets/SLA-Reports-two.png)

的 **事件分析** 此图下的部分显示在当前选定年份中针对程序发生的事件集。 每个事件都有一个时间范围、原因和一组注释。

![事件分析](/help/assets/sla-reporting3.png)

## SLA量度 {#sla-metrics}

* **作者合同**:这是您与Adobe Managed Services签署的合同中为创作层定义的SLA。
* **AMS创作SLA**:这是由Adobe或我们的供应商造成的生产创作层保理事件的正常运行时间。
* **创作SLA**:这是创作层的正常运行时间测量值，它忽略计划的停机时间（如维护时间）。
* **最终用户合同**:这是您与Adobe Managed Services签署的发布层合同中定义的SLA。
* **AMS最终用户SLA**:这是由Adobe或我们的供应商造成的生产发布层保理事件的正常运行时间。
* **最终用户SLA**:这是发布层的测量正常运行时间，忽略计划的停机时间（如维护时间）。

## 视频教程 {#video-tutorial}

此视频提供并概述了如何使用Cloud Manager报表生成的图表来查看您的项目环境。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
