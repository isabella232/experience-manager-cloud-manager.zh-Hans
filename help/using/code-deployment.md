---
title: 代码部署
description: 了解如何部署代码，以及执行此操作时Cloud Manager中会出现的情况。
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---


# 代码部署 {#code-deployment}

了解如何部署代码，以及执行此操作时Cloud Manager中会出现的情况。

## 使用Cloud Manager部署代码 {#deploying-code-with-cloud-manager}

配置生产管道（包括必要的存储库和环境）后，您便可以部署代码。

1. 单击 **部署** 从Cloud Manager开始部署过程。

   ![“部署”按钮](/help/assets/Deploy1.png)

1. 的 **管道执行** 屏幕。 单击 **生成** 以启动该过程。

   ![“生成”按钮](/help/assets/Deploy2.png)

生成过程会启动代码部署过程，包括以下步骤：

* 暂存部署
* 阶段测试
* 生产部署

您可以通过查看日志或查看结果来查看各种部署流程中的步骤，以了解测试标准。

## 部署步骤 {#deployment-steps}

在部署的每个步骤期间都会执行许多操作，本节对此进行了描述。 请参阅部分 [部署流程详细信息](#deployment-process) 有关代码本身如何在后台部署的技术详细信息。

### 暂存部署步骤 {#stage-deployment}

的 **暂存部署** 步骤包括以下操作：

* **验证**:此步骤可确保将管道配置为使用当前可用的资源，例如，已配置的分支存在且环境可用。
* **构建和单元测试**:此步骤将运行容器化生成流程。 查看文档 [构建环境](/help/getting-started/build-environment.md) 以了解详细信息。
* **代码扫描**:此步骤将评估应用程序代码的质量。 查看文档 [了解测试结果](/help/using/code-quality-testing.md) ，以了解有关测试过程的详细信息。
* **部署到暂存环境**

![暂存部署](/help/assets/Stage_Deployment1.png)

### 阶段测试步骤 {#stage-testing}

的 **阶段测试** 步骤包括以下操作：

* **安全测试**:此步骤将评估代码对AEM环境的安全影响。 查看文档 [了解测试结果](/help/using/code-quality-testing.md) ，以了解有关测试过程的详细信息。
   * **性能测试**:此步骤将评估代码的性能。 请参阅 [了解测试结果](/help/using/code-quality-testing.md) ，以了解有关测试过程的详细信息。

   ![阶段测试](/help/assets/Stage_Testing1.png)

### 生产部署步骤 {#production-deployment}

的 **生产部署** 步骤中，包括以下操作：

* **申请批准**
   * 配置管道时启用此选项。
   * 使用此选项，您可以计划生产部署，也可以单击 **现在** 立即执行生产部署。
* **计划生产部署**
   * 配置管道时启用此选项。
   * 计划的日期和时间以用户的时区来指定。
      ![计划部署](/help/assets/Production_Deployment1.png)
* **CSE支持** （如果启用）
* **部署到生产环境**

![生产部署](/help/assets/Prod_Deployment1.png)

部署完成后，您的代码将位于其目标环境中，您可以查看日志。

![部署完成](/help/assets/Production_Deployment2.png)

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

## 部署流程详细信息 {#deployment-process}

Cloud Manager将构建过程生成的所有target/*.zip文件上传到存储位置。 这些工件在管道的部署阶段期间从此位置进行检索。

当Cloud Manager部署到非生产拓扑时，其目标是尽快完成部署，从而将工件同时部署到所有节点，如下所示：

1. Cloud Manager确定每个对象是AEM还是调度程序包。
1. Cloud Manager从负载平衡器中删除所有调度程序，以在部署期间隔离环境。

   * 除非另有配置，否则您可以在开发和暂存部署中跳过负载平衡器更改，例如，对于开发环境，在非生产管道中分离和附加步骤，以及对于暂存环境，生产管道。

   ![跳过负载平衡器](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能预计主要由1-1-1个客户使用。

1. 每个AEM对象都会通过包管理器API部署到每个AEM实例，并且包依赖关系会确定部署顺序。

   * 要进一步了解如何使用软件包来安装新功能、在实例之间传输内容以及备份存储库内容，请参阅此文档 [包管理器。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)
   >[!NOTE]
   >
   >所有AEM对象都会部署到作者和发布者。 当需要特定于节点的配置时，应使用运行模式。 要了解有关运行模式如何允许您针对特定目的优化AEM实例的更多信息，请参阅 [将部署到AEMas a Cloud Service文档的“运行模式”部分。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)

1. 调度程序对象将部署到每个调度程序，如下所示：

   1. 当前配置将被备份并复制到临时位置。
   1. 除不可变文件外，所有配置都将被删除。 请参阅文档 [调度程序配置](/help/getting-started/dispatcher-configurations.md) 以了解更多详细信息。 这会清除目录，以确保不会留下任何孤立的文件。
   1. 该伪像被提取到 `httpd` 目录访问Advertising Cloud的帮助。 不可变文件不会被覆盖。 在部署时，您对Git存储库中的不可变文件所做的任何更改都将被忽略。 这些文件是AMS调度程序框架的核心文件，无法更改。
   1. Apache会执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，将从备份还原配置，重新加载服务，并将错误报告回Cloud Manager。
   1. 管道配置中指定的每个路径都将失效或从调度程序缓存中刷新。

   >[!NOTE]
   >
   >Cloud Manager需要调度程序对象包含完整文件集。 所有Dispatcher配置文件都必须存在于Git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，并且部署完成。

   >[!NOTE]
   >
   >您可以在开发和暂存部署中跳过负载平衡器更改，例如，对于开发环境、在非生产管道中分离和附加步骤，以及对于暂存环境，生产管道。

### 部署到生产阶段 {#deployment-production-phase}

部署到生产拓扑的流程略有不同，以最大限度地减少对AEM网站访客的影响。

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

要解决这些情况，可以在紧急模式下执行Cloud Manager生产管道。 使用此模式时，不会执行安全和性能测试步骤。 所有其他步骤（包括任何配置的批准步骤）都将像在普通管道执行模式中一样执行。

>[!NOTE]
>
>紧急管道执行模式功能由客户成功工程师逐个程序激活。

### 使用紧急管道执行模式 {#using-emergency-pipeline}

在启动生产管道执行时，如果已为程序激活紧急管道执行模式功能，则可以在正常或紧急模式下从对话框启动执行。

![运行管道选项](/help/assets/execution-emergency1.png)

在紧急模式下查看执行的管道执行详细信息页面时，屏幕顶部的痕迹导航会显示一个指示器，指示管道正在紧急模式下执行。

![紧急模式痕迹导航](/help/assets/execution-emergency2.png)

也可以通过Cloud Manager API或CLI在紧急模式下执行管道。 要在紧急模式下启动执行，请提交 `PUT` 使用查询参数向管道的执行端点发出请求 `?pipelineExecutionMode=EMERGENCY` 或者，在使用CLI时：

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## 重新执行生产部署 {#re-execute-deployment}

生产部署步骤已完成时，可以重新执行生产部署步骤。 完成类型不重要。 部署可能成功（仅适用于AMS程序）、取消或失败。 主要用例是生产部署步骤因临时原因而失败。 重新执行会使用相同的管道创建新执行。 此新执行包含三个步骤：

1. **验证步骤**  — 这基本上与正常管道执行期间发生的验证相同。
1. **生成步骤**  — 在重新执行的上下文中，生成步骤会复制工件，而实际上不会执行新的生成进程。
1. **生产部署步骤**  — 它使用与普通管道执行中的生产部署步骤相同的配置和选项。

生成步骤在UI中可能采用不同的方式进行标记，以反映该步骤是复制工件，而不是重新生成。

![重新执行](/help/assets/Re-deploy.png)

### 限制 {#limitations}

* 重新执行生产部署步骤仅适用于上次执行。
* 无法重新执行回滚执行或推送更新执行。
* 如果上次执行在生产部署步骤之前的任何时间点失败，则无法重新执行。

### 识别重新执行的执行 {#identifying}

要识别执行是否为重新执行，请 `trigger` 字段。 其价值将是 `RE_EXECUTE`.

### 触发重新执行 {#triggering}

要触发重新执行， `PUT` 需要向HAL链接发出请求 `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` 处于生产部署步骤状态。 如果此链接存在，则可以从该步骤重新启动执行。 如果不存在，则无法从该步骤重新启动执行。 此链接将只在生产部署步骤中存在

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

HAL链接的语法 `href` 值不会用作参考点。 实际值应始终从HAL链接中读取，而不是生成。

提交 `PUT` 对此端点的请求将导致 `201` 响应（如果成功），且响应主体将表示新执行。 这类似于通过API开始定期执行。
