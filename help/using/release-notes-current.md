---
title: 2021.11.0 版发行说明
description: 请阅读本页以了解Cloud Manager版本2021.11.0的相关信息
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0395fd4263ae37bce49c698e8e72ad7b08af046a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# 2021.10.0 版发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 版本2021.11.0。

>[!NOTE]
>请参阅 [最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) 以在AEMas a Cloud Service中查看Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 版本2021.11.0为2021年11月04日。
下一版本计划于2021年12月9日发布。

## 新增功能 {#whats-new}

* Git提交ID现在将显示在管道执行详细信息中，从而更便于跟踪已构建的代码。

* 的 `x-request-id` 响应标头现在在API操场上可见 [www.adobe.io](https://www.adobe.io/). 提交客户关怀问题以进行疑难解答时，此标题非常有用。

* 作为用户，我看到带零管道的管道卡为我提供了适当的指导。

* 现在提供了一个新的“管道”页面，该页面上提供了悬停时的状态弹出窗口，以便轻松查看详细信息摘要。 可以查看管道执行及其关联的详细信息。

* 编辑管道API现在支持设置调度程序失效和刷新路径。

* 编辑管道API现在支持更改部署阶段中使用的环境。

* OakPal扫描过程中对大型包进行了优化。

* 质量问题CSV文件现在将包含每个质量问题的时间戳。

* “环境”页面中的“管理”按钮在UI中将不再可见。

## 错误修复 {#bug-fixes}

* 某些非正统的生成配置会导致不必要的文件存储在管道的Maven对象缓存中，这会在启动和停止生成容器时导致不重要的网络I/O。

* 如果部署阶段不存在，则管道PATCHAPI会失败。

* 的 `ClientlibProxyResourceCheck` 当存在具有通用基本路径的客户端库时，质量规则会产生误报问题。

* 达到最大存储库数时的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。
