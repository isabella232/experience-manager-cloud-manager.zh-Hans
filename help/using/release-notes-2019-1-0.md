---
title: 2019.1.0 版发行说明
seo-title: AEM Cloud Manager 2019.1.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2019.1.0版的信息。
seo-description: 可查看本页以获取有关AEM Cloud Manager 2019.1.0版的信息。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: 发行信息
exl-id: 383ca5a0-4b0b-48e9-aa48-1d1388875329
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 4%

---

# 2019.1.0 版发行说明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本添加了对测试AEM Assets程序以及运行生成和代码质量步骤的其他管道类型的支持，可以选择部署到非生产环境。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.1.0的发行日期是2019年1月17日。

## 新增功能 {#whats-new}

* 添加了对AEM Assets性能测试的支持。 有关更多详细信息，请参阅配置[CI/CD管线](configuring-pipeline.md)。
* 添加了对仅运行生成和代码质量步骤以及部署到非生产环境的管道的支持。 有关更多详细信息，请参阅[配置CI/CD管线](configuring-pipeline.md)中的&#x200B;**仅限生产和代码质量管线**&#x200B;部分。
* 在构建环境中添加了对自定义环境变量的支持。
* 对于具有多个阶段或生产环境的客户，在[配置CI/CD管线](configuring-pipeline.md)页面中提供了将部署到作为生产管道一部分的环境选项。
* httpxt2dbm已添加到生成容器。
* 所有帮助菜单项都会打开一个新选项卡。

## 错误修复 {#bug-fixes}

* 在编辑程序时，可以取消选择所有页面集。
* 批准步骤的标题不正确。
* 在某些情况下，程序徽标的匹配不正确。
* 如果仅生成调度程序配置包，则部署步骤将失败。
* 未正确处理包含冷备用实例的环境。
* 程序切换器上出现了一些终止的程序。
* 如果在编辑管道时向git存储库添加了新分支，则可能不会立即选择该分支。
* 在某些屏幕上，“帮助”菜单中的“开发人员连接”图标不可见。
* 未在调度程序刷新配置对话框中正确处理选项卡键。

## 已知问题 {#known-issues}

* 在打开设置了“站点”（但未设置“资产”）和KPI的程序时，所有用户都会看到带有&#x200B;**设置程序**&#x200B;按钮的行动动员卡。 但是，只有具有“业务所有者”角色的用户才能实际单击&#x200B;**设置程序**&#x200B;按钮。
