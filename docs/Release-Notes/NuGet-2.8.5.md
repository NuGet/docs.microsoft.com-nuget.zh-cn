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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="a6659-104">NuGet 2.8.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="a6659-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="a6659-105">[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="a6659-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="a6659-106">NuGet 2.8.5 已于 2015 年 3 月 30 日发布。</span><span class="sxs-lookup"><span data-stu-id="a6659-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="a6659-107">它是一项次要更新我们 2.8.3 一些 VSIX 目标修补程序。</span><span class="sxs-lookup"><span data-stu-id="a6659-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="a6659-108">在此版本中，为已添加了 NuGet 包管理器对话框的支持[DNX 目标框架名字对象](https://github.com/aspnet/dnx)。</span><span class="sxs-lookup"><span data-stu-id="a6659-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="a6659-109">支持这些新框架名字对象包括：</span><span class="sxs-lookup"><span data-stu-id="a6659-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="a6659-110">**core50** -base 目标框架名字对象 (TFM) 与核心 CLR 兼容。</span><span class="sxs-lookup"><span data-stu-id="a6659-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="a6659-111">**dnx452** -使用完整 4.5.2 TFM 特定于基于 DNX 的应用的 framework 版本</span><span class="sxs-lookup"><span data-stu-id="a6659-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="a6659-112">**dnx46** -使用完整 4.6 版本的 framework TFM 特定于基于 DNX 的应用</span><span class="sxs-lookup"><span data-stu-id="a6659-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="a6659-113">**dnxcore50** -TFM 使用核心 5.0 版本的 framework 的特定于基于 DNX 的应用</span><span class="sxs-lookup"><span data-stu-id="a6659-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="a6659-114">一个 bug 已修复该程序包无法从正确安装到 FSharp 项目：</span><span class="sxs-lookup"><span data-stu-id="a6659-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="a6659-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="a6659-115">https://nuget.codeplex.com/workitem/4400</span></span>