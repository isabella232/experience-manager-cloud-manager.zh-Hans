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
source-git-commit: 9e33b90818c686f0b7aacaf0955c3f2eba05488f

---


# 评估阶段 {#evaluation}

“产品更新”向导的第一阶段是阶 **[!UICONTROL Evaluation]** 段。
您可以在此处使用可从向导直接访问的模式检测器来评估升级复杂性。 在此步骤结束时，您将有权访问评估报告。

生成的报告允许您通过检测以下模式来检查作者实例的升级性：

* 违反某些规则，并在受升级影响或覆盖的区域执行。

* 使用AEM 6.x功能或在新AEM上不向后兼容的API，它们在升级后可能会中断。

这是对升级到Adobe Experience Manager(AEM)6.5所涉及的开发工作的评估。

>[!NOTE]
>要了解有关模式检测器的更多信息，请参 [阅使用模式检测器评估升级复杂性](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## 运行求值器 {#running-evaluator}

请按照以下步骤生成评估报告：

1. 单击 **[!UICONTROL Run Evaluation]**。

   >[!NOTE]
   >该图案检测器可运行于任何环境。 但是，为了提高检测率并避免关键业务实例出现任何速度减慢，Cloud Manager将在创作实例的分阶段环境中运行它。

   ![](assets/Run-Evaluation.png)

1. 向导会通知您操作的状态。 在生成评 **估报告时** ，您 **** 会注意到正在进行或已完成。

   生成报告后，您可以单击以 **[!UICONTROL Download report]** 保存副本。

   ![](assets/Evaluation-1.png)


>[!NOTE]
>Cloud Manager中当前版本的产品更新向导仅支持评估 **阶段** 。 其他四个阶段，即 **补救**、执 **行**、验证 ******和完** 成计划即将推出。
