---
title: 管理您的环境
seo-title: 管理您的环境
description: 'null'
seo-description: 查看本页可查看用于在Cloud Manager中设置和运行CI/CD管线的生产和非生产环境列表。
uuid: 04e67572-11db-4d5d-acf3-fd7 f644 a95 f0
contentOwner: jsyal
products: SG_ EXPERIENCE MANAGER/CLEDNAGNANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8e6e6249a5b3a3a
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 管理您的环境 {#manage-your-environments}

云管理器 **的概述** 页面包含 **“环境** ”拼贴，其中列出了所有受管AEM环境。

每个列出的环境都会显示其关联状态。

![](assets/Manage_Environments1.png)

## 在Cloud Manager中访问环境 {#accessing-environments-in-cloud-manager}

**“环境”** 拼贴显示您的程序中供应的生产和舞台环境以及状态。

状态是环境中各个节点之间的垂直通电状态。如果所有节点都正在运行，则红色为红色；即使一个节点已停止，蓝色即使一个节点正在出现，蓝色也是蓝色；如果即使一个节点的电源状态不可用(以此优先级顺序)，也是如此。

![](assets/manage_environments-screen2.png)

### 环境 {#environments}

单击 **“管理** ”以显示 **“环境** ”屏幕。

**环境** 屏幕会在您的程序中显示 *每个用于生产* 和 *舞台* 环境(如果适用)的卡。环境名称在每张卡上方显示。卡包括环境中的节点，以及CPU的t恤大小、存储、区域和状态。

>[!NOTE]
>
>节点 **的STATUS** 表示VM的电源状态，并且不反映AEM在服务器上的状态。状态可能正在 **运行** (绿色圆形)、 **已停止** (红色圆形)、 **向上(** 蓝色圆形)或 **不可用** (黄色圆形)。

![](assets/Manage_Environments2.png)
