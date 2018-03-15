---
title: "NuGet CLI 列表命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "对于 nuget.exe 列出命令的引用"
keywords: "nuget 列表引用包列表的命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="3cd9a-104">(NuGet CLI) 中的列表命令</span><span class="sxs-lookup"><span data-stu-id="3cd9a-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="3cd9a-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="3cd9a-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3cd9a-106">显示从给定的源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="3cd9a-107">如果未不指定任何源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`，使用。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="3cd9a-108">如果`NuGet.Config`然后指定任何源`list`使用默认的源 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="3cd9a-109">用法</span><span class="sxs-lookup"><span data-stu-id="3cd9a-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="3cd9a-110">其中可选的搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="3cd9a-111">搜索条款将应用到的包、 标记和包说明的名称，就像它们在 nuget.org 上使用它们时。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="3cd9a-112">选项</span><span class="sxs-lookup"><span data-stu-id="3cd9a-112">Options</span></span>

| <span data-ttu-id="3cd9a-113">选项</span><span class="sxs-lookup"><span data-stu-id="3cd9a-113">Option</span></span> | <span data-ttu-id="3cd9a-114">描述</span><span class="sxs-lookup"><span data-stu-id="3cd9a-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3cd9a-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3cd9a-115">AllVersions</span></span> | <span data-ttu-id="3cd9a-116">列出所有版本的包。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-116">List all versions of a package.</span></span> <span data-ttu-id="3cd9a-117">默认情况下，显示仅最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="3cd9a-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3cd9a-118">ConfigFile</span></span> | <span data-ttu-id="3cd9a-119">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3cd9a-120">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3cd9a-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3cd9a-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3cd9a-122">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3cd9a-123">帮助</span><span class="sxs-lookup"><span data-stu-id="3cd9a-123">Help</span></span> | <span data-ttu-id="3cd9a-124">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3cd9a-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="3cd9a-125">IncludeDelisted</span></span> | <span data-ttu-id="3cd9a-126">*（3.2 +)*显示未列出的程序包。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="3cd9a-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3cd9a-127">NonInteractive</span></span> | <span data-ttu-id="3cd9a-128">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3cd9a-129">预发行版</span><span class="sxs-lookup"><span data-stu-id="3cd9a-129">PreRelease</span></span> | <span data-ttu-id="3cd9a-130">在列表中包含预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="3cd9a-131">源</span><span class="sxs-lookup"><span data-stu-id="3cd9a-131">Source</span></span> | <span data-ttu-id="3cd9a-132">指定要搜索的程序包源的列表。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="3cd9a-133">详细级别</span><span class="sxs-lookup"><span data-stu-id="3cd9a-133">Verbosity</span></span> | <span data-ttu-id="3cd9a-134">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="3cd9a-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3cd9a-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3cd9a-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3cd9a-136">示例</span><span class="sxs-lookup"><span data-stu-id="3cd9a-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
