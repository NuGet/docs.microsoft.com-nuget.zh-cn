---
title: NuGet 2.8.1 发行说明
description: NuGet 2.8.1 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545234"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="1c93b-103">NuGet 2.8.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="1c93b-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="1c93b-104">[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 发行说明](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="1c93b-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="1c93b-105">NuGet 2.8.1 已于 2014 年 4 月 2 日发布。</span><span class="sxs-lookup"><span data-stu-id="1c93b-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="1c93b-106">在版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="1c93b-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="1c93b-107">对 Windows Phone 8.1 项目的支持</span><span class="sxs-lookup"><span data-stu-id="1c93b-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="1c93b-108">此版本现在支持以下新目标框架名字对象可以用于面向 Windows Phone 8.1 项目记录的：</span><span class="sxs-lookup"><span data-stu-id="1c93b-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="1c93b-109">WindowsPhone81 / （适用于基于 Silverlight 的 Windows Phone 项目） 和 WP81</span><span class="sxs-lookup"><span data-stu-id="1c93b-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="1c93b-110">WindowsPhoneApp81 / WPA81 （对于基于 WinRT 的 Windows Phone 应用程序项目）</span><span class="sxs-lookup"><span data-stu-id="1c93b-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="1c93b-111">NuGet WebMatrix 扩展的更新</span><span class="sxs-lookup"><span data-stu-id="1c93b-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="1c93b-112">此版本更新到 WebMatrix 中找到的 NuGet 客户端[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，并使其如 XDT 转换使用的功能。</span><span class="sxs-lookup"><span data-stu-id="1c93b-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="1c93b-113">更重要的是 2.6.1 核心更新，WebMatrix 客户端将安装包含较新版本的 NuGet 包`.nuspec`架构，其中包括 ASP.NET NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1c93b-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="1c93b-114">有关 WebMatrix 扩展更新的详细信息，请参阅的那些特定[发行说明](../release-notes/nuget-2.6.1-for-WebMatrix.md)。</span><span class="sxs-lookup"><span data-stu-id="1c93b-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="1c93b-115">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="1c93b-115">Bug Fixes</span></span>
<span data-ttu-id="1c93b-116">除了这些功能，此版本的 NuGet 包括其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="1c93b-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="1c93b-117">出现的版本中解决的 16 总问题。</span><span class="sxs-lookup"><span data-stu-id="1c93b-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="1c93b-118">有关完整列表的工作项中已修复 NuGet 2.8.1，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="1c93b-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="1c93b-119">使用 Visual Studio"14"CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="1c93b-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="1c93b-120">在 Visual Studio"14"CTP 中发布的 2014 年 6 月第三，NuGet 2.8.1 包装盒中。</span><span class="sxs-lookup"><span data-stu-id="1c93b-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="1c93b-121">它支持这些功能仍保持在 par 与其他 2.8.1 VSIXes 类似于 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1c93b-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
