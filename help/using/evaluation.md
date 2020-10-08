---
title: 评估
seo-title: 评估
description: '本页是在产品更新向导中学习评估阶段的起点。 '
seo-description: 本页是在产品更新向导中学习评估阶段的起点。
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: 8d1a100420129d234fe21911f165621405a04a9b
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# 评估阶段 {#evaluation}

“产品更新”向导的第一阶段为 **[!UICONTROL Evaluation]** 阶段。
在这里，您可以使用可从向导直接访问的模式检测器来评估升级复杂性。 在此步骤结束时，您将有权访问评估报告。

生成的报告允许您通过检测以下模式检查作者实例是否进行升级：

* 违反某些规则，并在受升级影响或覆盖的区域执行。

* 使用AEM 6.x功能或新AEM上不向后兼容的API，升级后可能会中断。

这是对升级到Adobe Experience Manager(AEM)6.5所涉及的发展努力的评估。

>[!NOTE]
>
>要进一步了解模式检测器，请参 [阅使用模式检测器评估升级复杂性](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## 运行计算器 {#running-evaluator}

请按照以下步骤生成评估报告：

1. 单击 **[!UICONTROL Run Evaluation]**。

   >[!NOTE]
   >
   >图案检测器可以在任何环境上运行。 但是，为了提高检测率并避免关键业务实例的任何运行速度减慢，Cloud Manager将在创作实例的暂存环境运行它。

   ![](assets/Run-Evaluation.png)

1. 向导会通知您操作的状态。 在生成评 **估报告****时，您** 会注意到“正在进行”或“已完成”（如果适用）。

   生成报告后，您可以单击以 **[!UICONTROL Download report]** 保存副本。

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >Cloud Manager中当前版本的产品更新向导仅支持 **评估** 阶段。 其他四个阶段，即 **补救**、执 **行**、验 **证**&#x200B;和完 **成即** 将推出。
