---
title: "NuGet 2.8.5 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 2.8.5 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.8.5 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 发行说明

[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 已于 2015 年 3 月 30 日发布。 它是一项次要更新我们 2.8.3 一些 VSIX 目标修补程序。

在此版本中，为已添加了 NuGet 包管理器对话框的支持[DNX 目标框架名字对象](https://github.com/aspnet/dnx)。  支持这些新框架名字对象包括：

* **core50** -base 目标框架名字对象 (TFM) 与核心 CLR 兼容。
* **dnx452** -使用完整 4.5.2 TFM 特定于基于 DNX 的应用的 framework 版本
* **dnx46** -使用完整 4.6 版本的 framework TFM 特定于基于 DNX 的应用
* **dnxcore50** -TFM 使用核心 5.0 版本的 framework 的特定于基于 DNX 的应用

一个 bug 已修复该程序包无法从正确安装到 FSharp 项目：

https://nuget.codeplex.com/workitem/4400