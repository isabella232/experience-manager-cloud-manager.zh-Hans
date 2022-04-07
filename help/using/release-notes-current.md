---
title: 2022.4.0 版发行说明
description: 以下是Cloud Manager 2022.4.0版的发行说明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 3d4eea13c0f2e9c4030bbfd3b7c5c25336548498
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---


# Cloud Manager 2022.4.0版发行说明 {#release-notes}

本页记录了 [!UICONTROL Cloud Manager] 版本2022.4.0。

>[!NOTE]
>
>有关AEMas a Cloud Service中Cloud Manager的最新发行说明，请参阅 [Cloud Manager(位于AEMas a Cloud Service的最新发行说明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 发布日期 {#release-date}

的发行日期 [!UICONTROL Cloud Manager] 2022.4.0版于2022年4月7日发布。 下一版本计划于2022年5月5日发布。

## 新增功能 {#what-is-new}

* 已实施管道构建步骤的持续时间和成功率的改进，并将在4月之前逐步推广到所有客户。
* 现在，您可以通过在添加和编辑管道向导的输入字段中键入名称的前几个字符，然后从建议的匹配项中进行选择，轻松找到git分支。
* 的 **管道** 现在，页面已进行分页，以提高具有大量管道的程序的可用性。
   * 表中将显示每页50行。
* 的版本 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) Cloud Manager使用的已更新到版本36。
* OracleJDK现在是用于开发和操作AEM应用程序的默认JDK。 即使在Maven工具链中明确选择了替代选项，Cloud Manager构建过程仍会自动切换到使用OracleJDK。
   * 要详细了解如何切换到OracleJDK，请参阅 [构建环境文档。](/help/using/build-environment-details.md#using-java-support)
   * 请参阅 [Adobe Experience Manager的Java支持策略常见问题解答](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 以解决有关此更改的常见问题。
