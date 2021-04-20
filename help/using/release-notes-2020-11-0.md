---
title: 2020.11.0 版发行说明
seo-title: AEM Cloud Manager 2020.11.0发行说明
description: 可查看本页以获取Cloud Manager 2020.11.0版的相关信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.11.0版的信息
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 8%

---

# 2020.11.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2020.11.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.11.0的发布日期为2020年11月12日。

## 新增功能 {#whats-new}

* Cloud Manager中的&#x200B;**学习**&#x200B;选项卡将用UI中的新图像刷新。

## 错误修复 {#bug-fixes}

* 现在，将在部署日志中显式显示某些由客户引起的部署错误。

* 需要下载Maven插件，才能加载执行构建之前完成的依赖项。

* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。

* 有时，在代码扫描过程中，SonarQube进程不会开始。 现在将自动检测并尝试重新启动。

* 在性能测试中使用的站点爬网过程中，将自动重试在前三个深度遍历级别中超时的请求。