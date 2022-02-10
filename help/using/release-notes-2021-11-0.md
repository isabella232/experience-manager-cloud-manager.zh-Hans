---
title: 2021.11.0 版发行说明
description: 请阅读本页以了解Cloud Manager版本2021.11.0的相关信息
feature: Release Information
source-git-commit: 099a4490e3a8578b9f3485fd1514d1e97db977ab
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 75%

---

# 2021.11.0 版发行说明 {#release-notes-for}

以下部分概述了 [!UICONTROL Cloud Manager] 版本2021.11.0。

>[!NOTE]
>请参阅 [最新发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) 以在AEMas a Cloud Service中查看Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 版本2021.11.0为2021年11月04日。
下一版本计划于2021年12月16日发布。

## 新增功能 {#whats-new}

* Git Commit ID 现在将显示在管道执行详细信息中，以便更轻松地跟踪已生成的代码。

* `x-request-id` 响应标头现已在 [www.adobe.io](https://www.adobe.io/) 上的 API Playground 中可见。在提交客户关怀问题以进行疑难解答时，此标头很有用。

* 作为用户，我发现不带管道的管道信息卡为我提供了适当的指导。

* 现在软件提供了一个新的活动页面，可以在其中查看管道和代码执行等活动及其相关详细信息。随着时间的推移，此页面中列出的活动的范围将随着提供的详细信息而扩大。

* 现在提供了带悬停弹出框的新管道页面，以便轻松查看详细信息摘要。可以查看管道执行及其相关详细信息。

* 编辑管道API现在支持设置调度程序失效和刷新路径。

* Edit Pipeline API 现在支持更改部署阶段使用的环境。

* 已针对大型包在 OakPal 扫描过程中引入了优化。

* 质量问题 CSV 文件现在将包含每个质量问题的时间戳。

* “环境”页面中的“管理”按钮在UI中将不再可见。

## 错误修复 {#bug-fixes}

* 某些非正统的生成配置会导致在管道的 Maven 构件缓存中存储不必要的文件，这会在启动和停止生成容器时导致产生无关的网络 I/O。

* 如果部署阶段不存在，则管道 PATCH API 将失败。

* 如果存在带公共基本路径的客户端库，则 `ClientlibProxyResourceCheck` 质量规则会产生误报问题。

* 达到最大存储库数时显示的错误消息未指定错误原因。

* 在极少数情况下，管道因某些响应代码的重试处理不当而失败。
