---
title: 部署代码
seo-title: 部署代码
description: 提供Cloud Manager中部署流程的概述
seo-description: 了解在配置管道（存储库、环境和测试环境）后如何部署代码
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
>要了解如何在AEM as a Cloud Service中为Cloud Manager部署代码，请参阅[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)。

配置生产管道（存储库、环境和测试环境）后，您便可以部署代码。

1. 从Cloud Manager中单击&#x200B;**部署**&#x200B;以开始部署过程。

   ![](assets/Deploy1.png)

1. 此时将显示&#x200B;**Pipeline Execution**&#x200B;屏幕。

   单击&#x200B;**Build**&#x200B;以开始该过程。

   ![](assets/Deploy2.png)

1. 整个构建过程会部署您的代码。

   构建过程中涉及以下阶段：

   1. Stage Deployment
   1. 阶段测试
   1. 生产部署

   >[!NOTE]
   >
   >此外，您还可以通过查看日志或查看结果来查看各种部署流程中的步骤，以了解测试标准。

   Stage **Deployment**，涉及以下步骤：

   * 验证：此步骤可确保将管道配置为使用当前可用的资源，例如，配置的分支存在，且环境可用。
   * 构建和单元测试：此步骤将运行容器化生成流程。 有关构建环境的详细信息，请参阅[了解构建环境](/help/using/build-environment-details.md)。
   * 代码扫描：此步骤将评估应用程序代码的质量。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。
   * 部署到暂存环境

   ![](assets/Stage_Deployment1.png)

   **Stage Testing**&#x200B;涉及以下步骤：

   * 安全测试：此步骤将评估应用程序代码对AEM环境的安全影响。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。
   * 性能测试：此步骤将评估应用程序代码的性能。 有关测试过程的详细信息，请参阅[了解测试结果](understand-your-test-results.md)。

   ![](assets/Stage_Testing1.png)

   **生产部署**&#x200B;涉及以下步骤：

   * **申请批准** （如果已启用）
   * **计划生产部署** （如果启用）
   * **CSE支持** （如果启用）
   * **部署到生产环境**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >配置管道时，将启用&#x200B;**计划生产部署**。
   >
   >
   >使用此选项，您可以计划生产部署，也可以单击&#x200B;**Now**&#x200B;立即执行生产部署。
   >
   >
   >计划的日期和时间以用户的时区来指定。
   >
   >
   >单击&#x200B;**Confirm**&#x200B;以验证您的设置。

   ![](assets/Production_Deployment1.png)

   确认部署计划后，您的代码部署即告完成。

   当从上述步骤中选择&#x200B;**Now**&#x200B;选项时，将显示以下屏幕。

   ![](assets/Production_Deployment2.png)

## 超时 {#timeouts}

如果留下等待用户反馈的时间，以下步骤将超时：

| 步骤 | 超时 |
|--- |--- |
| 代码质量测试 | 7天 |
| 安全测试 | 7天 |
| 性能测试 | 7天 |
| 申请批准 | 7天 |
| 计划生产部署 | 7天 |
| CSE支持 | 7天 |

## 部署过程{#deployment-process}

以下部分介绍如何在阶段和生产阶段部署AEM和调度程序包。

Cloud Manager将构建过程生成的所有target/*.zip文件上传到存储位置。  这些工件在管道的部署阶段期间从此位置进行检索。

当Cloud Manager部署到非生产拓扑时，其目标是尽快完成部署，从而将工件同时部署到所有节点，如下所示：

1. Cloud Manager确定每个对象是AEM还是调度程序包。
1. Cloud Manager从负载平衡器中删除所有调度程序，以在部署期间隔离环境。

   除非另外配置，否则您可以在开发部署和暂存部署中跳过负载平衡器更改，即在非生产管道、开发环境和生产管道的暂存环境中分离和附加步骤。

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能预计主要由1-1-1个客户使用。

1. 每个AEM对象都会通过包管理器API部署到每个AEM实例，并且包依赖关系会确定部署顺序。

   要详细了解如何使用软件包来安装新功能、在实例之间传输内容以及备份存储库内容，请参阅如何使用软件包。

   >[!NOTE]
   >
   >所有AEM对象都会部署到作者和发布者。 当需要特定于节点的配置时，应使用运行模式。 要了解有关运行模式如何允许您针对特定目的优化AEM实例的更多信息，请参阅运行模式。

1. 调度程序对象将部署到每个调度程序，如下所示：

   1. 当前配置将被备份并复制到临时位置
   1. 除不可变文件外，所有配置都将被删除。 有关更多详细信息，请参阅管理调度程序配置。 这会清除目录，以确保不会留下任何孤立的文件。
   1. 对象将提取到`httpd`目录。  不可变文件不会被覆盖。 在部署时，您对Git存储库中的不可变文件所做的任何更改都将被忽略。  这些文件是AMS调度程序框架的核心文件，无法更改。
   1. Apache会执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，将从备份还原配置，重新加载服务，并将错误报告回Cloud Manager。
   1. 管道配置中指定的每个路径都将失效或从调度程序缓存中刷新。

   >[!NOTE]
   >Cloud Manager需要调度程序对象包含完整文件集。  所有Dispatcher配置文件都必须存在于Git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，并且部署完成。

   >[!NOTE]
   >在开发和暂存部署中，您可以跳过负载平衡器更改，即在非生产管道、开发人员环境和暂存环境的生产管道中分离和附加步骤。

### 部署到生产阶段{#deployment-production-phase}

部署到生产拓扑的流程略有不同，以便最大限度地减少对AEM Site访客的影响。

生产部署通常遵循与上述步骤相同的步骤，但采用滚动方式：

1. 部署AEM包以进行创作。
1. 从负载平衡器中分离Dispatcher1。
1. 将AEM包部署到publish1，将调度程序包并行部署到dispatcher1，并刷新调度程序缓存。
1. 将dispatcher1重新放入负载平衡器中。
1. 调度程序1恢复服务后，从负载平衡器中分离dispatcher2。
1. 将AEM包部署到publish2，将调度程序包并行部署到dispatcher2，并刷新调度程序缓存。
1. 将dispatcher2重新放入负载平衡器中。
此过程会一直持续到部署到达拓扑中的所有发布者和调度程序为止。
