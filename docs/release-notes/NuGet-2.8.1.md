---
title: NuGet 2.8.1 发行说明
description: NuGet 2.8.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776771"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="50609-103">NuGet 2.8.1 发行说明</span><span class="sxs-lookup"><span data-stu-id="50609-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="50609-104">[NuGet 2.8 发行说明](../release-notes/nuget-2.8.md)  | [NuGet 2.8.2 发行说明](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="50609-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="50609-105">NuGet 2.8.1 于2014年4月2日发布。</span><span class="sxs-lookup"><span data-stu-id="50609-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="50609-106">版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="50609-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="50609-107">支持 Windows Phone 8.1 项目</span><span class="sxs-lookup"><span data-stu-id="50609-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="50609-108">此版本现在支持以下新的目标框架名字对象，可用于针对 Windows Phone 8.1 项目：</span><span class="sxs-lookup"><span data-stu-id="50609-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="50609-109">基于 Silverlight 的 Windows Phone 项目的 WindowsPhone81/WP81 () </span><span class="sxs-lookup"><span data-stu-id="50609-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="50609-110">基于 WinRT 的 Windows Phone 应用项目的 WindowsPhoneApp81/WPA81 () </span><span class="sxs-lookup"><span data-stu-id="50609-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="50609-111">NuGet WebMatrix 扩展的更新</span><span class="sxs-lookup"><span data-stu-id="50609-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="50609-112">此版本将在 WebMatrix 中找到的 NuGet 客户端更新为 [nuget.exe](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1，并附带 it 功能，如 XDT 转换。</span><span class="sxs-lookup"><span data-stu-id="50609-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="50609-113">更重要的是，2.6.1 core 更新允许 WebMatrix 客户端安装包含最新版本的架构的 NuGet 包 `.nuspec` ，其中包括 ASP.NET NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="50609-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="50609-114">有关 WebMatrix 扩展更新的详细信息，请参阅这些特定的 [发行说明](../release-notes/nuget-2.6.1-for-WebMatrix.md)。</span><span class="sxs-lookup"><span data-stu-id="50609-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="50609-115">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="50609-115">Bug Fixes</span></span>
<span data-ttu-id="50609-116">除了这些功能以外，此版本的 NuGet 还包括其他 bug 修复。</span><span class="sxs-lookup"><span data-stu-id="50609-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="50609-117">此版本中解决了16个问题。</span><span class="sxs-lookup"><span data-stu-id="50609-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="50609-118">有关 NuGet 2.8.1 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="50609-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="50609-119">导致 with Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="50609-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="50609-120">在 Visual Studio "14" CTP 年6月 2014 3 日发布的 CTP 中，NuGet 2.8.1 随附在包装盒中。</span><span class="sxs-lookup"><span data-stu-id="50609-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="50609-121">它支持的功能与其他 2.8.1 VSIXes （例如 Visual Studio 2013 的功能）保持不变。</span><span class="sxs-lookup"><span data-stu-id="50609-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
