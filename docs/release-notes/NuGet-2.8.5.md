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
# <a name="nuget-285-release-notes"></a><span data-ttu-id="07a5f-103">NuGet 2.8.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="07a5f-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="07a5f-104">[NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 发行说明](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="07a5f-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="07a5f-105">NuGet 2.8.5 已于 2015 年 3 月 30 日发布。</span><span class="sxs-lookup"><span data-stu-id="07a5f-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="07a5f-106">它是一项次要更新我们 2.8.3 VSIX 某些目标修补程序。</span><span class="sxs-lookup"><span data-stu-id="07a5f-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="07a5f-107">在此版本中，NuGet 包管理器对话框添加了对支持[DNX 目标框架名字对象](https://github.com/aspnet/dnx)。</span><span class="sxs-lookup"><span data-stu-id="07a5f-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="07a5f-108">支持这些新框架名字对象包括：</span><span class="sxs-lookup"><span data-stu-id="07a5f-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="07a5f-109">**core50** -'base' 的目标框架名字对象 (TFM) 与核心 CLR 兼容。</span><span class="sxs-lookup"><span data-stu-id="07a5f-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="07a5f-110">**dnx452** -使用完整 4.5.2 TFM 特定于基于 DNX 的应用程序的 framework 版本</span><span class="sxs-lookup"><span data-stu-id="07a5f-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="07a5f-111">**dnx46** -使用完整 4.6 版本的 framework TFM 特定于基于 DNX 的应用程序</span><span class="sxs-lookup"><span data-stu-id="07a5f-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="07a5f-112">**dnxcore50** -使用核心 5.0 版本的 framework TFM 特定于基于 DNX 的应用程序</span><span class="sxs-lookup"><span data-stu-id="07a5f-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="07a5f-113">该阻止的包安装到 FSharp 项目正确修复一个 bug:</span><span class="sxs-lookup"><span data-stu-id="07a5f-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400