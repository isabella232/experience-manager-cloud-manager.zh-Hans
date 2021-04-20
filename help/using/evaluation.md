---
title: 评估
seo-title: 评估
description: '本页是在产品更新向导中学习评估阶段的起点。 '
seo-description: 本页是在产品更新向导中学习评估阶段的起点。
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---


# 评估阶段{#evaluation}

“产品更新”向导的第一阶段是&#x200B;**[!UICONTROL Evaluation]**阶段。
在此，您可以使用可从向导直接访问的模式检测器来评估升级复杂性。 在此步骤结束时，您将有权访问评估报告。

生成的报告允许您通过检测以下模式检查作者实例是否进行升级：

* 违反某些规则，并在受升级影响或覆盖的区域执行。

* 使用AEM 6.x功能或在新AEM上不向后兼容并且升级后可能会中断的API。

这是对升级到Adobe Experience Manager(AEM)6.5所涉发展努力的评估。

>[!NOTE]
>
>要进一步了解图案检测器，请参阅[使用图案检测器评估升级复杂性](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## 运行求值器{#running-evaluator}

请按照以下步骤生成评估报告：

1. 单击&#x200B;**[!UICONTROL Run Evaluation]**。

   >[!NOTE]
   >
   >图案检测器可以在任何环境上运行。 但是，为了提高检测率并避免关键业务实例出现任何速度减慢，Cloud Manager将在创作实例的暂存环境运行它。

   ![](assets/Run-Evaluation.png)

1. 向导会通知您操作的状态。 在生成评估报告时，您会注意到&#x200B;**正在进行**&#x200B;或&#x200B;**已完成**。

   生成报告后，您可以单击&#x200B;**[!UICONTROL Download report]**&#x200B;保存副本。

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >Cloud Manager中当前版本的产品更新向导仅支持&#x200B;**评估**&#x200B;阶段。 其他四个阶段即&#x200B;**Remediation**、**Execution**、**Validation**&#x200B;和&#x200B;**Completion**&#x200B;即将推出。
