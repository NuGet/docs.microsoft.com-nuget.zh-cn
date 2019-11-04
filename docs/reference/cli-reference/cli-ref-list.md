---
title: NuGet CLI 列表命令
description: 针对 nuget.exe list 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327734"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="802ac-103">list 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="802ac-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="802ac-104">**适用于:** 包消耗, 发布&bullet; **支持的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="802ac-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="802ac-105">显示来自给定源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="802ac-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="802ac-106">如果未指定任何源, 将使用全局配置文件`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`中定义的所有源。</span><span class="sxs-lookup"><span data-stu-id="802ac-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="802ac-107">如果`NuGet.Config`未指定源, 则`list`使用默认源 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="802ac-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="802ac-108">用法</span><span class="sxs-lookup"><span data-stu-id="802ac-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="802ac-109">其中, 可选搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="802ac-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="802ac-110">搜索词应用于包、标记和包说明的名称, 就像在 nuget.org 上使用时一样。</span><span class="sxs-lookup"><span data-stu-id="802ac-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="802ac-111">选项</span><span class="sxs-lookup"><span data-stu-id="802ac-111">Options</span></span>

| <span data-ttu-id="802ac-112">选项</span><span class="sxs-lookup"><span data-stu-id="802ac-112">Option</span></span> | <span data-ttu-id="802ac-113">描述</span><span class="sxs-lookup"><span data-stu-id="802ac-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="802ac-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="802ac-114">AllVersions</span></span> | <span data-ttu-id="802ac-115">列出包的所有版本。</span><span class="sxs-lookup"><span data-stu-id="802ac-115">List all versions of a package.</span></span> <span data-ttu-id="802ac-116">默认情况下, 仅显示最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="802ac-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="802ac-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="802ac-117">ConfigFile</span></span> | <span data-ttu-id="802ac-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="802ac-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="802ac-119">如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="802ac-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="802ac-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="802ac-120">ForceEnglishOutput</span></span> | <span data-ttu-id="802ac-121">*(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="802ac-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="802ac-122">Help</span><span class="sxs-lookup"><span data-stu-id="802ac-122">Help</span></span> | <span data-ttu-id="802ac-123">显示命令的帮助信息。</span><span class="sxs-lookup"><span data-stu-id="802ac-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="802ac-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="802ac-124">IncludeDelisted</span></span> | <span data-ttu-id="802ac-125">*(3.2 +)* 显示未列出的包。</span><span class="sxs-lookup"><span data-stu-id="802ac-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="802ac-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="802ac-126">NonInteractive</span></span> | <span data-ttu-id="802ac-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="802ac-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="802ac-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="802ac-128">PreRelease</span></span> | <span data-ttu-id="802ac-129">在列表中包括预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="802ac-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="802ac-130">Source</span><span class="sxs-lookup"><span data-stu-id="802ac-130">Source</span></span> | <span data-ttu-id="802ac-131">指定要搜索的包源列表。</span><span class="sxs-lookup"><span data-stu-id="802ac-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="802ac-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="802ac-132">Verbosity</span></span> | <span data-ttu-id="802ac-133">指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。</span><span class="sxs-lookup"><span data-stu-id="802ac-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="802ac-134">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="802ac-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="802ac-135">示例</span><span class="sxs-lookup"><span data-stu-id="802ac-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
