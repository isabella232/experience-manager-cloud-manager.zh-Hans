---
title: 部署代码
seo-title: Deploy your Code
description: 提供Cloud Manager中部署流程的概述
seo-description: Learn how to deploy your code once you have configured your pipeline (repository, environment, and testing environment)
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: Code Deployment
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 4c86446127c8cd66f964b192f3602f02fd2ddf8e
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# 部署代码 {#deploy-your-code}

## 使用Cloud Manager部署代码 {#deploying-code-with-cloud-manager}

>[!NOTE]
>要了解如何在AEMas a Cloud Service中部署Cloud Manager代码，请参阅 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager).

配置生产管道（存储库、环境和测试环境）后，您便可以部署代码。

1. 单击 **部署** 从Cloud Manager开始部署过程。

   ![](assets/Deploy1.png)

1. 的 **管道执行** 屏幕。

   单击 **生成** 以启动该过程。

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
   * 构建和单元测试：此步骤将运行容器化生成流程。 请参阅 [了解构建环境](/help/using/build-environment-details.md) 以了解有关生成环境的详细信息。
   * 代码扫描：此步骤将评估应用程序代码的质量。 请参阅 [了解测试结果](understand-your-test-results.md) ，以了解有关测试过程的详细信息。
   * 部署到暂存环境

   ![](assets/Stage_Deployment1.png)

   的 **阶段测试**，涉及以下步骤：

   * 安全测试：此步骤将评估应用程序代码对AEM环境的安全影响。 请参阅 [了解测试结果](understand-your-test-results.md) ，以了解有关测试过程的详细信息。
   * 性能测试：此步骤将评估应用程序代码的性能。 请参阅 [了解测试结果](understand-your-test-results.md) ，以了解有关测试过程的详细信息。

   ![](assets/Stage_Testing1.png)

   的 **生产部署**，涉及以下步骤：

   * **申请批准** （如果启用）
   * **计划生产部署** （如果启用）
   * **CSE支持** （如果启用）
   * **部署到生产环境**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >的 **计划生产部署** 在配置管道时启用。
   >
   >
   >使用此选项，您可以计划生产部署，也可以单击 **现在** 立即执行生产部署。
   >
   >
   >计划的日期和时间以用户的时区来指定。
   >
   >
   >单击 **确认** 以验证您的设置。

   ![](assets/Production_Deployment1.png)

   确认部署计划后，您的代码部署即告完成。

   当 **现在** 选项。

   ![](assets/Production_Deployment2.png)

## 超时 {#timeouts}

如果留下等待用户反馈的时间，以下步骤将超时：

| 步骤 | 超时 |
|--- |--- |
| 代码质量测试 | 14天 |
| 安全测试 | 14天 |
| 性能测试 | 14天 |
| 申请批准 | 14天 |
| 计划生产部署 | 14天 |
| CSE支持 | 14天 |

## 部署过程 {#deployment-process}

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
   1. 该伪像被提取到 `httpd` 目录访问Advertising Cloud的帮助。  不可变文件不会被覆盖。 在部署时，您对Git存储库中的不可变文件所做的任何更改都将被忽略。  这些文件是AMS调度程序框架的核心文件，无法更改。
   1. Apache会执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，将从备份还原配置，重新加载服务，并将错误报告回Cloud Manager。
   1. 管道配置中指定的每个路径都将失效或从调度程序缓存中刷新。

   >[!NOTE]
   >Cloud Manager需要调度程序对象包含完整文件集。  所有Dispatcher配置文件都必须存在于Git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，并且部署完成。

   >[!NOTE]
   >在开发和暂存部署中，您可以跳过负载平衡器更改，即在非生产管道、开发人员环境和暂存环境的生产管道中分离和附加步骤。

### 部署到生产阶段 {#deployment-production-phase}

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

## 紧急管道执行模式 {#emergency-pipeline}

在关键情况下，Adobe Managed Services客户可能需要将代码更改部署到其暂存和生产环境，而无需等待执行完整的Cloud Manager测试周期。

要解决这些情况，可能会在 *紧急* 模式。 使用此模式时，不执行安全性和性能测试步骤；所有其他步骤（包括任何已配置的批准步骤）均在正常管道执行模式下执行。

>[!NOTE]
>紧急管道执行模式功能由客户成功工程师按计划激活。

### 使用紧急管道执行模式 {#using-emergency-pipeline}

在启动生产管道执行时，如果此功能已激活，则可以从对话框中以正常或紧急模式启动执行，如下图所示。

![](assets/execution-emergency1.png)

此外，查看在紧急模式下运行的执行的管道执行详细信息页面时，屏幕顶部的痕迹导航会显示一个指示器，指示此特定执行使用了紧急模式。

![](assets/execution-emergency2.png)

也可以在此紧急模式下创建管道执行，这可以通过Cloud Manager API或CLI来完成。 要在紧急模式下启动执行，请使用查询参数向管道的执行端点提交PUT请求 `?pipelineExecutionMode=EMERGENCY` 或者，在使用CLI时：

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

>[!IMPORTANT]
>使用 `--emergency` 标记可能需要更新到最新 `aio-cli-plugin-cloudmanager` 版本。

## 重新执行生产部署 {#Reexecute-Deployment}

对于生产部署步骤已完成的执行，支持重新执行生产部署步骤。 完成类型不重要 — 部署可能成功（仅适用于AMS程序）、取消或失败。 尽管如此，主要用例预计是生产部署步骤因临时原因而失败的情况。 重新执行会使用相同的管道创建新执行。 此新执行包含三个步骤：

1. 验证步骤 — 这基本上与正常管道执行期间发生的验证相同。
1. 生成步骤 — 在重新执行的上下文中，生成步骤是复制工件，而不是实际执行新的生成过程。
1. 生产部署步骤 — 使用与正常管道执行中的生产部署步骤相同的配置和选项。

生成步骤在UI中的标记可能略有不同，以反映它是在复制工件，而不是重新生成。

![](assets/Re-deploy.png)

限制：

* 重新执行生产部署步骤将仅在上次执行时可用。
* 无法重新执行回滚执行。
* 如果上次执行是回滚执行，则无法重新执行。
* 如果上次执行是推送更新执行，则无法重新执行。
* 如果上次执行在生产部署步骤之前的任何时间点失败，则无法重新执行。

### 重新执行API {#Reexecute-API}

### 识别重新执行的执行

要识别执行是否为重新执行，可检查trigger字段。 其价值将是 *RE_EXECUTE*.

### 触发新执行

要触发重新执行，需要向HAL链接发出PUT请求 ```http://ns.adobe.com/adobecloud/rel/pipeline/reExecute``` 处于生产部署步骤状态。 如果此链接存在，则可以从该步骤重新启动执行。 如果不存在，则无法从该步骤重新启动执行。 在初始版本中，此链接将只在生产部署步骤中存在，但将来版本可能支持从其他步骤启动管道。 示例:

```Javascript
 {
  "_links": {
    "http://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


HAL链接的语法 *href*  上述值不打算用作参考点。 实际值应始终从HAL链接中读取，而不是生成。

提交 *PUT* 对此端点的请求将导致 *201* 响应（如果成功），且响应主体将表示新执行。 这类似于通过API开始定期执行。
