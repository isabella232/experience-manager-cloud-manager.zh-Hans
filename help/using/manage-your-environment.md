---
title: 管理环境
seo-title: 管理环境
description: 'null'
seo-description: 可查看用于在Cloud manager中设置和运行CI/CD管道的生产和非生产环境列表。
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
translation-type: tm+mt
source-git-commit: 2b71bb61e00d462a43519ec0a2dcfe9231fe53ff

---


# 管理环境 {#manage-your-environments}

Cloud manager的 **概述** ，页面中包括列出所 **有受管AEM环境的“** 环境”拼贴。

列出的每个环境都显示其关联的状态。

![](assets/Manage_Environments1.png)

## 在Cloud manager中访问环境 {#accessing-environments-in-cloud-manager}

“环 **境** ”拼贴显示程序中提供的生产和舞台环境以及状态。

状态是环境中节点间的累计电源状态。 如果所有节点都在运行，则为绿色；如果一个节点停止，则为红色；如果一个节点出现，则为蓝色；如果一个节点的电源状态不可用，则为黄色（按优先级顺序）。

![](assets/manage_environments-screen2.png)

### 环境 {#environments}

单击 **管理** ，以显示“ **环境** ”屏幕。

“环 **境** ”屏幕显示程序中 *的Production* and *Stage* environments（如果适用）的卡。 该环境的名称显示在每张卡的上方。 该卡包括环境中的节点表以及CPU的t恤尺寸、存储、区域和状态。

>[!NOTE]
>
>节 **点的STATUS** 表示VM的电源状态，但不反映服务器上AEM的状态。 状态可以是“ **运行** ”（绿色圆）、“已停止 **”（红色圆）、“启动”** （蓝色圆）或“不可 ******** 用”（黄色圆）。

![](assets/Manage_Environments2.png)
