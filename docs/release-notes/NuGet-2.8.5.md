---
title: NuGet 2.8.5 发行说明
description: 发行说明，了解 NuGet 2.8.5 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820074"
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