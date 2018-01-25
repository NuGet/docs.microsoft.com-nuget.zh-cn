---
title: "NuGet CLI 局部变量命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 局部变量命令参考"
keywords: "nuget 局部变量引用，局部变量命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="47cac-104">局部变量命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="47cac-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="47cac-105">**适用于：**打包消耗&bullet;**受支持的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="47cac-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="47cac-106">清除或列出本地 NuGet 资源，如 http 请求缓存、 包缓存和计算机范围全局包文件夹。</span><span class="sxs-lookup"><span data-stu-id="47cac-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="47cac-107">`locals`命令还可以用于显示这些位置的列表。</span><span class="sxs-lookup"><span data-stu-id="47cac-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="47cac-108">有关详细信息，请参阅[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)。</span><span class="sxs-lookup"><span data-stu-id="47cac-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="47cac-109">用法</span><span class="sxs-lookup"><span data-stu-id="47cac-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="47cac-110">其中`<cache>`是之一`all`， `http-cache`， `packages-cache`， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="47cac-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="47cac-111">选项</span><span class="sxs-lookup"><span data-stu-id="47cac-111">Options</span></span>

| <span data-ttu-id="47cac-112">选项</span><span class="sxs-lookup"><span data-stu-id="47cac-112">Option</span></span> | <span data-ttu-id="47cac-113">描述</span><span class="sxs-lookup"><span data-stu-id="47cac-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47cac-114">清除</span><span class="sxs-lookup"><span data-stu-id="47cac-114">Clear</span></span> | <span data-ttu-id="47cac-115">清除指定的缓存。</span><span class="sxs-lookup"><span data-stu-id="47cac-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="47cac-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="47cac-116">ConfigFile</span></span> | <span data-ttu-id="47cac-117">要应用的 NuGet 配置文件。</span><span class="sxs-lookup"><span data-stu-id="47cac-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="47cac-118">如果未指定， *%AppData%\NuGet\NuGet.Config*使用。</span><span class="sxs-lookup"><span data-stu-id="47cac-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="47cac-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="47cac-119">ForceEnglishOutput</span></span> | <span data-ttu-id="47cac-120">*（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。</span><span class="sxs-lookup"><span data-stu-id="47cac-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="47cac-121">帮助</span><span class="sxs-lookup"><span data-stu-id="47cac-121">Help</span></span> | <span data-ttu-id="47cac-122">显示的帮助命令的信息。</span><span class="sxs-lookup"><span data-stu-id="47cac-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="47cac-123">列表</span><span class="sxs-lookup"><span data-stu-id="47cac-123">List</span></span> | <span data-ttu-id="47cac-124">列出指定的缓存的位置或一起使用时的所有缓存的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="47cac-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="47cac-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="47cac-125">NonInteractive</span></span> | <span data-ttu-id="47cac-126">取消显示提示用户输入或确认。</span><span class="sxs-lookup"><span data-stu-id="47cac-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="47cac-127">详细级别</span><span class="sxs-lookup"><span data-stu-id="47cac-127">Verbosity</span></span> | <span data-ttu-id="47cac-128">指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。</span><span class="sxs-lookup"><span data-stu-id="47cac-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="47cac-129">另请参阅[环境变量](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="47cac-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="47cac-130">示例</span><span class="sxs-lookup"><span data-stu-id="47cac-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
