---
title: NuGet 2.8.2 发行说明
description: NuGet 2.8.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780371"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="e7ab0-103">NuGet 2.8.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="e7ab0-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="e7ab0-104">[NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)  | [NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="e7ab0-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="e7ab0-105">NuGet 2.8.2 于2014年5月22日发布。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="e7ab0-106">此版本仅包括对 nuget.exe 命令行、NuGet 包和其他 NuGet 包的更改。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="e7ab0-107">版本未包括更新的 Visual Studio 扩展或 WebMatrix 扩展。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="e7ab0-108">重要更新</span><span class="sxs-lookup"><span data-stu-id="e7ab0-108">Notable Updates</span></span>

<span data-ttu-id="e7ab0-109">最值得注意的更新在 nuget.exe 命令行和 NuGet. 服务器包 (中，用于自承载的 NuGet 源) 。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="e7ab0-110">重要 nuget.exe Bug 修复</span><span class="sxs-lookup"><span data-stu-id="e7ab0-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="e7ab0-111">nuget.exe 推送失败并继续重试</span><span class="sxs-lookup"><span data-stu-id="e7ab0-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="e7ab0-112">nuget.exe 推送不会正确发送基本身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="e7ab0-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="e7ab0-113">nuget.exe 推送不会跟随暂时重定向</span><span class="sxs-lookup"><span data-stu-id="e7ab0-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="e7ab0-114">重要说明 NuGet。服务器错误修复</span><span class="sxs-lookup"><span data-stu-id="e7ab0-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="e7ab0-115">NuGet 返回的 IsAbsoluteLatestVersion 值错误。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="e7ab0-116">已更新包</span><span class="sxs-lookup"><span data-stu-id="e7ab0-116">Packages Updated</span></span>

<span data-ttu-id="e7ab0-117">nuget.exe 的命令行和 NuGet。服务器修补程序作为 NuGet 包更新提供。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="e7ab0-118">还更新了2.8.2 的其他包。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="e7ab0-119">下面是已更新包的列表：</span><span class="sxs-lookup"><span data-stu-id="e7ab0-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="e7ab0-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e7ab0-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="e7ab0-121">NuGet 命令行</span><span class="sxs-lookup"><span data-stu-id="e7ab0-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="e7ab0-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e7ab0-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="e7ab0-123">NuGet。生成</span><span class="sxs-lookup"><span data-stu-id="e7ab0-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="e7ab0-124">[VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (包，而不是扩展) </span><span class="sxs-lookup"><span data-stu-id="e7ab0-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="e7ab0-125">所有更改</span><span class="sxs-lookup"><span data-stu-id="e7ab0-125">All Changes</span></span>
<span data-ttu-id="e7ab0-126">此版本中解决了10个问题。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="e7ab0-127">有关 NuGet 2.8.2 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="e7ab0-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
