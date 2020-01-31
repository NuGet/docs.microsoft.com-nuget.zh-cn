---
title: NuGet CLI 列表命令
description: 针对 nuget.exe list 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813333"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="c3e91-103">list 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="c3e91-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="c3e91-104">**适用于：** 包使用情况、发布 &bullet;**支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="c3e91-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c3e91-105">显示来自给定源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="c3e91-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="c3e91-106">如果未指定任何源，将使用全局配置文件中定义的所有源 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config`。</span><span class="sxs-lookup"><span data-stu-id="c3e91-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="c3e91-107">如果 `NuGet.Config` 未指定源，则 `list` 使用默认源（nuget.org）。</span><span class="sxs-lookup"><span data-stu-id="c3e91-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="c3e91-108">用量</span><span class="sxs-lookup"><span data-stu-id="c3e91-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="c3e91-109">其中，可选搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="c3e91-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="c3e91-110">搜索词应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。</span><span class="sxs-lookup"><span data-stu-id="c3e91-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="c3e91-111">选项</span><span class="sxs-lookup"><span data-stu-id="c3e91-111">Options</span></span>

| <span data-ttu-id="c3e91-112">选项</span><span class="sxs-lookup"><span data-stu-id="c3e91-112">Option</span></span> | <span data-ttu-id="c3e91-113">描述</span><span class="sxs-lookup"><span data-stu-id="c3e91-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3e91-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c3e91-114">AllVersions</span></span> | <span data-ttu-id="c3e91-115">列出包的所有版本。</span><span class="sxs-lookup"><span data-stu-id="c3e91-115">List all versions of a package.</span></span> <span data-ttu-id="c3e91-116">默认情况下，仅显示最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="c3e91-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="c3e91-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c3e91-117">ConfigFile</span></span> | <span data-ttu-id="c3e91-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c3e91-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c3e91-119">如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="c3e91-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c3e91-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c3e91-120">ForceEnglishOutput</span></span> | <span data-ttu-id="c3e91-121">*（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="c3e91-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c3e91-122">帮助</span><span class="sxs-lookup"><span data-stu-id="c3e91-122">Help</span></span> | <span data-ttu-id="c3e91-123">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="c3e91-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="c3e91-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="c3e91-124">IncludeDelisted</span></span> | <span data-ttu-id="c3e91-125">*（3.2 +）* 显示未列出的包。</span><span class="sxs-lookup"><span data-stu-id="c3e91-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="c3e91-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c3e91-126">NonInteractive</span></span> | <span data-ttu-id="c3e91-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="c3e91-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c3e91-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="c3e91-128">PreRelease</span></span> | <span data-ttu-id="c3e91-129">在列表中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="c3e91-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="c3e91-130">Source</span><span class="sxs-lookup"><span data-stu-id="c3e91-130">Source</span></span> | <span data-ttu-id="c3e91-131">指定要搜索的包源列表。</span><span class="sxs-lookup"><span data-stu-id="c3e91-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="c3e91-132">详细级别</span><span class="sxs-lookup"><span data-stu-id="c3e91-132">Verbosity</span></span> | <span data-ttu-id="c3e91-133">指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="c3e91-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c3e91-134">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c3e91-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c3e91-135">示例</span><span class="sxs-lookup"><span data-stu-id="c3e91-135">Examples</span></span>

<span data-ttu-id="c3e91-136">列出配置的源中的所有包：</span><span class="sxs-lookup"><span data-stu-id="c3e91-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="c3e91-137">列出与 Azure 相关的包，详细详细说明：</span><span class="sxs-lookup"><span data-stu-id="c3e91-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="c3e91-138">列出来自配置的源的 Azure 相关包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="c3e91-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="c3e91-139">列出指定源/源中与 JSON 相关的所有包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="c3e91-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="c3e91-140">列出来自多个源/源的 JSON 相关包：</span><span class="sxs-lookup"><span data-stu-id="c3e91-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

