---
title: "NuGet CLI 列表命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "对于 nuget.exe 列出命令的引用"
keywords: "nuget 列表引用包列表的命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="78bc7-104">(NuGet CLI) 中的列表命令</span><span class="sxs-lookup"><span data-stu-id="78bc7-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="78bc7-105">**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="78bc7-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="78bc7-106">显示从给定的源的包的列表。</span><span class="sxs-lookup"><span data-stu-id="78bc7-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="78bc7-107">如果未不指定任何源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`，使用。</span><span class="sxs-lookup"><span data-stu-id="78bc7-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="78bc7-108">如果`NuGet.Config`然后指定任何源`list`使用默认的源 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="78bc7-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="78bc7-109">用法</span><span class="sxs-lookup"><span data-stu-id="78bc7-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="78bc7-110">其中可选的搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="78bc7-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="78bc7-111">搜索条款将应用到的包、 标记和包说明的名称。</span><span class="sxs-lookup"><span data-stu-id="78bc7-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="78bc7-112">选项</span><span class="sxs-lookup"><span data-stu-id="78bc7-112">Options</span></span>
| <span data-ttu-id="78bc7-113">选项</span><span class="sxs-lookup"><span data-stu-id="78bc7-113">Option</span></span> | <span data-ttu-id="78bc7-114">描述</span><span class="sxs-lookup"><span data-stu-id="78bc7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78bc7-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="78bc7-115">AllVersions</span></span> | <span data-ttu-id="78bc7-116">列出所有版本的包。</span><span class="sxs-lookup"><span data-stu-id="78bc7-116">List all versions of a package.</span></span> <span data-ttu-id="78bc7-117">默认情况下，显示仅最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="78bc7-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="78bc7-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="78bc7-118">ConfigFile</span></span> | <span data-ttu-id="78bc7-119">*（2.5 +)* NuGet 要应用的配置文件。</span><span class="sxs-lookup"><span data-stu-id="78bc7-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="78bc7-120">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="78bc7-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="78bc7-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="78bc7-121">ForceEnglishOutput</span></span> | <span data-ttu-id="78bc7-122">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="78bc7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="78bc7-123">帮助</span><span class="sxs-lookup"><span data-stu-id="78bc7-123">Help</span></span> | <span data-ttu-id="78bc7-124">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="78bc7-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="78bc7-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="78bc7-125">IncludeDelisted</span></span> | <span data-ttu-id="78bc7-126">*（3.2 +)*显示未列出的程序包。</span><span class="sxs-lookup"><span data-stu-id="78bc7-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="78bc7-127">非交互式</span><span class="sxs-lookup"><span data-stu-id="78bc7-127">NonInteractive</span></span> | <span data-ttu-id="78bc7-128">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="78bc7-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="78bc7-129">预发行版</span><span class="sxs-lookup"><span data-stu-id="78bc7-129">PreRelease</span></span> | <span data-ttu-id="78bc7-130">在列表中包含预发行程序包。</span><span class="sxs-lookup"><span data-stu-id="78bc7-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="78bc7-131">源</span><span class="sxs-lookup"><span data-stu-id="78bc7-131">Source</span></span> | <span data-ttu-id="78bc7-132">指定要搜索的程序包源的列表。</span><span class="sxs-lookup"><span data-stu-id="78bc7-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="78bc7-133">详细级别</span><span class="sxs-lookup"><span data-stu-id="78bc7-133">Verbosity</span></span> | <span data-ttu-id="78bc7-134">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="78bc7-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="78bc7-135">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="78bc7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="78bc7-136">示例</span><span class="sxs-lookup"><span data-stu-id="78bc7-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
