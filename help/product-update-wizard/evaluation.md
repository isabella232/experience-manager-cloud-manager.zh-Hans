---
title: 评估阶段
seo-title: Evaluation Phase
description: 了解产品更新向导的评估阶段如何使用模式检测器评估升级复杂性。
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: ce2145da3b9e605e8a41bac28df520f14e255557
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 评估阶段 {#evaluation}

“产品更新”向导的第一个阶段是 **[!UICONTROL Evaluation]** 阶段，该阶段使用模式检测器直接在向导中评估升级复杂性。 在此步骤结束时，您将有权访问评估报告。

生成的报告允许您通过检测以下模式来检查创作实例的升级资格：

* 违反有关受升级影响或覆盖的区域的某些规则。

* 使用AEM 6.x功能或API，该API无法向后兼容新版本的AEM，并且可能会在升级后中断。

该报告是对升级到Adobe Experience Manager(AEM)6.5所涉发展工作的评估。

>[!NOTE]
>
>要了解有关模式检测器的更多信息，请参阅此文档 [使用模式检测器评估升级复杂性。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=en)

## 运行评估 {#running}

该模式检测器可以在任何环境中运行。 但是，为了提高检测率并避免业务关键型实例出现任何速度减慢，Cloud Manager将在创作实例的暂存环境中运行该实例。

按照以下步骤生成评估报告。

1. 按照文档中的说明启动向导 [产品更新向导。](/help/product-update-wizard/overview.md)

1. 单击 **[!UICONTROL Run Evaluation]**.

   ![运行评估](/help/assets/Run-Evaluation.png)

1. 向导会通知您操作的状态。 您会注意到 **正在进行** 或 **已完成** 在生成评估报告时（如果适用）。

1. 生成报表后，您可以单击 **[!UICONTROL Download report]** 保存副本。

   ![报表已创建](/help/assets/Evaluation-1.png)

Cloud Manager中当前版本的产品更新向导支持 **评估** 仅阶段。 其他四个阶段，即 **修正**, **执行**, **验证**&#x200B;和 **完成** 即将推出。
