---
title: 评估
seo-title: 评估
description: '本页作为产品更新向导中学习评估阶段的起点。 '
seo-description: 本页作为产品更新向导中学习评估阶段的起点。
uuid: 62d68e79-c2 ba-4d8 b-ba7 d-33709014d5 b6
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
discoiquuid: ebcc91a5-be9 e-4684-8146-d88 f4013 d4 d1
translation-type: tm+mt
source-git-commit: 2fda16bb4826171c993ec07c7ff3e38d1675b9f5

---


# Evaluation Phase {#evaluation}

Once you click **[!UICONTROL Start Update]**, the first phase in Product Update Wizard is the Evaluation phase. 在此阶段，您可以通过直接从向导访问的模式检测器来评估升级复杂性。在此步骤结束时，您将有权访问评估报告。

生成的报告允许您通过检测模式来检查作者实例以实现upgra可变性：

* 违反某些规则，并在升级会影响或覆盖的区域中完成。

* 使用AEM6.x功能或API，它不会在新AEM上向后兼容，并且在升级后可能会断开。


这是升级到Adobe Experience Manager(AEM)6.5所涉及的开发工作的评估。

>[!NOTE]
>To learn more about pattern detector, refer to [Assessing the Upgrade Complexity with the Pattern Detector](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## Running the Evaluator {#running-evaluator}

请按照以下步骤运行评估器：

1. Select **[!UICONTROL Run Evaluation]** to run the pattern detector. 图案检测器可在任何环境上运行。但是，为了提高检测速率并避免对业务关键实例造成任何减慢，云管理器将在创作实例上运行阶段环境。

![](assets/Run-Evaluation.png)

1. 向导将通知您操作的状态。You will notice **In progress** or **completed** as applicable when the evaluation report is being generated.

Once the report is generated, you can select [!UICONTROL Download] to save a copy of the evaluation report.

![](assets/Evaluation-1.png)

>[!NOTE]
>The other four phases succeeding **Evaluation** namely **Remediation**, **Execution**, **Validation**, and **Completion** are coming soon and are not available in the current release.
