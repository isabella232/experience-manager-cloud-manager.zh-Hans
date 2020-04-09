---
title: 2020.4.0 版发行说明
seo-title: AEM Cloud Manager 2020.4.0版本说明
description: 可查看本页以获取Cloud Manager 2020.4.0版的相关信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2020.4.0版的信息
translation-type: tm+mt
source-git-commit: ee7fc8a23dd0719eda84638c810842c2dc1772bb

---

# 2020.4.0 版发行说明 {#release-notes-for}

以下部分概述了2020.4.0版 [!UICONTROL Cloud Manager] 的一般发行说明。

## Release Date {#release-date}

版本2020.4.0 [!UICONTROL Cloud Manager] 的发布日期为2020年4月9日。

## 新增功能 {#whats-new}

* 对导航Cloud Manager概述页面所做的更改允许用户编辑或切换项目。
* 允许用户从Cloud Manager项目上的项目卡编辑登陆页的更改。
* 新管线状 **态管线运行** ，显示与其关联的环境。
* 改进了管道执行页面的可理解性。 这包括管道名称（仅限非生产管道）和类型的显示，以及指示管道状态是否为“进行中／已取消／失败”的徽章。
* 用于生成Git密码的过程对底层服务层中的问题具有更强的适应性。

## 错误修复 {#bug-fixes}

* 监视数据有时可能以错误的方式显示，或者根据技术值的微小差异根本不显示。
* 更新了构建容器中使用的Maven配置，以避免在下载对象元数据时出现死锁。
* 资产性能测试过程偶尔无法解密AEM密码，导致测试失败。
* 在安全测试中，具有待机实例的某些拓扑可能具有错误的负值。
* 如果舞台环境包含一个已停止的实例，则安全测试步骤有时会失败。
* Experience Cloud通知未得到一致接收。

