---
title: 2021.7.0 版发行说明
description: 可查看本页面以获取Cloud Manager 2021.7.0版的信息
feature: 发行信息
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---

# 2021.7.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.7.0的常规发行说明。

>[!NOTE]
>请参阅[当前发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as a Cloud Service中Cloud Manager的最新发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.7.0的发行日期是2021年7月15日。
下一版本计划于2021年8月12日发布。

## 新增功能 {#whats-new}

* 客户现在能够为其Cloud Manager构建过程使用Azul 8和11个JDK，并且可以选择将其中一个JDK用于与工具链兼容的Maven插件&#x200B;*或*&#x200B;整个Maven进程执行。

* 出站出口IP现在将记录在生成步骤日志文件中。

* “管理Git”按钮已被命名为“访问Git信息”，对话框已被直观刷新。

* 某些意外的拓扑重新配置可能会导致管道执行详细信息页面中不再提供详细的测试报告。

## 错误修复 {#bug-fixes}

* 手动导航到非现有执行的执行详细信息页面不会显示错误，只是显示无休止的加载屏幕。

* 在某些情况下，对于在“站点”性能中使用的失败容器，自动重试将不会在2小时内生效，从而导致测试失败。

## 已知问题 {#known-issues}

切换使用Azul JDK的客户应该注意到，并非所有现有应用程序都会在Azul JDK上编译而不出错。 强烈建议在切换前在本地进行测试。