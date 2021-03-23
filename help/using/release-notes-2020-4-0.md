---
title: 2020.4.0 版发行说明
seo-title: AEM Cloud Manager 2020.4.0发行说明
description: 可查看本页以获取Cloud Manager 2020.4.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.4.0版的信息
feature: 发行信息
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 38%

---

# 2020.4.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2020.4.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.4.0的发布日期为2020年4月09日。

## 新增功能 {#whats-new}

* 对导航云管理器概述页面所做的更改允许用户编辑或切换项目。
* 更改让用户能够从 Cloud Manager 登陆页面上的项目卡片编辑项目。
* 根据与管道关联的环境，会显示新的管道状态&#x200B;**管道正在运行**。
* 改进了管道执行页面的可理解性。这包括管道名称（仅限非生产管道）和类型的显示，以及一个徽章，用于指示管道状态是否为“进行中/已取消/失败”。
* 提高了用于生成 Git 密码的进程弹性，以应对基础服务层中的问题。

## 错误修复 {#bug-fixes}

* 监视数据有时可能以不正确的方式显示，或者根据技术值的微小差异根本不显示。
* 更新了生成容器中使用的 Maven 配置，以避免下载伪像元数据时出现死锁。
* 资产性能测试过程有时无法解密AEM密码，导致测试失败。
* 某些具有备用实例的拓扑在安全测试中可能具有错误负值。
* 如果舞台环境包含一个已停止的实例，则安全测试步骤有时会失败。
* 不能终如收到 Experience Cloud 通知。

