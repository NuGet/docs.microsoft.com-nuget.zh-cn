---
title: NuGet CLI 列表命令
description: nuget.exe list 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623066"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="43274-103"> (NuGet CLI) 列表命令</span><span class="sxs-lookup"><span data-stu-id="43274-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="43274-104">**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="43274-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="43274-105">显示来自给定源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="43274-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="43274-106">如果未指定任何源，将使用全局配置文件中定义的所有源 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="43274-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="43274-107">如果 `NuGet.Config` 未指定源，则 `list` 使用默认源 (nuget.org) 。</span><span class="sxs-lookup"><span data-stu-id="43274-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="43274-108">使用情况</span><span class="sxs-lookup"><span data-stu-id="43274-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="43274-109">其中，可选搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="43274-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="43274-110">[搜索词](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) 应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。</span><span class="sxs-lookup"><span data-stu-id="43274-110">[Search terms](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="43274-111">选项</span><span class="sxs-lookup"><span data-stu-id="43274-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="43274-112">列出包的所有版本。</span><span class="sxs-lookup"><span data-stu-id="43274-112">List all versions of a package.</span></span> <span data-ttu-id="43274-113">默认情况下，仅显示最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="43274-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="43274-114">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="43274-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="43274-115">如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="43274-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="43274-116">\* (3.5 +) \* 使用固定的、基于英语的区域性强制运行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="43274-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="43274-117">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="43274-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="43274-118">\* (3.2 +) \* 显示未列出的包。</span><span class="sxs-lookup"><span data-stu-id="43274-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="43274-119">禁止提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="43274-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="43274-120">在列表中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="43274-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="43274-121">指定要搜索的包源列表。</span><span class="sxs-lookup"><span data-stu-id="43274-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="43274-122">指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="43274-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="43274-123">另请参阅 [环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="43274-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43274-124">示例</span><span class="sxs-lookup"><span data-stu-id="43274-124">Examples</span></span>

<span data-ttu-id="43274-125">列出配置的源中的所有包：</span><span class="sxs-lookup"><span data-stu-id="43274-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="43274-126">列出与 Azure 相关的包，详细详细说明：</span><span class="sxs-lookup"><span data-stu-id="43274-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="43274-127">列出来自配置的源的 Azure 相关包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="43274-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="43274-128">列出指定源/源中与 JSON 相关的所有包的所有版本：</span><span class="sxs-lookup"><span data-stu-id="43274-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="43274-129">列出来自多个源/源的 JSON 相关包：</span><span class="sxs-lookup"><span data-stu-id="43274-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
