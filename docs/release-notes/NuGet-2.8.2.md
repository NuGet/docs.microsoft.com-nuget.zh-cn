---
title: NuGet 2.8.2 发行说明
description: NuGet 2.8.2 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551143"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="7ce2c-103">NuGet 2.8.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="7ce2c-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="7ce2c-104">[NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="7ce2c-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="7ce2c-105">NuGet 2.8.2 已于 2014 年 5 月 22，发布。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="7ce2c-106">此版本中，仅包含 nuget.exe 命令行，NuGet.Server 包与其他 NuGet 包的变化。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="7ce2c-107">发布未包含的更新的 Visual Studio 扩展或 WebMatrix 扩展。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="7ce2c-108">值得注意的更新</span><span class="sxs-lookup"><span data-stu-id="7ce2c-108">Notable Updates</span></span>

<span data-ttu-id="7ce2c-109">在 nuget.exe 命令行和 NuGet.Server 包 （适用于自承载的 NuGet 源） 中介绍了最值得注意的更新。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="7ce2c-110">重要的 nuget.exe Bug 修复</span><span class="sxs-lookup"><span data-stu-id="7ce2c-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="7ce2c-111">nuget.exe 推送会失败，并保留重试</span><span class="sxs-lookup"><span data-stu-id="7ce2c-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="7ce2c-112">nuget.exe 推送不会正确发送基本身份验证凭据</span><span class="sxs-lookup"><span data-stu-id="7ce2c-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="7ce2c-113">nuget.exe 推送不遵循临时重定向</span><span class="sxs-lookup"><span data-stu-id="7ce2c-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="7ce2c-114">重要 NuGet.Server 的 Bug 修复</span><span class="sxs-lookup"><span data-stu-id="7ce2c-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="7ce2c-115">IsAbsoluteLatestVersion NuGet.Server 返回的值不正确</span><span class="sxs-lookup"><span data-stu-id="7ce2c-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="7ce2c-116">更新包</span><span class="sxs-lookup"><span data-stu-id="7ce2c-116">Packages Updated</span></span>

<span data-ttu-id="7ce2c-117">Nuget.exe 命令行和 NuGet.Server 修补程序附带 NuGet 包更新。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="7ce2c-118">没有使用 2.8.2 以及更新其他包。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="7ce2c-119">下面是更新后的包的列表：</span><span class="sxs-lookup"><span data-stu-id="7ce2c-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="7ce2c-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="7ce2c-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="7ce2c-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="7ce2c-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="7ce2c-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="7ce2c-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="7ce2c-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="7ce2c-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="7ce2c-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （包，不扩展）</span><span class="sxs-lookup"><span data-stu-id="7ce2c-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="7ce2c-125">所有更改</span><span class="sxs-lookup"><span data-stu-id="7ce2c-125">All Changes</span></span>
<span data-ttu-id="7ce2c-126">出现了 10 个版本中解决的问题。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="7ce2c-127">有关完整列表的工作项中已修复 NuGet 2.8.2，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="7ce2c-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
