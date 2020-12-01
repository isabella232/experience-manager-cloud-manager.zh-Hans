---
title: 2020.11.0 版发行说明
seo-title: AEM Cloud Manager 2020.11.0发行说明
description: 可查看本页以获取Cloud Manager Release 2020.11.0的信息
seo-description: 可查看本页以获取AEM Cloud Manager 2020.11.0版的相关信息
translation-type: tm+mt
source-git-commit: 30d782f5a095b1b07ec4f2039def9ba30a559325
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 7%

---

# 2020.11.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2020.11.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.11.0的发布日期为2020年11月12日。

## 新增功能 {#whats-new}

* Cloud Manager中的&#x200B;**学习**&#x200B;选项卡会用UI中的新图像刷新。

## 错误修复 {#bug-fixes}

* 现在，某些客户导致的部署错误将在部署日志中显式显示。

* 需要下载Maven插件，才能加载执行构建之前完成的依赖项。

* 现在，从Cloud Manager页脚中选择语言的链接将导航到正确的位置。

* 有时，在代码扫描过程中，SonarQube进程不会开始。 现在将自动检测并尝试重新启动。

* 在性能测试中使用的站点爬网过程中，将自动重试在前三个深度遍历级别中超时的请求。