---
title: NuGet 2.8.5 发行说明
description: NuGet 2.8.5 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548620"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 发行说明

[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 已于 2015 年 3 月 30 日发布。 它是一项次要更新我们 2.8.3 VSIX 某些目标修补程序。

在此版本中，NuGet 包管理器对话框添加了对支持[DNX 目标框架名字对象](https://github.com/aspnet/dnx)。  支持这些新框架名字对象包括：

* **core50** -'base' 的目标框架名字对象 (TFM) 与核心 CLR 兼容。
* **dnx452** -使用完整 4.5.2 TFM 特定于基于 DNX 的应用程序的 framework 版本
* **dnx46** -使用完整 4.6 版本的 framework TFM 特定于基于 DNX 的应用程序
* **dnxcore50** -使用核心 5.0 版本的 framework TFM 特定于基于 DNX 的应用程序

该阻止的包安装到 FSharp 项目正确修复一个 bug:

https://nuget.codeplex.com/workitem/4400