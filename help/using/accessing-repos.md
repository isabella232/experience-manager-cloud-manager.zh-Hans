---
title: 访问存储库
seo-title: 访问存储库
description: 本页介绍如何访问和管理Git存储库。
seo-description: 可查看本页以了解如何访问和管理Git存储库。
feature: Git存储库
exl-id: 403fc93d-60fc-4439-8c9d-0a512ca34458
source-git-commit: 5bbe76a46b7a15ccbab85c4487d2a20aaf59a4e7
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---

# 访问存储库 {#accessing-repos}

您可以使用Cloud Manager UI中的Git自助服务帐户管理来访问和管理Git存储库。

## 使用自助式Git帐户管理 {#self-service-git}

使用Cloud Manager UI中提供的&#x200B;**访问存储库信息**&#x200B;按钮，其中最突出的是管道卡。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**Pipelines**&#x200B;卡。

1. 您将查看&#x200B;**访问存储库信息**&#x200B;选项，以访问和管理您的Git存储库。

   ![](assets/access-repo1.png)

   此外，如果选择&#x200B;**非生产**&#x200B;管道选项卡，您还将在此处查看&#x200B;**访问存储库信息**&#x200B;选项。

   ![](assets/access-repo-nonprod.png)


   >[!NOTE]
   >在“开发人员”或“部署管理器”角色中，用户可以看到&#x200B;**访问存储库信息**&#x200B;选项。 单击此按钮会打开一个对话框，通过该对话框，用户可以查找其Cloud Manager Git存储库的URL及其用户名和密码。

   ![](assets/access-repo-create.png)

   在Cloud Manager中管理Git的重要注意事项包括：

   * **URL**:存储库URL
   * **用户名**:用户名
   * **密码**:单击“生成口令 **”按钮时显示** 的值。


      >[!NOTE]
      >用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回Cloud Manager中的远程代码存储库。
