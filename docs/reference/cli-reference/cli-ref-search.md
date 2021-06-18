---
title: NuGet CLI 搜索命令
description: nuget.exe 搜索命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323656"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="fd838-103"> (NuGet CLI) 搜索命令</span><span class="sxs-lookup"><span data-stu-id="fd838-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="fd838-104">**适用于：** 包使用 &bullet; **受支持的版本：** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="fd838-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="fd838-105">使用提供的查询字符串搜索给定的源。</span><span class="sxs-lookup"><span data-stu-id="fd838-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="fd838-106">如果未指定任何源，将使用% AppData% \NuGet\NuGet.Config 中定义的所有源。</span><span class="sxs-lookup"><span data-stu-id="fd838-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="fd838-107">使用情况</span><span class="sxs-lookup"><span data-stu-id="fd838-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="fd838-108">其中，搜索词应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。</span><span class="sxs-lookup"><span data-stu-id="fd838-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="fd838-109">选项</span><span class="sxs-lookup"><span data-stu-id="fd838-109">Options</span></span>

| <span data-ttu-id="fd838-110">名称</span><span class="sxs-lookup"><span data-stu-id="fd838-110">Name</span></span> | <span data-ttu-id="fd838-111">说明</span><span class="sxs-lookup"><span data-stu-id="fd838-111">Description</span></span> | <span data-ttu-id="fd838-112">使用情况</span><span class="sxs-lookup"><span data-stu-id="fd838-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="fd838-113">早期</span><span class="sxs-lookup"><span data-stu-id="fd838-113">PreRelease</span></span> | <span data-ttu-id="fd838-114">默认情况下不包括预发行包，但可以通过使用此参数包含这些包</span><span class="sxs-lookup"><span data-stu-id="fd838-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="fd838-115">-预发行版</span><span class="sxs-lookup"><span data-stu-id="fd838-115">-PreRelease</span></span> |
| <span data-ttu-id="fd838-116">Source</span><span class="sxs-lookup"><span data-stu-id="fd838-116">Source</span></span> | <span data-ttu-id="fd838-117">要搜索的特定包源 () ，而不是查询中的默认源 __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="fd838-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="fd838-118">-源 `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="fd838-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="fd838-119">Take</span><span class="sxs-lookup"><span data-stu-id="fd838-119">Take</span></span> | <span data-ttu-id="fd838-120">要返回的结果数。</span><span class="sxs-lookup"><span data-stu-id="fd838-120">The number of results to return.</span></span> <span data-ttu-id="fd838-121">默认值为 20。</span><span class="sxs-lookup"><span data-stu-id="fd838-121">The default value is 20.</span></span> | <span data-ttu-id="fd838-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="fd838-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="fd838-123">详细程度</span><span class="sxs-lookup"><span data-stu-id="fd838-123">Verbosity</span></span> | <span data-ttu-id="fd838-124">要在输出中显示的详细信息的级别。</span><span class="sxs-lookup"><span data-stu-id="fd838-124">The level of detail to display in the output.</span></span> <span data-ttu-id="fd838-125">默认值为 " _正常_"。</span><span class="sxs-lookup"><span data-stu-id="fd838-125">The default is _normal_.</span></span> <span data-ttu-id="fd838-126"> (参见下面的注释) </span><span class="sxs-lookup"><span data-stu-id="fd838-126">(See the note below)</span></span>  | <span data-ttu-id="fd838-127">-详细级别 `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="fd838-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="fd838-128">帮助</span><span class="sxs-lookup"><span data-stu-id="fd838-128">Help</span></span> | <span data-ttu-id="fd838-129">显示命令的帮助信息</span><span class="sxs-lookup"><span data-stu-id="fd838-129">Displays help information for the command</span></span> | <span data-ttu-id="fd838-130">-Help</span><span class="sxs-lookup"><span data-stu-id="fd838-130">-Help</span></span> |

<span data-ttu-id="fd838-131">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fd838-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="fd838-132">详细级别：</span><span class="sxs-lookup"><span data-stu-id="fd838-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="fd838-133">_quiet_ -程序包 ID，版本</span><span class="sxs-lookup"><span data-stu-id="fd838-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="fd838-134">_标准_ 包 ID、版本、下载、说明预览</span><span class="sxs-lookup"><span data-stu-id="fd838-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="fd838-135">_详细_ -包 ID、版本、下载、完整说明、其他信息，如查询 URL</span><span class="sxs-lookup"><span data-stu-id="fd838-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="fd838-136">示例</span><span class="sxs-lookup"><span data-stu-id="fd838-136">Examples</span></span>

<span data-ttu-id="fd838-137">从默认源搜索与 *日志记录* 相关的包：</span><span class="sxs-lookup"><span data-stu-id="fd838-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="fd838-138">搜索与 *日志记录* 相关的包，详细详细说明：</span><span class="sxs-lookup"><span data-stu-id="fd838-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="fd838-139">搜索与 *日志记录* 相关的包，只显示前5个结果：</span><span class="sxs-lookup"><span data-stu-id="fd838-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="fd838-140">从指定的源/源搜索与 *JSON* 相关的包，包括预发布版本：</span><span class="sxs-lookup"><span data-stu-id="fd838-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="fd838-141">从多个源/源搜索 *JSON* 相关的包：</span><span class="sxs-lookup"><span data-stu-id="fd838-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
