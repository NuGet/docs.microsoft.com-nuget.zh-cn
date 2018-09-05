---
title: NuGet CLI 列表命令
description: Nuget.exe list 命令的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549796"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d63bf-103">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d63bf-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d63bf-104">**适用于：** 包使用、 发布&bullet;**支持的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="d63bf-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d63bf-105">显示来自给定源的包列表。</span><span class="sxs-lookup"><span data-stu-id="d63bf-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d63bf-106">如果指定了不到源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`，使用。</span><span class="sxs-lookup"><span data-stu-id="d63bf-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d63bf-107">如果`NuGet.Config`不指定任何源，然后`list`使用默认的源 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="d63bf-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d63bf-108">用法</span><span class="sxs-lookup"><span data-stu-id="d63bf-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d63bf-109">其中的可选搜索词将筛选显示的列表。</span><span class="sxs-lookup"><span data-stu-id="d63bf-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d63bf-110">就像它们是在 nuget.org 上使用它们时，搜索词将应用于包、 标记和包说明的名称。</span><span class="sxs-lookup"><span data-stu-id="d63bf-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="d63bf-111">选项</span><span class="sxs-lookup"><span data-stu-id="d63bf-111">Options</span></span>

| <span data-ttu-id="d63bf-112">选项</span><span class="sxs-lookup"><span data-stu-id="d63bf-112">Option</span></span> | <span data-ttu-id="d63bf-113">描述</span><span class="sxs-lookup"><span data-stu-id="d63bf-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63bf-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d63bf-114">AllVersions</span></span> | <span data-ttu-id="d63bf-115">列出所有版本的包。</span><span class="sxs-lookup"><span data-stu-id="d63bf-115">List all versions of a package.</span></span> <span data-ttu-id="d63bf-116">默认情况下，显示仅最新的包版本。</span><span class="sxs-lookup"><span data-stu-id="d63bf-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="d63bf-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d63bf-117">ConfigFile</span></span> | <span data-ttu-id="d63bf-118">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="d63bf-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d63bf-119">如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。</span><span class="sxs-lookup"><span data-stu-id="d63bf-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d63bf-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d63bf-120">ForceEnglishOutput</span></span> | <span data-ttu-id="d63bf-121">*（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="d63bf-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d63bf-122">帮助</span><span class="sxs-lookup"><span data-stu-id="d63bf-122">Help</span></span> | <span data-ttu-id="d63bf-123">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="d63bf-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="d63bf-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="d63bf-124">IncludeDelisted</span></span> | <span data-ttu-id="d63bf-125">*（3.2 +)* 显示取消列出的包。</span><span class="sxs-lookup"><span data-stu-id="d63bf-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="d63bf-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d63bf-126">NonInteractive</span></span> | <span data-ttu-id="d63bf-127">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="d63bf-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d63bf-128">预发行版</span><span class="sxs-lookup"><span data-stu-id="d63bf-128">PreRelease</span></span> | <span data-ttu-id="d63bf-129">在列表中包括预发行包。</span><span class="sxs-lookup"><span data-stu-id="d63bf-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="d63bf-130">源</span><span class="sxs-lookup"><span data-stu-id="d63bf-130">Source</span></span> | <span data-ttu-id="d63bf-131">指定要搜索的包源的列表。</span><span class="sxs-lookup"><span data-stu-id="d63bf-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="d63bf-132">详细级别</span><span class="sxs-lookup"><span data-stu-id="d63bf-132">Verbosity</span></span> | <span data-ttu-id="d63bf-133">指定的输出中显示的详细信息：*正常*，*静默*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="d63bf-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d63bf-134">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d63bf-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d63bf-135">示例</span><span class="sxs-lookup"><span data-stu-id="d63bf-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
