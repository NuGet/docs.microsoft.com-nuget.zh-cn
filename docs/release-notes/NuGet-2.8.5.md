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
# <a name="nuget-285-release-notes"></a><span data-ttu-id="21978-103">NuGet 2.8.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="21978-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="21978-104">[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)  | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="21978-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="21978-105">NuGet 2.8.5 于2015年3月30日发布。</span><span class="sxs-lookup"><span data-stu-id="21978-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="21978-106">这是对 2.8.3 VSIX 的一个小更新，其中包含一些目标修补程序。</span><span class="sxs-lookup"><span data-stu-id="21978-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="21978-107">在此版本中，为 [DNX 目标框架名字对象](https://github.com/aspnet/dnx)添加了对 NuGet 包管理器对话框的支持。</span><span class="sxs-lookup"><span data-stu-id="21978-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="21978-108">支持的以下新框架名字对象包括：</span><span class="sxs-lookup"><span data-stu-id="21978-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="21978-109">**core50** -与核心 CLR 兼容的 "基" 目标框架名字对象 (TFM) 。</span><span class="sxs-lookup"><span data-stu-id="21978-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="21978-110">**dnx452** -特定于使用完整4.5.2 版本 framework 的基于 DNX 的应用的 TFM</span><span class="sxs-lookup"><span data-stu-id="21978-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="21978-111">**dnx46** -特定于使用完整4.6 版 framework 的基于 DNX 的应用的 TFM</span><span class="sxs-lookup"><span data-stu-id="21978-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="21978-112">**dnxcore50** -特定于使用 TFM 核心5.0 版本的基于 DNX 的应用的</span><span class="sxs-lookup"><span data-stu-id="21978-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="21978-113">修复了一个 bug，使包无法正确安装到 Fsharp.core 项目中：</span><span class="sxs-lookup"><span data-stu-id="21978-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400