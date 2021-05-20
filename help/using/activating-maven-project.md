---
title: Maven 项目版本处理
seo-title: Maven 项目版本处理
description: 进一步了解Maven项目版本处理。
seo-description: 可查看本页以了解有关Maven项目版本处理的更多信息。
feature: 入门
exl-id: a1d676e0-27cc-4b0d-8799-527c0520946a
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# Maven 项目版本处理 {#project-version}

## 了解Maven项目版本处理{#understanding-project-version}

对于暂存和生产部署，Cloud Manager会生成一个唯一的递增版本。

此版本可在管道执行详细信息页面和活动页面上查看。 运行内部版本后，将更新Maven项目以使用此版本，并在git存储库中创建一个标记，并将该版本作为其名称。

如果原始项目版本符合某些标准，则更新的Maven项目版本将合并原始项目版本和Cloud Manager生成的版本。 但是，标记始终使用生成的版本。 要进行此合并，原始项目版本必须由三个版本区段（例如1.0.0或1.2.3，但不能是1.0或1）组成，并且原始版本不能以 — SNAPSHOT结尾。

如果原始版本不符合此标准，则生成的版本将作为新版本区段附加到原始版本中。 生成的版本也将稍作修改，以包含正确的排序和版本处理。 例如，假定生成的版本为2019.926.121356.0000020490:

| **版本号** | **pom.xml中的版本** | **注释** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_0000020490 | 格式正确的原始版本 |
| 1.0.0 — 快照 | 2019.926.121356.0000020490 | 快照版本，覆盖 |
| 1 | 2019.926.121356.0000020490 | 版本不完整，被覆盖 |

>[!NOTE]
>
>无论原始版本是否纳入到Cloud Manager初始化的版本中，原始版本都可用作名为&#x200B;*cloudManagerOriginalVersion.*&#x200B;的Maven属性。
