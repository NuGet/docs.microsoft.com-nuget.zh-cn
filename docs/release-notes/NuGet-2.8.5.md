---
title: NuGet 2.8.5 发行说明
description: NuGet 2.8.5 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780352"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 发行说明

[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)  | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 于2015年3月30日发布。 这是对 2.8.3 VSIX 的一个小更新，其中包含一些目标修补程序。

在此版本中，为 [DNX 目标框架名字对象](https://github.com/aspnet/dnx)添加了对 NuGet 包管理器对话框的支持。  支持的以下新框架名字对象包括：

* **core50** -与核心 CLR 兼容的 "基" 目标框架名字对象 (TFM) 。
* **dnx452** -特定于使用完整4.5.2 版本 framework 的基于 DNX 的应用的 TFM
* **dnx46** -特定于使用完整4.6 版 framework 的基于 DNX 的应用的 TFM
* **dnxcore50** -特定于使用 TFM 核心5.0 版本的基于 DNX 的应用的

修复了一个 bug，使包无法正确安装到 Fsharp.core 项目中：

https://nuget.codeplex.com/workitem/4400