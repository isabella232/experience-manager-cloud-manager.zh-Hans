---
title: 部署代码
seo-title: 部署代码
description: 'null'
seo-description: 配置管道(存储库、环境和测试环境)后，即可部署代码。请参阅本页以了解更多信息。
uuid: e3807e1-437e-4922-ba48-0bcadf293 a99
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: using
discoiquuid: 832a4647-7b83-4a9d-b373-30FE16092 b15
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---


# 部署代码 {#deploy-your-code}

## 使用Cloud Manager部署代码 {#deploying-code-with-cloud-manager}

配置 **了渠道** (存储库、环境和测试环境)后，即可部署代码。

1. 单击 **Cloud Manager中** 的部署以启动部署过程。

   ![](assets/Deploy1.png)

1. 此时将显示 **“管道执行”** 屏幕。

   单击 **构建** 以启动进程。

   ![](assets/Deploy2.png)

1. 完整的构建过程可部署您的代码。

   构建过程涉及以下步骤：

   1. Stage Deployment
   1. Stage Testing
   1. 生产部署
   >[!NOTE]
   >
   >此外，您还可以查看各种部署流程中的步骤，方法是查看日志或查看结果，以了解测试条件。

   **Stage Deployment**&#x200B;包括以下步骤：

   * Build&amp; Unit Testing
   * 代码扫描
   * 部署到Stage
   ![](assets/Stage_Deployment1.png)

   **Stage Testing**，涉及以下步骤：

   * 安全测试
   * 性能测试
   ![](assets/Stage_Testing1.png)

   **Production Deployment**&#x200B;包括以下步骤：

   * **Approval for Approval** (If enabled)
   * **计划生产部署(** 如果启用)
   * **CSE支持** (如果启用)
   * **部署到生产**
   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >配置渠道时启用 **计划生产部署** 。
   >
   >
   >使用此选项，您可以安排生产演示或单击 **立即** 执行生产部署。
   >
   >
   >计划的日期和时间是在用户的时区中指定的。
   >
   >
   >单击 **确认** 以验证设置。

   ![](assets/Production_Deployment1.png)

   确认部署计划后，代码部署完成。

   此时将显示以下屏幕显示， **当从以上步骤选择“现在** ”选项时。

   ![](assets/Production_Deployment2.png)

## 部署流程 {#deployment-process}

以下部分介绍了AEM和调度程序包在舞台阶段和生产阶段的部署方式。

Cloud Manager将构建流程生成的所有目标/*.zip文件上载到存储位置。在管道的部署阶段从该位置检索这些伪像。

当Cloud Manager部署到非生产拓扑时，目标是尽可能快地完成部署，因此自然效果会同时部署到所有节点：

1. Cloud Manager可确定每个伪像是AEM还是调度程序包。
1. Cloud Manager会删除负载平衡器中的所有调度程序，以在部署过程中隔离环境。
1. 每个AEM伪像通过包管理器API部署到每个AEM实例，包的方法决定部署顺序。

   要进一步了解如何使用包安装新功能、在实例之间传输内容和备份存储库内容，请参阅如何使用包。

   >[!NOTE]
   >
   >所有AEM伪像都部署到作者和发布者。当需要特定于节点的配置时，应利用运行模式。要进一步了解运行模式如何允许您根据特定用途调整AEM实例，请参阅运行模式。

1. 调度程序伪像按照如下所示部署到每个调度程序：

   1. 当前配置将备份并复制到临时位置
   1. 除可模拟文件外，所有配置均被删除。有关更多详细信息，请参阅管理Dispatcher配置。这将清除目录以确保不会留下孤立的文件。
   1. 伪像被提取到httpd目录。不可模拟的文件不会覆盖。在部署时，您对git存储库中的不可模拟文件所做的任何更改都将被忽略。这些文件是AMS调度程序框架的核心，无法更改。
   1. Apache执行config测试。如果未找到错误，则重新加载服务。如果发生错误，则从备份恢复配置，重新加载服务，并将错误报告回Cloud Manager。
   1. 在管道配置中指定的每个路径都将失效或从调度程序缓存中刷新。
   >[!NOTE]
   >
   >Cloud Manager希望调度程序伪像包含完整的文件集。所有调度程序配置文件都必须显示在Git存储库中。缺少文件或文件夹将导致部署失败。

1. 在将所有AEM和调度程序包成功部署到所有节点之后，调度程序将添加回负载平衡器，部署完成。

### 部署到生产阶段 {#deployment-production-phase}

为了最大程度地减少对AEM站点访客的影响，部署到生产拓扑的过程略有不同。

制作部署通常遵循上述步骤，但采用滚动方式：

1. 部署AEM包以供创作。
1. 将调度程序从负载平衡器分离1。
1. 将AEM包部署到发布1，调度程序包到调度程序1，刷新调度程序缓存。
1. 将调度程序返回负载平衡器。
1. 调度程序返回到服务后，从负载平衡器分离调度程序2。
1. 将AEM包部署到发布并将调度程序包部署到调度程序2，刷新调度程序缓存。
1. 将调度程序放回负载平衡器中。
此过程一直持续到部署到达拓扑中的所有发布者和调度程序。


