---
title: 2019.1.0发行说明
seo-title: 适用于2019.1.0的AEM Cloud Manager发行说明
description: 请参阅本页获取Cloud Manager版本2019.1.0的信息。
seo-description: 请参阅本页获取AEM Cloud Manager版本2019.1.0的信息。
uuid: af5808f-828f-4846-bee4-1e62194 b48 ad
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8ba8d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2019.1.0发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版增加了支持AEM Assets程序的支持，以及运行构建和代码质量步骤的其他管道类型，可选择部署到非生产环境。

## 发布日期 {#release-date}

版本2019.1.0 [!UICONTROL Cloud Manager] 的发布日期为2019年月17日。

## 新增功能 {#whats-new}

* 增加了对AEM Assets性能测试的支持。有关更多详细信息，请参阅配置 [CI/CD Pipeline](configuring-pipeline.md)。
* 新增了对仅运行、编码质量步骤和部署到非生产环境的管线的支持。有关更多详细信息，请参阅配置CI/CD管道中的 **非生产和代码质量仅限渠道**[](configuring-pipeline.md) 部分部分。
* 在构建环境中添加了对自定义环境变量的支持。有关更多详细信息，请参阅 [创建AEM应用程序项目](create-an-application-project.md) 。
* 对于具有多个阶段或生产环境的客户，可在 [配置CI/CD管道](configuring-pipeline.md) 页面中选择将哪个环境部署作为生产管道的一部分。
* 已添加httxt2dbm以构建容器。
* 所有帮助菜单项都将打开一个新选项卡。

## 错误修复 {#bug-fixes}

* 编辑程序时，可以取消选择所有页面集。
* 批准步骤的标题有误。
* 在某些情况下，节目徽标遮罩不正确。
* 如果只构建了调度程序配置包，则部署步骤将失败。
* 包含冷待机实例的环境未正确处理。
* 某些已终止的程序显示在程序切换程序上。
* 如果在编辑管道时将新分支添加到Git存储库，则可能无法立即选择该分支。
* 在某些屏幕上，“帮助”菜单中的开发人员连接图标不可见。
* 在调度程序刷新配置对话框中，选项卡键未正确处理。

## 已知问题 {#known-issues}

* 打开具有站点但未设置资产的程序时，所有用户都会看到一个对操作卡具有 **“设置程序** ”按钮的调用卡。但是，只有“企业主”角色中的用户才能单击 **“设置计划** ”按钮。