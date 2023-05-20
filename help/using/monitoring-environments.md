---
title: 监控环境
description: 了解如何在 Cloud Manager 中监控环境。
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 100%

---


# 监控环境 {#monitoring-environments}

了解如何在 Cloud Manager 中监控环境。

## 量度阈值 {#thresholds}

在 [!UICONTROL Cloud Manager] 中，通过观察环境中的各个实例并跟踪每个实例的各种量度来监控系统。每个量度都有两个定义的阈值：警告阈值和关键阈值。

如果量度超过其关键阈值，则将被视为处于关键状态。如果量度超过其警告阈值（但低于其关键阈值），则将被视为处于警告状态。阈值由 Adobe Managed Services 设置，并且可以在 [!UICONTROL Cloud Manager] 中进行可视化。在大多数情况下，客户之间的阈值是一致的，但在某些情况下，Adobe Managed Services 将修改阈值以符合特定的客户要求。应直接向您的客户成功工程师 (CSE) 咨询有关阈值的问题。

## 访问系统监控功能 {#accessing-system-monitoring}

执行以下步骤可访问系统监控功能。

1. 登录到 **Managed Services - 项目**&#x200B;登陆页面。

   ![Managed Services 项目](/help/assets/ProgramLanding.png)

1. 单击项目信息卡上的第四个图标。

   ![设置](/help/assets/first-timea1.png)


或者，您可以通过 [!UICONTROL Cloud Manager] 中的&#x200B;**报告**&#x200B;全局导航菜单来导航到&#x200B;**系统监控**&#x200B;登陆页面。

## 系统监控概述 {#system-monitoring-overview}

系统监控概述页面列出了项目中受监控的环境，并报告了跨四个独立类别的高级别运行状况：

* 主机
* 存储
* 网络
* 应用程序

每个类别中的状态均为各个量度的摘要。如果某个类别中的任意量度处于关键状态，则对于概述页面而言，整个类别都处于关键状态。可以在环境级别和实例级别查看同一摘要。

![系统监控概述](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>默认情况下，在导航到此页面时，生产环境实例是可见的，也可以查看其他环境。

## 系统监控详细信息 {#system-monitoring-detail}

要查看特定量度的详细信息，您可以单击左侧导航中的某个类别或单击特定实例的类别指示器之一。每个详细信息页面均显示该类别中量度的一系列图表。您可以查看环境中所有实例或某个特定实例的量度。您可以使用右上角的下拉框在环境和实例之间切换。

![选择环境](/help/assets/System_Monitoring1.png)

左侧导航将显示当前所选类别中的可用量度，其中包含当前所选环境和实例的数据。

![监控量度](/help/assets/System_Monitoring2.png)

单个图表将显示状态和一段时间内的数据图表以及阈值。如果显示多个实例，则每个实例的数据将位于一个单独的系列中。

![量度图表](/help/assets/Monitoring_Graphs1.png)

通过单击图例中的系列，可以在图表上隐藏该系列。例如，如果您单击警告阈值系列，则您将只看到关键阈值。

![修改图表](/help/assets/Monitoring_Graphs2.png)

### 量度定义 {#metric-definitions}

#### 主机 {#host}

* **每核心负载**：CPU 正在执行或处于等待状态的进程数在一 (load1)、五 (load5) 和十五 (load15) 分钟时段内的平均值
* **进程计数**：当前打开的进程数
* **用户计数**：具有活动 shell 会话的用户的数量
* **内存使用**：当前分配的系统内存的百分比
* **JVM 内存**：分配的 Java 堆的大小（以 MB 为单位）
* **旧一代空间**：当前分配的 JVM 旧一代内存的百分比

#### 网络 {#network}

* **CQ 端口检查**：访问 AEM 或 Dispatcher 端口的响应时间（以秒为单位）
   * 创作、发布和 Dispatcher 具有不同的量度。

#### 存储 {#storage}

* **磁盘空间**：主机上每个挂载点的已用磁盘空间（以 MB 为单位）
   * 每个挂载点具有不同的量度。
   * 至少有 `/` 和 `/mnt` 的量度，但根据具体的实例配置，可能会提供额外的挂载点量度。
* **文件夹大小**
* **AEM 区段存储**：AEM 区段存储的已用磁盘空间（以 GB 为单位）

#### 应用程序 {#application}

* **复制代理**：测试复制事件所用的时间（以秒为单位）
   * 每个复制代理均具有单独的量度。
* **Dispatcher 刷新**：当前位于 Dispatcher 刷新队列中的项目数

## SLA 报告 {#sla-reporting}

客户可以查看签订的服务水平协议 (SLA) 下的生产 AEM 环境的性能。这可以通过&#x200B;**报告**&#x200B;屏幕上的子菜单实现。

以下图表显示了 2018 年的月度 SLA 达到情况。

![SLA 2018 图表](/help/assets/SLA-Reports-one.png)

与使用系统监控图表时一样，滚存数据点可显示该月的具体值。

![数据点滚存](/help/assets/SLA-Reports-two.png)

此图表下的&#x200B;**事件分析**&#x200B;部分显示在当前选定年份中发生的与项目相关的事件集。每个事件均具有一个时间范围、一个原因和一组注释。

![事件分析](/help/assets/sla-reporting3.png)

## SLA 量度 {#sla-metrics}

* **作者合同**：这是您与 Adobe Managed Services 签订的合同中为创作层定义的 SLA。
* **AMS 作者 SLA**：这是测量出的由 Adobe 或我们的供应商引起的生产创作层保理事件的正常运行时间。
* **作者 SLA**：这是测量出的创作层的正常运行时间，忽略了计划的停机时间，例如维护时段。
* **最终用户合同**：这是您与 Adobe Managed Services 签订的合同中为发布层定义的 SLA。
* **AMS 最终用户 SLA**：这是测量出的由 Adobe 或我们的供应商引起的生产发布层保理事件的正常运行时间。
* **最终用户 SLA**：这是测量出的发布层的正常运行时间，忽略了计划的停机时间，例如维护时段。

## 视频教程 {#video-tutorial}

本视频概述了使用 Cloud Manager 报告生成的图表来查看项目环境。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
