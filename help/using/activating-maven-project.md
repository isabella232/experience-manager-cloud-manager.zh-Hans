---
title: Maven 项目版本处理
seo-title: Maven 项目版本处理
description: 进一步了解Maven项目版本处理。
seo-description: 可查看本页以了解有关Maven项目版本处理的更多信息。
translation-type: tm+mt
source-git-commit: e2187565e7f06d64841eb2af9b4b1a56feb5ebe4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# Maven 项目版本处理 {#project-version}

## 了解Maven项目版本处理{#understanding-project-version}

对于舞台和生产部署，Cloud Manager可生成一个独特的递增版本。

此版本可在管道执行详细信息页面和活动页面上查看。 运行内部版本时，Maven项目将更新为使用此版本，并在git存储库中以该版本为名称创建标记。

如果原始项目版本满足某些条件，则更新的Maven项目版本将合并原始项目版本和Cloud Manager生成的版本。 但是，标记始终使用生成的版本。 要进行此合并，原始项目版本必须仅包含三个版本段（例如1.0.0或1.2.3，但不能包含1.0或1），并且原始版本不能以-SNAPSHOT结束。

如果原始版本满足此条件，则生成的版本将作为新版本段附加到原始版本。 生成的版本也将稍作修改，以包含正确的排序和版本处理。 例如，假定生成的版本为2019.926.121356.000020490:

| **版本** | **pom中的版本** | **注释** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_0000020490 | 格式正确的原始版本 |
| 1.0.0-快照 | 2019.926.121356.0000020490 | 快照版本，已覆盖 |
| 1 | 2019.926.121356.0000020490 | 版本不完整，被覆盖 |

>[!NOTE]
>
>无论原始版本是否已并入云管理器初始化版本，原始版本都可作为名称为&#x200B;*cloudManagerOriginalVersion的Maven属性使用。*
