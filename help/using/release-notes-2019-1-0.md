---
title: 2019.1.0发行说明
seo-title: AEM Cloud Manager 2019.1.0版本说明
description: 可查看本页以获取Cloud Manager 2019.1.0版的相关信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.1.0版的信息。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 发行说明
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 12d787ef2f9b2dd229b8ed0f8c602fbf5c06aa80

---


# 2019.1.0发行说明 {#release-notes-for}

2018.9.0版 [!UICONTROL Cloud Manager] 本增加了对AEM资产程序以及运行构建和代码质量步骤的其他管道类型的支持测试，可以选择部署到非生产环境。

## 发布日期 {#release-date}

版本2019.1.0 [!UICONTROL Cloud Manager] 的发布日期为2019年1月17日。

## 新增功能 {#whats-new}

* 增加了对AEM Assets性能测试的支持。 有关更多详细信息，请参 [阅配置CI/CD](configuring-pipeline.md)管道。
* 增加了对仅运行构建和代码质量步骤的管道以及部署到非生产环境的管道的支持。 有关更多详 **细信息，请参阅配置CI/CD管道中的“仅非生**[](configuring-pipeline.md) 产和代码质量管道”部分。
* 在构建环境中增加了对自定义环境变量的支持。 有关更多详细 [信息，请参阅创建AEM应用程序项目](create-an-application-project.md) 。
* 对于具有多个阶段或生产环境的客户，可在“配置CI/CD管道”页面中选择将部署到哪个环境作为生产管道的一部分 [](configuring-pipeline.md) 。
* httxt2dbm已添加到构建容器。
* 所有帮助菜单项都会打开一个新选项卡。

## 错误修复 {#bug-fixes}

* 编辑程序时，可以取消选择所有页面集。
* 批准步骤的标题不正确。
* 在某些情况下，程序徽标的遮罩不正确。
* 如果仅构建了调度程序配置包，则部署步骤将失败。
* 包含冷备用实例的环境处理不正确。
* 程序切换器上出现一些终止的程序。
* 如果在编辑管道时向git存储库添加了新分支，则可能无法立即选择该分支。
* 在某些屏幕上，“帮助”菜单中的“开发人员连接”图标不可见。
* 在调度程序刷新配置对话框中未正确处理选项卡键。

## 已知问题 {#known-issues}

* 在打开设置了“站点”（但未设置“资产”和“KPI”）的程序时，所有用户都会看到带有“设置程序”按钮的 **行动动员卡** 。 但是，只有“业务所有者”角色的用户实际上可以单击“设 **置程序** ”按钮。