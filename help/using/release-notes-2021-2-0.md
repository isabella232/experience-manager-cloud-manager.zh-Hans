---
title: 2021.2.0 版发行说明
seo-title: AEM Cloud Manager 2021.2.0发行说明
description: 可查看本页面以获取有关Cloud Manager 2020.2.0版的信息
seo-description: 可查看本页以获取有关AEM Cloud Manager 2021.2.0版的信息
exl-id: 4f3c3a63-141b-414f-a24e-1870e985873a
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# 2021.2.0 版发行说明 {#release-notes-for}

以下部分概述了[!UICONTROL Cloud Manager]版本2021.2.0的常规发行说明。

## 发布日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.2.0的发行日期是2021年2月11日。

## 新增功能 {#whats-new}

* 项目和沙盒创建中使用的AEM项目原型已更新到版本25。

* 代码扫描过程中标识的已弃用API列表已得到细化，以包含最新Cloud ServiceSDK版本中已弃用的其他类和方法。

* 生产部署现在可并行部署到配对的发布实例和调度程序实例。

* 更新了Cloud Manager的SonarQube配置文件，以删除Sonar规则`squid:S2142`。 这不再与线程中断检查冲突。

* 现在，将动态删除客户`pom.xml`文件中设置的带声纳前缀的属性，以避免生成和质量扫描失败。

* 已添加其他代码质量规则以解决Cloud Service兼容性问题。

## 错误修复 {#bug-fixes}

* 有时，CI/CD（部署）管道在性能测试步骤中失败，原因是运行负载测试的容器遇到错误。

* 有时，即使只发生一个异常，加载测试容器也会报告运行失败。 仅当测试过程无法还原时，才会报告失败。

* 存储环境名称的方式之间存在某些大小写不匹配，这将导致性能测试失败。

* 某些管道故障被错误地报告为管道错误。
