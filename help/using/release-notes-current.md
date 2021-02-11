---
title: 2021.2.0 版发行说明
seo-title: AEM Cloud Manager 2021.2.0发行说明
description: 可查看本页以获取Cloud Manager Release 2021.2.0的相关信息
seo-description: 可查看本页以获取AEM Cloud Manager 2021.2.0版的相关信息
translation-type: tm+mt
source-git-commit: d956c7a2d3833e357920a9602e4f5a5b37f2c98a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# 2021.2.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2021.2.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.2.0的发布日期为2021年2月11日。

## 新增功能 {#whats-new}

* 项目和沙箱创建中使用的AEM项目原型已更新为版本25。

* 代码扫描过程中标识的已弃用API的列表已得到改进，以包括最新Cloud ServiceSDK版本中已弃用的其他类和方法。

* 现在，生产部署可并行部署到成对的发布和调度程序实例。

* SonarQueb用户档案, Cloud Manager已更新以删除Sonar规则`squid:S2142`。 这不再与线程中断检查冲突。

* 现在，将动态删除客户`pom.xml`文件中设置的带声纳前缀的属性，以避免生成和质量扫描失败。

* 已添加其他代码质量规则以解决Cloud Service兼容性问题。

## 错误修复 {#bug-fixes}

* 有时，由于运行负载测试的容器遇到错误，CI/CD（部署）管道在性能测试步骤中失败。

* 有时，即使只发生一个异常，负载测试容器也会将运行报告为失败。 仅当无法恢复测试进程时，才会报告失败。

* 环境名称存储方式之间的某些大小写不匹配会导致性能测试失败。

* 某些管线故障被错误报告为管线错误。