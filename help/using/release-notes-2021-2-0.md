---
title: 2021.2.0 版发行说明
seo-title: AEM Cloud Manager 2021.2.0发行说明
description: 可查看本页以获取Cloud Manager 2021.2.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2021.2.0版的信息
translation-type: tm+mt
source-git-commit: b5233e1932888b515d8dc26a6493cbd26686bc3c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# 2021.2.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager] 2021.2.0版的一般发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.2.0的发布日期为2021年2月11日。

## 新增功能 {#whats-new}

* 在“项目”和“沙箱创建”中使用的AEM Project原型已更新为版本25。

* 在代码扫描过程中识别的已弃用API的列表已得到改进，以包括最新Cloud Service SDK版本中已弃用的其他类和方法。

* 生产部署现在可并行部署到成对的发布和调度程序实例。

* SonarQube用户档案 for Cloud Manager已更新，以删除Sonar规则`squid:S2142`。 这不再与线程中断检查冲突。

* 现在，将动态删除客户`pom.xml`文件中设置的属性，以避免生成和质量扫描失败。

* 已添加其他代码质量规则，以解决Cloud Service兼容性问题。

## 错误修复 {#bug-fixes}

* 有时，CI/CD（部署）管道在性能测试步骤期间失败，原因是运行负载测试的容器遇到错误。

* 有时，即使只发生一个异常，负载测试容器也会将运行报告为失败。 只有在无法恢复测试进程时才会报告失败。

* 存储环境名称之间的某些大小写不匹配会导致性能测试失败。

* 某些管线故障被错误地报告为管线错误。