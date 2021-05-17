---
title: 部署代码
seo-title: 部署代码
description: 提供有关Cloud Manager中部署过程的概述
seo-description: 了解配置管道后如何部署代码(存储库、环境和测试环境)
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: 代码部署
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: df2f598f91201d362f54b17e4092ff6bd6a72cec
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 1%

---

# 部署代码 {#deploy-your-code}

## 使用Cloud Manager {#deploying-code-with-cloud-manager}部署代码

>[!NOTE]
>要了解如何将AEM中Cloud Manager的代码作为Cloud Service部署，请参阅[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)。

配置生产管道(存储库、环境和测试环境)后，您就可以部署代码了。

1. 单击云管理器中的&#x200B;**部署**&#x200B;以开始部署过程。

   ![](assets/Deploy1.png)

1. 将显示&#x200B;**管线执行**&#x200B;屏幕。

   单击&#x200B;**构建**&#x200B;以开始进程。

   ![](assets/Deploy2.png)

1. 整个构建过程会部署您的代码。

   构建过程中涉及以下阶段：

   1. 阶段部署
   1. 舞台测试
   1. 生产部署

   >[!NOTE]
   >
   >此外，您还可以查看日志或查看测试标准的结果，以查看各个部署流程中的步骤。

   Stage **Deployment**，涉及以下步骤：

   * 验证：此步骤可确保将管道配置为使用当前可用的资源，例如，已配置的分支存在，这些环境可用。
   * 构建和单元测试：此步骤运行容器化的生成过程。 有关构建环境的详细信息，请参阅[了解构建环境](/help/using/build-environment-details.md)。
   * 代码扫描：此步骤将评估应用程序代码的质量。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。
   * 部署到舞台

   ![](assets/Stage_Deployment1.png)

   **阶段测试**&#x200B;涉及以下步骤：

   * 安全测试：此步骤评估您的应用程序代码对AEM环境的安全影响。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。
   * 性能测试：此步骤将评估应用程序代码的性能。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。

   ![](assets/Stage_Testing1.png)

   **生产部署**&#x200B;涉及以下步骤：

   * **申请批准** （如果启用）
   * **计划 Production Deployment** （如果启用）
   * **CSE支持** （如果启用）
   * **部署到生产**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >配置管线时，将启用&#x200B;**计划生产部署**。
   >
   >
   >使用此选项，您可以计划生产部署或单击&#x200B;**Now**&#x200B;立即执行生产部署。
   >
   >
   >计划的日期和时间根据用户的时区指定。
   >
   >
   >单击&#x200B;**确认**&#x200B;验证设置。

   ![](assets/Production_Deployment1.png)

   确认部署计划后，您的代码部署即告完成。

   当从上述步骤中选择&#x200B;**Now**&#x200B;选项时，将显示以下屏幕。

   ![](assets/Production_Deployment2.png)

## 超时 {#timeouts}

如果等待用户反馈，以下步骤将超时：

| 步骤 | 超时 |
|--- |--- |
| 代码质量测试 | 7天 |
| 安全测试 | 7天 |
| 性能测试 | 7天 |
| 申请批准 | 7天 |
| 计划生产部署 | 7天 |
| CSE支持 | 7天 |

## 部署进程{#deployment-process}

以下部分介绍如何在阶段阶段和生产阶段部署AEM和调度程序包。

Cloud Manager将构建过程生成的所有目标/*.zip文件上传到存储位置。  在管线的部署阶段从此位置检索这些对象。

当Cloud Manager部署到非生产拓扑时，其目标是尽快完成部署，从而将对象同时部署到所有节点，如下所示：

1. Cloud Manager确定每个对象是AEM包还是调度程序包。
1. Cloud Manager将从负载平衡器中删除所有调度程序，以在部署过程中隔离环境。

   除非另外配置，否则您可以跳过开发和舞台部署中的负载平衡器更改，即在非生产管道中为开发环境分离和附加步骤，并为舞台环境分离和附加生产管道。

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能预计主要由1-1-1个客户使用。

1. 每个AEM对象都通过包管理器API部署到每个AEM实例，包依赖关系决定部署顺序。

   要进一步了解如何使用包安装新功能、在实例之间传输内容以及备份存储库内容，请参阅如何使用包。

   >[!NOTE]
   >
   >所有AEM对象均部署到作者和发布者。 当需要特定于节点的配置时，应使用运行模式。 要进一步了解运行模式如何允许您针对特定目的调整AEM实例，请参阅运行模式。

1. 调度程序对象将部署到每个调度程序，如下所示：

   1. 当前配置将备份并复制到临时位置
   1. 除不可变文件外，所有配置都将被删除。 有关详细信息，请参阅管理调度程序配置。 这将清除目录，以确保不留下任何孤立文件。
   1. 对象将提取到`httpd`目录。  不可改写的文件不会被覆盖。 在部署时，您对git存储库中的不可变文件所做的任何更改都将被忽略。  这些文件是AMS调度程序框架的核心，无法更改。
   1. Apache执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，则从备份中恢复配置，重新加载服务，并将错误报告回云管理器。
   1. 在管线配置中指定的每个路径失效或从调度程序缓存中刷新。

   >[!NOTE]
   >Cloud Manager需要调度程序对象包含完整的文件集。  所有调度程序配置文件都必须位于git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，部署完成。

   >[!NOTE]
   >您可以跳过开发和舞台部署中的负载平衡器更改，即在非生产管道中为开发人员环境分离和附加步骤，在生产管道中为舞台环境分离和附加步骤。

### 部署到生产阶段{#deployment-production-phase}

部署到生产拓扑的过程略有不同，以最大限度地减少对AEM Site访客的影响。

生产部署通常遵循与上面相同的步骤，但以滚动方式：

1. 部署AEM包进行创作。
1. 从负载平衡器中分离调度程序1。
1. 将AEM包部署到publish1，将调度程序包并行地刷新调度程序缓存到dispatcher1。
1. 将dispatcher1放回负载平衡器中。
1. 调度程序1恢复服务后，请从负载平衡器中分离调度程序2。
1. 将AEM包部署到publish2，将调度程序包并行地刷新调度程序缓存，部署到dispatcher2。
1. 将dispatcher2放回负载平衡器中。
此过程将一直持续到部署到达拓扑中的所有发布者和调度程序为止。
