---
title: 使用“新建项目”向导
description: 请阅读本页，了解如何使用向导创建AEM应用程序项目
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: cb791a4f148ba394687b5e824b75fe1386d83c18
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# 使用“新建项目”向导 {#using-the-wizard}

作为新客户载入到Cloud Manager后，您将获得一个空的git存储库。 为了帮助您入门，Cloud Manger提供了一个向导，用于根据 [AEM项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) 作为起点。

请按照以下步骤使用向导创建AEM项目。

1. 登录Cloud Manager(位于 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 并选择相应的组织。

1. 如果你还没有， [创建项目。](program-setup.md) 创建程序后，Cloud Manager将识别到尚未设置存储库，并会在 **概述** 屏幕。

   ![创建项目CTA](/help/assets/image2018-10-3_14-29-44.png)

1. 单击 **创建** 以启动向导并提供重要值。

   * **标题**  — 这是项目的标题，默认情况下设置为项目的名称。
   * **新建分支名称**  — 这是Git存储库的初始分支，默认情况下将为 `main`.

   ![项目值](/help/assets/screen_shot_2018-10-08at55825am.png)

1. 该对话框有一个抽屉，通过向底部单击手柄可打开抽屉。 该对话框以扩展形式显示AEM项目原型的所有配置参数。 这些参数具有根据 **标题** 您已提供，无需修改。 请在此处说明这些信息。

   ![详细的原型参数](/help/assets/screen_shot_2018-10-08at60032am.png)

1. 单击 **创建** 使用原型创建起始项目，并提交到命名的git分支。

你现在有基础项目！ 现在，您可以设置管道。

## 现有客户或迁移客户 {#existing-migrating}

如果您是当前迁移到的Adobe Managed Services(AMS)客户或内部部署AEM客户，则可能已在git或其他版本控制系统中拥有项目代码。

在这种情况下，您会将项目导入Cloud Manager git存储库。
