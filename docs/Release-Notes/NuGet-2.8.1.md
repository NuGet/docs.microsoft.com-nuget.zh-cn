---
title: "NuGet 2.8.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "发行说明，了解 NuGet 2.8.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.8.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="fb3ee-104">NuGet 2.8.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="fb3ee-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="fb3ee-105">[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 发行说明](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="fb3ee-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="fb3ee-106">NuGet 2.8.1 已于 2014 年 4 月 2 日发布。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="fb3ee-107">发行版中的值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="fb3ee-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="fb3ee-108">对 Windows Phone 8.1 项目的支持</span><span class="sxs-lookup"><span data-stu-id="fb3ee-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="fb3ee-109">此版本现在支持以下新目标框架名字对象可以用于记录的目标 Windows Phone 8.1 项目：</span><span class="sxs-lookup"><span data-stu-id="fb3ee-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="fb3ee-110">WindowsPhone81 / WP81 （对于基于 Silverlight 的 Windows Phone 项目）</span><span class="sxs-lookup"><span data-stu-id="fb3ee-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="fb3ee-111">WindowsPhoneApp81 / WPA81 （对于基于 WinRT 的 Windows Phone 应用程序项目）</span><span class="sxs-lookup"><span data-stu-id="fb3ee-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="fb3ee-112">更新 NuGet WebMatrix 扩展</span><span class="sxs-lookup"><span data-stu-id="fb3ee-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="fb3ee-113">此版本更新到 WebMatrix 中找到 NuGet 客户端[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，并使它如 XDT 转换使用的功能。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="fb3ee-114">更重要的是，2.6.1 核心更新使 WebMatrix 客户端安装包含较新版本的 NuGet 包`.nuspec`架构，包括 ASP.NET NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="fb3ee-115">有关 WebMatrix 扩展更新的详细信息，请参阅这些特定[发行说明](../release-notes/nuget-2.6.1-for-WebMatrix.md)。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="fb3ee-116">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="fb3ee-116">Bug Fixes</span></span>
<span data-ttu-id="fb3ee-117">除了这些功能，此版本的 NuGet 包括其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="fb3ee-118">出现了 16 的总问题在版本中解决。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="fb3ee-119">有关工作的完整列表项固定在 NuGet 2.8.1，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="fb3ee-120">使用 Visual Studio"14"CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="fb3ee-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="fb3ee-121">在 Visual Studio"14"CTP 中发布了第三 2014 年 6 月，NuGet 2.8.1 包装盒中。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="fb3ee-122">它支持这些功能仍保持在 par 与其他 2.8.1 VSIXes 如 Visual Studio 2013 的一个。</span><span class="sxs-lookup"><span data-stu-id="fb3ee-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
