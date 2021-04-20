---
title: 2019.1.0 版发行说明
seo-title: AEM Cloud Manager 2019.1.0发行说明
description: 可查看本页以获取Cloud Manager 2019.1.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.1.0版的信息。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: Release Information
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 4%

---


# 2019.1.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本增加了对测试AEM Assets项目以及运行构建和代码质量步骤的其他管线类型的支持，可以选择部署到非生产环境。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.1.0的发布日期为2019年1月17日。

## 新增功能 {#whats-new}

* 增加了对AEM Assets性能测试的支持。 有关详细信息，请参阅配置[CI/CD管道](configuring-pipeline.md)。
* 增加了对仅运行构建和代码质量步骤的管道以及部署到非生产环境的管道的支持。 有关更多详细信息，请参阅[配置CI/CD管道](configuring-pipeline.md)中的&#x200B;**非生产和代码质量专用管道**&#x200B;部分。
* 在构建环境中增加了对自定义环境变量的支持。
* 对于具有多个阶段或生产环境的客户，可在[配置CI/CD管道](configuring-pipeline.md)页中选择将部署到哪个环境作为生产管道的一部分。
* httxt2dbm已添加到生成容器。
* 所有帮助菜单项都会打开一个新选项卡。

## 错误修复 {#bug-fixes}

* 编辑项目时，可以取消选择所有页面集。
* 批准步骤的标题不正确。
* 在某些情况下，项目徽标的遮罩不正确。
* 如果仅构建调度程序配置包，则部署步骤将失败。
* 包含冷备用实例的环境处理不正确。
* 某些已终止的项目显示在项目切换器上。
* 如果在编辑管道时向git存储库添加了新分支，则可能尚未立即进行选择。
* 在某些屏幕上，“帮助”菜单中的“开发人员连接”图标不可见。
* 未在调度程序刷新配置对话框中正确处理Tab键。

## 已知问题 {#known-issues}

* 在打开设置了站点（而未设置资产、KPI）的项目时，所有用户都会看到带有&#x200B;**设置项目**&#x200B;按钮的操作卡。 但是，只有“业务所有者”角色的用户实际上可以单击&#x200B;**设置项目**&#x200B;按钮。