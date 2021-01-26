---
title: NuGet CLI 列表命令
description: nuget.exe list 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780062"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="5c6a8-103"> (NuGet CLI) 列表命令</span><span class="sxs-lookup"><span data-stu-id="5c6a8-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="5c6a8-104">**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="5c6a8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5c6a8-105">显示来自给定源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="5c6a8-106">如果未指定任何源，将使用全局配置文件中定义的所有源 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="5c6a8-107">如果 `NuGet.Config` 未指定源，则 `list` 使用默认源 (nuget.org) 。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="5c6a8-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="5c6a8-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="5c6a8-109">其中，可选搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="5c6a8-110">[搜索词](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="5c6a8-111">选项</span><span class="sxs-lookup"><span data-stu-id="5c6a8-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="5c6a8-112">列出包的所有版本。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-112">List all versions of a package.</span></span> <span data-ttu-id="5c6a8-113">默认情况下，仅显示最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5c6a8-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5c6a8-115">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5c6a8-116">*(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5c6a8-117">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="5c6a8-118">*(3.2 +)* 显示未列出的包。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5c6a8-119">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="5c6a8-120">在列表中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="5c6a8-121">要搜索的包源。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-121">The package source to search.</span></span> <span data-ttu-id="5c6a8-122">可以使用选项多次指定多个源 `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5c6a8-123">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="5c6a8-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="5c6a8-124">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5c6a8-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5c6a8-125">示例</span><span class="sxs-lookup"><span data-stu-id="5c6a8-125">Examples</span></span>

<span data-ttu-id="5c6a8-126">列出配置的源中的所有包：</span><span class="sxs-lookup"><span data-stu-id="5c6a8-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="5c6a8-127">列出与 Azure 相关的包，详细详细说明：</span><span class="sxs-lookup"><span data-stu-id="5c6a8-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="5c6a8-128">列出来自配置的源的 Azure 相关包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="5c6a8-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="5c6a8-129">列出指定源/源中与 JSON 相关的所有包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="5c6a8-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="5c6a8-130">列出来自多个源/源的 JSON 相关包：</span><span class="sxs-lookup"><span data-stu-id="5c6a8-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
