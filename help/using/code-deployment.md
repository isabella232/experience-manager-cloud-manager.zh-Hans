---
title: 代码部署
description: 了解如何部署代码以及在部署代码时 Cloud Manager 中会发生什么情况。
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: ht
source-wordcount: '1609'
ht-degree: 100%

---


# 代码部署 {#code-deployment}

了解如何部署代码以及在部署代码时 Cloud Manager 中会发生什么情况。

## 使用 Cloud Manager 部署代码 {#deploying-code-with-cloud-manager}

配置生产管道（包括必要的存储库和环境）后，便可以部署代码。

1. 单击 Cloud Manager 中的&#x200B;**部署**&#x200B;开始部署过程。

   ![“部署”按钮](/help/assets/Deploy1.png)

1. 此时将显示&#x200B;**管道执行**&#x200B;屏幕。单击&#x200B;**构建**&#x200B;开始此流程。

   ![“构建”按钮](/help/assets/Deploy2.png)

构建过程会启动代码部署过程，包括以下步骤：

* 暂存部署
* 暂存测试
* 生产部署

您可以通过查看日志或依据测试标准审查结果，来审查各种部署过程的步骤。

## 部署步骤 {#deployment-steps}

在执行部署的每个步骤时，将执行大量操作，此部分介绍了这些操作。查看[部署过程详细信息](#deployment-process)部分，了解有关如何在幕后部署代码本身的技术详细信息。

### 暂存部署步骤 {#stage-deployment}

**暂存部署**&#x200B;步骤包含以下操作：

* **验证**：此步骤可确保将管道配置为使用当前可用的资源，例如，存在已配置分支的资源以及环境可用的资源。
* **构建和单元测试**：此步骤运行容器化的构建过程。有关详细信息，请参阅[构建环境](/help/getting-started/build-environment.md)文档。
* **代码扫描**：此步骤评估应用程序代码的质量。有关测试过程的详细信息，请参阅[了解测试结果](/help/using/code-quality-testing.md)文档。
* **部署到暂存**

![暂存部署](/help/assets/Stage_Deployment1.png)

### 暂存测试步骤 {#stage-testing}

**暂存测试**&#x200B;步骤包含以下操作：

* **安全性测试**：此步骤评估代码对 AEM 环境产生的安全影响。有关测试过程的详细信息，请参阅[了解测试结果](/help/using/code-quality-testing.md)文档。
   * **性能测试**：此步骤评估代码的性能。有关测试过程的详细信息，请参阅[了解测试结果](/help/using/code-quality-testing.md)。

   ![暂存测试](/help/assets/Stage_Testing1.png)

### 生产部署步骤 {#production-deployment}

**生产部署**&#x200B;步骤包含以下操作：

* **申请审批**
   * 配置管道时将启用此选项。
   * 利用此选项，您可以计划生产部署，也可以单击&#x200B;**立即**&#x200B;来立即执行生产部署。
* **计划生产部署**
   * 配置管道时将启用此选项。
   * 根据用户的时区指定计划的日期和时间。
      ![计划部署](/help/assets/Production_Deployment1.png)
* **CSE 支持**（如果已启用）
* **部署到生产**

![生产部署](/help/assets/Prod_Deployment1.png)

部署完成后，代码将位于其目标环境中，并且您可以查看日志。

![部署完成](/help/assets/Production_Deployment2.png)

## 超时 {#timeouts}

如果继续等待用户反馈，则以下步骤将超时：

| 步骤 | 超时 |
|--- |--- |
| 代码质量测试 | 14 天 |
| 安全性测试 | 14 天 |
| 性能测试 | 14 天 |
| 申请批准 | 14 天 |
| 计划生产部署 | 14 天 |
| CSE 支持 | 14 天 |

## 部署过程详细信息 {#deployment-process}

Cloud Manager 将构建过程生成的所有 target/*.zip 文件上传到存储位置。在管道的部署阶段，将从该位置检索这些工件。

当 Cloud Manager 部署到非生产拓扑时，目标是尽快完成部署，因此，工件将同时部署到所有节点，如下所示：

1. Cloud Manager 确定每个工件是 AEM 还是 Dispatcher 包。
1. Cloud Manager 会从负载平衡器中移除所有 Dispatcher，以在部署期间隔离环境。

   * 除非另有配置，否则，您可以跳过开发和暂存部署中的负载平衡器更改，即对于开发环境，跳过非生产管道中的分离和附加步骤；对于暂存环境，跳过生产管道中的分离和附加步骤。

   ![跳过负载平衡器](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能应主要由 1-1-1 客户使用。

1. 每个 AEM 工件均通过包管理器 API 部署到每个 AEM 实例，其中包依赖关系将确定部署顺序。

   * 要了解有关如何使用包安装新功能、在实例之间传输内容以及备份存储库内容的更多信息，请参阅[包管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)文档。
   >[!NOTE]
   >
   >所有 AEM 工件都会部署供作者和发布者使用。在需要特定于节点的配置时，应利用运行模式。要了解有关运行模式如何允许您针对特定目的调整 AEM 实例的更多信息，请参阅[“部署到 AEM as a Cloud Service”文档的“运行模式”部分](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)。

1. Dispatcher 工件将部署到每个 Dispatcher，如下所示：

   1. 当前配置已备份并复制到临时位置。
   1. 已删除所有配置（不可变文件除外）。有关更多详细信息，请参阅 [Dispatcher 配置](/help/getting-started/dispatcher-configurations.md)文档。这会清空目录，确保没有留下孤立文件。
   1. 工件将提取到 `httpd` 目录。不会覆盖不可变文件。在部署时，将忽略您对 Git 存储库中的不可变文件所做的任何更改。这些文件是 AMS Dispatcher 框架的核心，无法更改。
   1. Apache 执行配置测试。如果未发现任何错误，则将重新加载服务。如果发生错误，则从备份中恢复配置，重新加载服务，并将错误报告回 Cloud Manager。
   1. 管道配置中指定的每个路径都将失效或从 Dispatcher 缓存中进行刷新。

   >[!NOTE]
   >
   >Cloud Manager 要求 Dispatcher 工件包含完整文件集。所有 Dispatcher 配置文件都必须在 Git 存储库中。缺少文件或文件夹将导致部署失败。

1. 在将所有 AEM 和 Dispatcher 包成功部署到所有节点后，会将 Dispatcher 重新添加到负载平衡器，同时完成部署。

   >[!NOTE]
   >
   >您可以跳过开发和暂存部署中的负载平衡器更改，即对于开发环境，跳过非生产管道中的分离和附加步骤；对于暂存环境，跳过生产管道中的分离和附加步骤。

### 部署到生产阶段 {#deployment-production-phase}

部署到生产拓扑的过程略有不同，旨在尽量减小对 AEM 网站访客产生的影响。

生产部署通常遵循与上述相同的步骤，但它采用的是滚动方式：

1. 将 AEM 包部署到作者。
1. 从负载平衡器分离 dispatcher1。
1. 以并行方式将 AEM 包部署到 publish1，并将 Dispatcher 包部署到 dispatcher1，同时刷新 Dispatcher 缓存。
1. 将 dispatcher1 放回负载平衡器中。
1. 在将 dispatcher1 重新投入使用后，就会从负载平衡器中分离 dispatcher2。
1. 以并行方式将 AEM 包部署到 publish2，并将 Dispatcher 包部署到 dispatcher2，同时刷新 Dispatcher 缓存。
1. 将 dispatcher2 放回负载平衡器中。

此过程将持续进行，直到部署到达拓扑中的所有发布者和 Dispatcher 为止。

## 紧急管道执行模式 {#emergency-pipeline}

在关键情况下，Adobe Managed Services 客户可能需要将代码更改部署到其暂存和生产环境中，而不是等到执行完整的 Cloud Manager 测试周期。

为了处理这些情况，可以在紧急模式下执行 Cloud Manager 生产管道。在使用此模式时，不执行安全性测试和性能测试步骤。所有其他步骤（包括任何已配置的审批步骤）都会像在正常管道执行模式中那样执行。

>[!NOTE]
>
>紧急管道执行模式功能由客户成功工程师逐个项目激活。

### 使用紧急管道执行模式 {#using-emergency-pipeline}

在启动生产管道执行时，如果已为项目激活紧急管道执行模式功能，则可以从对话框中以正常模式或紧急模式启动执行。

![运行管道选项](/help/assets/execution-emergency1.png)

在查看紧急模式下的执行运行的管道执行详细信息页面时，屏幕顶部的痕迹导航会显示一个指示器，指明管道正在紧急模式下执行。

![紧急模式痕迹导航](/help/assets/execution-emergency2.png)

要在紧急模式下执行管道，也可以通过 Cloud Manager API 或 CLI 实现。要在紧急模式下启动执行，请使用查询参数 `?pipelineExecutionMode=EMERGENCY` 或在使用 CLI 时将 `PUT` 请求提交到管道的执行端点：

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## 重新执行生产部署 {#re-execute-deployment}

生产部署步骤的重新执行适用于生产部署步骤已完成的执行。完成类型并不重要。部署的完成类型可以是成功（仅适用于 AMS 项目）、已取消或不成功。主要用例是生产部署步骤因瞬态原因导致失败的情况。重新执行时，将使用相同的管道来创建一个新的执行。此新执行包括三个步骤：

1. **验证步骤** – 此步骤基本上与正常管道执行期间进行的验证相同。
1. **构建步骤** – 在重新执行的上下文中，构建步骤将复制工件，而实际上并不执行新的构建过程。
1. **生产部署步骤** – 此步骤使用与正常管道执行中的生产部署步骤相同的配置和选项。

构建步骤可能在 UI 中具有不同的标签，以反映它将复制而不是重新生成工件。

![重新执行](/help/assets/Re-deploy.png)

### 限制 {#limitations}

* 生产部署步骤的重新执行仅适用于上一次执行。
* 重新执行不适用于回滚执行或推送更新执行。
* 如果上一次执行在生产部署步骤前的任何时间点失败，则无法重新执行。

### 识别重新执行的情况 {#identifying}

要识别某个执行是否为重新执行，可以检查 `trigger` 字段。其值将为 `RE_EXECUTE`。

### 触发重新执行 {#triggering}

要触发重新执行，需要对生产部署步骤状态的 HAL 链接 `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` 发出 `PUT` 请求。如果存在此链接，则可以从该步骤重新开始执行。如果此链接不存在，则无法从该步骤重新开始执行。此链接仅始终出现在生产部署步骤中

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

HAL 链接的 `href` 值的语法将不会用作参考点。应始终从 HAL 链接读取实际值而不是生成实际值。

通过将 `PUT` 请求提交到此端点，将产生 `201` 响应（如果成功），并且响应正文将是新执行的表示形式。这类似于通过 API 开始常规执行。
